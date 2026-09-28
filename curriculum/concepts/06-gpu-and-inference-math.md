# Concept note 6 — GPUs, rooflines and why inference optimizations work

Used in weeks 11–12. Hardware figures are rounded public spec-sheet numbers for dense (non-sparse) math — use them for reasoning, not for benchmarking claims.

| GPU | BF16 dense | HBM | Bandwidth | Ridge point (FLOP/byte) |
|---|---|---|---|---|
| A100 80GB SXM | ~312 TFLOP/s | 80 GB | ~2.0 TB/s | ~155 |
| H100 SXM | ~989 TFLOP/s | 80 GB | ~3.35 TB/s | ~295 |
| L4 | ~121 TFLOP/s | 24 GB | ~0.3 TB/s | ~400 |

---

## 1. The mental model of a GPU

```
 HBM (80 GB, ~3 TB/s) ──► L2 cache (tens of MB) ──► per-SM shared memory / L1 (~200 KB each, >10 TB/s aggregate)
                                                      ──► registers ──► CUDA cores + Tensor Cores
```

- A GPU is ~100+ **streaming multiprocessors (SMs)**; each runs many **warps** of 32 threads in lock-step.
- **Tensor Cores** do small matrix multiply-accumulates (e.g. BF16/FP8 tiles) and provide almost all of the FLOPs. Non-matmul ops (softmax, norms, activations) run on the much slower general CUDA cores.
- **CUDA programming model:** a kernel is launched as a **grid** of **thread blocks**; a block runs on one SM and can share fast on-chip memory. Coalesced (contiguous) memory access by a warp is essential for bandwidth.
- **Triton** lets you write block-level kernels in Python: you program a *tile*, the compiler handles threads, coalescing and shared memory.

Every operation is limited by one of three things (Horace He): **compute** (FLOPs), **memory bandwidth** (bytes moved from HBM), or **overhead** (Python, kernel launches, host sync). Profile before optimizing.

## 2. Roofline and arithmetic intensity

```
arithmetic intensity  I = FLOPs performed / bytes moved to/from HBM
attainable FLOP/s     = min( peak FLOP/s ,  I × bandwidth )
```

- If `I` < ridge point → memory-bound → buy bandwidth, move fewer bytes (fusion, quantization, batching).
- If `I` > ridge point → compute-bound → use Tensor Cores, lower precision FP8, better kernels.

**Matmul** `(m × k) @ (k × n)` in BF16: FLOPs = `2mkn`; bytes ≈ `2(mk + kn + mn)`.
- Square `4096³`: I ≈ `2·4096³ / (2·3·4096²)` ≈ 1365 → compute-bound.
- **Decode, batch B:** activations `(B × d)` times weights `(d × d)`: I ≈ `2Bd² / (2d² + …)` ≈ **B**. At batch 1 that is ~1 FLOP/byte against a ridge point of ~295 → the GPU idles >99% of its Tensor Cores. Batch size is *the* lever for decode throughput.
- **Elementwise ops** (GELU, residual add, RMSNorm): ~1 FLOP per 2–4 bytes → always memory-bound → the reason **kernel fusion** matters (do several elementwise ops in one pass over memory; `torch.compile` does much of this automatically).

## 3. KV cache, batching and serving

- **KV cache** (concept note 2): memory = `2 · L · n_kv · d_head · bytes · tokens`. It trades memory for not recomputing K/V — and then becomes the thing that limits batch size.
- **Static batching:** wait for a batch, run until the *longest* sequence finishes. Short requests wait, GPU slots idle.
- **Continuous (in-flight) batching** (Orca → vLLM, TGI, TensorRT-LLM): schedule at the granularity of **one decode iteration**; finished sequences leave and new ones join every step.
- **PagedAttention** (vLLM): store the KV cache in fixed-size **blocks** (e.g. 16 tokens) addressed through a per-sequence block table, like OS virtual memory. Removes the fragmentation of reserving `max_len` contiguous memory per request, so many more sequences fit → larger batch → higher throughput. It also enables sharing blocks between sequences (parallel sampling, common prefixes).
- **Prefix caching:** reuse KV blocks for identical prompt prefixes (system prompt, few-shot examples, a document asked about repeatedly). Cuts TTFT and prefill FLOPs; does nothing for decode.
- **Chunked prefill** (Sarathi-Serve): split long prefills into chunks and mix them with ongoing decodes, so one long prompt does not stall everyone's next token (protects TPOT at some TTFT cost).
- **Disaggregated prefill/decode:** run the compute-bound and bandwidth-bound phases on different GPU pools.
- **Metrics:** TTFT (queueing + prefill), TPOT / inter-token latency (decode), throughput (tokens/s across all users), and **goodput** (throughput that meets your latency SLOs). Always report percentiles (p50/p99) at a stated concurrency.

## 4. FlashAttention — same math, fewer bytes

Naive attention writes the `T × T` score matrix to HBM, reads it for softmax, writes probabilities, reads them again for `P V`: **Θ(T²) HBM traffic**, memory-bound for large T.

FlashAttention tiles Q, K, V into blocks that fit in on-chip SRAM and never materializes the full matrix. The trick that makes the softmax work block by block is the **online softmax**: keep a running max `m` and running denominator `ℓ` per query row, and rescale the partial output when a new block raises the max:

```
for each K/V block j:
    S_j   = Q_blk K_jᵀ / √d
    m_new = max(m, rowmax(S_j))
    P_j   = exp(S_j − m_new)
    ℓ     = exp(m − m_new) · ℓ + rowsum(P_j)
    O     = exp(m − m_new) · O + P_j V_j
    m     = m_new
O = O / ℓ
```

HBM traffic drops to roughly `Θ(T² d² / M)` for SRAM size M (vs `Θ(T d + T²)`), and the backward pass **recomputes** attention from saved statistics rather than storing the T × T matrix — trading cheap FLOPs for expensive bytes. It is exact, not an approximation. FA2 improves parallelism and work partitioning; FA3 exploits Hopper features (asynchrony, FP8).

## 5. Precision and quantization

| Format | Bits (sign/exp/mantissa) | Notes |
|---|---|---|
| FP32 | 1/8/23 | master weights, optimizer states |
| FP16 | 1/5/10 | small range → needs loss scaling in training |
| BF16 | 1/8/7 | FP32's range, less precision; default for training/inference |
| FP8 E4M3 / E5M2 | 1/4/3, 1/5/2 | Hopper+ Tensor Cores; ~2× BF16 throughput; needs scaling factors |
| INT8 | 8-bit integer | weights and/or activations with scales |
| INT4 / NF4 | 4-bit | weight-only; dequantize on the fly |

- **Weight-only quantization** (INT4/INT8 weights, BF16 compute) shrinks bytes read per decode step → faster **memory-bound** decode and more room for KV cache. It barely helps compute-bound prefill.
- **Weight + activation quantization** (e.g. FP8, W8A8) also speeds compute-bound work but must handle **activation outliers** (LLM.int8 keeps outlier dimensions in 16-bit; SmoothQuant migrates scale from activations to weights).
- **GPTQ:** quantize weights column by column and update the remaining weights to compensate for the error, using second-order (Hessian) information from calibration data.
- **AWQ:** a small fraction of weight channels matter most (those multiplied by large activations); scale them up before quantizing to protect them.
- **KV-cache quantization** (FP8/INT8 KV) doubles the tokens you can cache.
- Always re-run your P6 evals after quantizing — perplexity alone hides task regressions.

## 6. Speculative decoding

A small **draft** model proposes `k` tokens; the large **target** model scores all `k` in **one** forward pass (a mini-prefill — compute is cheap when you are memory-bound). Token i is accepted with probability `min(1, p_target(x)/p_draft(x))`; on rejection, resample from the normalized residual `max(0, p_target − p_draft)`. This makes the output distribution **exactly** the target model's.

With per-token acceptance rate α, expected tokens per target pass = `(1 − α^{k+1}) / (1 − α)`. Speedup depends on α (draft quality) and on the draft's cost. Variants: Medusa (extra decoding heads), EAGLE (feature-level draft), n-gram/prompt-lookup drafting (free when outputs copy the input — great for code edits and RAG).

## 7. Training memory and parallelism (week 12)

Mixed-precision Adam needs about **16 bytes per parameter** before activations: BF16 weights (2) + BF16 grads (2) + FP32 master weights (4) + Adam m and v (4 + 4). An 8B model → ~128 GB → does not fit one 80 GB GPU even with tiny batches.

| Strategy | Splits | Communication | Use when |
|---|---|---|---|
| DDP | data; full replica per GPU | all-reduce gradients | model fits one GPU |
| ZeRO-1 / 2 / 3 (FSDP ≈ ZeRO-3) | optimizer states / + gradients / + parameters | reduce-scatter + all-gather | model states do not fit |
| Tensor parallel (Megatron) | each matmul across GPUs (column then row split) | all-reduce inside every layer | within a node (NVLink) |
| Pipeline parallel | layers across GPUs; micro-batches | point-to-point activations; bubble overhead | across nodes, very deep models |
| Sequence / context parallel | the sequence dimension | attention needs K/V exchange (ring) | very long contexts |
| Expert parallel | MoE experts across GPUs | all-to-all token routing | MoE models |

**Activation (gradient) checkpointing:** keep only some activations in the forward pass and recompute the rest in the backward pass — roughly +30% compute for a large memory saving.

## 8. Checkpoint questions

1. At what batch size does decode of an 8B BF16 model become compute-bound on an H100 (ignore KV reads)? What changes when you include KV-cache reads at 8K context?
2. Why does INT4 weight-only quantization speed up decode but not prefill?
3. Why is FlashAttention faster even though its backward pass does *more* FLOPs?
4. Your p99 TTFT spikes when a few users send 30K-token prompts. Which two serving features address this and what do they trade off?
5. Memory per GPU for full fine-tuning of an 8B model with ZeRO-3 on 8 GPUs (states only)?

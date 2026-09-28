# Concept note 1 — Attention and the modern Transformer block

Used in weeks 1–2 and 4. Follow the order: **intuition → Q/K/V → equation → tensor shapes → PyTorch → visualization → experiment**. Try to fill in each shape yourself before you read it.

---

## 1. Intuition

A token's embedding on its own says *what the token is*, not *what it means here*. "bank" needs "river" or "loan" from elsewhere in the sequence. Attention is a **learned, content-based lookup**: every position asks a question, every position advertises what it contains, and each position collects a weighted mix of the others' information according to how well the question matches.

- **Query (q):** "what am I looking for?"
- **Key (k):** "what do I contain, for matching purposes?"
- **Value (v):** "what do I hand over if you pick me?"

Keys and values are separate because *what makes a token relevant* and *what information it should contribute* are different things.

## 2. The equation

For one head:

```
Attention(Q, K, V) = softmax( (Q Kᵀ) / √d_k  +  M ) V
```

- `Q = X W_Q`, `K = X W_K`, `V = X W_V` (self-attention: all from the same `X`)
- Cross-attention: `Q = X_dec W_Q`, `K = X_enc W_K`, `V = X_enc W_V`
- `M` is an additive mask: `0` where attention is allowed, `-inf` where it is not
  - **causal mask:** position *i* may only see *j ≤ i* (decoder / LM)
  - **padding mask:** no one may attend *to* pad tokens (batching variable-length inputs)

**Why √d_k?** If the entries of q and k are roughly independent with variance 1, then `q·k` is a sum of d_k terms and has variance ≈ d_k. Without scaling, logits grow like √d_k, softmax saturates towards one-hot, and gradients through softmax vanish. Dividing by √d_k keeps the logit variance ≈ 1 regardless of head size. (You verify this experimentally in week 1.)

## 3. Tensor shapes (multi-head, batched)

Notation: `B` batch, `T` query length, `S` key/value length (`S = T` for self-attention), `d` = d_model, `h` heads, `d_h = d / h`.

| Step | Operation | Shape |
|---|---|---|
| input | `x` | `(B, T, d)` |
| fused projection | `x @ W_qkv`, `W_qkv: (d, 3d)` | `(B, T, 3d)` |
| split | `q, k, v = chunk(3, dim=-1)` | 3 × `(B, T, d)` |
| split heads | `view(B, T, h, d_h).transpose(1, 2)` | `(B, h, T, d_h)` |
| scores | `q @ k.transpose(-2, -1) / √d_h` | `(B, h, T, S)` |
| mask | `scores + M`, `M` broadcast from `(T, S)` or `(B, 1, 1, S)` | `(B, h, T, S)` |
| weights | `softmax(scores, dim=-1)` — over **keys** | `(B, h, T, S)` |
| mix | `weights @ v` | `(B, h, T, d_h)` |
| merge heads | `transpose(1, 2).reshape(B, T, d)` | `(B, T, d)` |
| output projection | `@ W_o`, `W_o: (d, d)` | `(B, T, d)` |

Cost: the score matrix is `(B, h, T, S)` → **O(T²) memory and O(T² d) FLOPs**. This one fact explains FlashAttention (week 11), the KV cache (week 4) and most long-context research.

## 4. PyTorch skeleton (you write the rest)

```python
import math, torch, torch.nn as nn, torch.nn.functional as F

def sdpa(q, k, v, mask=None):            # q:(B,h,T,dh) k,v:(B,h,S,dh)
    scores = q @ k.transpose(-2, -1) / math.sqrt(q.size(-1))
    if mask is not None:                  # mask: True = blocked
        scores = scores.masked_fill(mask, float("-inf"))
    return F.softmax(scores, dim=-1) @ v

class MHA(nn.Module):
    def __init__(self, d, h):
        super().__init__()
        self.h, self.qkv, self.o = h, nn.Linear(d, 3 * d, bias=False), nn.Linear(d, d, bias=False)
    def forward(self, x, causal=True):
        B, T, d = x.shape
        q, k, v = self.qkv(x).chunk(3, dim=-1)
        q, k, v = (t.view(B, T, self.h, d // self.h).transpose(1, 2) for t in (q, k, v))
        mask = torch.triu(torch.ones(T, T, dtype=torch.bool, device=x.device), 1) if causal else None
        return self.o(sdpa(q, k, v, mask).transpose(1, 2).reshape(B, T, d))
```

Tests to write (P1):
1. `torch.allclose(sdpa(...), F.scaled_dot_product_attention(..., is_causal=True), atol=1e-6)`
2. **No-future-leakage:** change tokens at positions > t; outputs at ≤ t must not change.
3. Copy weights into `nn.MultiheadAttention` and compare outputs.
4. A fully masked row must not produce NaNs (decide how you handle it).

## 5. Visualization and experiments (week 1)

- Plot `weights[0, head]` as a `T × T` heatmap for a toy sequence; the causal mask shows as the upper triangle.
- Remove `/√d_h`; for `d_h ∈ {16, 64, 256}` plot mean softmax entropy at init. Expect entropy to collapse as `d_h` grows.
- Measure peak memory vs `T` (1K, 2K, 4K, 8K): confirm the quadratic curve.

---

## 6. The modern (Llama/Qwen-style) decoder block

```
x ─┬─────────────────────────────┐
   └─ RMSNorm ─ Attention(RoPE, GQA) ─ + ─┬──────────────────────┐
                                          └─ RMSNorm ─ SwiGLU FFN ─ + ─→ out
```

**Pre-norm** (normalize *inside* the residual branch) keeps an identity path from the input to the output of every layer, so gradients flow cleanly and training is stable without elaborate warmup. The original Transformer used post-norm (`LN(x + sublayer(x))`), which is harder to train deep.

### LayerNorm vs RMSNorm

```
LayerNorm(x) = γ ⊙ (x − μ) / √(σ² + ε) + β
RMSNorm(x)   = γ ⊙ x / √(mean(x²) + ε)
```

RMSNorm drops the mean-centering and bias: cheaper, and empirically just as good for LLMs.

### FFN vs SwiGLU

```
FFN(x)    = W₂ · GELU(W₁ x)                        W₁: d→4d, W₂: 4d→d   (8d² params)
SwiGLU(x) = W₂ · ( SiLU(W₁ x) ⊙ (W₃ x) )           W₁,W₃: d→d_ff, W₂: d_ff→d
```

With `d_ff = 8/3 · d` SwiGLU has 3·d·d_ff = 8d² params — same budget as the GELU FFN, better quality.

### Parameter count (check your implementation against this)

Per layer ≈ `4d²` (attention: Q, K, V, O) + `8d²` (FFN) = **12d²**; with GQA the K and V projections shrink to `2 · d · (n_kv · d_h)`. Total ≈ `12 · L · d²` + `V · d` (embeddings; ×2 if input and output embeddings are untied).

### RoPE (rotary position embedding)

Instead of adding a position vector, rotate each 2-D pair of q and k dimensions by an angle proportional to the position:

```
for pair i with frequency θ_i = base^(−2i/d_h):
  [q_{2i}, q_{2i+1}] at position m  →  R(m θ_i) · [q_{2i}, q_{2i+1}]
```

Because rotations compose, `⟨R(mθ) q, R(nθ) k⟩ = ⟨q, R((n−m)θ) k⟩`: the attention score depends only on the **relative** offset `m − n`. Your week-2 test checks exactly this numerically. Two memory layouts exist (interleaved pairs vs "rotate half"); weights trained with one are wrong with the other — a classic bug when loading checkpoints.

### GQA / MQA

- **MHA:** `h` query heads, `h` K/V heads.
- **MQA:** `h` query heads share **1** K/V head.
- **GQA:** `h` query heads share `n_kv` K/V heads (`h / n_kv` queries per group).

Why it matters: during decoding you re-read the whole KV cache for every token, so KV bytes are the bottleneck (week 4, week 11). KV bytes/token = `2 · L · n_kv · d_h · bytes_per_elem`. For Llama-3-8B (L=32, h=32, n_kv=8, d_h=128, bf16) GQA gives 128 KiB/token instead of 512 KiB with MHA — a 4× smaller cache, so ~4× more concurrent sequences.

### Encoder vs decoder vs encoder-decoder

| | Attention mask | Typical objective | Used for in 2026 |
|---|---|---|---|
| Encoder-only (BERT) | bidirectional | masked LM | embedding models, rerankers, classifiers |
| Decoder-only (GPT, Llama, Qwen) | causal | next-token prediction | LLMs, VLM language backbones |
| Encoder-decoder (T5, Whisper) | encoder bidirectional + decoder causal + cross-attention | seq2seq | speech recognition, translation |

Decoder-only won for LLMs because one objective (next token) on all text scales simply, every token is a training signal, and generation, in-context learning and KV caching fit naturally.

### Mixture of Experts (week 4)

Replace the FFN with `E` expert FFNs and a router `g(x) = softmax(W_r x)`; send each token to its top-k experts and sum their outputs weighted by the router probabilities. Total parameters grow with `E`, **active** parameters (and FLOPs per token) grow only with `k`. Without an auxiliary **load-balancing loss** (e.g. Switch: `α · E · Σ_i f_i · P_i`, with `f_i` = fraction of tokens routed to expert i and `P_i` = mean router probability for i), the router collapses onto a few experts.

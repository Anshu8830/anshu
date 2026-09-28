# 8. Skill checkpoints

After each phase: close the laptop, set a timer, and do the checkpoint **without tutorials, docs or AI assistants**. Explain out loud (or on paper) and then build. Mark each item ✅ / 🟡 / ❌ in the tracker's *Summary → self-rating* column. Anything 🟡/❌ goes into the next Sunday's catch-up slot.

Format for each phase: **Explain** (you can teach it to a colleague, with equations/numbers) and **Build** (you can write it from a blank file in the stated time).

---

## Phase 0 — ML/DL revision (diagnostic, Mon 28 Sep)

The 10-question diagnostic is in [02-prerequisite-assessment.md](02-prerequisite-assessment.md#diagnostic-self-test-mon-28-sep-60-minutes-close-book). Re-take it on Wed 30 Sep.
- **Explain:** MLE → cross-entropy; AdamW vs Adam+L2; why warmup; double descent; calibration.
- **Build (45 min):** manual backward of Linear → LayerNorm → GELU → Linear → softmax-CE, verified with `gradcheck`.

## Phase 1 — Transformers (end of W2; MoE end of W4)
- **Explain:**
  - every tensor shape in multi-head attention, and why softmax is over the key dimension;
  - √d_k scaling (variance argument); causal vs padding masks;
  - pre-norm vs post-norm; RMSNorm vs LayerNorm; SwiGLU parameter budget;
  - RoPE: the rotation and the relative-position property; the two memory layouts;
  - MHA vs GQA vs MQA and the KV-cache bytes formula;
  - encoder-only vs decoder-only vs encoder-decoder, and where each is used today;
  - MoE routing, top-k, load-balancing loss, total vs active parameters.
- **Build (90 min):** a Llama-style decoder block (RMSNorm, RoPE, GQA, SwiGLU) with a causal-leakage test and a parameter-count test.

## Phase 2 — LLMs & language modeling (end of W4)
- **Explain:**
  - byte-level BPE training and encoding; vocabulary-size trade-offs; why tokenization causes arithmetic/spelling failures;
  - next-token prediction, cross-entropy, teacher forcing, exposure bias, perplexity, bits-per-byte;
  - the full "prompt → next token" path including chat template, prefill, decode and sampling (concept note 2);
  - KV-cache memory for a given model and context; why decode is memory-bound;
  - temperature, top-k, top-p, min-p, beam search — and when each is appropriate;
  - Kaplan vs Chinchilla; C ≈ 6ND; tokens-per-parameter heuristic and why modern small models are trained far past it.
- **Build (2 h):** a BPE trainer + encoder/decoder on a text file; a training loop with warmup+cosine AdamW; KV-cache generation with top-p sampling.

## Phase 3 — Embeddings & IR (end of W5)
- **Explain:** cosine vs dot vs L2 and normalization; InfoNCE and in-batch/hard negatives; bi-encoder vs cross-encoder vs late interaction; every term of BM25; IVF, PQ with ADC, HNSW search/build and their knobs; filtering in vector DBs; Recall@K, MRR, nDCG.
- **Build (2 h):** BM25 with an inverted index + IVF-PQ in NumPy + an nDCG@10 evaluator on a small labelled set.

## Phase 4 — RAG (end of W6)
- **Explain:** each pipeline stage, the failure it fixes and the failure it can cause (concept note 4 table); HyDE; parent-child; contextual retrieval; RRF; lost-in-the-middle; agentic vs graph RAG; RAG vs long context for a given scenario.
- **Build (2 h):** hybrid retrieval + RRF + cross-encoder rerank + cited generation with abstention over a folder of documents.

## Phase 5 — LLM evaluation (end of W7)
- **Explain:** error analysis → taxonomy → golden set; faithfulness vs correctness vs relevance; judge biases and calibration (κ, TPR/TNR); bootstrap and paired tests; A/B test design; regression gates; agent evals (outcome vs trajectory, pass^k, tool-call metrics).
- **Build (90 min):** a faithfulness metric via claim decomposition + a paired-bootstrap comparison of two systems with a CI.

## Phase 6 — Fine-tuning & post-training (end of W9)
- **Explain:** pretraining vs continued pretraining vs SFT; chat templates and loss masking; LoRA math, init and α/r; QLoRA (NF4, double quant, paged optimizers); when to fine-tune vs RAG vs prompt; the DPO derivation; ORPO/KTO/SimPO in one sentence each.
- **Build (2 h):** SFT loop with assistant-only masking on a small model; a `LoRALinear` module; the DPO loss with a unit test.

## Phase 7 — AI agents (end of W10)
- **Explain:** the agent loop and how tool results re-enter context; ReAct; plan-and-execute; reflection with verifiers; short- vs long-term memory and compaction; multi-agent orchestration trade-offs; human-in-the-loop placement; prompt injection, the lethal trifecta and least-privilege tools; how LangGraph (StateGraph, reducers, checkpointer, `interrupt()`) and LangChain (`create_agent`, middleware) map onto your raw loop; when not to use a framework.
- **Build (2 h):** a framework-free agent with 3 tools, max-steps, retries, an approval gate and a trajectory log; then the same flow as a LangGraph graph.

## Phase 8 — MCP (end of W10)
- **Explain:** hosts, clients, servers; tools vs resources vs prompts; stdio vs Streamable HTTP; what the 2026-07-28 stateless core changed and what was deprecated; authorization flow for HTTP servers; tool-description design.
- **Build (60 min):** an MCP server with one tool, one resource and one prompt, tested with the MCP Inspector and called from your agent.

## Phase 9 — Inference & GPU optimization (end of W11)
- **Explain:** SMs, warps, Tensor Cores, HBM vs SRAM; roofline and arithmetic intensity with numbers for matmul and decode; compute- vs memory- vs overhead-bound; kernel fusion; FlashAttention's online softmax and why it is faster; PagedAttention, continuous batching, prefix caching, chunked prefill; TTFT/TPOT/throughput/goodput; FP16/BF16/FP8/INT8/INT4, GPTQ, AWQ; speculative decoding's acceptance rule and expected speedup; vLLM vs TensorRT-LLM.
- **Build (90 min):** a roofline calculator for a given model/GPU/batch; tiled online-softmax attention that matches naive attention.

## Phase 10 — Multimodal (end of W12)
- **Explain:** patches → tokens (ViT); CLIP's symmetric contrastive loss; how a VLM projects vision features into the LM's embedding space and its training stages; OCR-based vs OCR-free document retrieval (ColPali); Whisper as an encoder-decoder; how you would handle video.
- **Build (90 min):** CLIP-style zero-shot classifier + a page-image retriever answering a question about a chart.

## Phase 11 — Advanced training (end of W12)
- **Explain:** 16-bytes/param training memory; activation checkpointing; DDP vs ZeRO-1/2/3/FSDP; tensor, pipeline, sequence/context and expert parallelism and their communication patterns; data pipeline stages (extraction, filtering, dedup, mixing, synthetic data) and why each matters.
- **Build (45 min):** a memory calculator and a written parallelism plan for 70B on 64 GPUs.

## Phase 12 — RL for AI (end of W9)
- **Explain:** MDP view of generation; return, value, advantage; the policy-gradient theorem and baselines; actor-critic and GAE; PPO's clip; the RLHF objective with KL; RLVR; GRPO's group advantage and its known biases (Dr. GRPO, DAPO); reward hacking with examples; how RL connects to test-time compute in reasoning models.
- **Build (90 min):** REINFORCE with baseline on a toy LM reward; the GRPO loss with unit tests on synthetic data.

## Phase 13 — Research skills (continuous; final check W14)
- **Explain:** for any paper on the list — the problem, the key idea in three sentences, the one equation, the main evidence and its weaknesses.
- **Build:** given a new (post-2025) LLM paper, in **one day**: a 1-page note, a minimal implementation of its core idea, and the smallest experiment that could falsify it.
- **Portfolio evidence by 31 Dec:** ~15 paper notes, 6 reproductions with plots, public project READMEs.

## Capstone (W14)
See the acceptance criteria in [09-capstone-ai-software-engineer.md](09-capstone-ai-software-engineer.md#acceptance-criteria-31-dec).

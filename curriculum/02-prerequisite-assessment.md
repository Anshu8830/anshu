# 2. Prerequisite assessment — what you can skip

Your stated background: strong software/backend/infra/DevOps engineering, intermediate ML and DL, working Python and PyTorch. This page turns that into concrete decisions.

## Skip entirely (0 hours)

| Area | Why you can skip | Where it reappears (as a tool, not a topic) |
|---|---|---|
| Software engineering, testing, code review | Core strength | Every project ships with tests; the capstone *is* a software-engineering agent |
| Backend / APIs (FastAPI, async, streaming) | Core strength | RAG and agent services (W6, W10) |
| Cloud, infra, DevOps, Docker, Kubernetes | Core strength | Sandboxed code execution (W10, capstone), GPU rentals |
| Databases | Core strength | Only pgvector's ANN indexes are new (W5) |
| CI/CD | Core strength | Eval regression gates (W7), capstone CI |
| Python | Core strength | — |
| Classical ML algorithms (trees, SVMs, clustering) | Not on the critical path to LLM engineering | k-means reappears inside IVF/PQ (W5) — you implement it there |

## Quick revision only (Phase 0: Mon 28 – Wed 30 Sep, ~10 h)

Do the diagnostic first (below). Anything you answer confidently in under two minutes is skipped.

| Topic | What exactly to revise | Resource (primary) | Exercise |
|---|---|---|---|
| Probability → loss functions | MLE ⇒ cross-entropy / NLL; softmax as a categorical distribution; KL divergence | [UDL ch. 5](https://udlbook.github.io/udlbook/) | Derive cross-entropy from MLE for a categorical output |
| Linear algebra | Matrix calculus for backprop; rank / low-rank factorization (needed for LoRA in W8) | [Matrix Calculus for DL](https://explained.ai/matrix-calculus/) | Derive `∂L/∂W` for `y = xW` with batch dims |
| Optimization | SGD + momentum, Adam vs AdamW (decoupled weight decay), warmup + cosine schedules, gradient clipping | [UDL ch. 6–7](https://udlbook.github.io/udlbook/) | Implement AdamW; match `torch.optim.AdamW` to 1e-6 |
| Backpropagation | Manual backward for softmax-CE, Linear, LayerNorm, GELU | [Karpathy: Backprop Ninja](https://www.youtube.com/watch?v=q8SA3rM6ckI) (only if the diagnostic fails) | Manual backward of a 2-layer MLP with LayerNorm, checked with `gradcheck` |
| Bias/variance, regularization | Double descent; weight decay, dropout, early stopping — why LLMs are trained very differently (often < 1 epoch) | [UDL ch. 8–9](https://udlbook.github.io/udlbook/) | — |
| Evaluation | Train/val/test hygiene, leakage, P/R/F1, ROC-AUC vs PR-AUC, calibration (ECE) | [UDL](https://udlbook.github.io/udlbook/) | Implement ECE |
| PyTorch | einops, autograd internals, memory/FLOP accounting, profiler basics | [CS336 L2 trace](https://cs336.stanford.edu/lectures/?trace=lecture_02) | FLOPs + memory of a 1B model incl. Adam states |
| Neural networks / CNNs | Only as a contrast for ViT (patch embedding is a strided conv) | revisited in W12 | — |

Videos: only the Backprop Ninja video (1h55m) is recommended, and only if you fail the backprop items. No beginner courses.

## Diagnostic self-test (Mon 28 Sep, 60 minutes, close-book)

Answer on paper. Mark each ✅ (confident), 🟡 (shaky), ❌ (can't). Revise only 🟡/❌ items.

1. Derive `∂L/∂z = softmax(z) − y` for cross-entropy on logits z.
2. Write the backward pass of LayerNorm (in terms of the normalized input).
3. Write the AdamW update, including bias correction, and explain how it differs from Adam + L2.
4. Why does a linear warmup help Transformers train? What goes wrong without it?
5. A model has 1B parameters. How many bytes for weights, gradients and Adam states in mixed precision?
6. FLOPs of a `(B, T, d) @ (d, 4d)` matmul.
7. What is double descent, and why doesn't classic bias/variance intuition predict LLM behaviour?
8. PR-AUC vs ROC-AUC — which do you report for a 1%-positive retrieval-style problem, and why?
9. What does `torch.no_grad()` change vs `model.eval()`?
10. Explain what `x.view(B, T, h, d//h).transpose(1, 2)` does to memory layout and when you need `.contiguous()`.

Score ≥ 8 ✅: do the AdamW exercise and move straight to attention on Tuesday (you gain 1.5 days — spend them on CS336 A1 early).

## Mapping your strengths onto the new material

| You already know | Maps to | Advantage |
|---|---|---|
| Latency/throughput, queueing, p99s | TTFT / TPOT / goodput, continuous batching | You will find W11 intuitive; focus on the GPU side |
| Virtual memory / paging | PagedAttention | Same idea, applied to the KV cache |
| Caching | KV cache, prefix caching, prompt caching | Same trade-offs: memory vs recompute |
| Indexes (B-trees, inverted indexes) | BM25 inverted index, HNSW, IVF | Algorithms differ, engineering intuition transfers |
| Distributed systems, collectives | DDP/FSDP/TP/PP communication | You mainly need the memory math |
| Testing & CI | Eval harnesses, regression gates | Evals *are* tests for stochastic systems |
| Sandboxing, least privilege | Agent security, tool permissions | Direct transfer — most agent security is classic security |

The genuinely new parts for you are the **math of models and training**, **ML research literacy**, and **GPU performance reasoning**. That is where the hours go.

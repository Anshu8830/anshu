# 3. Month-by-month plan (adjusted to a 28 September 2026 start)

Hours assume 3.5 h Mon–Fri + 4 h Saturday. Day-level detail is in [04-week-by-week.md](04-week-by-week.md) and the Excel tracker.

---

## Late September (Mon 28 – Wed 30 Sep) — Phase 0, ~10 h

- **Theme:** targeted revision driven by a diagnostic, not a course.
- **Do:** diagnostic self-test → AdamW from scratch → manual backprop (Linear/LayerNorm/GELU/softmax-CE) → PyTorch resource accounting (CS336 L2).
- **Exit criteria:** you can derive softmax-CE and LayerNorm gradients and compute memory/FLOPs for a 1B model without notes.

## October — Transformers and language models from scratch (W1 Thu – W5), ~97 h

| Week | Dates | Focus | Output |
|---|---|---|---|
| W1 (Thu–Sat) | 1–3 Oct | Attention from first principles | **P1** attention module + tests |
| W2 | 5–10 Oct | Llama-style block: RMSNorm, SwiGLU, RoPE, GQA; encoder-decoder | **P2** Transformer |
| W3 | 12–17 Oct | BPE tokenizer, training loop, train on TinyStories (CS336 A1) | **P3** part 1, reproduction #1 |
| W4 | 19–24 Oct | KV cache, sampling, inference arithmetic, scaling laws, MoE | **P3** part 2, reproduction #2 |
| W5 | 26–31 Oct | Embeddings, BM25, IVF-PQ, HNSW, IR metrics | **P4** retrieval engine, reproduction #3 |

- **Primary resources:** Karpathy (build intuition in code), CS336 Spring 2026 lectures + Assignment 1 test suite, concept notes 1–3, IR book + Pinecone FAISS series.
- **Papers:** Attention Is All You Need, GPT-1/2/3, BERT, RMSNorm, GLU variants, Pre-LN, RoFormer, MQA, GQA, BPE, SentencePiece, nucleus sampling, Kaplan, Chinchilla, Switch, Mixtral, InfoNCE/CPC, SBERT, DPR, BEIR, PQ, HNSW.
- **Exit criteria (31 Oct):** a GPT you wrote, trained on a tokenizer you wrote, generating text with a KV cache you wrote; you can explain "prompt → next token" with real numbers; your retrieval engine matches published BM25 numbers on SciFact.

## November — Applications, evaluation and post-training (W6 – W9), ~86 h

| Week | Dates | Focus | Output |
|---|---|---|---|
| W6 | 2–7 Nov | RAG basic → advanced → agentic/graph; framework mapping | **P5** advanced RAG |
| W7 | 9–14 Nov | Error analysis, golden sets, calibrated judges, RAG metrics, statistics, agent evals | **P6** eval framework |
| W8 | 16–21 Nov | SFT from scratch, chat templates, LoRA from scratch, QLoRA on 8B | **P7** part 1, reproduction #4 |
| W9 | 23–28 Nov | Policy gradients, PPO/RLHF, DPO, RLVR/GRPO, reward hacking | **P7** part 2, reproduction #5 |

- **Primary resources:** Anthropic Contextual Retrieval, Clavié talk, Kiela CS25 lecture; Hamel Husain's eval guides + Anthropic agent-evals post; HF LLM Course ch. 11–12, CS336 lectures 15–16, "LoRA Without Regret"; Spinning Up + Lambert's RLHF book.
- **Compute:** first real GPU spend — ~10–20 GPU-hours on a rented 24–80 GB GPU (QLoRA on 8B, GRPO on a 0.6–1.5B model).
- **Exit criteria (28 Nov):** every change to your RAG system is judged by a harness with confidence intervals; you have an adapter you trained, DPO and GRPO runs using your own loss implementations, and you can derive DPO on a whiteboard.

## December — Agents, systems, multimodal and the capstone (W10 – W14), ~97 h

| Week | Dates | Focus | Output |
|---|---|---|---|
| W10 | 30 Nov – 5 Dec | Agents from first principles → LangChain/LangGraph → MCP | **P8** research agent, **P9** MCP server |
| W11 | 7–12 Dec | GPU architecture, rooflines, Triton basics, FlashAttention, vLLM, quantization, speculative decoding | **P10** vLLM report, reproduction #6 |
| W12 | 14–19 Dec | Distributed training & data (working knowledge); ViT, CLIP, VLMs, documents, audio | **P11** multimodal RAG |
| W13 | 21–26 Dec | Capstone integration (25 Dec = buffer) | Capstone M1–M5 |
| W14 | 28–31 Dec | Capstone hardening, final close-book assessment, 2027 plan | Capstone v1 + portfolio |

- **Primary resources:** Anthropic agent/context/tool posts, MCP 2026-07-28 spec, LangChain Academy "Intro to LangGraph"; Modal GPU Glossary, Google DeepMind scaling book, Horace He, Gordić "Inside vLLM"; Ultra-Scale Playbook; Raschka's multimodal article, nanoVLM, ColPali; mini-swe-agent, SWE-bench.
- **Compute:** ~10–20 GPU-hours (vLLM benchmarks, nanoVLM, ColPali indexing, capstone evals) plus API costs for the capstone's frontier-model tier.
- **Exit criteria (31 Dec):** capstone v1 resolves a measured fraction of real issues in your own repos and a SWE-bench subset, under human approval, with an eval report; you pass every phase checkpoint close-book.

## January → June 2027 (continuation)

| Month | Focus |
|---|---|
| January | Capstone v2; CS336 A2 (Triton FlashAttention-2, DDP, sharded optimizer) |
| February | CS336 A3 (scaling) + A4 (data pipeline); full paper reproduction #1 |
| March | CS336 A5 (GRPO on OLMo-2 1B) + RL at scale; choose a specialization track |
| April–June | Specialization track (research engineer / LLM systems / AI architect / frontier-model engineer) |

Details: [10-2027-continuation.md](10-2027-continuation.md).

## Buffers and slippage rules

- **Sunday** is rest. Use it for catch-up at most twice a month.
- If you fall more than **one day behind**, cut in this order: SECONDARY reading → optional videos → the "stretch" parts of a coding task. Never cut the project deliverable or the checkpoint.
- If you fall more than **one week behind** by mid-November, move W12's multimodal half into January and keep the capstone dates.
- The Excel tracker's Summary sheet shows *ahead/behind* against today's date automatically.

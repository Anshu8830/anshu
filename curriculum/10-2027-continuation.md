# 10. 2027 continuation plan

2026 gives you breadth with real depth in the core. 2027 converts it into a specialization. **Q1 is common to all tracks** (it finishes the deferred items); **Q2 onward** you pick one primary track and one secondary.

---

## Q1 2027 (January – March): finish the deferred core

| Weeks | Focus | Primary resource | Output |
|---|---|---|---|
| Jan W1–W2 | Capstone v2: full SWE-bench Verified run, error analysis, RL-ready task environment | [SWE-bench](https://github.com/SWE-bench/SWE-bench) | Public write-up with results |
| Jan W3–W5 | **CS336 Assignment 2 (Systems):** profiling, FlashAttention-2 forward/backward in Triton, DDP, optimizer-state sharding | [assignment2-systems](https://github.com/stanford-cs336/assignment2-systems), [FlashAttention-2 paper](https://arxiv.org/abs/2307.08691), [Umar Jamil FA in Triton](https://www.youtube.com/watch?v=zy8ChVd_oTM) | Your own Triton FA2 benchmarked vs PyTorch SDPA |
| Feb W1–W2 | **CS336 Assignment 3 (Scaling laws):** IsoFLOP study, fitting, extrapolation | [assignment3-scaling](https://github.com/stanford-cs336/assignment3-scaling) | Scaling-law report |
| Feb W3–W4 | **CS336 Assignment 4 (Data):** Common Crawl extraction, quality/toxicity filtering, dedup (MinHash), PII | [assignment4-data](https://github.com/stanford-cs336/assignment4-data), [FineWeb](https://arxiv.org/abs/2406.17557) | Filtered dataset + ablation |
| Mar W1–W3 | **CS336 Assignment 5 (Alignment & reasoning RL):** GRPO on OLMo-2 1B with vLLM rollouts; optional SFT/DPO supplement | [assignment5-alignment](https://github.com/stanford-cs336/assignment5-alignment), [RLHF Book](https://rlhfbook.com/) | Reasoning-RL report |
| Mar W4 | Distributed training hands-on: implement TP and PP by reading/extending picotron; 2–8 GPU runs | [picotron](https://github.com/huggingface/picotron), [Ultra-Scale Playbook](https://huggingface.co/spaces/nanotron/ultrascale-playbook) | TP/PP from scratch at small scale |

Throughout Q1: one full paper reproduction (pick a 2026 paper with public code and a claim testable on ≤ 8 GPUs), written up publicly.

---

## Q2 2027 onward: pick a track

### Track A — AI research engineer
*Goal: run experiments that produce new knowledge; co-author papers.*
- **Learn:** experimental design and ablation discipline at scale; μP / hyperparameter transfer; optimizer research (AdamW variants, second-order-ish methods); interpretability basics (probing, sparse autoencoders); long-context methods (YaRN, ring attention); SSMs / linear attention; evaluation science (contamination, construct validity).
- **Resources:** CS336 (all assignments complete), [How to Scale Your Model](https://jax-ml.github.io/scaling-book/), [Schulman's research guide](http://joschu.net/blog/opinionated-guide-ml-research.html), recent NeurIPS/ICLR/ICML papers in one sub-area.
- **Milestones:** 3 reproductions → 1 original small-scale study (e.g. a data-mixture or RL-reward-design question) → workshop paper or detailed public report → contribute to an open research codebase (OLMo, TRL, nanochat, lm-eval-harness).

### Track B — LLM systems / inference engineer
*Goal: make models fast and cheap in production.*
- **Learn:** CUDA properly (PMPP book chapters + GPU MODE lectures), CUTLASS/CuTe concepts, Triton at depth, NCCL and collectives, FP8/FP4 numerics, vLLM and SGLang internals (scheduler, KV manager, speculative decoding), TensorRT-LLM engines, disaggregated serving, multi-LoRA serving, LLM routers and caches.
- **Resources:** [GPU MODE lectures](https://github.com/gpu-mode/lectures), [GPU Glossary](https://modal.com/gpu-glossary), [vLLM](https://github.com/vllm-project/vllm), [TensorRT-LLM](https://nvidia.github.io/TensorRT-LLM/), [ML Engineering Open Book](https://github.com/stas00/ml-engineering).
- **Milestones:** a custom fused kernel that beats the PyTorch baseline in your P10 stack → a merged PR to vLLM/SGLang (start with docs/tests/benchmarks) → a serving-cost case study with SLO-based goodput.

### Track C — AI architect / applied AI lead
*Goal: design reliable AI systems for real organisations.*
- **Learn:** evaluation-driven development at team scale (annotation workflows, eval ops), guardrails and AI security (red-teaming, OWASP LLM Top 10), governance and data privacy, cost modelling across API vs self-hosted, agent platforms in production (LangGraph deployment, durable execution, MCP gateways and auth), multimodal document pipelines, build-vs-buy decisions.
- **Resources:** [Anthropic engineering posts](https://www.anthropic.com/engineering/building-effective-agents), [Demystifying evals for AI agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents), [OWASP LLM Top 10](https://genai.owasp.org/llm-top-10/), [MCP spec](https://modelcontextprotocol.io/specification/2026-07-28), [LangGraph](https://docs.langchain.com/oss/python/langgraph/overview).
- **Milestones:** reference architectures (RAG platform, agent platform, eval platform) with ADRs → an internal/external talk → lead a production deployment with an eval-gated release process.

### Track D — Frontier-model engineer (pretraining / post-training at scale)
*Goal: work on the teams that train frontier models.*
- **Learn:** large-scale pretraining runs end to end (data → tokenizer → architecture → stability → checkpoints), MoE at scale (expert parallelism, balancing), FP8 training, fault tolerance, large-scale RL infrastructure (async rollouts, verl/OpenRLHF-style systems), reward modelling and RLVR environment design, long-context and multimodal pretraining, safety/alignment techniques (Constitutional AI, RLAIF).
- **Resources:** [DeepSeek-V3 report](https://arxiv.org/abs/2412.19437), [Qwen3 report](https://arxiv.org/abs/2505.09388), [Smol Training Playbook](https://huggingface.co/spaces/HuggingFaceTB/smol-training-playbook), [Ultra-Scale Playbook](https://huggingface.co/spaces/nanotron/ultrascale-playbook), [Tülu 3](https://arxiv.org/abs/2411.15124), [nanochat](https://github.com/karpathy/nanochat).
- **Milestones:** pretrain a ~1B model on a multi-GPU node with your own data pipeline → full post-training stack (SFT → DPO → RLVR) with an open eval suite → public technical report.

---

## Recommended combination for you

Given a strong infrastructure background, **Track B (LLM systems) as primary + Track A or D as secondary** is the highest-leverage path: systems skills are scarce, map directly onto your existing expertise, and are required on every frontier-model team. If you prefer building products and leading teams, choose **Track C primary + Track B secondary**.

## Keeping current (every week, 2 hours)

- Skim new papers on Hugging Face Papers / arXiv in your track; fully read one.
- Re-check the tools you depend on (MCP spec revisions, LangChain/LangGraph releases, vLLM release notes) — this field changes quarterly.
- Keep adding to your paper-notes repo; every quarter, publish one reproduction or technical write-up.

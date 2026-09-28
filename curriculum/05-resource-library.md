# 5. Complete resource library

Every link was checked on 28 September 2026. **PRIMARY** = what you follow; **SECONDARY** = optional alternative; **REFERENCE** = lookup only. The Excel tracker's *Resources* sheet has the same list with the weeks each item is used.

---

## Freshness warnings (read first)

- **Stanford CS336:** use the **Spring 2026** offering ([site](https://cs336.stanford.edu/), [lectures repo](https://github.com/stanford-cs336/lectures), [YouTube playlist](https://www.youtube.com/playlist?list=PLoROMvodv4rMqXOcazWaTUHhq-yembLCV)). The [Spring 2025 archive](https://cs336.stanford.edu/spring2025/) and its [playlist](https://www.youtube.com/playlist?list=PLoROMvodv4rOY23Y0BoGoBGgQ1zmU_MT_) are fine fallbacks, but the 2026 Assignment 5 is GRPO-first. The assignment repos (`stanford-cs336/assignment1-basics` … `assignment5-alignment`) are updated in place — pull the latest.
- **MCP:** the current spec is **2026-07-28** (stateless request/response core; the `initialize` handshake and session header are gone; roots, sampling, logging and the legacy HTTP+SSE transport are deprecated; tasks moved to an extension). Most blog posts, courses and videos — including the Hugging Face and DeepLearning.AI MCP courses — were written against the 2025 revisions. Learn concepts from them, check wire-level details against the [2026-07-28 spec](https://modelcontextprotocol.io/specification/2026-07-28) and the [release notes](https://blog.modelcontextprotocol.io/posts/2026-07-28/).
- **LangChain:** anything written before LangChain **1.0** (October 2025) that uses `AgentExecutor`, `initialize_agent` or LCEL-heavy agent chains is outdated. Current agents use `create_agent` (built on LangGraph) with middleware; docs moved to `docs.langchain.com`.
- **Moved docs:** Unsloth docs now live at `unsloth.ai/docs`; LlamaIndex at `developers.llamaindex.ai`; the Hugging Face Evaluation Guidebook's maintained version is the `OpenEvals` Space, not the GitHub repo.
- **Karpathy's GPT videos** build GPT-2-era blocks (LayerNorm, learned absolute positions, GELU MLP). Build them, then replace with RMSNorm, RoPE, SwiGLU and GQA in week 2 — that replacement is the point.
- **Hardware numbers** in blog posts age fast; reason with the ratios (FLOP/byte), not the absolute figures.

---

## Courses

| Tier | Course | Use it for | Weeks |
|---|---|---|---|
| PRIMARY | [Stanford CS336: Language Modeling from Scratch (Spring 2026)](https://cs336.stanford.edu/) — [lectures](https://github.com/stanford-cs336/lectures), [videos](https://www.youtube.com/playlist?list=PLoROMvodv4rMqXOcazWaTUHhq-yembLCV), [A1](https://github.com/stanford-cs336/assignment1-basics), [A2](https://github.com/stanford-cs336/assignment2-systems), [A3](https://github.com/stanford-cs336/assignment3-scaling), [A4](https://github.com/stanford-cs336/assignment4-data), [A5](https://github.com/stanford-cs336/assignment5-alignment) | Tokenization, architectures, training, GPUs, parallelism, scaling laws, inference, evaluation, data, post-training/RLVR | W1–W12 (A1 in W3; A2–A5 in 2027) |
| PRIMARY | [Karpathy — Neural Networks: Zero to Hero](https://karpathy.ai/zero-to-hero.html) (selected lectures only) | Building intuition in code: backprop, GPT, tokenizer | W1–W3 |
| PRIMARY | [Hugging Face LLM Course — ch. 11 (SFT/LoRA)](https://huggingface.co/learn/llm-course/chapter11/1) and [ch. 12 (reasoning/GRPO)](https://huggingface.co/learn/llm-course/chapter12) | Practical fine-tuning with TRL | W8–W9 |
| SECONDARY | [LangChain Academy — Introduction to LangGraph](https://academy.langchain.com/courses/intro-to-langgraph) (free) | LangGraph state, persistence, human-in-the-loop | W10 |
| SECONDARY | [Hugging Face MCP Course](https://huggingface.co/learn/mcp-course/en/unit0/introduction) | MCP concepts + building servers (2025-era spec) | W10 |
| SECONDARY | [Hugging Face Agents Course](https://huggingface.co/learn/agents-course/en/unit0/introduction) (incl. [LangGraph unit](https://huggingface.co/learn/agents-course/unit2/langgraph/introduction)) | smolagents / LlamaIndex / LangGraph side by side | W10 |
| SECONDARY | [DeepLearning.AI — Agentic AI (Andrew Ng)](https://www.deeplearning.ai/courses/agentic-ai) | Framework-free agent design patterns (reflection, tools, planning, multi-agent) | W10 |
| SECONDARY | [DeepLearning.AI — MCP: Build Rich-Context AI Apps with Anthropic](https://www.deeplearning.ai/courses/mcp-build-rich-context-ai-apps-with-anthropic) | Hands-on MCP client/server | W10 |
| SECONDARY | [smol-course (Hugging Face)](https://github.com/huggingface/smol-course) | Small-model SFT, preference alignment, eval | W8 |
| SECONDARY | [Foundations of Deep RL — Pieter Abbeel (6 lectures)](https://www.youtube.com/playlist?list=PLwRJQ4m4UJjNymuBM9RdmB3Z9N5-0IlY0) | Compact RL theory (L3 policy gradients, L4 TRPO/PPO) | W9 |
| REFERENCE | [HF Community Computer Vision Course](https://huggingface.co/learn/computer-vision-course/en/unit0/welcome/welcome) | ViT, CLIP units | W12 |
| REFERENCE | [HF Audio Course](https://huggingface.co/learn/audio-course/en/chapter6/introduction) | ASR/TTS | W12 |

## Books and long-form guides (all free online unless noted)

| Tier | Book / guide | Use it for |
|---|---|---|
| PRIMARY | [Understanding Deep Learning — Simon Prince](https://udlbook.github.io/udlbook/) | Phase 0 revision (ch. 5–9); transformer and RL chapters as reference |
| PRIMARY | [How to Scale Your Model — Google DeepMind](https://jax-ml.github.io/scaling-book/) | Rooflines, transformer math, parallelism (TPU-flavoured but general) |
| PRIMARY | [The Ultra-Scale Playbook — Hugging Face](https://huggingface.co/spaces/nanotron/ultrascale-playbook) | DP/ZeRO/TP/PP/CP with measurements |
| PRIMARY | [RLHF Book — Nathan Lambert](https://rlhfbook.com/) (print edition by Manning) | Reward models, PPO, DPO, RLVR, post-training practice |
| PRIMARY | [Introduction to Information Retrieval — Manning, Raghavan, Schütze](https://nlp.stanford.edu/IR-book/) | TF-IDF, BM25, evaluation |
| PRIMARY | [OpenAI Spinning Up in Deep RL](https://spinningup.openai.com/en/latest/) | RL concepts and policy-gradient derivations |
| SECONDARY | [Build a Large Language Model (From Scratch) — Raschka (code)](https://github.com/rasbt/LLMs-from-scratch) | Alternative GPT-from-scratch walkthrough |
| SECONDARY | [Build a Reasoning Model (From Scratch) — Raschka (code)](https://github.com/rasbt/reasoning-from-scratch) | Inference-time scaling, RL, distillation on Qwen3 |
| SECONDARY | [The Smol Training Playbook — Hugging Face](https://huggingface.co/spaces/HuggingFaceTB/smol-training-playbook) | How a real 3B model was trained end-to-end |
| SECONDARY | [LLM Evaluation Guidebook — Hugging Face](https://huggingface.co/spaces/OpenEvals/evaluation-guidebook) | Benchmark design and pitfalls |
| REFERENCE | [Machine Learning Engineering Open Book — Stas Bekman](https://github.com/stas00/ml-engineering) | Training infrastructure, debugging at scale |
| REFERENCE | [The Matrix Calculus You Need for Deep Learning](https://explained.ai/matrix-calculus/) | Backprop derivations |

## Articles and blog posts

| Topic | Tier | Link |
|---|---|---|
| Transformer | PRIMARY | [The Illustrated Transformer — Jay Alammar](https://jalammar.github.io/illustrated-transformer/) |
| Transformer | SECONDARY | [The Annotated Transformer — Harvard NLP](https://nlp.seas.harvard.edu/annotated-transformer/) |
| Architectures | PRIMARY | [The Big LLM Architecture Comparison — Raschka (updated 2026)](https://magazine.sebastianraschka.com/p/the-big-llm-architecture-comparison) |
| Inference | PRIMARY | [LLM Visualization — Brendan Bycroft](https://bbycroft.net/llm) |
| Inference | PRIMARY | [Transformer Inference Arithmetic — kipply](https://kipply.github.io/blog/transformer-inference-arithmetic/) |
| MoE | PRIMARY | [A Visual Guide to Mixture of Experts — Grootendorst](https://newsletter.maartengrootendorst.com/p/a-visual-guide-to-mixture-of-experts) |
| Quantization | PRIMARY | [A Visual Guide to Quantization — Grootendorst](https://newsletter.maartengrootendorst.com/p/a-visual-guide-to-quantization) |
| Vector search | PRIMARY | [Faiss: The Missing Manual — Pinecone](https://www.pinecone.io/learn/series/faiss/) ([PQ](https://www.pinecone.io/learn/series/faiss/product-quantization/), [HNSW](https://www.pinecone.io/learn/series/faiss/hnsw/)) |
| RAG | PRIMARY | [Introducing Contextual Retrieval — Anthropic](https://www.anthropic.com/news/contextual-retrieval) |
| RAG | SECONDARY | [Beyond the Basics of RAG — Ben Clavié (notes)](https://parlance-labs.com/education/rag/ben.html) |
| Evals | PRIMARY | [Your AI Product Needs Evals — Hamel Husain](https://hamel.dev/blog/posts/evals/) |
| Evals | PRIMARY | [Using LLM-as-a-Judge: A Complete Guide — Hamel Husain](https://hamel.dev/blog/posts/llm-judge/) |
| Evals | SECONDARY | [Evaluating the Effectiveness of LLM-Evaluators — Eugene Yan](https://eugeneyan.com/writing/llm-evaluators/) |
| Agent evals | PRIMARY | [Demystifying evals for AI agents — Anthropic](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents) |
| Fine-tuning | PRIMARY | [LoRA Without Regret — Thinking Machines](https://thinkingmachines.ai/blog/lora/) |
| RL | SECONDARY | [Reward Hacking in RL — Lilian Weng](https://lilianweng.github.io/posts/2024-11-28-reward-hacking/) |
| Reasoning | SECONDARY | [Why We Think — Lilian Weng](https://lilianweng.github.io/posts/2025-05-01-thinking/) |
| Agents | PRIMARY | [Building effective agents — Anthropic](https://www.anthropic.com/engineering/building-effective-agents) |
| Agents | PRIMARY | [Effective context engineering for AI agents — Anthropic](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents) |
| Agents | SECONDARY | [Writing effective tools for agents — Anthropic](https://www.anthropic.com/engineering/writing-tools-for-agents) |
| Agents | SECONDARY | [How we built our multi-agent research system — Anthropic](https://www.anthropic.com/engineering/multi-agent-research-system) |
| Agents | SECONDARY | [LLM Powered Autonomous Agents — Lilian Weng](https://lilianweng.github.io/posts/2023-06-23-agent/) |
| Agent security | PRIMARY | [The lethal trifecta — Simon Willison](https://simonwillison.net/2025/Jun/16/the-lethal-trifecta/) |
| Agent security | REFERENCE | [OWASP Top 10 for LLM Applications](https://genai.owasp.org/llm-top-10/) |
| GPUs | PRIMARY | [GPU Glossary — Modal](https://modal.com/gpu-glossary) |
| GPUs | PRIMARY | [Making Deep Learning Go Brrrr — Horace He](https://horace.io/brrr_intro.html) |
| Serving | PRIMARY | [Inside vLLM — Aleksa Gordić](https://www.aleksagordic.com/blog/vllm) |
| Multimodal | PRIMARY | [Understanding Multimodal LLMs — Raschka](https://magazine.sebastianraschka.com/p/understanding-multimodal-llms) |
| Multimodal | PRIMARY | [Vision Language Models (Better, faster, stronger) — Hugging Face](https://huggingface.co/blog/vlms-2025) |
| Multimodal | SECONDARY | [nanoVLM blog](https://huggingface.co/blog/nanovlm), [ColPali blog](https://huggingface.co/blog/manu/colpali) |
| Code agents | PRIMARY | [Aider repository map](https://aider.chat/docs/repomap.html) |
| Research | PRIMARY | [How to Read a Paper — S. Keshav](http://ccr.sigcomm.org/online/files/p83-keshavA.pdf) |
| Research | PRIMARY | [A Recipe for Training Neural Networks — Karpathy](http://karpathy.github.io/2019/04/25/recipe/) |
| Research | SECONDARY | [An Opinionated Guide to ML Research — John Schulman](http://joschu.net/blog/opinionated-guide-ml-research.html) |

## Videos

Durations are approximate (±10%).

| Video | Instructor / channel | Duration | Why watch | Section |
|---|---|---|---|---|
| [Building makemore Part 4: Becoming a Backprop Ninja](https://www.youtube.com/watch?v=q8SA3rM6ckI) | Andrej Karpathy | 1h55m | Manual gradient flow drill — only if the diagnostic fails | P0 |
| [The spelled-out intro to neural networks and backpropagation: building micrograd](https://www.youtube.com/watch?v=VMj-3S1tku0) | Andrej Karpathy | 2h25m | Optional; autograd from zero | P0 |
| [Transformers, the tech behind LLMs \| DL5](https://www.youtube.com/watch?v=wjZofJX0v4M) | 3Blue1Brown | 27m | Geometric intuition for embeddings and prediction | P1 |
| [Attention in transformers, step-by-step \| DL6](https://www.youtube.com/watch?v=eMlx5fFNoYc) | 3Blue1Brown | 26m | Clearest visual explanation of Q/K/V and masking | P1 |
| [Attention Is All You Need (paper explained)](https://www.youtube.com/watch?v=iDulhoQ2pro) | Yannic Kilcher | ~28m | Paper walk-through; model for how to read papers | P1, P13 |
| [Attention is all you need (Transformer) — model explanation incl. math](https://www.youtube.com/watch?v=bCz4OMemCcA) | Umar Jamil | ~58m | Math-first alternative to the above | P1 |
| [Let's build GPT: from scratch, in code, spelled out](https://www.youtube.com/watch?v=kCc8FmEb1nY) | Andrej Karpathy | 1h56m | Bigram → decoder block in code | P1 |
| [Stanford CS336 Spring 2026 — Lecture 3: Architectures](https://www.youtube.com/watch?v=lVynu4bo1rY) | Tatsu Hashimoto | ~1h20m | Evidence-based survey of modern block design | P1 |
| [LLaMA explained: KV-Cache, RoPE, RMS Norm, GQA, SwiGLU](https://www.youtube.com/watch?v=Mn_9W1nCFLo) | Umar Jamil | ~1h10m | Derivation-level RoPE and GQA | P1 |
| [Coding LLaMA 2 from scratch in PyTorch](https://www.youtube.com/watch?v=oM4VmoabDAI) | Umar Jamil | ~3h | Optional code-along of the full Llama block + KV cache | P1, P2 |
| [Let's build the GPT Tokenizer](https://www.youtube.com/watch?v=zduSFxRajkE) | Andrej Karpathy | 2h13m | Byte-level BPE and its failure modes | P2 |
| [Stanford CS336 Spring 2026 — Lecture 1: Overview, Tokenization](https://www.youtube.com/watch?v=JuoVZkPBiKk) | Percy Liang | ~1h20m | The LM pipeline and tokenizer design space | P2 |
| [Stanford CS336 Spring 2026 — full playlist](https://www.youtube.com/playlist?list=PLoROMvodv4rMqXOcazWaTUHhq-yembLCV) (L4 MoE, L5 GPUs, L6 kernels, L7–8 parallelism, L9/11 scaling, L10 inference, L12 eval, L13–14 data, L15 post-training, L16 RLVR, L17 multimodality) | Liang, Hashimoto | ~1h20m each | The spine for systems, scaling and post-training | P2, P9, P11, P6, P12 |
| [Let's reproduce GPT-2 (124M)](https://www.youtube.com/watch?v=l8pRSuU81PU) | Andrej Karpathy | ~4h | Optional: training-speed engineering (mixed precision, compile, DDP) | P2, P9 |
| [Stanford CS229: Building Large Language Models](https://www.youtube.com/watch?v=9vM4p9NN0Ts) | Yann Dubois | ~1h44m | One-sitting overview of the full LLM stack | P2 |
| [Deep Dive into LLMs like ChatGPT](https://www.youtube.com/watch?v=7xTGNNLPyMI) | Andrej Karpathy | 3h31m | Optional big-picture refresher (general audience) | P2, P6 |
| [HNSW for Vector Search Explained and Implemented with Faiss](https://www.youtube.com/watch?v=QvKMwLjdK-s) | James Briggs | ~35m | Visual HNSW before the paper | P3 |
| [Stanford CS25 V3: Retrieval Augmented Language Models](https://www.youtube.com/watch?v=mE7IDf2SmJg) | Douwe Kiela | 1h19m | Research map of RAG | P4 |
| [Beyond the Basics of Retrieval for Augmenting Generation](https://www.youtube.com/watch?v=0nA5QG3087g) | Ben Clavié | ~1h | Practitioner's retrieval stack + evaluation | P4 |
| [L3 Policy Gradients and Advantage Estimation](https://www.youtube.com/watch?v=AKbX1Zvo7r8) | Pieter Abbeel | ~1h | Rigorous PG derivation (then L4 TRPO/PPO in the playlist) | P12 |
| [RLHF explained with math derivations and the PyTorch code](https://www.youtube.com/watch?v=qGyFrqc34yc) | Umar Jamil | ~2h | PPO-based RLHF with code | P12 |
| [DPO explained: Bradley-Terry model, log probabilities, math](https://www.youtube.com/watch?v=hvGa5Mba4c8) | Umar Jamil | ~50m | DPO derivation line by line | P6 |
| [How We Build Effective Agents](https://www.youtube.com/watch?v=D7_ipDqhtwk) | Barry Zhang (Anthropic) | ~15m | Agent design principles | P7 |
| [FlashAttention — Stanford MLSys #67](https://www.youtube.com/watch?v=gMOAud7hZg4) | Tri Dao | ~1h | IO-aware attention from the author | P9 |
| [Fast LLM Serving with vLLM and PagedAttention](https://www.youtube.com/watch?v=Oq2SN7uutbQ) | vLLM authors | ~30–40m | KV-cache paging and batching | P9 |
| [Speculative Decoding: When Two LLMs are Faster than One](https://www.youtube.com/watch?v=S-8yr_RibJ4) | Efficient NLP | ~12m | Acceptance rule, intuitively | P9 |
| [Flash Attention derived and coded from first principles with Triton](https://www.youtube.com/watch?v=zy8ChVd_oTM) | Umar Jamil | ~7h | 2027 stretch: write FA in Triton | P9 |
| [GPU MODE lectures](https://www.youtube.com/channel/UCJgIbYl6C5no72a0NUAPcTA) ([code/slides](https://github.com/gpu-mode/lectures)) | GPU MODE community | ~1h each | 2027 CUDA/Triton track | P9 |
| [Coding a Multimodal (Vision) Language Model from scratch in PyTorch](https://www.youtube.com/watch?v=vAmKB7iPkWw) ([code](https://github.com/hkproj/pytorch-paligemma)) | Umar Jamil | ~5h45m | How image tokens enter an LM (watch ~2h of it) | P10 |
| [Stanford CS230 Lecture 8 — Career Advice / Reading Research Papers](https://www.youtube.com/watch?v=733m6qBH-jI) | Andrew Ng | ~1h10m | Practical paper-reading strategy | P13 |

## Papers

The full ordered list with prerequisites, sections to read, what to implement and what to reproduce is [07-paper-reading-list.md](07-paper-reading-list.md) (generated; also the *Papers* sheet in Excel).

## GitHub repositories

| Tier | Repo | Why |
|---|---|---|
| PRIMARY | [stanford-cs336/assignment1-basics](https://github.com/stanford-cs336/assignment1-basics) | Tokenizer + LM test suite = your W3 spec |
| PRIMARY | [stanford-cs336/lectures](https://github.com/stanford-cs336/lectures) | Executable lecture traces (2026) |
| PRIMARY | [karpathy/minbpe](https://github.com/karpathy/minbpe) | Reference BPE |
| PRIMARY | [karpathy/nanoGPT](https://github.com/karpathy/nanoGPT), [karpathy/build-nanogpt](https://github.com/karpathy/build-nanogpt) | Reference GPT training |
| SECONDARY | [karpathy/nanochat](https://github.com/karpathy/nanochat) | Full-stack small ChatGPT: pretrain → SFT → RL → serve |
| SECONDARY | [harvardnlp/annotated-transformer](https://github.com/harvardnlp/annotated-transformer) | Encoder-decoder reference |
| PRIMARY | [xhluca/bm25s](https://github.com/xhluca/bm25s) | Fast BM25 to validate yours |
| REFERENCE | [pgvector/pgvector](https://github.com/pgvector/pgvector) | Postgres ANN (HNSW, IVFFlat) |
| PRIMARY | [docling-project/docling](https://github.com/docling-project/docling) | Document parsing (PDF layout, tables) |
| PRIMARY | [illuin-tech/colpali](https://github.com/illuin-tech/colpali) | ColPali / ColQwen visual retrieval |
| PRIMARY | [UKGovernmentBEIS/inspect_ai](https://github.com/UKGovernmentBEIS/inspect_ai) | Eval framework for tasks and agents |
| REFERENCE | [EleutherAI/lm-evaluation-harness](https://github.com/EleutherAI/lm-evaluation-harness) | Standard benchmarks |
| REFERENCE | [sierra-research/tau-bench](https://github.com/sierra-research/tau-bench) | Agent benchmark with state checks |
| PRIMARY | [rasbt/reasoning-from-scratch](https://github.com/rasbt/reasoning-from-scratch) | Reasoning/RL code on Qwen3 |
| PRIMARY | [langchain-ai/langgraph](https://github.com/langchain-ai/langgraph) | Stateful agent graphs |
| SECONDARY | [openai/openai-agents-python](https://github.com/openai/openai-agents-python) | Agents SDK |
| SECONDARY | [huggingface/smolagents](https://github.com/huggingface/smolagents) | Code-as-action agents |
| SECONDARY | [huggingface/mcp-course](https://github.com/huggingface/mcp-course), [huggingface/agents-course](https://github.com/huggingface/agents-course) | Course code |
| PRIMARY | [SWE-agent/mini-swe-agent](https://github.com/SWE-agent/mini-swe-agent) | 100-line coding agent — capstone reference |
| PRIMARY | [SWE-bench/SWE-bench](https://github.com/SWE-bench/SWE-bench) | Capstone evaluation harness |
| PRIMARY | [vllm-project/vllm](https://github.com/vllm-project/vllm) | Serving engine (P10) |
| REFERENCE | [NVIDIA/TensorRT-LLM](https://github.com/NVIDIA/TensorRT-LLM) | NVIDIA's serving stack |
| REFERENCE | [modal-labs/gpu-glossary](https://github.com/modal-labs/gpu-glossary) | Source of the GPU glossary |
| PRIMARY | [huggingface/picotron](https://github.com/huggingface/picotron) | Readable 4D parallelism (2027: implement TP/PP) |
| PRIMARY | [huggingface/nanoVLM](https://github.com/huggingface/nanoVLM) | Readable VLM training |
| SECONDARY | [hkproj/pytorch-paligemma](https://github.com/hkproj/pytorch-paligemma) | VLM from scratch |
| REFERENCE | [natolambert/rlhf-book](https://github.com/natolambert/rlhf-book) | RLHF book source |
| REFERENCE | [jax-ml/scaling-book](https://github.com/jax-ml/scaling-book) | Scaling book source/discussions |

## Documentation

| Tier | Docs | Weeks |
|---|---|---|
| PRIMARY | [Transformers chat templates](https://huggingface.co/docs/transformers/chat_templating) | W8 |
| PRIMARY | [TRL SFTTrainer](https://huggingface.co/docs/trl/sft_trainer) (+ DPO/GRPO trainers in the same docs), [TRL: LoRA without regret](https://huggingface.co/docs/trl/en/lora_without_regret) | W8–W9 |
| PRIMARY | [Unsloth fine-tuning guide](https://unsloth.ai/docs/get-started/fine-tuning-llms-guide) | W8 |
| REFERENCE | [Sentence-Transformers](https://sbert.net/), [Qdrant](https://qdrant.tech/documentation/) | W5 |
| REFERENCE | [Ragas metrics](https://docs.ragas.io/en/stable/concepts/metrics/available_metrics/), [Inspect](https://inspect.aisi.org.uk/), [LangSmith evaluation](https://docs.langchain.com/langsmith/evaluation) | W7, W10 |
| PRIMARY | [MCP specification 2026-07-28](https://modelcontextprotocol.io/specification/2026-07-28) (previous: [2025-11-25](https://modelcontextprotocol.io/specification/2025-11-25)) | W10 |
| PRIMARY | [LangGraph](https://docs.langchain.com/oss/python/langgraph/overview), [LangChain middleware](https://docs.langchain.com/oss/python/langchain/middleware/overview), [create_agent reference](https://reference.langchain.com/python/langchain/agents/factory/create_agent) | W10 |
| SECONDARY | [OpenAI Agents SDK](https://openai.github.io/openai-agents-python/), [smolagents](https://huggingface.co/docs/smolagents), [LlamaIndex](https://developers.llamaindex.ai/python/framework/) ([Workflows](https://developers.llamaindex.ai/python/framework/module_guides/workflow/)) | W6, W10 |
| PRIMARY | [Triton tutorials](https://triton-lang.org/main/getting-started/tutorials/) | W11 |
| PRIMARY | [vLLM docs — prefix caching design](https://docs.vllm.ai/en/stable/design/prefix_caching/) | W11 |
| REFERENCE | [TensorRT-LLM docs](https://nvidia.github.io/TensorRT-LLM/) | W11 |
| REFERENCE | [Docling docs](https://docling-project.github.io/docling/) | W6, W12 |
| REFERENCE | [SWE-bench](https://www.swebench.com/) | W13 |
| REFERENCE | [PyTorch install](https://pytorch.org/get-started/locally/) | W1 |

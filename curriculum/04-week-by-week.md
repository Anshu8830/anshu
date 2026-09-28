# 4. Week-by-week curriculum (28 Sep - 31 Dec 2026)

> Generated from `tools/plan_data.py` + `tools/plan_weeks.py` by `python tools/build.py`. Edit the data files, not this page.

**14 weeks - 82 study days - 290 planned hours** (Mon-Fri 3.5 h, Sat 4.0 h, Sunday = rest/catch-up; 25 Dec is a buffer day).

How to read each week: **PRIMARY** is what you actually follow; **SECONDARY** is an optional alternative explanation if the primary does not click; **REFERENCE** is for lookup only. Every paper is read with the three-pass method and gets a half-page note in your repo (`papers/NN-name.md`).

| Week | Dates | Focus | Phases | Hours | Project |
|---|---|---|---|---|---|
| [W1](#week-1) | Mon 28 Sep - Sat 03 Oct | Diagnostic revision -> attention from scratch | P0 (Mon-Wed), P1 (Thu-Sat) | 21.5 | Project 1 - Attention from scratch |
| [W2](#week-2) | Mon 05 Oct - Sat 10 Oct | The modern Transformer block (Llama-style) + encoder-decoder | P1 | 21.5 | Project 2 - Transformer from scratch |
| [W3](#week-3) | Mon 12 Oct - Sat 17 Oct | Tokenization + training a small GPT (CS336 Assignment 1) | P2 | 21.5 | Project 3 (part 1) - Tokenizer + small GPT |
| [W4](#week-4) | Mon 19 Oct - Sat 24 Oct | Inside inference: KV cache, sampling, scaling laws, MoE | P2 (+ P1 MoE, P11 scaling intro) | 21.5 | Project 3 (part 2) - inference + scaling + MoE |
| [W5](#week-5) | Mon 26 Oct - Sat 31 Oct | Embeddings, contrastive learning and vector search internals | P3 | 21.5 | Project 4 - Embedding & retrieval engine |
| [W6](#week-6) | Mon 02 Nov - Sat 07 Nov | RAG: beginner -> advanced -> research level | P4 | 21.5 | Project 5 - Advanced RAG |
| [W7](#week-7) | Mon 09 Nov - Sat 14 Nov | Evaluation like a professional AI team | P5 (+ P4 metrics) | 21.5 | Project 6 - RAG/LLM evaluation framework |
| [W8](#week-8) | Mon 16 Nov - Sat 21 Nov | Fine-tuning: SFT, chat templates, LoRA and QLoRA | P6 | 21.5 | Project 7 (part 1) - SFT + LoRA/QLoRA |
| [W9](#week-9) | Mon 23 Nov - Sat 28 Nov | RL for LLMs: RLHF, DPO, RLVR/GRPO and reasoning models | P12 + P6 (preference optimization) | 21.5 | Project 7 (part 2) - DPO + GRPO |
| [W10](#week-10) | Mon 30 Nov - Sat 05 Dec | Agents from first principles + MCP | P7, P8 | 21.5 | Project 8 - AI research agent; Project 9 - MCP server |
| [W11](#week-11) | Mon 07 Dec - Sat 12 Dec | GPUs and LLM inference optimization | P9 | 21.5 | Project 10 - Optimize & serve an LLM with vLLM |
| [W12](#week-12) | Mon 14 Dec - Sat 19 Dec | Distributed training & data (working knowledge) + multimodal AI | P11 (Mon-Tue), P10 (Wed-Sat) | 21.5 | Project 11 - Multimodal RAG |
| [W13](#week-13) | Mon 21 Dec - Sat 26 Dec | Capstone build: AI Software Engineer (integration) | CAP | 18 | Capstone milestones M1-M5 |
| [W14](#week-14) | Mon 28 Dec - Thu 31 Dec | Capstone hardening, final assessment, 2027 plan | CAP | 14 | Capstone milestones M6-M8 |

---

<a id="week-1"></a>
## Week 1 - Diagnostic revision -> attention from scratch

**Dates:** Mon 28 Sep - Sat 03 Oct 2026 - **Phases:** P0 (Mon-Wed), P1 (Thu-Sat) - **Planned hours:** 21.5

**Goal.** Close the specific gaps in your ML/DL foundations in three days (not three weeks), then build scaled dot-product and multi-head attention from first principles.

**Learning flow.** Intuition (3Blue1Brown) -> Q/K/V -> equation -> tensor shapes -> PyTorch -> attention-map visualization -> sqrt(d_k) experiment

### Reading
- **PRIMARY:** [Understanding Deep Learning (Prince), ch. 5-9 - targeted revision](https://udlbook.github.io/udlbook/); [CS336 2026 Lecture 2 trace - PyTorch, einops, resource accounting](https://cs336.stanford.edu/lectures/?trace=lecture_02); [Concept note: attention & transformer shapes](concepts/01-attention-and-transformer.md); [The Illustrated Transformer (Alammar)](https://jalammar.github.io/illustrated-transformer/)
- **SECONDARY:** [The Matrix Calculus You Need for Deep Learning](https://explained.ai/matrix-calculus/); [The Annotated Transformer](https://nlp.seas.harvard.edu/annotated-transformer/)
- **REFERENCE:** [How to Read a Paper (Keshav)](http://ccr.sigcomm.org/online/files/p83-keshavA.pdf)

### Videos

| Video | Instructor / channel | Duration | Why watch | Covers |
|---|---|---|---|---|
| [Building makemore Part 4: Becoming a Backprop Ninja](https://www.youtube.com/watch?v=q8SA3rM6ckI) | Andrej Karpathy | 1h55m | Only if the diagnostic shows you can't write a manual backward pass; the best drill for gradient flow. | P0 backprop |
| [Transformers, the tech behind LLMs \| DL5](https://www.youtube.com/watch?v=wjZofJX0v4M) | 3Blue1Brown | 27m | Geometric intuition for embeddings and next-token prediction before any equations. | P1 intuition |
| [Attention in transformers, step-by-step \| DL6](https://www.youtube.com/watch?v=eMlx5fFNoYc) | 3Blue1Brown | 26m | Clearest visual explanation of Q, K, V and why masking exists. | P1 attention |

### Papers

| Paper | Authors (year) | Read carefully | Implement |
|---|---|---|---|
| [How to Read a Paper](http://ccr.sigcomm.org/online/files/p83-keshavA.pdf) | S. Keshav (2007) | Whole paper (2 pages). | A paper-notes template in your repo. |
| [Attention Is All You Need](https://arxiv.org/abs/1706.03762) | Vaswani, Shazeer, Parmar, Uszkoreit, Jones, Gomez, Kaiser, Polosukhin (2017) | 3.1-3.2.3 (attention + multi-head), 3.5 (positional encoding), Table 3 ablations. | Scaled dot-product attention, MHA, sinusoidal PE (P1/P2). |

### Coding exercises

- AdamW from scratch (match torch.optim.AdamW to 1e-6)
- Manual backward for Linear -> LayerNorm -> GELU -> Linear -> softmax-CE; verify with gradcheck
- Scaled dot-product attention with causal + padding masks; compare to F.scaled_dot_product_attention
- MultiHeadAttention (fused QKV) + cross-attention; compare to nn.MultiheadAttention with copied weights

### Project: Project 1 - Attention from scratch

**Deliverable:** `attention.py` + pytest suite (shape, equivalence, no-future-leakage tests) + notebook with attention maps and the sqrt(d_k) ablation

### Knowledge checkpoint (close-book)

- [ ] Write every tensor shape in MHA from input (B,T,d_model) to output without notes.
- [ ] Explain why scores are divided by sqrt(d_k) and show the softmax-entropy plot that proves it.
- [ ] Explain the difference between causal masking and padding masking and where each is applied.
- [ ] State the time and memory complexity of attention in T and d.

### Day by day

| Date | Phase | Type | Task | What to do | Link | h | Output |
|---|---|---|---|---|---|---|---|
| Mon 28 Sep | P0 | Setup | **Workspace + GPU plan** | Create one monorepo for all 2026 projects (uv, pytest, ruff, wandb or tensorboard). Decide compute: Mac/Colab for small runs, rented A10/L4/4090 by the hour for training weeks. | [link](https://pytorch.org/get-started/locally/) | 0.5 | Repo skeleton |
| Mon 28 Sep | P0 | Review | **Diagnostic self-test** | Take the Phase 0 self-test in the checkpoints file. Anything you answer confidently in <2 min is skipped this week. | [link](08-skill-checkpoints.md) | 1 | List of gaps |
| Mon 28 Sep | P0 | Reading | **Probability -> MLE -> cross-entropy; optimizers** | UDL ch. 5 (loss functions as MLE) and ch. 6 (SGD, momentum, Adam). Then implement AdamW from scratch and match PyTorch. | [link](https://udlbook.github.io/udlbook/) | 2 | adamw.py + test |
| Tue 29 Sep | P0 | Video | **Backprop by hand** | Backprop Ninja (skip if diagnostic passed). Exercise: manual backward for Linear->LayerNorm->GELU->Linear->softmax-CE; verify with torch.autograd.gradcheck. | [link](https://www.youtube.com/watch?v=q8SA3rM6ckI) | 2 | manual_backward.py |
| Tue 29 Sep | P0 | Reading | **Matrix calculus refresh** | Parr & Howard sections on vector chain rule + UDL ch. 7. Derive dL/dlogits = softmax - onehot and the LayerNorm backward on paper. | [link](https://explained.ai/matrix-calculus/) | 1.5 | 1-page derivation |
| Wed 30 Sep | P0 | Video | **PyTorch + resource accounting** | CS336 L2 (trace + video in 2026 playlist): tensors, einops, FLOPs and memory accounting. Exercise: FLOPs of a (B,T,d)x(d,4d) matmul; memory of a 1B model in fp32/bf16 incl. Adam states. | [link](https://cs336.stanford.edu/lectures/?trace=lecture_02) | 1.5 | accounting.md |
| Wed 30 Sep | P0 | Reading | **Generalization revision** | UDL ch. 8-9: bias/variance, double descent, weight decay, dropout, early stopping. 1 hour max. | [link](https://udlbook.github.io/udlbook/) | 1 |  |
| Wed 30 Sep | P0 | Code | **Evaluation revision** | Implement precision/recall/F1, ROC-AUC vs PR-AUC and expected calibration error (ECE) on a toy classifier. | [link](https://udlbook.github.io/udlbook/) | 1 | metrics.py |
| Thu 01 Oct | P1 | Video | **Attention intuition** | 3Blue1Brown DL5 + DL6 back to back. | [link](https://www.youtube.com/watch?v=eMlx5fFNoYc) | 1 |  |
| Thu 01 Oct | P1 | Reading | **Illustrated Transformer** | Read end-to-end; sketch the encoder/decoder data flow yourself. | [link](https://jalammar.github.io/illustrated-transformer/) | 1 | Hand-drawn diagram |
| Thu 01 Oct | P13 | Paper | **Attention Is All You Need (3-pass)** | Read Keshav (15 min), then the paper: 3.1-3.2.3, 3.5, Table 3. Write notes with tensor shapes. | [link](https://arxiv.org/abs/1706.03762) | 1.5 | Paper notes #1 |
| Fri 02 Oct | P1 | Reading | **Math -> tensor shapes** | Work through the attention concept note; fill every shape in the table yourself before reading the answer. | [link](concepts/01-attention-and-transformer.md) | 1 |  |
| Fri 02 Oct | P1 | Code | **Scaled dot-product attention** | Implement SDPA with causal + padding masks. Tests: equals F.scaled_dot_product_attention (atol 1e-6); perturbing future tokens does not change past outputs. | [link](concepts/01-attention-and-transformer.md) | 2.5 | P1: sdpa + tests |
| Sat 03 Oct | P1 | Code | **Multi-head + cross attention** | Fused QKV projection, split heads with view/transpose (or einops), output projection; cross-attention variant. Test against nn.MultiheadAttention with copied weights. | [link](https://nlp.seas.harvard.edu/annotated-transformer/) | 2.5 | P1: mha.py |
| Sat 03 Oct | P1 | Experiment | **Attention experiments** | (a) remove 1/sqrt(d_k): plot softmax entropy vs d_k; (b) visualize attention maps on a toy sequence; (c) measure attention-matrix memory vs T. | [link](concepts/01-attention-and-transformer.md) | 1.5 | P1 notebook (DONE) |

---

<a id="week-2"></a>
## Week 2 - The modern Transformer block (Llama-style) + encoder-decoder

**Dates:** Mon 05 Oct - Sat 10 Oct 2026 - **Phases:** P1 - **Planned hours:** 21.5

**Goal.** Build a decoder-only GPT with the components every 2026 open model uses, plus an encoder-decoder for contrast.

**Learning flow.** Karpathy build -> CS336 architecture lecture -> implement each component with a unit test -> assemble -> train on toy task

### Reading
- **PRIMARY:** [Let's build GPT (Karpathy) - code along](https://www.youtube.com/watch?v=kCc8FmEb1nY); [CS336 2026 Lecture 3 - Architectures & hyperparameters (slides)](https://github.com/stanford-cs336/lectures/blob/main/lecture_03.pdf); [Concept note: attention & transformer (RoPE, RMSNorm, SwiGLU, GQA sections)](concepts/01-attention-and-transformer.md)
- **SECONDARY:** [The Big LLM Architecture Comparison (Raschka, updated 2026)](https://magazine.sebastianraschka.com/p/the-big-llm-architecture-comparison); [The Annotated Transformer (encoder-decoder reference)](https://nlp.seas.harvard.edu/annotated-transformer/)
- **REFERENCE:** [Build a Large Language Model (From Scratch) code](https://github.com/rasbt/LLMs-from-scratch)

### Videos

| Video | Instructor / channel | Duration | Why watch | Covers |
|---|---|---|---|---|
| [Let's build GPT: from scratch, in code, spelled out](https://www.youtube.com/watch?v=kCc8FmEb1nY) | Andrej Karpathy | 1h56m | Fastest route from bigram model to a working decoder block; you will diverge from it with modern components. | P1 implementation |
| [Stanford CS336 Spring 2026 - Lecture 3: Architectures](https://www.youtube.com/watch?v=lVynu4bo1rY) | Tatsu Hashimoto (Stanford) | ~1h20m | Evidence-based survey of pre-norm, RMSNorm, SwiGLU, RoPE, GQA and hyperparameter conventions across real LLMs. | P1 architecture |
| [LLaMA explained: KV-Cache, RoPE, RMS Norm, GQA, SwiGLU](https://www.youtube.com/watch?v=Mn_9W1nCFLo) | Umar Jamil | ~1h10m | Best derivation-level explanation of RoPE and GQA with code. | P1 RoPE/GQA |

### Papers

| Paper | Authors (year) | Read carefully | Implement |
|---|---|---|---|
| [Improving Language Understanding by Generative Pre-Training (GPT-1)](https://cdn.openai.com/research-covers/language-unsupervised/language_understanding_paper.pdf) | Radford, Narasimhan, Salimans, Sutskever (2018) | Sections 1, 3.1-3.3. | - |
| [BERT: Pre-training of Deep Bidirectional Transformers](https://arxiv.org/abs/1810.04805) | Devlin, Chang, Lee, Toutanova (2018) | Sections 3.1-3.2 (MLM, NSP), Figure 1. | Masked-LM objective on your encoder (optional). |
| [Language Models are Unsupervised Multitask Learners (GPT-2)](https://cdn.openai.com/better-language-models/language_models_are_unsupervised_multitask_learners.pdf) | Radford, Wu, Child, Luan, Amodei, Sutskever (2019) | Sections 2.1-2.3 (data, input representation, model changes). | Byte-level BPE (P3). |
| [Root Mean Square Layer Normalization](https://arxiv.org/abs/1910.07467) | Zhang, Sennrich (2019) | Sections 2-3. | RMSNorm layer + test. |
| [GLU Variants Improve Transformer](https://arxiv.org/abs/2002.05202) | Shazeer (2020) | Whole paper (4 pages). | SwiGLU FFN. |
| [On Layer Normalization in the Transformer Architecture](https://arxiv.org/abs/2002.04745) | Xiong et al. (2020) | Sections 1, 3 (skip proofs on first pass). | Pre-norm vs post-norm switch. |
| [RoFormer: Enhanced Transformer with Rotary Position Embedding](https://arxiv.org/abs/2104.09864) | Su, Lu, Pan, Murtadha, Wen, Liu (2021) | Sections 3.1-3.4. | RoPE + numerical relative-position test. |
| [Fast Transformer Decoding: One Write-Head is All You Need (MQA)](https://arxiv.org/abs/1911.02150) | Shazeer (2019) | Sections 2-3. | MQA as GQA special case. |
| [GQA: Training Generalized Multi-Query Transformer Models](https://arxiv.org/abs/2305.13245) | Ainslie, Lee-Thorp, de Jong, Zemlyanskiy, Lebron, Sanghai (2023) | Sections 2-3, Figure 2. | GQA attention. |

### Coding exercises

- LayerNorm and RMSNorm from scratch (tests vs torch)
- FFN(GELU) vs SwiGLU
- RoPE with relative-position property test
- GQA with n_kv_heads (MHA and MQA as special cases)
- Decoder-only GPT config + parameter-count function
- Encoder-decoder Transformer trained on sequence reversal / 3-digit addition

### Project: Project 2 - Transformer from scratch

**Deliverable:** `model.py` (GPT with RoPE/RMSNorm/SwiGLU/GQA) + `seq2seq.py` (encoder-decoder) + tests + toy-task accuracy >99%

### Knowledge checkpoint (close-book)

- [ ] Draw a Llama-style block from memory with pre-norm placement.
- [ ] Prove numerically that RoPE makes q.k depend only on (m - n).
- [ ] Derive KV-cache bytes for MHA vs GQA vs MQA for a given config.
- [ ] Explain why decoder-only won for LLMs and where encoders still win (embeddings, rerankers).

### Day by day

| Date | Phase | Type | Task | What to do | Link | h | Output |
|---|---|---|---|---|---|---|---|
| Mon 05 Oct | P1 | Video | **Let's build GPT (code along)** | Watch at 1.25x and type the code; stop at each stage and predict the next change before Karpathy makes it. | [link](https://www.youtube.com/watch?v=kCc8FmEb1nY) | 2.5 | gpt_karpathy.py |
| Mon 05 Oct | P1 | Reading | **Annotated Transformer skim** | Skim the encoder-decoder parts you will need on Saturday. | [link](https://nlp.seas.harvard.edu/annotated-transformer/) | 1 |  |
| Tue 06 Oct | P1 | Video | **CS336 L3 - Architectures** | Video + slides: pre vs post norm, RMSNorm, SwiGLU, RoPE, parallel layers, d_ff = 8/3 d, head dim conventions. | [link](https://www.youtube.com/watch?v=lVynu4bo1rY) | 1.5 | Notes |
| Tue 06 Oct | P1 | Reading | **Big LLM Architecture Comparison** | Read the Llama, Qwen, DeepSeek (MLA/MoE) and gpt-oss sections. | [link](https://magazine.sebastianraschka.com/p/the-big-llm-architecture-comparison) | 1 |  |
| Tue 06 Oct | P13 | Paper | **Pre-LN, RMSNorm, GLU variants** | Short reads: Pre-LN sec. 1+3 (skip proofs), RMSNorm sec. 3, GLU Variants (whole). | [link](https://arxiv.org/abs/2002.04745) | 1 | Paper notes #2 |
| Wed 07 Oct | P1 | Code | **Block components** | Embeddings + (learned/sinusoidal) PE, LayerNorm & RMSNorm, FFN vs SwiGLU, pre-norm residual block, weight tying. Parameter-count function tested against ~12*L*d^2 + embeddings. | [link](concepts/01-attention-and-transformer.md) | 3.5 | P2: components + tests |
| Thu 08 Oct | P1 | Video | **RoPE / GQA explained** | Umar Jamil LLaMA explained - RoPE, RMSNorm, GQA, SwiGLU sections. | [link](https://www.youtube.com/watch?v=Mn_9W1nCFLo) | 1 |  |
| Thu 08 Oct | P13 | Paper | **RoFormer** | Sections 3.1-3.4. | [link](https://arxiv.org/abs/2104.09864) | 0.5 |  |
| Thu 08 Oct | P1 | Code | **Implement RoPE** | Rotation form; test that <RoPE(q,m), RoPE(k,n)> depends only on m-n; compare interleaved (GPT-J) vs half-split (GPT-NeoX/Llama HF) layouts. | [link](concepts/01-attention-and-transformer.md) | 2 | P2: rope.py + test |
| Fri 09 Oct | P13 | Paper | **MQA + GQA** | MQA sec. 2-3, GQA sec. 2-3. Compute KV-cache bytes for a Llama-3-8B-like config under MHA/GQA/MQA. | [link](https://arxiv.org/abs/2305.13245) | 1 | KV math table |
| Fri 09 Oct | P1 | Code | **GQA + assemble GPT** | GQA via repeat_interleave; flags for MHA/MQA. Assemble decoder-only GPT (dataclass config). Tests: causal leakage, shapes, param count. | [link](concepts/01-attention-and-transformer.md) | 2.5 | P2: model.py |
| Sat 10 Oct | P1 | Project | **Encoder-decoder Transformer** | Bidirectional encoder + decoder with cross-attention; train on sequence reversal or 3-digit addition until >99% exact match. | [link](https://nlp.seas.harvard.edu/annotated-transformer/) | 3 | P2: seq2seq.py |
| Sat 10 Oct | P1 | Review | **Encoder vs decoder write-up** | BERT sec. 3 skim (15 min). Write 1 page: encoder-only vs decoder-only vs enc-dec, and why decoder-only dominates LLMs. | [link](https://arxiv.org/abs/1810.04805) | 1 | P2 README (DONE) |

---

<a id="week-3"></a>
## Week 3 - Tokenization + training a small GPT (CS336 Assignment 1)

**Dates:** Mon 12 Oct - Sat 17 Oct 2026 - **Phases:** P2 - **Planned hours:** 21.5

**Goal.** Own the full pretraining path: raw text -> BPE tokens -> training loop -> a model that writes TinyStories.

**Learning flow.** Tokenizer intuition (Karpathy) -> BPE algorithm -> implement + test (A1 tests are your spec) -> LM objective math -> training loop -> run -> ablate

### Reading
- **PRIMARY:** [CS336 Assignment 1 (Basics) - handout + tests are the spec](https://github.com/stanford-cs336/assignment1-basics); [Let's build the GPT Tokenizer (Karpathy) + minbpe](https://www.youtube.com/watch?v=zduSFxRajkE); [Concept note: prompt -> next token (loss, perplexity sections)](concepts/02-prompt-to-next-token.md)
- **SECONDARY:** [minbpe reference implementation](https://github.com/karpathy/minbpe); [nanoGPT reference](https://github.com/karpathy/nanoGPT)
- **REFERENCE:** [A Recipe for Training Neural Networks (Karpathy)](http://karpathy.github.io/2019/04/25/recipe/)

### Videos

| Video | Instructor / channel | Duration | Why watch | Covers |
|---|---|---|---|---|
| [Let's build the GPT Tokenizer](https://www.youtube.com/watch?v=zduSFxRajkE) | Andrej Karpathy | 2h13m | Explains byte-level BPE, regex pre-tokenization, special tokens and the weird failures tokenization causes. | P2 tokenization |
| [Stanford CS336 Spring 2026 - Lecture 1: Overview, Tokenization](https://www.youtube.com/watch?v=JuoVZkPBiKk) | Percy Liang (Stanford) | ~1h20m | Frames the whole LM pipeline and the tokenizer design space used in A1. | P2 tokenization |

### Papers

| Paper | Authors (year) | Read carefully | Implement |
|---|---|---|---|
| [Neural Machine Translation of Rare Words with Subword Units (BPE)](https://arxiv.org/abs/1508.07909) | Sennrich, Haddow, Birch (2015) | Section 3.2 + Algorithm 1. | BPE trainer (P3). |
| [SentencePiece](https://arxiv.org/abs/1808.06226) | Kudo, Richardson (2018) | Sections 2-3. | Train BPE vs unigram and compare. |
| [Language Models are Few-Shot Learners (GPT-3)](https://arxiv.org/abs/2005.14165) | Brown et al. (2020) | Sections 2.1-2.3, Table 2.1, Figure 1.2. | - |

### Coding exercises

- Byte-level BPE trainer (naive -> incremental pair counts) with GPT-2 regex + special tokens
- Encoder/decoder with round-trip tests; pass the A1 tokenizer tests
- memmap dataset + batch sampler, own AdamW, warmup+cosine LR, grad clipping, checkpointing
- Top-k / top-p / temperature generation

### Project: Project 3 (part 1) - Tokenizer + small GPT

**Deliverable:** BPE tokenizer passing A1 tests; ~20-30M-param GPT trained on TinyStories with loss curves; Reproduction #1 ablation report

### Knowledge checkpoint (close-book)

- [ ] Explain BPE training and encoding, including why byte-level BPE never produces UNK.
- [ ] Convert a validation loss to perplexity and bits-per-byte.
- [ ] Explain teacher forcing and exposure bias.
- [ ] Given a diverging loss curve, list the first five things you check.

### Day by day

| Date | Phase | Type | Task | What to do | Link | h | Output |
|---|---|---|---|---|---|---|---|
| Mon 12 Oct | P2 | Video | **Let's build the GPT Tokenizer** | Watch with minbpe open; pause to implement get_stats/merge yourself. | [link](https://www.youtube.com/watch?v=zduSFxRajkE) | 2.5 |  |
| Mon 12 Oct | P13 | Paper | **BPE (Sennrich) + GPT-2 input representation** | BPE sec. 3.2 + Algorithm 1; GPT-2 sec. 2.2. | [link](https://arxiv.org/abs/1508.07909) | 1 | Paper notes #3 |
| Tue 13 Oct | P2 | Video | **CS336 L1 - Overview & tokenization** | Video + A1 handout BPE section. | [link](https://www.youtube.com/watch?v=JuoVZkPBiKk) | 1.5 |  |
| Tue 13 Oct | P2 | Code | **BPE trainer v1** | Naive byte-level BPE trainer with GPT-2 pre-tokenization regex and special tokens. | [link](https://github.com/stanford-cs336/assignment1-basics) | 2 | P3: bpe_train.py |
| Wed 14 Oct | P2 | Code | **BPE trainer v2 + tokenizer** | Incremental pair-count updates, parallel pre-tokenization on chunk boundaries; 10K vocab on TinyStories; encode/decode; run A1 tokenizer tests. | [link](https://github.com/stanford-cs336/assignment1-basics) | 2 | P3: tokenizer passes A1 tests |
| Wed 14 Oct | P2 | Experiment | **SentencePiece vs BPE** | Read SentencePiece sec. 2-3; train BPE vs unigram on same text; compare bytes/token and vocab-size trade-off (embedding params vs sequence length). | [link](https://arxiv.org/abs/1808.06226) | 1.5 | Comparison table |
| Thu 15 Oct | P2 | Reading | **LM objective math** | Concept note: next-token prediction, cross-entropy = NLL, teacher forcing, perplexity, bits-per-byte. | [link](concepts/02-prompt-to-next-token.md) | 1 |  |
| Thu 15 Oct | P2 | Code | **Training loop (A1 components)** | memmap token dataset, random batch sampler, own AdamW, warmup + cosine LR, grad clipping, checkpoint save/load; pass the A1 tests for each. | [link](https://github.com/stanford-cs336/assignment1-basics) | 2.5 | P3: train.py |
| Fri 16 Oct | P2 | Experiment | **Train on TinyStories** | ~20-30M params on one rented GPU (or smaller on MPS). Log train/val loss, tokens/s, estimated MFU. Aim for the A1 handout's TinyStories target. | [link](https://github.com/stanford-cs336/assignment1-basics) | 3.5 | Loss curves |
| Sat 17 Oct | P2 | Code | **Generation + sampling** | Temperature, top-k, top-p sampling; generate 20 stories; read them critically. | [link](https://arxiv.org/abs/1904.09751) | 2 | generate.py |
| Sat 17 Oct | P13 | Experiment | **Reproduction #1 - architecture ablations** | RoPE vs NoPE vs learned absolute; pre-norm vs post-norm at high LR (Pre-LN paper claim); 3-point LR sweep. Plot and explain. | [link](https://arxiv.org/abs/2002.04745) | 2 | Ablation report |

---

<a id="week-4"></a>
## Week 4 - Inside inference: KV cache, sampling, scaling laws, MoE

**Dates:** Mon 19 Oct - Sat 24 Oct 2026 - **Phases:** P2 (+ P1 MoE, P11 scaling intro) - **Planned hours:** 21.5

**Goal.** Be able to explain - with numbers - exactly what happens from 'user enters a prompt' to 'the next token is emitted', and why.

**Learning flow.** Walkthrough diagram -> KV cache implementation -> sampling algorithms -> inference arithmetic -> scaling-law fit on your own runs -> MoE

### Reading
- **PRIMARY:** [Concept note: prompt -> next token (full walkthrough + memory math)](concepts/02-prompt-to-next-token.md); [CS336 2026 Lecture 10 trace - Inference](https://cs336.stanford.edu/lectures/?trace=lecture_10); [CS336 2026 Lecture 9 slides - Scaling laws](https://github.com/stanford-cs336/lectures/blob/main/lecture_09.pdf); [CS336 2026 Lecture 4 slides - Attention alternatives & MoE](https://github.com/stanford-cs336/lectures/blob/main/lecture_04.pdf)
- **SECONDARY:** [Transformer Inference Arithmetic (kipply)](https://kipply.github.io/blog/transformer-inference-arithmetic/); [A Visual Guide to Mixture of Experts (Grootendorst)](https://newsletter.maartengrootendorst.com/p/a-visual-guide-to-mixture-of-experts); [LLM Visualization (Bycroft) - 3D walk through one token](https://bbycroft.net/llm)
- **REFERENCE:** [CS336 2026 playlist (lectures 4, 9, 10, 11)](https://www.youtube.com/playlist?list=PLoROMvodv4rMqXOcazWaTUHhq-yembLCV)

### Videos

| Video | Instructor / channel | Duration | Why watch | Covers |
|---|---|---|---|---|
| [Stanford CS336 Spring 2026 - Lectures 4 (MoE), 9 & 11 (Scaling laws), 10 (Inference)](https://www.youtube.com/playlist?list=PLoROMvodv4rMqXOcazWaTUHhq-yembLCV) | Hashimoto / Liang (Stanford) | ~1h20m each | The most rigorous current treatment of these topics; watch 10 and 9 fully, 4 and 11 selectively. | P2 inference/scaling, P1 MoE |
| [Stanford CS229: Building Large Language Models (LLMs)](https://www.youtube.com/watch?v=9vM4p9NN0Ts) | Yann Dubois (Stanford) | ~1h44m | Optional single-sitting overview tying pretraining, scaling laws, evaluation and post-training together. | P2 overview |

### Papers

| Paper | Authors (year) | Read carefully | Implement |
|---|---|---|---|
| [The Curious Case of Neural Text Degeneration](https://arxiv.org/abs/1904.09751) | Holtzman, Buys, Du, Forbes, Choi (2019) | Sections 3-5. | Top-p sampling. |
| [Scaling Laws for Neural Language Models](https://arxiv.org/abs/2001.08361) | Kaplan et al. (2020) | Sections 1-3, Figures 1-4. | - |
| [Training Compute-Optimal Large Language Models (Chinchilla)](https://arxiv.org/abs/2203.15556) | Hoffmann et al. (2022) | Sections 3.1-3.3 (three approaches), Table 3. | C = 6ND calculator. |
| [Switch Transformers](https://arxiv.org/abs/2101.03961) | Fedus, Zoph, Shazeer (2021) | Sections 2.1-2.2 (routing, aux loss). | Top-k router + aux loss. |
| [Mixtral of Experts](https://arxiv.org/abs/2401.04088) | Jiang et al. (2024) | Section 2. | - |

### Coding exercises

- KV cache (pre-allocated, RoPE position offsets), prefill vs decode paths
- Greedy, beam search, temperature, top-k, top-p, min-p, repetition penalty
- Sliding-window perplexity evaluator
- Top-k routed MoE FFN with load-balancing aux loss

### Project: Project 3 (part 2) - inference + scaling + MoE

**Deliverable:** KV-cache speedup plot, sampling study, mini IsoFLOP fit (Reproduction #2), dense-vs-MoE comparison, and a close-book 'prompt -> token' write-up

### Knowledge checkpoint (close-book)

- [ ] Compute KV-cache bytes/token and total KV memory for Llama-3-8B at 8K context, batch 16.
- [ ] Explain why decode is memory-bandwidth-bound and prefill is compute-bound.
- [ ] Given compute C, estimate Chinchilla-optimal N and D.
- [ ] Explain top-p vs top-k vs temperature on the same logits vector.

### Day by day

| Date | Phase | Type | Task | What to do | Link | h | Output |
|---|---|---|---|---|---|---|---|
| Mon 19 Oct | P2 | Reading | **Prompt -> next token walkthrough** | Read the concept note, then step through Bycroft's 3D visualization for one token. | [link](concepts/02-prompt-to-next-token.md) | 1 |  |
| Mon 19 Oct | P2 | Code | **KV cache** | Pre-allocated K/V tensors per layer, RoPE offsets, prefill vs decode code paths; measure ms/token with vs without cache as T grows. | [link](concepts/02-prompt-to-next-token.md) | 2.5 | P3: kv_cache.py + plot |
| Tue 20 Oct | P13 | Paper | **Neural text degeneration** | Holtzman et al. sec. 3-5 (why greedy/beam degenerate; nucleus sampling). | [link](https://arxiv.org/abs/1904.09751) | 1 | Paper notes #4 |
| Tue 20 Oct | P2 | Code | **Sampling suite** | Beam search, top-p, min-p, repetition penalty; experiment distinct-n vs perplexity across settings; sliding-window perplexity eval. | [link](https://arxiv.org/abs/1904.09751) | 2.5 | P3: sampling study |
| Wed 21 Oct | P2 | Video | **CS336 L10 - Inference** | Trace + video: prefill/decode, arithmetic intensity, KV cache, batching. | [link](https://cs336.stanford.edu/lectures/?trace=lecture_10) | 1.5 |  |
| Wed 21 Oct | P2 | Reading | **Transformer inference arithmetic** | kipply's post; redo its numbers for a model you care about. | [link](https://kipply.github.io/blog/transformer-inference-arithmetic/) | 1 |  |
| Wed 21 Oct | P2 | Review | **Inference math exercises** | FLOPs/token ~ 2N; KV bytes/token = 2*L*n_kv*d_head*bytes; decode lower bound = bytes moved / bandwidth. Why long context is expensive (memory + positional extrapolation). | [link](concepts/02-prompt-to-next-token.md) | 1 | inference_math.md |
| Thu 22 Oct | P11 | Reading | **Scaling laws** | CS336 L9 slides + video; Kaplan sec. 1-3 figures; Chinchilla sec. 3 (IsoFLOP approaches). | [link](https://arxiv.org/abs/2203.15556) | 1.5 | Paper notes #5 |
| Thu 22 Oct | P13 | Experiment | **Reproduction #2 - mini IsoFLOP** | 3 compute budgets x 4 model sizes on TinyStories (short runs in the background). Fit N_opt vs C and compare the exponent with Chinchilla (~0.5). Use C ~ 6ND. | [link](https://arxiv.org/abs/2203.15556) | 2 | isoflop.ipynb |
| Fri 23 Oct | P1 | Reading | **Mixture of Experts** | CS336 L4 slides/video + Grootendorst visual guide; Switch sec. 2.1-2.2; Mixtral sec. 2. | [link](https://newsletter.maartengrootendorst.com/p/a-visual-guide-to-mixture-of-experts) | 1.5 |  |
| Fri 23 Oct | P1 | Code | **MoE layer** | Token-choice top-k router, experts as SwiGLU FFNs, load-balancing auxiliary loss; swap into GPT. | [link](https://arxiv.org/abs/2101.03961) | 2 | moe.py |
| Sat 24 Oct | P1 | Experiment | **Dense vs MoE** | 8 experts top-2 vs dense at matched active params and tokens: loss, tokens/s, expert-utilization histogram. | [link](https://arxiv.org/abs/2101.03961) | 2 | MoE report |
| Sat 24 Oct | P2 | Review | **Phase 1-2 checkpoint** | Close-book: write 'prompt -> next token' with your own diagram and numbers; answer the Phase 1 and 2 checkpoint questions. | [link](08-skill-checkpoints.md) | 2 | P3 (DONE) |

---

<a id="week-5"></a>
## Week 5 - Embeddings, contrastive learning and vector search internals

**Dates:** Mon 26 Oct - Sat 31 Oct 2026 - **Phases:** P3 - **Planned hours:** 21.5

**Goal.** Understand retrieval mathematically and algorithmically - from InfoNCE to BM25 to IVF-PQ and HNSW - and build your own engine.

**Learning flow.** Similarity intuition -> contrastive loss math -> sparse retrieval math -> IR metrics -> ANN algorithms -> implement + benchmark against FAISS/pgvector

### Reading
- **PRIMARY:** [Concept note: retrieval & vector search](concepts/03-retrieval-and-vector-search.md); [Introduction to Information Retrieval - ch. 6 & 11.4.3 (BM25)](https://nlp.stanford.edu/IR-book/html/htmledition/irbook.html); [Faiss: The Missing Manual (Pinecone) - indexes, PQ, HNSW chapters](https://www.pinecone.io/learn/series/faiss/)
- **SECONDARY:** [bm25s (fast reference BM25)](https://github.com/xhluca/bm25s); [The Faiss library paper](https://arxiv.org/abs/2401.08281)
- **REFERENCE:** [pgvector](https://github.com/pgvector/pgvector); [Qdrant docs](https://qdrant.tech/documentation/); [Sentence-Transformers docs](https://sbert.net/)

### Videos

| Video | Instructor / channel | Duration | Why watch | Covers |
|---|---|---|---|---|
| [HNSW for Vector Search Explained and Implemented with Faiss](https://www.youtube.com/watch?v=QvKMwLjdK-s) | James Briggs | ~35m | Visual walk-through of the HNSW layers and parameters before you read the paper. | P3 ANN |

### Papers

| Paper | Authors (year) | Read carefully | Implement |
|---|---|---|---|
| [Representation Learning with Contrastive Predictive Coding (InfoNCE)](https://arxiv.org/abs/1807.03748) | van den Oord, Li, Vinyals (2018) | Section 2.3 (InfoNCE). | InfoNCE with in-batch negatives. |
| [Sentence-BERT](https://arxiv.org/abs/1908.10084) | Reimers, Gurevych (2019) | Sections 3-4. | Bi-encoder fine-tune. |
| [Dense Passage Retrieval for Open-Domain QA](https://arxiv.org/abs/2004.04906) | Karpukhin et al. (2020) | Sections 3.1-3.2, 5. | In-batch negatives. |
| [BEIR: Heterogeneous Benchmark for Zero-shot IR](https://arxiv.org/abs/2104.08663) | Thakur, Reimers, Ruckle, Srivastava, Gurevych (2021) | Sections 3-5, Table 2. | nDCG@10 harness. |
| [Product Quantization for Nearest Neighbor Search](https://doi.org/10.1109/TPAMI.2010.57) | Jegou, Douze, Schmid (2011) | Sections II-III (PQ, ADC/SDC). | PQ + ADC in NumPy. |
| [Efficient and Robust ANN Search using HNSW Graphs](https://arxiv.org/abs/1603.09320) | Malkov, Yashunin (2016) | Sections 3-4, Algorithms 1-4. | NSW/HNSW search. |
| [The Faiss Library](https://arxiv.org/abs/2401.08281) | Douze et al. (2024) | Sections 3-5 (skim). | - |

### Coding exercises

- InfoNCE with in-batch negatives; fine-tune a small bi-encoder
- Inverted index + BM25 from scratch; compare with bm25s
- Recall@K, Precision@K, MRR, nDCG from scratch
- IVF (k-means) + PQ with ADC lookup tables in NumPy
- NSW/HNSW greedy search; recall-latency curves vs FAISS IndexHNSWFlat

### Project: Project 4 - Embedding & retrieval engine

**Deliverable:** `retrieval-engine` package (BM25, Flat, IVF-PQ, HNSW, hybrid RRF, cross-encoder rerank, pgvector/Qdrant backend) + benchmark report

### Knowledge checkpoint (close-book)

- [ ] Derive each term of BM25 and explain k1 and b.
- [ ] Explain PQ asymmetric distance computation and its memory cost per vector.
- [ ] Explain HNSW search and what M, efConstruction, efSearch trade off.
- [ ] Explain when hybrid beats dense and why BM25 is a strong zero-shot baseline (BEIR).

### Day by day

| Date | Phase | Type | Task | What to do | Link | h | Output |
|---|---|---|---|---|---|---|---|
| Mon 26 Oct | P3 | Reading | **Embeddings + contrastive learning** | Concept note; SBERT sec. 3; DPR sec. 3 (in-batch negatives); InfoNCE (CPC sec. 2.3). | [link](concepts/03-retrieval-and-vector-search.md) | 1.5 | Paper notes #6 |
| Mon 26 Oct | P3 | Code | **InfoNCE + bi-encoder fine-tune** | Implement InfoNCE with temperature; fine-tune all-MiniLM-L6-v2 on QA pairs for 1 epoch; MRR before/after. | [link](https://sbert.net/) | 2 | P4: contrastive.py |
| Tue 27 Oct | P3 | Reading | **TF-IDF + BM25** | IR book ch. 6 and sec. 11.4.3. | [link](https://nlp.stanford.edu/IR-book/html/htmledition/irbook.html) | 1 |  |
| Tue 27 Oct | P3 | Code | **BM25 from scratch** | Inverted index, k1/b, IDF variants; compare scores/speed with bm25s on BEIR SciFact. | [link](https://github.com/xhluca/bm25s) | 2.5 | P4: bm25.py |
| Wed 28 Oct | P3 | Code | **IR metrics** | Recall@K, Precision@K, MRR, nDCG@K from scratch with unit tests; BEIR paper sec. 3-5. | [link](https://arxiv.org/abs/2104.08663) | 1 | metrics.py |
| Wed 28 Oct | P13 | Experiment | **Reproduction #3 - BEIR baseline** | BM25 vs dense (e5/bge-small) vs hybrid RRF on SciFact + NFCorpus; your BM25 nDCG@10 on SciFact should land within ~0.02 of the BEIR table. | [link](https://arxiv.org/abs/2104.08663) | 2.5 | Results table |
| Thu 29 Oct | P3 | Reading | **IVF + PQ** | Pinecone chapters on vector indexes and PQ; PQ paper sec. II-III. | [link](https://www.pinecone.io/learn/series/faiss/product-quantization/) | 1.5 |  |
| Thu 29 Oct | P3 | Code | **IVF-PQ in NumPy** | k-means coarse quantizer + nprobe; PQ with m sub-spaces x 256 centroids; ADC tables; recall@10 vs nprobe and bytes/vector. | [link](https://doi.org/10.1109/TPAMI.2010.57) | 2 | P4: ivfpq.py |
| Fri 30 Oct | P3 | Video | **HNSW** | James Briggs video, then HNSW paper sec. 3-4 (Algorithms 1-4). | [link](https://www.youtube.com/watch?v=QvKMwLjdK-s) | 1.5 |  |
| Fri 30 Oct | P3 | Code | **NSW/HNSW** | Single-layer NSW with beam search (efSearch), then hierarchy (optional); compare with FAISS IndexHNSWFlat over M/efSearch. | [link](https://arxiv.org/abs/1603.09320) | 2 | P4: hnsw.py + curves |
| Sat 31 Oct | P3 | Project | **Assemble retrieval engine** | One interface over BM25, Flat, IVF-PQ, HNSW (yours + FAISS), hybrid RRF, cross-encoder reranker, metadata filters, and one DB backend (pgvector HNSW or Qdrant). | [link](https://www.pinecone.io/learn/series/faiss/) | 3 | P4 package |
| Sat 31 Oct | P3 | Review | **Benchmark report** | Recall/nDCG/latency/memory table across indexes; notes on pre- vs post-filtering in vector DBs. | [link](concepts/03-retrieval-and-vector-search.md) | 1 | P4 (DONE) |

---

<a id="week-6"></a>
## Week 6 - RAG: beginner -> advanced -> research level

**Dates:** Mon 02 Nov - Sat 07 Nov 2026 - **Phases:** P4 - **Planned hours:** 21.5

**Goal.** Build a serious, measurable RAG system - not a PDF chatbot - where every stage is a swappable, ablated component.

**Learning flow.** Baseline pipeline + golden set v0 -> chunking -> query-side methods -> reranking & multi-vector -> agentic/graph RAG -> ablation table

### Reading
- **PRIMARY:** [RAG paper (Lewis et al.)](https://arxiv.org/abs/2005.11401); [Beyond the Basics of RAG (Clavie) - notes page](https://parlance-labs.com/education/rag/ben.html); [Introducing Contextual Retrieval (Anthropic)](https://www.anthropic.com/news/contextual-retrieval)
- **SECONDARY:** [Docling docs (document parsing)](https://docling-project.github.io/docling/); [Concept note: RAG & evaluation metrics](concepts/04-rag-and-evaluation-metrics.md)
- **REFERENCE:** [BGE-M3 paper](https://arxiv.org/abs/2402.03216); [ColBERT paper](https://arxiv.org/abs/2004.12832)

### Videos

| Video | Instructor / channel | Duration | Why watch | Covers |
|---|---|---|---|---|
| [Stanford CS25: V3 - Retrieval Augmented Language Models](https://www.youtube.com/watch?v=mE7IDf2SmJg) | Douwe Kiela (Stanford CS25) | 1h19m | Research-level map of RAG: retriever/generator training, architectures, open problems. | P4 foundations |
| [Beyond the Basics of Retrieval for Augmenting Generation](https://www.youtube.com/watch?v=0nA5QG3087g) | Ben Clavie (Answer.AI) | ~1h | Practitioner's 'MVP++': BM25 + bi-encoder + reranker + metadata filters, and how to evaluate. | P4 advanced retrieval |

### Papers

| Paper | Authors (year) | Read carefully | Implement |
|---|---|---|---|
| [Retrieval-Augmented Generation for Knowledge-Intensive NLP](https://arxiv.org/abs/2005.11401) | Lewis et al. (2020) | Sections 2.1-2.4. | - |
| [Precise Zero-Shot Dense Retrieval without Relevance Labels (HyDE)](https://arxiv.org/abs/2212.10496) | Gao, Ma, Lin, Callan (2022) | Section 3. | HyDE stage in P5. |
| [Lost in the Middle](https://arxiv.org/abs/2307.03172) | Liu, Lin, Hewitt, Paranjape, Bevilacqua, Petroni, Liang (2023) | Sections 2-4. | - |
| [ColBERT: Late Interaction over BERT](https://arxiv.org/abs/2004.12832) | Khattab, Zaharia (2020) | Section 3. | MaxSim reranker. |
| [M3-Embedding (BGE-M3)](https://arxiv.org/abs/2402.03216) | Chen, Xiao, Zhang, Luo, Lian, Liu (2024) | Sections 3-4. | Use its three heads in P5. |
| [Self-RAG](https://arxiv.org/abs/2310.11511) | Asai, Wu, Wang, Sil, Hajishirzi (2023) | Abstract, Section 3 overview. | - |
| [From Local to Global: A Graph RAG Approach](https://arxiv.org/abs/2404.16130) | Edge et al. (2024) | Sections 2-3. | Optional entity graph. |

### Coding exercises

- Baseline pipeline with citations (then map it onto LangChain / LlamaIndex abstractions)
- Chunkers: fixed, recursive, structure-aware, semantic, parent-child, contextual headers
- Query rewriting, multi-query, HyDE, decomposition
- Hybrid + RRF + cross-encoder + context compression
- Multi-vector (MaxSim) reranker
- Agentic router with iterative retrieval

### Project: Project 5 - Advanced RAG

**Deliverable:** Config-driven RAG service (FastAPI, streaming, citations with spans, abstention) + ablation table on golden set

### Knowledge checkpoint (close-book)

- [ ] Name the failure mode each stage fixes and the one it can introduce.
- [ ] Explain when HyDE helps and when it hurts.
- [ ] Explain parent-child retrieval and contextual chunk headers.
- [ ] Decide RAG vs long-context for a given corpus size, latency and cost budget.

### Day by day

| Date | Phase | Type | Task | What to do | Link | h | Output |
|---|---|---|---|---|---|---|---|
| Mon 02 Nov | P4 | Video | **RAG foundations** | RAG paper sec. 2 (RAG-Sequence vs RAG-Token) + Kiela CS25 lecture. | [link](https://www.youtube.com/watch?v=mE7IDf2SmJg) | 1.5 | Paper notes #7 |
| Mon 02 Nov | P4 | Code | **Baseline pipeline + golden set v0** | Docling parse -> fixed chunks -> embed -> retrieve (P4) -> numbered sources -> answer with citations. Write 30 real Q/A pairs now. | [link](https://docling-project.github.io/docling/) | 2 | P5 baseline |
| Tue 03 Nov | P4 | Video | **Advanced retrieval practice** | Clavie talk + Anthropic Contextual Retrieval. | [link](https://www.youtube.com/watch?v=0nA5QG3087g) | 1 |  |
| Tue 03 Nov | P4 | Experiment | **Chunking study** | Fixed vs recursive vs structure-aware vs semantic; parent-child; contextual headers; metadata filters. Measure recall@5 on golden set. | [link](https://www.anthropic.com/news/contextual-retrieval) | 2.5 | Chunking table |
| Wed 04 Nov | P13 | Paper | **HyDE + query-side methods** | HyDE sec. 3; multi-query, decomposition, conversational rewriting. | [link](https://arxiv.org/abs/2212.10496) | 1 |  |
| Wed 04 Nov | P4 | Code | **Full retrieval chain** | Rewrite -> multi-query -> hybrid -> RRF -> cross-encoder rerank -> extractive compression -> generate; ablate each stage. | [link](https://arxiv.org/abs/2212.10496) | 2.5 | P5 chain |
| Thu 05 Nov | P4 | Paper | **Lost in the Middle** | Sec. 2-4; implement context ordering (best chunks at edges) and token budgets. | [link](https://arxiv.org/abs/2307.03172) | 1 |  |
| Thu 05 Nov | P4 | Paper | **Late interaction** | ColBERT sec. 3 (MaxSim); BGE-M3 dense+sparse+multi-vector. | [link](https://arxiv.org/abs/2004.12832) | 1 |  |
| Thu 05 Nov | P4 | Code | **Multi-vector path** | BGE-M3 multi-vector or ColBERT-style MaxSim reranker vs cross-encoder: quality vs latency. | [link](https://arxiv.org/abs/2402.03216) | 1.5 |  |
| Fri 06 Nov | P4 | Paper | **Agentic & graph RAG** | Self-RAG overview; GraphRAG sec. 2-3; retrieval planning (whether / what / how many hops). | [link](https://arxiv.org/abs/2404.16130) | 1.5 |  |
| Fri 06 Nov | P4 | Code | **Agentic RAG router** | Answer-directly / retrieve / decompose router, sufficiency check, max hops; optional entity graph for global questions. | [link](https://arxiv.org/abs/2310.11511) | 2 | router.py |
| Sat 07 Nov | P4 | Project | **P5 polish** | Config-driven pipeline, span-level citations, abstain when unsupported, caching, streaming FastAPI endpoint. | [link](https://arxiv.org/abs/2005.11401) | 2.5 | P5 service |
| Sat 07 Nov | P4 | Reading | **Map P5 onto LangChain + LlamaIndex** | Read-only: how LangChain (document loaders, text splitters, retrievers, vector-store integrations) and LlamaIndex (nodes, indices, query engines, rerankers) name the stages you just built. You should recognise every abstraction as something you already wrote. | [link](https://developers.llamaindex.ai/python/framework/) | 0.5 | mapping table |
| Sat 07 Nov | P4 | Review | **Ablation table v0** | Retrieval recall@5 + manual answer check per configuration (full metrics next week). | [link](concepts/04-rag-and-evaluation-metrics.md) | 1 | P5 (DONE) |

---

<a id="week-7"></a>
## Week 7 - Evaluation like a professional AI team

**Dates:** Mon 09 Nov - Sat 14 Nov 2026 - **Phases:** P5 (+ P4 metrics) - **Planned hours:** 21.5

**Goal.** Turn 'it seems better' into numbers you can defend: golden sets, calibrated judges, confidence intervals and CI gates.

**Learning flow.** Error analysis on real traces -> taxonomy -> datasets -> judges + calibration vs your labels -> RAG metrics -> statistics -> agent evals -> framework

### Reading
- **PRIMARY:** [Your AI Product Needs Evals (Husain)](https://hamel.dev/blog/posts/evals/); [Using LLM-as-a-Judge: A Complete Guide (Husain)](https://hamel.dev/blog/posts/llm-judge/); [Demystifying evals for AI agents (Anthropic)](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents); [Concept note: RAG & evaluation metrics](concepts/04-rag-and-evaluation-metrics.md)
- **SECONDARY:** [Evaluating the Effectiveness of LLM-Evaluators (Eugene Yan)](https://eugeneyan.com/writing/llm-evaluators/); [LLM Evaluation Guidebook (Hugging Face)](https://huggingface.co/spaces/OpenEvals/evaluation-guidebook); [CS336 2026 Lecture 12 trace - Evaluation](https://cs336.stanford.edu/lectures/?trace=lecture_12)
- **REFERENCE:** [Ragas metric definitions](https://docs.ragas.io/en/stable/concepts/metrics/available_metrics/); [Inspect (UK AISI) eval framework](https://inspect.aisi.org.uk/); [lm-evaluation-harness](https://github.com/EleutherAI/lm-evaluation-harness)

### Videos

| Video | Instructor / channel | Duration | Why watch | Covers |
|---|---|---|---|---|
| [Stanford CS336 Spring 2026 - Lecture 12: Evaluation](https://www.youtube.com/playlist?list=PLoROMvodv4rMqXOcazWaTUHhq-yembLCV) | Percy Liang (Stanford) | ~1h20m | How benchmarks are built and broken (contamination, prompt sensitivity) - the research view of eval. | P5 benchmarks |

### Papers

| Paper | Authors (year) | Read carefully | Implement |
|---|---|---|---|
| [Judging LLM-as-a-Judge with MT-Bench and Chatbot Arena](https://arxiv.org/abs/2306.05685) | Zheng et al. (2023) | Sections 3-4. | Pairwise judge with swap. |
| [G-Eval](https://arxiv.org/abs/2303.16634) | Liu, Iter, Xu, Wang, Xu, Zhu (2023) | Section 2. | Rubric judge. |
| [RAGAS: Automated Evaluation of RAG](https://arxiv.org/abs/2309.15217) | Es, James, Espinosa-Anke, Schockaert (2023) | Section 3. | Your own faithfulness metric. |
| [Who Validates the Validators?](https://arxiv.org/abs/2404.12272) | Shankar, Zamfirescu-Pereira, Hartmann, Parameswaran, Arawjo (2024) | Sections 1, 4-6. | Judge calibration loop. |
| [tau-bench: Tool-Agent-User Interaction](https://arxiv.org/abs/2406.12045) | Yao, Shinn, Razavi, Narasimhan (2024) | Sections 3-4. | pass^k metric. |

### Coding exercises

- Trace viewer + error taxonomy
- Pointwise, pairwise (position-swapped) and reference judges
- Judge-human agreement (Cohen's kappa, TPR/TNR)
- Context precision/recall, faithfulness via claim verification, answer relevance, citation accuracy
- Paired bootstrap CIs + CI regression gate
- Agent task schema with state-based graders

### Project: Project 6 - RAG/LLM evaluation framework

**Deliverable:** `ragevals`: versioned datasets, retrieval + judge metrics, calibration report, bootstrap CIs, GitHub Actions regression gate, HTML report; P5 ablations re-scored with CIs

### Knowledge checkpoint (close-book)

- [ ] Explain faithfulness vs correctness vs answer relevance with an example that passes one and fails another.
- [ ] List three LLM-judge biases and how you mitigated each.
- [ ] Decide whether a 2-point improvement on 150 examples is real (show the CI).
- [ ] Explain pass^k and state-based grading for agents.

### Day by day

| Date | Phase | Type | Task | What to do | Link | h | Output |
|---|---|---|---|---|---|---|---|
| Mon 09 Nov | P5 | Reading | **Evals mindset** | Husain 'Your AI Product Needs Evals' + first half of the judge guide. | [link](https://hamel.dev/blog/posts/evals/) | 1.5 |  |
| Mon 09 Nov | P5 | Experiment | **Error analysis + golden set v1** | Read 50 P5 traces, open-code failures into a taxonomy; grow the golden set to 100+ (human-written, synthetic-then-verified, unanswerable/adversarial). | [link](https://hamel.dev/blog/posts/evals/) | 2 | taxonomy.md + dataset |
| Tue 10 Nov | P13 | Paper | **LLM-as-judge research** | MT-Bench sec. 3-4 (biases), G-Eval sec. 2, Yan's survey, Shankar 'Who Validates the Validators'. | [link](https://arxiv.org/abs/2306.05685) | 1.5 | Paper notes #8 |
| Tue 10 Nov | P5 | Code | **Judges + calibration** | Binary rubric judge, pairwise with position swap, reference-based correctness. Label 60 examples yourself; iterate until judge-human kappa >= 0.6. | [link](https://hamel.dev/blog/posts/llm-judge/) | 2 | judges.py + calibration |
| Wed 11 Nov | P5 | Reading | **RAG metric definitions** | RAGAS sec. 3 + concept note. | [link](https://arxiv.org/abs/2309.15217) | 1 |  |
| Wed 11 Nov | P5 | Code | **RAG metrics from scratch** | Context precision/recall (gold passages), faithfulness (claim extraction -> per-claim support check), answer relevance, citation accuracy; compare with the ragas library. | [link](https://docs.ragas.io/en/stable/concepts/metrics/available_metrics/) | 2.5 | rag_metrics.py |
| Thu 12 Nov | P5 | Video | **Benchmarks & contamination** | CS336 L12 trace/video; skim the HF Evaluation Guidebook. | [link](https://cs336.stanford.edu/lectures/?trace=lecture_12) | 1 |  |
| Thu 12 Nov | P5 | Reading | **Statistics for evals** | Bootstrap CIs, paired tests (paired bootstrap / McNemar), sample sizes; online A/B tests (unit of randomization, guardrails); human-eval protocols and inter-annotator agreement. | [link](concepts/04-rag-and-evaluation-metrics.md) | 1 | stats.py |
| Thu 12 Nov | P5 | Code | **Standard benchmark harnesses** | Run lm-evaluation-harness on a small open model (ARC-easy, HellaSwag, GSM8K subset); write one custom Inspect task. | [link](https://inspect.aisi.org.uk/) | 1.5 |  |
| Fri 13 Nov | P5 | Reading | **Agent & tool-call evals** | Anthropic agent-evals post; tau-bench sec. 3-4 (pass^k, DB-state checks); tool-selection accuracy, argument AST match, trajectory efficiency. | [link](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents) | 1.5 |  |
| Fri 13 Nov | P5 | Code | **Agent eval schema** | Task format, outcome graders (tests pass / state), trajectory graders, cost/latency; write 20 tasks for P8 and the capstone. | [link](https://arxiv.org/abs/2406.12045) | 2 | agent_tasks.jsonl |
| Sat 14 Nov | P5 | Project | **Build ragevals** | Runners, metrics, calibration report, bootstrap CIs, pytest + GitHub Actions gate that fails on a significant regression, markdown/HTML report. | [link](https://hamel.dev/blog/posts/llm-judge/) | 3 | P6 package |
| Sat 14 Nov | P5 | Review | **Re-score P5 ablations** | Publish the ablation table with CIs and pick the production config. | [link](concepts/04-rag-and-evaluation-metrics.md) | 1 | P6 (DONE) |

---

<a id="week-8"></a>
## Week 8 - Fine-tuning: SFT, chat templates, LoRA and QLoRA

**Dates:** Mon 16 Nov - Sat 21 Nov 2026 - **Phases:** P6 - **Planned hours:** 21.5

**Goal.** Fine-tune an open model for a task you will reuse in the capstone, having implemented SFT and LoRA yourself first.

**Learning flow.** Post-training landscape -> chat templates & masking -> SFT from scratch -> LoRA math + implementation -> QLoRA on 8B -> data -> eval

### Reading
- **PRIMARY:** [Hugging Face LLM Course ch. 11 - Supervised fine-tuning](https://huggingface.co/learn/llm-course/chapter11/1); [CS336 2026 Lecture 15 slides - Mid/post-training (SFT/RLHF)](https://github.com/stanford-cs336/lectures/blob/main/lecture_15.pdf); [LoRA Without Regret (Thinking Machines)](https://thinkingmachines.ai/blog/lora/); [Concept note: post-training math](concepts/05-post-training-math.md)
- **SECONDARY:** [Transformers chat templates docs](https://huggingface.co/docs/transformers/chat_templating); [TRL SFTTrainer docs](https://huggingface.co/docs/trl/sft_trainer); [Unsloth fine-tuning guide](https://unsloth.ai/docs/get-started/fine-tuning-llms-guide); [smol-course](https://github.com/huggingface/smol-course)
- **REFERENCE:** [A Visual Guide to Quantization (Grootendorst)](https://newsletter.maartengrootendorst.com/p/a-visual-guide-to-quantization); [TRL: LoRA without regret recipe](https://huggingface.co/docs/trl/en/lora_without_regret)

### Videos

| Video | Instructor / channel | Duration | Why watch | Covers |
|---|---|---|---|---|
| [Stanford CS336 Spring 2026 - Lecture 15: Mid/post-training (SFT/RLHF)](https://www.youtube.com/playlist?list=PLoROMvodv4rMqXOcazWaTUHhq-yembLCV) | Tatsu Hashimoto (Stanford) | ~1h20m | Current, research-grounded view of what SFT and RLHF actually change in a model. | P6 landscape |

### Papers

| Paper | Authors (year) | Read carefully | Implement |
|---|---|---|---|
| [Training LMs to Follow Instructions with Human Feedback (InstructGPT)](https://arxiv.org/abs/2203.02155) | Ouyang et al. (2022) | Sections 3.1-3.5, Figure 2. | SFT with loss masking; RM loss. |
| [LoRA: Low-Rank Adaptation](https://arxiv.org/abs/2106.09685) | Hu et al. (2021) | Sections 4.1-4.2, 7. | LoRALinear from scratch. |
| [QLoRA](https://arxiv.org/abs/2305.14314) | Dettmers, Pagnoni, Holtzman, Zettlemoyer (2023) | Section 3. | NF4 quantize/dequantize toy. |

### Coding exercises

- SFT in plain PyTorch: chat template, assistant-only loss masking (-100), packing
- LoRALinear from scratch (init, alpha/r, merge/unmerge) and injection into attention + MLP
- QLoRA 7-8B run (Unsloth or TRL + PEFT + bitsandbytes)
- Dataset builder with dedup and decontamination

### Project: Project 7 (part 1) - SFT + LoRA/QLoRA

**Deliverable:** Fine-tuned adapter for your capstone task (recommended: tool-calling JSON for your own tools), with baseline vs LoRA vs QLoRA eval report and Reproduction #4

### Knowledge checkpoint (close-book)

- [ ] Show exactly which tokens contribute to the loss for a 3-turn chat.
- [ ] Derive LoRA's parameter count and explain B=0 initialization and alpha/r.
- [ ] Explain NF4 and double quantization at the level of bits.
- [ ] Decide between prompt engineering, RAG, LoRA, full FT and continued pretraining for three scenarios.

### Day by day

| Date | Phase | Type | Task | What to do | Link | h | Output |
|---|---|---|---|---|---|---|---|
| Mon 16 Nov | P6 | Video | **Post-training landscape** | CS336 L15 slides + video; InstructGPT sec. 3.1-3.5; pretraining vs continued pretraining vs instruction tuning. | [link](https://github.com/stanford-cs336/lectures/blob/main/lecture_15.pdf) | 1.5 | Paper notes #9 |
| Mon 16 Nov | P6 | Reading | **Chat templates** | HF LLM course ch. 11 + chat templating docs; inspect the Jinja template of Qwen3 or Llama-3 and its special tokens. | [link](https://huggingface.co/docs/transformers/chat_templating) | 2 |  |
| Tue 17 Nov | P6 | Code | **SFT from scratch** | SmolLM2-360M or Qwen3-0.6B-Base: chat template, assistant-only masking with -100, packing caveats, eval loss; then replicate with TRL SFTTrainer and compare loss curves. | [link](https://huggingface.co/docs/trl/sft_trainer) | 3.5 | P7: sft.py |
| Wed 18 Nov | P6 | Paper | **LoRA** | LoRA sec. 4 + 'LoRA Without Regret'. | [link](https://arxiv.org/abs/2106.09685) | 1 |  |
| Wed 18 Nov | P6 | Code | **LoRA from scratch** | LoRALinear (freeze base, A random, B=0, alpha/r, dropout, merge/unmerge); inject into q,k,v,o + MLP; verify trainable params; compare with PEFT. | [link](https://thinkingmachines.ai/blog/lora/) | 2.5 | P7: lora.py |
| Thu 19 Nov | P6 | Paper | **QLoRA + quantization basics** | QLoRA sec. 3; first half of the quantization visual guide (absmax, zero-point, block-wise). | [link](https://arxiv.org/abs/2305.14314) | 1 |  |
| Thu 19 Nov | P6 | Experiment | **QLoRA an 8B model** | Qwen3-8B or Llama-3.1-8B on one 24 GB GPU via Unsloth (or TRL+PEFT+bitsandbytes). Track VRAM and tokens/s; save adapter; merge for serving. | [link](https://unsloth.ai/docs/get-started/fine-tuning-llms-guide) | 2.5 | Adapter |
| Fri 20 Nov | P6 | Reading | **Dataset preparation** | Task spec, sourcing, synthetic generation with verification, dedup, decontamination vs eval set, chat formatting, splits (smol-course modules). | [link](https://github.com/huggingface/smol-course) | 1.5 |  |
| Fri 20 Nov | P6 | Code | **Build the P7 dataset** | 2-5K examples for your capstone task (e.g. JSON tool calls for your own MCP tools) + held-out eval set. | [link](https://github.com/huggingface/smol-course) | 2 | dataset v1 |
| Sat 21 Nov | P13 | Experiment | **P7 runs + Reproduction #4** | Baseline vs LoRA r in {8, 64} vs QLoRA; LR sweep to test the ~10x-higher optimal LoRA LR finding; eval with P6 harness + tool-call exact match; forgetting check. | [link](https://thinkingmachines.ai/blog/lora/) | 3 | Runs |
| Sat 21 Nov | P6 | Review | **Report + publish adapter** | Write the report; push the adapter to the HF Hub (private). | [link](https://arxiv.org/abs/2106.09685) | 1 | P7 part 1 (DONE) |

---

<a id="week-9"></a>
## Week 9 - RL for LLMs: RLHF, DPO, RLVR/GRPO and reasoning models

**Dates:** Mon 23 Nov - Sat 28 Nov 2026 - **Phases:** P12 + P6 (preference optimization) - **Planned hours:** 21.5

**Goal.** Learn only the RL that matters for modern LLMs, derive DPO and GRPO yourself, and run both.

**Learning flow.** Policy-gradient intuition -> REINFORCE on a toy LM -> PPO/RLHF -> DPO derivation + implementation -> RLVR/GRPO -> run GRPO -> reward hacking

### Reading
- **PRIMARY:** [OpenAI Spinning Up - Parts 1 and 3](https://spinningup.openai.com/en/latest/); [RLHF Book (Lambert)](https://rlhfbook.com/); [CS336 2026 Lecture 16 slides - Post-training: RLVR](https://github.com/stanford-cs336/lectures/blob/main/lecture_16.pdf); [Concept note: post-training math (PPO, DPO, GRPO)](concepts/05-post-training-math.md)
- **SECONDARY:** [HF LLM Course ch. 12 - Build reasoning models (GRPO)](https://huggingface.co/learn/llm-course/chapter12); [Build a Reasoning Model (From Scratch) code](https://github.com/rasbt/reasoning-from-scratch); [Why We Think (Weng)](https://lilianweng.github.io/posts/2025-05-01-thinking/); [Reward Hacking in RL (Weng)](https://lilianweng.github.io/posts/2024-11-28-reward-hacking/)
- **REFERENCE:** [CS336 Assignment 5 (GRPO on OLMo-2 1B) - full version deferred to 2027](https://github.com/stanford-cs336/assignment5-alignment)

### Videos

| Video | Instructor / channel | Duration | Why watch | Covers |
|---|---|---|---|---|
| [L3 Policy Gradients and Advantage Estimation (Foundations of Deep RL)](https://www.youtube.com/watch?v=AKbX1Zvo7r8) | Pieter Abbeel | ~1h | Compact, rigorous policy-gradient derivation; watch L4 (TRPO/PPO) from the same playlist next. | P12 policy gradients |
| [Reinforcement Learning from Human Feedback explained with math derivations and the PyTorch code](https://www.youtube.com/watch?v=qGyFrqc34yc) | Umar Jamil | ~2h | Walks from policy gradients to PPO-based RLHF with code; watch the PPO + RLHF sections. | P12 RLHF/PPO |
| [Direct Preference Optimization (DPO) explained: Bradley-Terry model, log probabilities, math](https://www.youtube.com/watch?v=hvGa5Mba4c8) | Umar Jamil | ~50m | Line-by-line derivation of the DPO loss. | P6 DPO |
| [Stanford CS336 Spring 2026 - Lecture 16: Post-training RLVR](https://www.youtube.com/playlist?list=PLoROMvodv4rMqXOcazWaTUHhq-yembLCV) | Tatsu Hashimoto (Stanford) | ~1h20m | Up-to-date treatment of RL with verifiable rewards and reasoning models. | P12 RLVR |

### Papers

| Paper | Authors (year) | Read carefully | Implement |
|---|---|---|---|
| [Deep RL from Human Preferences](https://arxiv.org/abs/1706.03741) | Christiano, Leike, Brown, Martic, Legg, Amodei (2017) | Sections 1-2. | Bradley-Terry RM loss. |
| [Proximal Policy Optimization Algorithms](https://arxiv.org/abs/1707.06347) | Schulman, Wolski, Dhariwal, Radford, Klimov (2017) | Sections 2-5. | PPO clip loss. |
| [Direct Preference Optimization](https://arxiv.org/abs/2305.18290) | Rafailov, Sharma, Mitchell, Ermon, Manning, Finn (2023) | Sections 4-5 (derivation), Appendix A.1. | DPO loss from scratch. |
| [DeepSeekMath (introduces GRPO)](https://arxiv.org/abs/2402.03300) | Shao et al. (2024) | Section 4 (4.1-4.2). | GRPO loss. |
| [DeepSeek-R1](https://arxiv.org/abs/2501.12948) | DeepSeek-AI (2025) | Sections 2-3. | - |
| [Tulu 3: Pushing Frontiers in Open Post-Training](https://arxiv.org/abs/2411.15124) | Lambert et al. (2024) | RLVR section + data sections (skim). | - |
| [Understanding R1-Zero-Like Training: A Critical Perspective (Dr. GRPO)](https://arxiv.org/abs/2503.20783) | Liu et al. (2025) | Sections 2-3. | Dr. GRPO normalization flag. |
| [DAPO: Open-Source LLM RL System at Scale](https://arxiv.org/abs/2503.14476) | Yu et al. (2025) | Section 3. | Clip-higher option. |
| [s1: Simple Test-Time Scaling](https://arxiv.org/abs/2501.19393) | Muennighoff et al. (2025) | Sections 2-3. | Budget forcing at inference. |
| [Chain-of-Thought Prompting](https://arxiv.org/abs/2201.11903) | Wei et al. (2022) | Sections 2-3. | - |

### Coding exercises

- REINFORCE with baseline on a toy LM reward
- Bradley-Terry reward-model loss
- DPO loss from scratch (+ TRL comparison)
- GRPO loss from scratch (group advantages, clipping, KL, token-level averaging, Dr. GRPO flag)
- Verifiable reward functions with anti-hacking tests

### Project: Project 7 (part 2) - DPO + GRPO

**Deliverable:** DPO run on your SFT model and a GRPO run on verifiable math with reward/length/accuracy curves + Reproduction #5 + reward-hacking log

### Knowledge checkpoint (close-book)

- [ ] Derive the policy-gradient theorem (log-derivative trick) and explain the baseline.
- [ ] Write the PPO clipped objective and explain what the clip prevents.
- [ ] Derive the DPO loss from the KL-constrained RL objective.
- [ ] Explain GRPO's group-relative advantage and the length bias Dr. GRPO removes.
- [ ] Give three concrete reward-hacking examples and a mitigation for each.

### Day by day

| Date | Phase | Type | Task | What to do | Link | h | Output |
|---|---|---|---|---|---|---|---|
| Mon 23 Nov | P12 | Reading | **RL essentials** | Spinning Up Part 1 (key concepts) and Part 3 (policy optimization); Abbeel L3. | [link](https://spinningup.openai.com/en/latest/spinningup/rl_intro3.html) | 1.5 |  |
| Mon 23 Nov | P12 | Code | **REINFORCE on a toy LM** | Train your W3 GPT (or a tiny model) to maximize a verifiable reward; compare variance with/without baseline. | [link](https://www.youtube.com/watch?v=AKbX1Zvo7r8) | 2 | reinforce.py |
| Tue 24 Nov | P12 | Paper | **PPO + RLHF** | PPO sec. 3-5; Christiano 2017 method; InstructGPT RM/PPO sections; RLHF book reward-model + policy-gradient chapters. | [link](https://arxiv.org/abs/1707.06347) | 1.5 | Paper notes #10 |
| Tue 24 Nov | P12 | Video | **RLHF with code** | Umar Jamil RLHF video - PPO + RLHF sections. | [link](https://www.youtube.com/watch?v=qGyFrqc34yc) | 1 |  |
| Tue 24 Nov | P12 | Code | **Reward model** | Bradley-Terry loss + scalar head on your SFT model; train on ~2K preference pairs; report pairwise accuracy. | [link](https://rlhfbook.com/) | 1 | rm.py |
| Wed 25 Nov | P6 | Paper | **DPO derivation** | DPO sec. 4-5 + Appendix A.1, with Umar Jamil's DPO video. | [link](https://www.youtube.com/watch?v=hvGa5Mba4c8) | 1 |  |
| Wed 25 Nov | P6 | Code | **DPO from scratch** | Policy/reference log-probs of chosen vs rejected, beta; train on your P7 SFT model with a preference subset; compare with TRL DPOTrainer; skim ORPO/KTO/SimPO differences. | [link](https://arxiv.org/abs/2305.18290) | 2.5 | P7: dpo.py |
| Thu 26 Nov | P12 | Paper | **Reasoning models + RLVR** | DeepSeekMath sec. 4 (GRPO), DeepSeek-R1 sec. 2-3, Tulu 3 RLVR section, CS336 L16; skim 'Why We Think'. | [link](https://arxiv.org/abs/2402.03300) | 2 | Paper notes #11 |
| Thu 26 Nov | P12 | Reading | **Reward hacking + verifiers** | Weng's reward-hacking post; design format + answer verifiers and tests that try to hack them. | [link](https://lilianweng.github.io/posts/2024-11-28-reward-hacking/) | 1.5 | verifiers.py |
| Fri 27 Nov | P12 | Paper | **Dr. GRPO + DAPO** | Dr. GRPO sec. 2-3 (length bias), DAPO sec. 3 (clip-higher, dynamic sampling, token-level loss, overlong shaping); HF course ch. 12. | [link](https://arxiv.org/abs/2503.20783) | 1 |  |
| Fri 27 Nov | P12 | Code | **GRPO from scratch** | Group sampling, normalized advantages, clipped ratio, KL to reference, token-level averaging; unit-test on synthetic logits; rollouts via HF generate or vLLM. | [link](https://huggingface.co/learn/llm-course/en/chapter12/4) | 2.5 | P7: grpo.py |
| Sat 28 Nov | P13 | Experiment | **GRPO run + Reproduction #5** | Qwen3-0.6B (or Qwen2.5-0.5B/1.5B-Instruct) on GSM8K-style math, 1 rented GPU for 3-4 h (your loop or TRL GRPOTrainer). Track reward, length, held-out accuracy; compare length growth with/without Dr. GRPO normalization. | [link](https://arxiv.org/abs/2503.20783) | 3 | GRPO curves |
| Sat 28 Nov | P12 | Review | **Connect to reasoning models** | Write-up: RLVR, test-time compute, s1 budget forcing (s1 sec. 2-3), and the reward hacks you observed. | [link](https://arxiv.org/abs/2501.19393) | 1 | P7 (DONE) |

---

<a id="week-10"></a>
## Week 10 - Agents from first principles + MCP

**Dates:** Mon 30 Nov - Sat 05 Dec 2026 - **Phases:** P7, P8 - **Planned hours:** 21.5

**Goal.** Build an agent with no framework, understand every moving part, then map it onto LangGraph and friends and expose tools through your own MCP server.

**Learning flow.** Agent = LLM + loop + tools + state -> raw loop -> planning/reflection/memory -> security + HITL -> MCP -> frameworks -> research agent + eval

### Reading
- **PRIMARY:** [Building effective agents (Anthropic)](https://www.anthropic.com/engineering/building-effective-agents); [Effective context engineering for AI agents (Anthropic)](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents); [MCP specification 2026-07-28 (current)](https://modelcontextprotocol.io/specification/2026-07-28); [MCP 2026-07-28 release notes (what changed: stateless core, deprecations)](https://blog.modelcontextprotocol.io/posts/2026-07-28/)
- **SECONDARY:** [Writing effective tools for agents (Anthropic)](https://www.anthropic.com/engineering/writing-tools-for-agents); [How we built our multi-agent research system (Anthropic)](https://www.anthropic.com/engineering/multi-agent-research-system); [LLM Powered Autonomous Agents (Weng)](https://lilianweng.github.io/posts/2023-06-23-agent/); [LangChain Academy - Introduction to LangGraph (free)](https://academy.langchain.com/courses/intro-to-langgraph); [Hugging Face MCP Course](https://huggingface.co/learn/mcp-course/en/unit0/introduction); [Hugging Face Agents Course](https://huggingface.co/learn/agents-course/en/unit0/introduction)
- **REFERENCE:** [LangGraph docs](https://docs.langchain.com/oss/python/langgraph/overview); [LangChain middleware docs](https://docs.langchain.com/oss/python/langchain/middleware/overview); [LangChain create_agent reference](https://reference.langchain.com/python/langchain/agents/factory/create_agent); [LangSmith evaluation docs](https://docs.langchain.com/langsmith/evaluation); [HF Agents Course - LangGraph unit](https://huggingface.co/learn/agents-course/unit2/langgraph/introduction); [OpenAI Agents SDK docs](https://openai.github.io/openai-agents-python/); [LlamaIndex Workflows docs](https://developers.llamaindex.ai/python/framework/module_guides/workflow/); [smolagents docs](https://huggingface.co/docs/smolagents); [OWASP Top 10 for LLM apps](https://genai.owasp.org/llm-top-10/); [The lethal trifecta (Willison)](https://simonwillison.net/2025/Jun/16/the-lethal-trifecta/); [mini-swe-agent (100-line reference agent)](https://github.com/SWE-agent/mini-swe-agent)

### Videos

| Video | Instructor / channel | Duration | Why watch | Covers |
|---|---|---|---|---|
| [How We Build Effective Agents](https://www.youtube.com/watch?v=D7_ipDqhtwk) | Barry Zhang (Anthropic) - AI Engineer Summit | ~15m | Three principles: don't build agents for everything, keep them simple, think like your agent. | P7 design |

### Papers

| Paper | Authors (year) | Read carefully | Implement |
|---|---|---|---|
| [ReAct: Synergizing Reasoning and Acting](https://arxiv.org/abs/2210.03629) | Yao et al. (2022) | Sections 2-3. | Raw agent loop. |
| [Reflexion](https://arxiv.org/abs/2303.11366) | Shinn, Cassano, Berman, Gopinath, Narasimhan, Yao (2023) | Section 3. | Self-critique step. |
| [MemGPT: Towards LLMs as Operating Systems](https://arxiv.org/abs/2310.08560) | Packer et al. (2023) | Sections 2-3. | Memory tiers in P8. |

### Coding exercises

- Raw agent loop: tool schemas, tool-call parsing, execution, stop conditions, retries, cost accounting, trajectory logs
- Plan-and-execute, self-critique with a verifier, memory compaction, long-term episodic/semantic memory
- Approval gates, tool allow-lists, sandboxed code execution, prompt-injection test cases
- MCP server (tools + resources + prompts) over stdio and Streamable HTTP; MCP client in your agent
- LangChain create_agent + middleware rebuild of the raw loop
- LangGraph StateGraph with reducers, checkpointer, interrupt(), streaming; P8 production version on LangGraph

### Project: Project 8 - AI research agent; Project 9 - MCP server

**Deliverable:** Raw-loop reference agent + LangGraph production research agent (plan -> search -> read -> synthesize with citations -> critique) evaluated on 20 tasks; MCP server with tests + auth; LangChain/LangGraph/smolagents/Agents SDK/LlamaIndex comparison note

### Knowledge checkpoint (close-book)

- [ ] Write an agent loop from memory, including how tool results re-enter the context.
- [ ] Explain short-term vs long-term memory and when to compact context.
- [ ] Explain indirect prompt injection and the lethal trifecta; show your mitigations.
- [ ] Explain MCP hosts/clients/servers, the three server primitives, transports, and what the 2026-07-28 stateless core changed.
- [ ] Map LangGraph's StateGraph/checkpointer/interrupt and LangChain's create_agent/middleware onto the parts of your raw loop.

### Day by day

| Date | Phase | Type | Task | What to do | Link | h | Output |
|---|---|---|---|---|---|---|---|
| Mon 30 Nov | P7 | Reading | **Agent design principles** | Anthropic 'Building effective agents' + Barry Zhang talk; ReAct sec. 2-3. | [link](https://www.anthropic.com/engineering/building-effective-agents) | 1 | Paper notes #12 |
| Mon 30 Nov | P7 | Code | **Raw agent loop** | No framework. JSON-schema tools (search via P5, sandboxed python exec, file read), parse tool calls, execute, append results, max-steps, retries, token/cost accounting, trajectory logs. | [link](https://arxiv.org/abs/2210.03629) | 2.5 | P8: loop.py |
| Tue 01 Dec | P7 | Reading | **Planning, reflection, memory** | Weng agents post; Reflexion sec. 3; MemGPT sec. 2-3; Anthropic context-engineering post. | [link](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents) | 1.5 |  |
| Tue 01 Dec | P7 | Code | **Plan/reflect/remember** | Plan-and-execute mode, verifier-driven self-critique, context compaction, episodic + semantic long-term memory in a vector store, typed state persisted to Postgres/SQLite. | [link](https://arxiv.org/abs/2310.08560) | 2 | P8: memory.py |
| Wed 02 Dec | P7 | Reading | **Tools, security, multi-agent** | Anthropic tool-writing post; OWASP LLM Top 10; lethal trifecta; Anthropic multi-agent research system. | [link](https://www.anthropic.com/engineering/writing-tools-for-agents) | 1.5 |  |
| Wed 02 Dec | P7 | Code | **HITL + security + multi-agent** | Approval gates for side-effecting tools, allow-lists, sandbox, injection tests (poisoned document in the RAG corpus); orchestrator + 2 sub-agents. | [link](https://simonwillison.net/2025/Jun/16/the-lethal-trifecta/) | 2 | security tests |
| Thu 03 Dec | P8 | Reading | **MCP spec** | 2026-07-28 spec (architecture, tools/resources/prompts, transports, authorization) + release notes; HF MCP course unit 1. Note: many tutorials still show the older stateful 2025 revisions. | [link](https://modelcontextprotocol.io/specification/2026-07-28) | 1.5 |  |
| Thu 03 Dec | P8 | Code | **Project 9 - MCP server** | Python SDK server over your retrieval engine: tools (search, fetch_doc), resources (doc://{id}), prompts (cite-answer); stdio + Streamable HTTP; test with MCP Inspector; call it from your agent. | [link](https://huggingface.co/learn/mcp-course/en/unit0/introduction) | 2 | P9 server |
| Fri 04 Dec | P7 | Code | **LangChain 1.0 agents** | Chat models + messages, @tool, structured output, create_agent, middleware (human-in-the-loop, summarization). Rebuild your raw loop with create_agent and map every piece; note that create_agent returns a compiled LangGraph graph. | [link](https://docs.langchain.com/oss/python/langchain/middleware/overview) | 1 | langchain_agent.py |
| Fri 04 Dec | P7 | Code | **LangGraph core** | StateGraph, typed state + reducers, conditional edges, checkpointer (persistence, time travel), interrupt() for approval, streaming. LangChain Academy 'Intro to LangGraph' modules 1-3 (selected lessons) as you code. | [link](https://academy.langchain.com/courses/intro-to-langgraph) | 1.5 | langgraph_agent.py |
| Fri 04 Dec | P7 | Reading | **Other frameworks** | Tiny example each: smolagents CodeAgent, OpenAI Agents SDK (handoffs, guardrails, sessions), LlamaIndex Workflows. Write a 1-page comparison including LangChain/LangGraph. | [link](https://openai.github.io/openai-agents-python/) | 1 | frameworks.md |
| Sat 05 Dec | P7 | Project | **Project 8 - research agent on LangGraph** | Production version built on LangGraph (your raw loop stays as the reference): question -> plan -> search (arXiv API + your RAG via MCP) -> read -> synthesize with citations -> self-critique -> revise; interrupt() before final; traces in LangSmith or your own tracer. Compare traces with the raw loop. | [link](https://docs.langchain.com/oss/python/langgraph/overview) | 3 | P8 agent |
| Sat 05 Dec | P7 | Review | **Evaluate agent + harden MCP** | Run the 20 W7 tasks: citation faithfulness, success, steps, cost. Add auth to the HTTP transport per the spec. | [link](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents) | 1 | P8 + P9 (DONE) |

---

<a id="week-11"></a>
## Week 11 - GPUs and LLM inference optimization

**Dates:** Mon 07 Dec - Sat 12 Dec 2026 - **Phases:** P9 - **Planned hours:** 21.5

**Goal.** Explain every serving optimization from hardware first principles, then prove it with measurements on vLLM.

**Learning flow.** GPU hardware -> roofline & arithmetic intensity -> profiling & kernels -> FlashAttention -> serving (batching, paging, prefix cache) -> quantization -> speculative decoding -> benchmark

### Reading
- **PRIMARY:** [Modal GPU Glossary](https://modal.com/gpu-glossary); [How to Scale Your Model - All About Rooflines (Google DeepMind)](https://jax-ml.github.io/scaling-book/roofline/); [Making Deep Learning Go Brrrr (Horace He)](https://horace.io/brrr_intro.html); [Inside vLLM: Anatomy of a High-Throughput Inference System (Gordic)](https://www.aleksagordic.com/blog/vllm); [Concept note: GPU & inference math](concepts/06-gpu-and-inference-math.md)
- **SECONDARY:** [CS336 2026 Lecture 5 slides - GPUs/TPUs](https://github.com/stanford-cs336/lectures/blob/main/lecture_05.pdf); [CS336 2026 Lecture 6 trace - Kernels, Triton](https://cs336.stanford.edu/lectures/?trace=lecture_06); [Triton tutorials](https://triton-lang.org/main/getting-started/tutorials/); [A Visual Guide to Quantization](https://newsletter.maartengrootendorst.com/p/a-visual-guide-to-quantization)
- **REFERENCE:** [vLLM docs - automatic prefix caching](https://docs.vllm.ai/en/stable/design/prefix_caching/); [TensorRT-LLM docs](https://nvidia.github.io/TensorRT-LLM/); [GPU MODE lectures (code + slides)](https://github.com/gpu-mode/lectures)

### Videos

| Video | Instructor / channel | Duration | Why watch | Covers |
|---|---|---|---|---|
| [FlashAttention - Tri Dao \| Stanford MLSys #67](https://www.youtube.com/watch?v=gMOAud7hZg4) | Tri Dao (Stanford MLSys Seminar) | ~1h | The author explains IO-awareness, tiling and recomputation. | P9 FlashAttention |
| [Fast LLM Serving with vLLM and PagedAttention](https://www.youtube.com/watch?v=Oq2SN7uutbQ) | vLLM authors (Woosuk Kwon, Zhuohan Li) | ~30-40m | Why KV-cache fragmentation limits batch size and how paging fixes it. | P9 serving |
| [Speculative Decoding: When Two LLMs are Faster than One](https://www.youtube.com/watch?v=S-8yr_RibJ4) | Efficient NLP | ~12m | Short, precise explanation of the acceptance rule. | P9 speculative decoding |
| [Flash Attention derived and coded from first principles with Triton (Python)](https://www.youtube.com/watch?v=zy8ChVd_oTM) | Umar Jamil | ~7h | Optional deep dive (2027 track): derive and write FA in Triton, incl. backward pass. | P9 kernels (stretch) |

### Papers

| Paper | Authors (year) | Read carefully | Implement |
|---|---|---|---|
| [FlashAttention](https://arxiv.org/abs/2205.14135) | Dao, Fu, Ermon, Rudra, Re (2022) | Sections 2-3 (algorithm, IO analysis). | Tiled online-softmax attention in PyTorch. |
| [Efficient Memory Management for LLM Serving with PagedAttention](https://arxiv.org/abs/2309.06180) | Kwon et al. (2023) | Sections 3-4, 6. | - |
| [Sarathi-Serve (chunked prefill)](https://arxiv.org/abs/2403.02310) | Agrawal et al. (2024) | Sections 2-4. | - |
| [Fast Inference from Transformers via Speculative Decoding](https://arxiv.org/abs/2211.17192) | Leviathan, Kalman, Matias (2022) | Sections 2-3. | Speculative sampling. |
| [LLM.int8()](https://arxiv.org/abs/2208.07339) | Dettmers, Lewis, Belkada, Zettlemoyer (2022) | Sections 3-4. | - |
| [GPTQ](https://arxiv.org/abs/2210.17323) | Frantar, Ashkboos, Hoefler, Alistarh (2022) | Sections 3-4 (idea level). | - |
| [AWQ: Activation-aware Weight Quantization](https://arxiv.org/abs/2306.00978) | Lin et al. (2023) | Section 3. | - |

### Coding exercises

- Roofline calculator (FLOPs, bytes, intensity, ridge point) for matmul / attention / decode
- torch.profiler + torch.compile on your GPT; Triton vector-add and fused-softmax kernels
- Tiled online-softmax attention in PyTorch (numerically equal to naive)
- Speculative sampling with your small/large GPT pair
- vLLM load tests across precision, prefix caching and spec decoding

### Project: Project 10 - Optimize & serve an LLM with vLLM

**Deliverable:** Benchmark report (TTFT p50/p99, TPOT, throughput vs concurrency; BF16 vs FP8 vs INT4; prefix cache; spec decoding) with every result explained via roofline/memory math + Reproduction #6

### Knowledge checkpoint (close-book)

- [ ] Compute the arithmetic intensity of decode at batch 1 and the batch size where it becomes compute-bound on an H100.
- [ ] Explain why FlashAttention is faster despite doing the same (or more) FLOPs.
- [ ] Explain PagedAttention, continuous batching and chunked prefill, and their effect on TTFT/TPOT.
- [ ] Pick a quantization scheme for a latency-bound chatbot vs a throughput-bound batch job and justify it.

### Day by day

| Date | Phase | Type | Task | What to do | Link | h | Output |
|---|---|---|---|---|---|---|---|
| Mon 07 Dec | P9 | Reading | **GPU architecture** | GPU Glossary (SM, warp, tensor core, HBM, L2, shared memory, occupancy); CS336 L5 slides + video. | [link](https://modal.com/gpu-glossary) | 1.5 |  |
| Mon 07 Dec | P9 | Reading | **Compute vs memory vs overhead** | Horace He 'brrr'. | [link](https://horace.io/brrr_intro.html) | 1 |  |
| Mon 07 Dec | P9 | Review | **Roofline exercises** | Scaling-book roofline chapter; intensity of (B,d)x(d,d) in bf16; H100 ridge point; decode-bound analysis. | [link](https://jax-ml.github.io/scaling-book/roofline/) | 1 | roofline.py |
| Tue 08 Dec | P9 | Video | **Kernels & Triton** | CS336 L6 trace + video; CUDA model (grid/block/thread, coalescing) from the glossary. | [link](https://cs336.stanford.edu/lectures/?trace=lecture_06) | 1.5 |  |
| Tue 08 Dec | P9 | Code | **Profile + first kernels** | torch.profiler on your GPT (top kernels, memory-bound ops), torch.compile speedup; write Triton vector-add and fused softmax and benchmark vs PyTorch. | [link](https://triton-lang.org/main/getting-started/tutorials/02-fused-softmax.html) | 2 | kernels/ |
| Wed 09 Dec | P13 | Paper | **FlashAttention** | Sec. 2-3 (tiling, online softmax, recomputation, IO complexity) + Tri Dao talk; FA2 abstract. | [link](https://arxiv.org/abs/2205.14135) | 1.5 | Paper notes #13 |
| Wed 09 Dec | P9 | Code | **Online-softmax tiled attention** | Block loops in PyTorch; verify equality with naive attention; count HBM reads/writes analytically. | [link](https://www.youtube.com/watch?v=gMOAud7hZg4) | 2 | flash_ref.py |
| Thu 10 Dec | P9 | Reading | **Serving systems** | vLLM paper sec. 3-4; Gordic 'Inside vLLM'; Sarathi-Serve abstract + sec. 3; TTFT, TPOT/ITL, throughput, goodput. | [link](https://www.aleksagordic.com/blog/vllm) | 1.5 |  |
| Thu 10 Dec | P9 | Reading | **Quantization for inference** | FP32/FP16/BF16/FP8/INT8/INT4 layouts; LLM.int8 outliers; GPTQ and AWQ core ideas; KV-cache quantization; second half of the visual guide. | [link](https://newsletter.maartengrootendorst.com/p/a-visual-guide-to-quantization) | 2 | quant notes |
| Fri 11 Dec | P9 | Paper | **Speculative decoding** | Leviathan et al. sec. 2-3 + Efficient NLP video. | [link](https://arxiv.org/abs/2211.17192) | 1 |  |
| Fri 11 Dec | P9 | Code | **Speculative sampling** | Draft = tiny GPT, target = larger GPT; acceptance rate and speedup vs k. | [link](https://www.youtube.com/watch?v=S-8yr_RibJ4) | 1.5 | specdec.py |
| Fri 11 Dec | P9 | Reading | **TensorRT-LLM overview** | Engine building, in-flight batching, FP8/FP4; compare with vLLM (read-only). | [link](https://nvidia.github.io/TensorRT-LLM/) | 1 |  |
| Sat 12 Dec | P9 | Project | **Project 10 - vLLM serving** | Serve Qwen3-8B (and/or your merged P7 model) on a rented GPU; load test at concurrency 1/8/32/128; BF16 vs FP8 vs AWQ-INT4; prefix caching on/off; speculative decoding on/off. | [link](https://github.com/vllm-project/vllm) | 3 | Benchmarks |
| Sat 12 Dec | P13 | Review | **Perf report + Reproduction #6** | Explain every number with roofline/memory math; continuous vs static batching throughput. | [link](https://arxiv.org/abs/2309.06180) | 1 | P10 (DONE) |

---

<a id="week-12"></a>
## Week 12 - Distributed training & data (working knowledge) + multimodal AI

**Dates:** Mon 14 Dec - Sat 19 Dec 2026 - **Phases:** P11 (Mon-Tue), P10 (Wed-Sat) - **Planned hours:** 21.5

**Goal.** Reason fluently about training memory and parallelism strategies, then build a multimodal RAG system over documents, images and audio.

**Learning flow.** Memory math -> DP/ZeRO/FSDP -> TP/PP -> data pipelines | ViT/CLIP -> VLM architecture -> documents/audio -> multimodal RAG

### Reading
- **PRIMARY:** [The Ultra-Scale Playbook (Hugging Face)](https://huggingface.co/spaces/nanotron/ultrascale-playbook); [Understanding Multimodal LLMs (Raschka)](https://magazine.sebastianraschka.com/p/understanding-multimodal-llms); [Vision Language Models (Better, faster, stronger) - HF 2025](https://huggingface.co/blog/vlms-2025); [nanoVLM (repo + blog)](https://github.com/huggingface/nanoVLM)
- **SECONDARY:** [CS336 2026 Lecture 7 trace + Lecture 8 slides - Parallelism](https://cs336.stanford.edu/lectures/?trace=lecture_07); [CS336 2026 Lectures 13-14 traces - Data](https://cs336.stanford.edu/lectures/?trace=lecture_14); [picotron (4D parallelism in <300 lines/file)](https://github.com/huggingface/picotron); [HF Computer Vision Course - CLIP unit](https://huggingface.co/learn/computer-vision-course/en/unit4/multimodal-models/clip-and-relatives/clip); [ColPali blog](https://huggingface.co/blog/manu/colpali)
- **REFERENCE:** [The Smol Training Playbook](https://huggingface.co/spaces/HuggingFaceTB/smol-training-playbook); [ML Engineering Open Book (Bekman)](https://github.com/stas00/ml-engineering); [HF Audio Course - TTS unit](https://huggingface.co/learn/audio-course/en/chapter6/introduction); [CS336 2026 Lecture 17 trace - multimodality](https://cs336.stanford.edu/lectures/?trace=lecture_17)

### Videos

| Video | Instructor / channel | Duration | Why watch | Covers |
|---|---|---|---|---|
| [Coding a Multimodal (Vision) Language Model from scratch in PyTorch](https://www.youtube.com/watch?v=vAmKB7iPkWw) | Umar Jamil | ~5h45m | Watch the SigLIP encoder, projector and token-merging sections (~2h) - exactly how images become LM tokens. | P10 VLMs |
| [Stanford CS336 Spring 2026 - Lectures 7-8 (Parallelism)](https://www.youtube.com/playlist?list=PLoROMvodv4rMqXOcazWaTUHhq-yembLCV) | Liang / Hashimoto (Stanford) | ~1h20m each | Collective communication and DP/TP/PP trade-offs with real numbers. | P11 distributed |

### Papers

| Paper | Authors (year) | Read carefully | Implement |
|---|---|---|---|
| [ZeRO: Memory Optimizations Toward Training Trillion Parameter Models](https://arxiv.org/abs/1910.02054) | Rajbhandari, Rasley, Ruwase, He (2019) | Sections 4-5. | - |
| [Megatron-LM](https://arxiv.org/abs/1909.08053) | Shoeybi et al. (2019) | Section 3. | - |
| [The FineWeb Datasets](https://arxiv.org/abs/2406.17557) | Penedo et al. (2024) | Sections 3-4. | - |
| [An Image is Worth 16x16 Words (ViT)](https://arxiv.org/abs/2010.11929) | Dosovitskiy et al. (2020) | Section 3.1. | Patch embedding. |
| [Learning Transferable Visual Models from Natural Language Supervision (CLIP)](https://arxiv.org/abs/2103.00020) | Radford et al. (2021) | Sections 2.1-2.5, Figure 3 pseudocode. | Symmetric CLIP loss. |
| [Visual Instruction Tuning (LLaVA)](https://arxiv.org/abs/2304.08485) | Liu, Li, Wu, Lee (2023) | Sections 3-4. | - |
| [ColPali: Efficient Document Retrieval with VLMs](https://arxiv.org/abs/2407.01449) | Faysse et al. (2024) | Sections 3-4. | Page-image retrieval in P11. |
| [Robust Speech Recognition via Large-Scale Weak Supervision (Whisper)](https://arxiv.org/abs/2212.04356) | Radford, Kim, Xu, Brockman, McLeavey, Sutskever (2022) | Sections 2-3. | - |

### Coding exercises

- Training-memory calculator (weights, grads, Adam states, activations; DDP vs ZeRO-1/2/3)
- (optional) DDP/FSDP of your GPT on 2 GPUs with torchrun
- CLIP loss + patch embedding; zero-shot classification with OpenCLIP
- nanoVLM read-through + short run (or SmolVLM fine-tune with TRL)
- Docling + ColPali/ColQwen page retrieval + Whisper ingestion

### Project: Project 11 - Multimodal RAG

**Deliverable:** Multimodal RAG over PDFs with charts/tables + audio: hybrid text/page-image retrieval, VLM answers with page citations, evaluated on 50 multimodal questions

### Knowledge checkpoint (close-book)

- [ ] Compute training memory for an 8B model under DDP vs ZeRO-3 on 8x80GB.
- [ ] Choose a parallelism layout for 70B on 64 GPUs and justify it.
- [ ] Explain image -> patches -> embeddings -> projector -> LM tokens.
- [ ] Explain why ColPali-style retrieval can beat OCR pipelines on visually rich documents.

### Day by day

| Date | Phase | Type | Task | What to do | Link | h | Output |
|---|---|---|---|---|---|---|---|
| Mon 14 Dec | P11 | Reading | **Memory + data parallelism** | Ultra-Scale Playbook: memory anatomy, activation recomputation, gradient accumulation, DP, ZeRO-1/2/3; ZeRO sec. 5; mixed precision. | [link](https://huggingface.co/spaces/nanotron/ultrascale-playbook) | 2 | Paper notes #14 |
| Mon 14 Dec | P11 | Code | **Memory calculator** | 8B full fine-tune under DDP vs ZeRO-3 on 8x80GB incl. activations and checkpointing; optional DDP/FSDP run of your GPT on 2 GPUs. | [link](https://arxiv.org/abs/1910.02054) | 1.5 | mem_calc.py |
| Tue 15 Dec | P11 | Reading | **Model parallelism** | Playbook TP (column/row), sequence/context parallel, PP (GPipe, 1F1B); Megatron sec. 3; CS336 L7-8; read picotron tensor_parallel.py. | [link](https://github.com/huggingface/picotron) | 2 |  |
| Tue 15 Dec | P11 | Reading | **Pretraining data** | CS336 L13-14 (sources, filtering, dedup, mixing, synthetic) + FineWeb sec. 3-4. Exercise: layout for 70B on 64xH100 + a data-pipeline sketch. | [link](https://arxiv.org/abs/2406.17557) | 1.5 | design.md |
| Wed 16 Dec | P10 | Paper | **ViT + CLIP** | ViT sec. 3.1 (patches as tokens; CNN revision: patch embed = strided conv); CLIP sec. 2 + Figure 3; SigLIP abstract. | [link](https://arxiv.org/abs/2103.00020) | 1.5 | Paper notes #15 |
| Wed 16 Dec | P10 | Code | **CLIP from the loss up** | Symmetric InfoNCE + patch embedding; zero-shot classification and text-image retrieval with OpenCLIP. | [link](https://huggingface.co/learn/computer-vision-course/en/unit4/multimodal-models/clip-and-relatives/clip) | 2 | clip.ipynb |
| Thu 17 Dec | P10 | Reading | **VLM architecture** | Raschka multimodal article; LLaVA sec. 3-4 (projector, 2-stage training); HF VLMs 2025; Umar Jamil PaliGemma sections. | [link](https://magazine.sebastianraschka.com/p/understanding-multimodal-llms) | 1.5 |  |
| Thu 17 Dec | P10 | Code | **nanoVLM** | Read vision encoder -> modality projector -> LM; run a short training (or fine-tune SmolVLM with TRL); inspect how image tokens enter the sequence. | [link](https://github.com/huggingface/nanoVLM) | 2 | vlm notes |
| Fri 18 Dec | P10 | Paper | **Documents, audio, video** | ColPali sec. 3-4 + blog; OCR (Docling) vs OCR-free; tables/charts; Whisper sec. 2 + run it; TTS overview; video = frame sampling + VLM. | [link](https://arxiv.org/abs/2407.01449) | 1.5 |  |
| Fri 18 Dec | P10 | Code | **Multimodal ingestion** | PDF -> Docling text/tables + page images -> ColPali/ColQwen embeddings; audio -> Whisper transcripts with timestamps. | [link](https://github.com/illuin-tech/colpali) | 2 | ingest.py |
| Sat 19 Dec | P10 | Project | **Project 11 - multimodal RAG** | Hybrid text + page-image retrieval; VLM answers over retrieved pages with page citations; voice queries via Whisper. | [link](https://github.com/illuin-tech/colpali) | 3 | P11 app |
| Sat 19 Dec | P10 | Review | **Evaluate** | 50 multimodal questions (charts, tables, scanned pages) through ragevals; text-only vs image retrieval. | [link](concepts/04-rag-and-evaluation-metrics.md) | 1 | P11 (DONE) |

---

<a id="week-13"></a>
## Week 13 - Capstone build: AI Software Engineer (integration)

**Dates:** Mon 21 Dec - Sat 26 Dec 2026 - **Phases:** CAP - **Planned hours:** 18

**Goal.** Integrate the components you already built into one repo-aware coding agent.

**Learning flow.** Design review -> repo understanding -> agent core -> execution & testing -> routing & HITL -> multimodal + MCP -> evaluation

### Reading
- **PRIMARY:** [Capstone spec in this repo](09-capstone-ai-software-engineer.md); [mini-swe-agent (read all ~100 lines first)](https://github.com/SWE-agent/mini-swe-agent); [Aider repository map (tree-sitter + graph ranking)](https://aider.chat/docs/repomap.html); [SWE-bench harness](https://github.com/SWE-bench/SWE-bench)
- **SECONDARY:** [RouteLLM paper](https://arxiv.org/abs/2406.18665); [Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)
- **REFERENCE:** [SWE-bench leaderboards](https://www.swebench.com/); [Demystifying evals for AI agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents)

### Papers

| Paper | Authors (year) | Read carefully | Implement |
|---|---|---|---|
| [SWE-bench](https://arxiv.org/abs/2310.06770) | Jimenez, Yang, Wettig, Yao, Pei, Press, Narasimhan (2023) | Sections 2-3. | Harness integration. |
| [RouteLLM](https://arxiv.org/abs/2406.18665) | Ong et al. (2024) | Sections 3-4. | Router in capstone. |

### Coding exercises

- repo-intel MCP server (tree-sitter symbols, repo map, hybrid code search)
- Agent core with read/search/edit/test/shell/git tools in a no-network Docker sandbox
- Edit-test loop, approval gates, model router
- Screenshot/diagram input via VLM
- SWE-bench subset + in-house task evaluation

### Project: Capstone milestones M1-M5

**Deliverable:** Working end-to-end agent that fixes real issues in your own repos under human approval

### Knowledge checkpoint (close-book)

- [ ] See the capstone acceptance criteria.

### Day by day

| Date | Phase | Type | Task | What to do | Link | h | Output |
|---|---|---|---|---|---|---|---|
| Mon 21 Dec | CAP | Review | **Design review** | Re-read the capstone spec, threat model and eval plan; read mini-swe-agent end to end. | [link](https://github.com/SWE-agent/mini-swe-agent) | 1 | ADR.md |
| Mon 21 Dec | CAP | Project | **M1 - repo understanding** | tree-sitter parsing, symbol graph + ranked repo map, function/class-level chunking, hybrid code search via P4; expose as a 'repo-intel' MCP server. | [link](https://aider.chat/docs/repomap.html) | 2.5 | M1 |
| Tue 22 Dec | CAP | Project | **M2 - agent core** | Planner -> executor loop from P8 with read_file, search_code, edit_file (patch), run_tests, run_shell (Docker, no network), git_diff; task scratchpad + long-term repo notes. | [link](https://github.com/SWE-agent/mini-swe-agent) | 3.5 | M2 |
| Wed 23 Dec | CAP | Project | **M3 - execution, testing, routing, HITL** | Reproduce the bug with a failing test first; edit-test loop with budget; approval before applying patches; router: small vLLM model for cheap steps, frontier model for planning/editing, with fallback. | [link](https://arxiv.org/abs/2406.18665) | 3.5 | M3 |
| Thu 24 Dec | CAP | Project | **M4 - multimodal + MCP + observability** | Screenshot/diagram of a bug -> VLM description; docs RAG (P5); MCP client to your servers (P9 + repo-intel); per-step tracing. | [link](https://huggingface.co/blog/vlms-2025) | 3.5 | M4 |
| Fri 25 Dec | CAP | Buffer | **Rest / buffer (25 Dec)** | Holiday. Use only to catch up if you are behind. |  | 0 |  |
| Sat 26 Dec | CAP | Project | **M5 - evaluation** | 30 in-house tasks (bug fix, add test, refactor) + 20-50 SWE-bench Lite/Verified instances via the official harness: resolve rate, cost, steps, approval rate. | [link](https://github.com/SWE-bench/SWE-bench) | 4 | M5 results |

---

<a id="week-14"></a>
## Week 14 - Capstone hardening, final assessment, 2027 plan

**Dates:** Mon 28 Dec - Thu 31 Dec 2026 - **Phases:** CAP - **Planned hours:** 14

**Goal.** Fix what the evals reveal, harden security, and finish the year with a measured, documented system.

**Learning flow.** Error analysis -> fixes + ablations -> security hardening + CI -> demo -> close-book assessment -> 2027 plan

### Reading
- **PRIMARY:** [Capstone spec - milestones M6-M8](09-capstone-ai-software-engineer.md); [2027 continuation plan](10-2027-continuation.md)

### Coding exercises

- Ablations: repo map, routing, reflection
- Injection tests, secret redaction, budgets, timeouts
- Eval regression suite in CI

### Project: Capstone milestones M6-M8

**Deliverable:** Capstone v1 + results table + demo + public write-up

### Knowledge checkpoint (close-book)

- [ ] Pass every phase checkpoint close-book.
- [ ] Explain every design decision in the capstone and the eval evidence behind it.

### Day by day

| Date | Phase | Type | Task | What to do | Link | h | Output |
|---|---|---|---|---|---|---|---|
| Mon 28 Dec | CAP | Project | **M6 - error analysis + ablations** | Fix the top failure modes; ablate repo map, routing, reflection. | [link](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents) | 3.5 | M6 |
| Tue 29 Dec | CAP | Project | **M7 - hardening** | Prompt-injection tests (malicious README/issue text), secret redaction, cost/time budgets; eval regression suite in CI via ragevals. | [link](https://genai.owasp.org/llm-top-10/) | 3.5 | M7 |
| Wed 30 Dec | CAP | Project | **M8 - demo + write-up** | Architecture, results table, lessons learned, recorded demo. | [link](09-capstone-ai-software-engineer.md) | 2 | Capstone (DONE) |
| Wed 30 Dec | P13 | Review | **Final close-book assessment** | All phase checkpoints; update the skills sheet honestly. | [link](08-skill-checkpoints.md) | 1.5 | Assessment |
| Thu 31 Dec | P13 | Review | **Retrospective + 2027 plan** | Pick a 2027 track; schedule the deferred items into Q1. | [link](10-2027-continuation.md) | 2 | 2027 plan |
| Thu 31 Dec | P13 | Review | **Publish portfolio** | Clean READMEs for the 11 projects + capstone; a 'what I built in 13 weeks' post. | [link](09-capstone-ai-software-engineer.md) | 1.5 | Portfolio |


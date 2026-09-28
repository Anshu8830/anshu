# AI Software Engineer — 2026 curriculum

A project-driven plan to go from strong software engineer with intermediate ML/DL to an engineer who can implement, train, evaluate, optimize and serve modern AI systems and read current research — scheduled day by day from **Monday 28 September to Thursday 31 December 2026**.

**Start here:** open the Excel tracker [`tracker/AI_Engineer_2026_Plan.xlsx`](tracker/AI_Engineer_2026_Plan.xlsx) (tick tasks as you go) and read [1. Executive roadmap](curriculum/01-executive-roadmap.md).

## At a glance

- **14 weeks · 82 study days · ~290 hours** (3.5 h Mon–Fri, 4 h Sat, Sundays off; 25 Dec buffer).
- The requested scope is ~800–1,000 hours, so every topic is assigned a depth — **MASTER**, **WORKING** or **DEFER → 2027** — instead of being dropped. The trade-offs are spelled out in the roadmap.
- **11 projects + capstone**, each reused by later ones; **6 small paper reproductions**; ~80 papers ordered easiest → hardest.
- **One primary resource per topic.** Stanford CS336 (Spring 2026) is the spine for language modelling, systems and post-training; Karpathy, 3Blue1Brown, Umar Jamil, the Google DeepMind scaling book, Hugging Face playbooks/courses, Anthropic's engineering posts, Hamel Husain, Nathan Lambert and others are primary where they explain a topic better.
- Every link was checked on 28 Sep 2026.

| Week | Dates | Focus | Project |
|---|---|---|---|
| W1 | 28 Sep – 3 Oct | Diagnostic ML/DL revision → attention from scratch | P1 Attention |
| W2 | 5–10 Oct | Llama-style Transformer block + encoder-decoder | P2 Transformer |
| W3 | 12–17 Oct | BPE tokenizer + training a small GPT (CS336 A1) | P3 part 1 |
| W4 | 19–24 Oct | KV cache, sampling, inference math, scaling laws, MoE | P3 part 2 |
| W5 | 26–31 Oct | Embeddings, BM25, IVF-PQ, HNSW | P4 Retrieval engine |
| W6 | 2–7 Nov | RAG basic → advanced → agentic/graph | P5 Advanced RAG |
| W7 | 9–14 Nov | Evaluation: judges, faithfulness, statistics, agent evals | P6 Eval framework |
| W8 | 16–21 Nov | SFT, chat templates, LoRA, QLoRA | P7 Fine-tune (1) |
| W9 | 23–28 Nov | RL for LLMs: PPO/RLHF, DPO, RLVR/GRPO | P7 Fine-tune (2) |
| W10 | 30 Nov – 5 Dec | Agents from first principles, LangChain/LangGraph, MCP | P8 Research agent, P9 MCP server |
| W11 | 7–12 Dec | GPUs, rooflines, FlashAttention, vLLM, quantization | P10 vLLM serving |
| W12 | 14–19 Dec | Distributed training (working) + multimodal | P11 Multimodal RAG |
| W13–W14 | 21–31 Dec | Capstone: AI Software Engineer | Capstone |

## Contents

| # | Document | What's in it |
|---|---|---|
| 1 | [Executive roadmap](curriculum/01-executive-roadmap.md) | Phases, weeks, hours, depth per topic, scope trade-offs |
| 2 | [Prerequisite assessment](curriculum/02-prerequisite-assessment.md) | What you skip, what you revise, the day-1 diagnostic |
| 3 | [Month-by-month plan](curriculum/03-month-by-month.md) | Sep → Dec 2026 (+ Jan–Jun 2027 outline), slippage rules |
| 4 | [Week-by-week curriculum](curriculum/04-week-by-week.md) | Every week: reading (primary/secondary/reference), videos, papers, coding, project, hours, deliverable, checkpoint, day-by-day table |
| 5 | [Resource library](curriculum/05-resource-library.md) | Courses, books, articles, videos (with durations and why), repos, docs, freshness warnings |
| 6 | [Project ladder](curriculum/06-project-ladder.md) | P1–P11 + capstone: specs, skills, dependencies, compute budget |
| 7 | [Paper reading list](curriculum/07-paper-reading-list.md) | Easiest → hardest: why, prerequisites, sections, implement, reproduce |
| 8 | [Skill checkpoints](curriculum/08-skill-checkpoints.md) | Close-book "explain + build" tests after each phase |
| 9 | [Capstone: AI Software Engineer](curriculum/09-capstone-ai-software-engineer.md) | Architecture, components, approval policy, threat model, milestones, eval plan |
| 10 | [2027 continuation](curriculum/10-2027-continuation.md) | Deferred items (Q1) + tracks: research engineer, LLM systems, AI architect, frontier-model engineer |

**Concept notes** (the "teach me" layer — intuition → math → shapes → code → experiment):
[attention & Transformer](curriculum/concepts/01-attention-and-transformer.md) ·
[prompt → next token](curriculum/concepts/02-prompt-to-next-token.md) ·
[retrieval & vector search](curriculum/concepts/03-retrieval-and-vector-search.md) ·
[RAG & evaluation metrics](curriculum/concepts/04-rag-and-evaluation-metrics.md) ·
[post-training math (LoRA, DPO, GRPO)](curriculum/concepts/05-post-training-math.md) ·
[GPU & inference math](curriculum/concepts/06-gpu-and-inference-math.md)

## The Excel tracker

[`tracker/AI_Engineer_2026_Plan.xlsx`](tracker/AI_Engineer_2026_Plan.xlsx) has five sheets:

| Sheet | Contents |
|---|---|
| **Summary** | Progress dashboard (tasks/hours done, ahead/behind vs today, by phase, by week), **what you already know** (skip / quick revision), **what you are learning** with target level (MASTER / WORKING / DEFER-2027) and a self-rating column |
| **Daily Plan** | 167 tasks: date, day, week, phase, type, topic, description, link, hours, deliverable/assignment, **Done** (☐/☑ dropdown), notes. Done rows turn green; overdue dates turn red |
| **Projects** | P1–P11 + capstone with due dates, deliverables, skills, status dropdown, done tick |
| **Papers** | All papers with difficulty, week, link, why, prerequisites, sections, implement/reproduce, read tick |
| **Resources** | Every course/book/article/video/repo/doc used, with the weeks it appears in |

Tick a task by choosing ☑ in the *Done* column. If you use Excel 365 you can also convert that column to native checkboxes (Insert → Checkbox); the formulas count both.

## Editing the plan

The week-by-week page, the paper list and the Excel file are generated from two data files so they never drift apart:

```bash
pip install openpyxl
python tools/build.py        # validates links/hours, rewrites curriculum/04, curriculum/07 and the xlsx
```

- `tools/plan_data.py` — link registry, phases, projects, papers, skills map
- `tools/plan_weeks.py` — the day-by-day schedule
- `tools/build.py` — validation + rendering (fails if a day's hours don't match the budget or a link key is unknown)

The committed workbook was additionally recalculated with LibreOffice so formula values show up in previewers; Excel and Google Sheets recalculate on open either way.

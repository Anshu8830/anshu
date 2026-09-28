# Concept note 3 — Embeddings, sparse retrieval and vector search internals

Used in week 5 (and the multi-vector parts in weeks 6 and 12).

---

## 1. Similarity

For vectors `q, d ∈ ℝⁿ`:

```
dot(q, d)    = Σ qᵢ dᵢ
cos(q, d)    = dot(q, d) / (‖q‖ ‖d‖)
‖q − d‖²     = ‖q‖² + ‖d‖² − 2 dot(q, d)
```

If all vectors are L2-normalized, the three rankings are identical (`‖q − d‖² = 2 − 2cos`). That is why you normalize embeddings and then use inner-product indexes (FAISS `IndexFlatIP`, pgvector `vector_ip_ops` / `vector_cosine_ops`). If a model was trained with dot product and **not** normalized, normalizing changes its behaviour — read the model card.

## 2. Where embeddings come from: contrastive learning

A bi-encoder maps query and passage independently to vectors (so passages can be pre-computed and indexed). It is trained so matching pairs score higher than non-matching ones.

**InfoNCE with in-batch negatives** (DPR, SBERT variants, E5, BGE): for a batch of N pairs `(qᵢ, dᵢ)`,

```
L = −(1/N) Σᵢ log  exp(sim(qᵢ, dᵢ)/τ) / Σⱼ exp(sim(qᵢ, dⱼ)/τ)
```

- It is a softmax cross-entropy where the "classes" are the N passages in the batch; the other N−1 are free negatives.
- **Temperature τ** (≈0.01–0.05) controls how hard the loss focuses on the closest negatives.
- **Hard negatives** (BM25 results that are *not* relevant) teach fine distinctions and matter more than batch size past a point.
- CLIP (week 12) uses the same loss symmetrically over image→text and text→image.

**Bi-encoder vs cross-encoder vs late interaction**

| | Scoring | Cost | Use |
|---|---|---|---|
| Bi-encoder | `sim(f(q), g(d))`, one vector each | pre-compute docs; ANN search | first-stage retrieval |
| Cross-encoder | `score = h([q; d])`, full attention across both | one forward pass per (q, d) pair | reranking top 20–100 |
| Late interaction (ColBERT) | `Σ_{i∈q} max_{j∈d} qᵢ·dⱼ` (MaxSim over token vectors) | stores a vector per token | high-quality retrieval / reranking; ColPali for page images |

## 3. Sparse retrieval: TF-IDF and BM25

**BM25** score of document D for query Q:

```
score(D, Q) = Σ_{t ∈ Q} IDF(t) · f(t, D) · (k₁ + 1) / ( f(t, D) + k₁ · (1 − b + b · |D| / avgdl) )

IDF(t) = ln( (N − n(t) + 0.5) / (n(t) + 0.5) + 1 )
```

- `f(t, D)`: term frequency; the `k₁` term **saturates** it (the 10th occurrence adds far less than the 1st). k₁ ≈ 1.2–2.0.
- `b` (≈0.75) controls **length normalization**: long documents are penalized for accidental matches.
- `IDF` rewards rare terms. N = number of docs, n(t) = docs containing t.
- Implementation: an **inverted index** `term → [(doc_id, tf), …]`; only postings of query terms are touched, which is why BM25 is fast.

Why BM25 still matters: it nails exact identifiers (error codes, function names, SKUs), needs no training, and BEIR shows it is a strong **zero-shot** baseline where dense models trained on other domains can lose. Dense retrieval wins on paraphrase and semantic matches. **Hybrid** gets both.

**Reciprocal Rank Fusion** (hybrid without score calibration):

```
RRF(d) = Σ_{rankers r} 1 / (k + rank_r(d)),   k ≈ 60
```

## 4. Approximate nearest neighbour (ANN) search

Exact search is `O(N · n)` per query. For 10M vectors × 1024 dims that is 10¹⁰ multiply-adds per query and 40 GB of float32 — too slow and too big. ANN trades a little recall for orders of magnitude in speed and memory.

### 4.1 IVF (inverted file)
1. Train k-means with `nlist` centroids (e.g. √N to 16√N).
2. Assign each vector to its nearest centroid's list.
3. Query: find the `nprobe` nearest centroids and scan only their lists.

Cost ≈ `nlist + (nprobe / nlist) · N` distance computations. `nprobe` is the recall/speed knob.

### 4.2 Product quantization (PQ)
Compress each vector to a few bytes:
1. Split the n-dim vector into `m` sub-vectors of n/m dims.
2. For each sub-space, train k-means with `k* = 256` centroids (a codebook).
3. Store each vector as `m` one-byte codes → **m bytes per vector** (e.g. 1024-dim float32 = 4096 bytes → m = 64 gives 64 bytes, 64× smaller).

**Asymmetric distance computation (ADC):** for a query q, precompute a table `T[j][c] = ‖q⁽ʲ⁾ − centroid_{j,c}‖²` (m × 256 entries). The approximate distance to any database vector is then `Σ_j T[j][code_j]` — **m table lookups and adds**, no floating-point vector math. IVF-PQ combines both: IVF picks the lists, PQ makes scanning them cheap (usually on residuals `x − centroid`).

### 4.3 HNSW (hierarchical navigable small world graphs)
- Each vector is a node linked to ~M near neighbours. Each node is also assigned a maximum layer drawn from an exponentially decaying distribution, so upper layers are sparse "highways".
- **Search:** start at the entry point in the top layer, greedily move to the neighbour closest to q until no improvement, drop a layer, repeat; on layer 0 run a beam search keeping the `efSearch` best candidates.
- **Build:** insert nodes one at a time using the same search with `efConstruction`, then connect to M neighbours chosen by a diversity heuristic (not just the M closest).
- Complexity ≈ `O(log N)` hops. Trade-offs: `M` ↑ = better recall, more memory; `efSearch` ↑ = better recall, slower queries. Memory ≈ raw vectors + `~2M` links per node — HNSW does **not** compress vectors, so it is often paired with quantization in production.

### 4.4 Vector databases
FAISS is a **library** (indexes in your process). pgvector, Qdrant, Milvus, etc. are **databases**: persistence, CRUD, replication, and — critically — **filtering**. Filtering with ANN is hard: post-filtering can return fewer than k results; pre-filtering can break graph connectivity. Read how your DB does it (pgvector iterative scans, Qdrant's filterable HNSW) and benchmark with your real filters.

## 5. IR metrics

For a query with ranked results `r₁, r₂, …` and a set of relevant documents `Rel`:

```
Precision@K = |{relevant in top K}| / K
Recall@K    = |{relevant in top K}| / |Rel|
MRR         = mean over queries of 1 / rank of the first relevant result
DCG@K       = Σ_{i=1..K} (2^{relᵢ} − 1) / log₂(i + 1)
nDCG@K      = DCG@K / IDCG@K          (IDCG = DCG of the ideal ordering)
```

- **Recall@K** is what matters for RAG's first stage (did the right chunk make it into the context at all?).
- **MRR / nDCG** matter when order matters (reranking, UI search).
- Always report the metric on **your** queries — leaderboards (MTEB, BEIR) choose candidates, they do not choose for you.

## 6. Checkpoint questions

1. Derive why normalized vectors make cosine, dot and L2 rankings identical.
2. What does k₁ = 0 do to BM25? What does b = 0 do?
3. Memory for 50M 768-dim vectors: float32 flat vs IVF-PQ with m = 48 (ignore list overhead).
4. Why can HNSW + a restrictive metadata filter return fewer than k results, and what are the fixes?
5. When would you pick a cross-encoder reranker over a late-interaction model?

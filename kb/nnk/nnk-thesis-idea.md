# NNK Thesis Idea — Working Memory

Date: 2026-04-21

## Core idea
NNK (Non-Negative Kernel Regression) reframes neighborhood definition as a **non-negative sparse approximation** problem in kernel space.

Instead of defining neighbors by a fixed `k` or distance threshold alone, NNK starts from a candidate local set (often kNN) and solves for **non-negative weights** that reconstruct a query point in RKHS. The nonzero coefficients define the true neighbors.

This gives a unifying view:
- neighborhood selection = sparse representation
- weights = reconstruction coefficients
- geometry = pruning of redundant neighbors

The key conceptual claim is that **nearest neighbors, sparse coding, and geometry are the same object viewed from different angles**.

## Why it matters
Classical kNN / epsilon-neighborhoods are thresholding methods: they select points based only on query-to-point similarity and ignore redundancy among neighbors.

NNK improves this by accounting for:
- query-to-neighbor similarity
- neighbor-to-neighbor similarity
- local geometric diversity

As a result, NNK produces neighborhoods that are:
- adaptive rather than fixed-size
- sparse but meaningful
- geometrically diverse
- more robust to hyperparameters like `k`
- better suited for graph construction and downstream learning

## Signature geometric insight
The main theorem is the **Kernel Ratio Interval (KRI)**.

For a query `q` and two candidate neighbors `i` and `j`, both can be active only if their relative similarities satisfy a kernel ratio constraint. Intuitively:
- if two candidates are too similar to each other, one becomes redundant
- NNK keeps neighbors that explain different directions around the query
- the selected neighbors form a local convex polytope around the query

This is the most elegant part of the thesis: the solution is not just sparse, but **geometrically interpretable**.

## Thesis-level contributions distilled
1. **Neighborhoods as sparse approximation**
   - Reinterprets kNN/epsilon-neighborhoods as thresholding-based sparse coding.
   - Positions NNK as a better sparse approximation objective.

2. **NNK neighborhood algorithm**
   - Solve non-negative kernel regression on a local candidate set.
   - Nonzero weights define adaptive neighbors and edge strengths.

3. **Geometry via KRI and polytope view**
   - NNK prunes geometrically redundant points.
   - Neighborhoods correspond to convex polytopes / directional spanning sets.

4. **Connection to pursuit methods**
   - Strong relationship to OMP / basis pursuit / non-negative least squares.
   - NNK acts like an efficient one-shot local OMP using a good candidate set.

5. **Graph construction**
   - Leads to sparse, high-quality graphs.
   - Improves graph SSL and manifold learning while keeping runtime practical.

6. **Interpolation view**
   - NNK yields a local polytope interpolator.
   - Interpolative like simplicial approaches, but more practical and adaptive in high dimension.

7. **DeepNNK**
   - Applies NNK to deep feature embeddings.
   - Gives a local geometric/interpolative view of neural network behavior.
   - Useful for generalization estimation, explainability, self-supervised evaluation, few-shot learning, and dataset distance.

8. **NNK-Means**
   - Extends the idea into summarization / dictionary learning.
   - Learns representative atoms with geometry-aware non-negative sparse coding.

9. **Geometry of deep learning / MGMs**
   - Uses NNK polytopes to measure invariance, curvature, and intrinsic dimension in learned representations.
   - Applies especially well to self-supervised learning analysis.

## High-level research identity of the work
This thesis is not just "a better nearest-neighbor method."
It is a **general geometric framework** for thinking about:
- local representation
- graph construction
- interpolation
- summarization
- deep feature analysis

The recurring theme is:
**learn from local non-negative sparse structure rather than blunt proximity.**

## Strong future directions to iterate on

### 1. Noise-aware / robust NNK
A known limitation in the thesis is that NNK can be too aggressive in pruning when features are noisy or include non-informative dimensions.
Potential directions:
- regularized NNK with controlled redundancy
- uncertainty-aware kernels
- robust objectives / slack in KRI
- Bayesian or probabilistic NNK
- feature denoising before neighborhood optimization

### 2. Learn the kernel jointly with NNK
The theory is powerful but still depends on the kernel.
Potential work:
- learn kernels optimized for NNK sparsity + downstream utility
- deep metric learning objectives that explicitly favor NNK geometry
- task-specific kernels for text, multimodal embeddings, graphs, biological sequences

### 3. NNK as a modern retrieval / memory primitive for AI
Very promising AI angle:
- retrieval for RAG that prefers geometrically diverse evidence, not redundant nearest chunks
- exemplar selection for in-context learning
- adaptive memory graph construction for agents
- neighborhood-based calibration and confidence estimation for LLM embeddings
- explanation by showing minimal non-redundant supporting examples

### 4. NNK for representation learning objectives
Instead of using NNK only after embeddings are learned, use it during training.
Ideas:
- train embeddings so same-class or semantically related points form stable NNK polytopes
- loss terms encouraging desirable intrinsic dimension / curvature / invariance profiles
- NNK-consistent SSL objectives
- NNK-based regularization for collapse avoidance

### 5. NNK for graph foundation models / GNNs
Potential directions:
- build better input graphs for GNNs from raw features
- dynamic NNK graphs across layers
- pruning redundant edges in large graph transformers
- local polytope aggregation instead of fixed message passing neighborhoods

### 6. NNK for multimodal and generative AI
Interesting opportunity:
- image-text neighborhood alignment
- diverse retrieval of support examples across modalities
- latent-space geometry diagnostics for generative models
- adversarial / OOD detection using local polytope support size and shape
- diffusion / generative manifold analysis using NNK graph metrics

### 7. NNK for dataset curation and distillation
Building on NNK-Means:
- representative subset selection for foundation model fine-tuning
- coreset construction with geometry guarantees
- de-duplication beyond plain nearest-neighbor similarity
- curriculum design based on interpolation spread / local geometric complexity

### 8. Educational / visualization layer
This idea is highly visual and teachable.
Great outreach / productizable path:
- interactive 2D/3D demo showing kNN vs NNK
- animate KRI pruning cones / planes
- show polytope formation live as points move
- explain deep representation geometry through NNK polytopes

This could become a signature explanatory artifact for the work.

## Implementation demos reviewed
Two implementation demos were shared and reviewed on 2026-04-21.

### 1. GPU image demo
A Colab-style PyTorch + FAISS GPU implementation that:
- uses MNIST image features (flattened pixels)
- builds a top-k candidate neighborhood with FAISS inner-product search
- solves an approximate NNK objective with iterative thresholding on GPU
- compares weighted kNN vs NNK classification on the same neighborhood candidates
- reports sparsity reduction by counting nonzeros in the resulting weights

Important implementation idea:
- NNK can be made practical by using **fast ANN/kNN retrieval first**, then solving a **small local non-negative optimization** per query.
- This supports a modern systems framing: retrieval + local sparse reranking.

### 2. Text demo
A Colab-style text pipeline that:
- extracts sentence embeddings using Hugging Face models (example: XLM-R)
- uses FAISS for nearest-neighbor retrieval over text embeddings
- solves the NNK weights with a custom non-negative QP solver
- compares kNN vs NNK for intent classification on Amazon MASSIVE
- exposes an explainability mode by printing which examples remain after NNK pruning

Important implementation idea:
- NNK is not limited to geometric toy data or images; it works naturally on **embedding spaces from modern language models**.
- This strongly supports future applications in **retrieval, example selection, explanation, and memory pruning for AI systems**.

### Implementation takeaway
These demos make the broader thesis direction much more concrete:

**NNK = candidate retrieval + local non-negative sparse support selection.**

That decomposition is highly compatible with modern AI systems because it maps onto:
- ANN search infrastructure
- embedding-based pipelines
- reranking layers
- retrieval/exemplar selection for language and multimodal systems

This is probably the cleanest path to turning the theory into practical AI tooling.

## Most promising AI application buckets
If focusing effort, likely strongest near-term buckets are:
1. **RAG / retrieval diversity and evidence pruning**
2. **Deep embedding analysis and model diagnostics**
3. **Few-shot / non-parametric classifiers on learned embeddings**
4. **Graph construction for foundation-model feature spaces**
5. **Dataset summarization / distillation / deduplication**
6. **Embedding-space reranking layers for text and multimodal systems**

## Working thesis for future iteration
NNK can be evolved from a neighborhood algorithm into a broader principle:

**A local intelligence primitive for AI systems:**
select a minimal, non-redundant, geometrically meaningful support set around a query, then reason/interpolate/decide using that support.

That framing feels broader and more modern than the original nearest-neighbor framing while staying faithful to the math.

## Suggested next concrete work items
- Re-read thesis and extract a compact “NNK for modern AI” position paper outline
- Identify which assumptions in KRI / NNK survive for modern embedding spaces from transformers
- Prototype NNK-based retrieval reranking on embedding search results
- Prototype NNK-based exemplar selection for few-shot prompting / ICL
- Build a visual explainer for KRI and local polytope formation
- Revisit robustness to noise / redundancy with a modern benchmark suite
- Explore NNK as a regularizer or loss term in representation learning

## Short one-line essence
NNK is a geometry-aware, non-negative sparse neighborhood principle that turns local similarity into an adaptive support set for learning, interpolation, graphs, and modern AI systems.

# NNK Ideas Log

Date: 2026-04-21

## Context
Charlie wants a durable place to save the ongoing discussion around the NNK thesis, the algorithm itself, and future research directions. The immediate motivation was that the chat discussion was getting too long to comfortably read inline.

## What was reviewed
### Thesis materials reviewed
Core thesis chapter files reviewed:
- `NNK_Thesis_LaTex/chapters/nnk_neighbors.tex`
- `NNK_Thesis_LaTex/chapters/nnk_interpolation.tex`
- `NNK_Thesis_LaTex/chapters/nnk_means.tex`
- `NNK_Thesis_LaTex/chapters/GOL_nnk.tex`

These cover:
- NNK neighborhood theory
- sparse approximation interpretation of neighborhoods
- KRI / geometric characterization
- interpolation and DeepNNK
- NNK-Means and dictionary-learning / clustering connection
- geometry of deep learning via NNK graphs / MGMs

### Implementation demos reviewed
Two Python demos were reviewed:
- GPU demo: MNIST + FAISS + PyTorch + approximate GPU NNK solver
- Text demo: sentence embeddings + FAISS + custom non-negative QP solver + Amazon MASSIVE classification

These demos made the systems interpretation concrete:
- retrieval / candidate generation first
- local non-negative sparse support selection second

## Core conceptual summary
NNK reframes neighborhood definition as a **non-negative sparse coding problem** in kernel / embedding space.

This is the central unification:
- thresholding sparse coding ↔ kNN / epsilon neighborhoods
- orthogonalized non-negative sparse approximation ↔ NNK
- dictionary learning ↔ clustering / summarization (NNK-Means)

This suggests the thesis is not just about one algorithm, but about a broader principle:
**local structure in data can be understood as sparse support selection under geometric constraints.**

## Key discussion pivot
Charlie emphasized that before talking about applications, the more important research direction is:

> If neighborhoods are sparse coding representations, how can we import other sparse coding concepts into neighborhood definitions?

This is the real next-step research program.

## Main algorithmic idea under discussion
NNK should be seen as only one point in a larger design space of sparse neighborhood models.

The more general question is:
- what sparse coding priors or formulations lead to useful new neighborhood definitions?
- which of them preserve locality and geometric interpretability?
- which ones become genuinely new neighborhood algorithms rather than just generic pursuit methods?

## Sparse-coding-to-neighborhood directions discussed

### 1. Structured sparsity → structured neighborhoods
Potential analogues:
- group sparsity
- hierarchical sparsity
- block sparsity
- tree sparsity

Neighborhood interpretation:
- pick neighbors across groups/scales/subspaces instead of from one undifferentiated pool
- enforce diversity with structure, not just pairwise redundancy pruning

### 2. Robust sparse coding → robust neighborhoods
Potential analogues:
- noise-aware objectives
- outlier slack
- Huber / robust losses
- elastic net style penalties
- controlled redundancy for stability

Motivation:
- plain NNK may over-prune under noisy or irrelevant dimensions
- robust NNK could preserve the geometry while improving stability

### 3. Multi-scale / overcomplete sparse coding → multi-scale neighborhoods
Potential analogues:
- union of multiple kernels
- multiple bandwidths
- multiple feature views
- overcomplete candidate dictionaries

Motivation:
- a neighborhood need not come from one kernel / one scale only
- could address kernel sensitivity and representation scale issues

### 4. Dictionary coherence / sparse coding diagnostics → neighborhood quality theory
Potential analogue:
- local coherence as a way to reason about when thresholding is enough and when NNK-style optimization is necessary

Motivation:
- sharpen the theory of neighborhood optimality
- explain when kNN is near-optimal vs when geometry-aware pruning matters

### 5. Learned dictionaries / prototypes → prototype neighborhoods
Potential analogue:
- neighborhoods over learned atoms instead of raw points
- mixture of instance and prototype support sets

Motivation:
- extend NNK-Means beyond summarization toward neighborhood definition itself

### 6. Analysis sparse models → operator-defined neighborhoods
More speculative:
- define neighborhoods via sparse local operator responses rather than synthesis from points

Motivation:
- could yield a fundamentally different notion of local structure

### 7. Symmetry-aware / shift-aware sparse models → transformation-aware neighborhoods
Potential analogue:
- neighborhoods modulo transformations or group actions
- support sets stable under nuisance transformations

Motivation:
- tie NNK more directly to invariance/equivariance and representation learning

## Strongest near-term algorithmic candidates
From the discussion, the most promising near-term directions appear to be:

1. **Robust / noise-aware NNK**
2. **Structured sparsity neighborhoods**
3. **Multi-scale / multi-kernel NNK**

These seem like the cleanest next steps that remain faithful to the thesis core.

## Three concrete candidate algorithm families

### Elastic / Robust NNK
Add:
- non-negative reconstruction
- mild L2 or elastic-net regularization
- explicit residual slack / noise model

Goal:
- reduce brittleness
- avoid over-pruning in noisy high-dimensional settings

### Group NNK
Partition candidates into groups:
- scales
- modalities
- channels
- semantic clusters

Goal:
- select non-redundant support with structural priors
- make neighborhoods more balanced and semantically meaningful

### Multi-kernel NNK
Use candidate support from:
- multiple kernels
- multiple bandwidths
- multiple feature representations

Goal:
- overcome single-kernel sensitivity
- define neighborhoods across scales/views

## Philosophical constraint identified
Not every sparse coding method should be called a neighborhood.

A good neighborhood generalization should preserve:
1. **locality** — selected support should still be meaningfully near the query in some representation
2. **interpretability** — there should still be a geometric or statistical reason why those support points were selected

If the support becomes arbitrary or nonlocal, it stops being a neighborhood and becomes generic sparse coding.

## New systems interpretation from demos
The implementation demos suggest a clean practical view:

**NNK = candidate retrieval + local non-negative sparse reranking**

This may be a useful algorithmic abstraction independent of application domain.

## Working research framing
A possible next-paper / next-chapter framing:

**From sparse neighborhoods to structured sparse neighborhoods**

Possible progression:
- kNN = thresholding
- NNK = non-negative sparse coding
- NNK-Means = dictionary learning / clustering
- next = robust, structured, and multi-scale neighborhood models

## Suggested next steps
1. Build a compact matrix: sparse coding concept → neighborhood analogue → geometric meaning → practical viability
2. Formalize robust / elastic NNK first, since it directly addresses a known weakness
3. Explore group / multi-kernel NNK as a second branch
4. Revisit sparse coding theory tools (coherence, recovery conditions, structured sparsity theory) from the neighborhood lens
5. Keep the focus on algorithmic principles before jumping too fast into applications

## Notes
- A longer distilled memory note also exists at `memory/2026-04-21-nnk-thesis-idea.md`
- This file is intended as a readable running log for future repo import / paper planning

---
title: "Understanding MLPs as Hashing Functions: A Geometric Perspective"
date: 2024-08-15
excerpt: When we think about Multi-Layer Perceptrons (MLPs), we often visualize them as interconnected neurons processing information. However, there's an elegant alternative perspective: viewing MLPs as sophisticated hashing functions that partition input space and map these partitions to outputs.
permalink: /posts/2024/08/mlp-geometry/
categories:
  - research
tags:
  - deep learning
  - MLP
toc: true
toc_sticky: true
---
WORK IN PROGRESS. 

# Understanding MLPs Through the Lens of Hashing

When we think about Multi-Layer Perceptrons (MLPs), we often visualize them as interconnected neurons processing information. However, there's an elegant alternative perspective: viewing MLPs as sophisticated hashing functions that partition input space and map these partitions to outputs. This mental model, which I'll share from my experiences at Tenyx Research, provides powerful insights into how neural networks learn and adapt.

## The Basic Building Block: Neurons as Hyperplanes

At its core, a single neuron (perceptron) acts as a hyperplane that divides the input space into two regions. When we apply a ReLU activation function, we're essentially deciding which side of this hyperplane we're interested in. This simple geometric interpretation leads to a fascinating observation: **each neuron creates a partition in the input space**.

## From Individual Neurons to MLPs

When we stack multiple neurons together to form an MLP, something remarkable happens. Each layer creates increasingly refined partitions of the input space. Here's a concrete example:

```
Hash Code Output
0 0 0 0 1 → f(1)
...
0 1 1 0 0 → g(9)
0 1 1 0 1 → h(10)
```

In this example, a layer with 5 neurons could theoretically create 2^5 = 32 different partitions. However, in practice, we often find that only a subset of these partitions (in this case, 7) are actually utilized. This observation has profound implications for both model efficiency and learning dynamics.

## Learning as Partition Refinement

When an MLP learns, it's essentially doing two things simultaneously:
1. Adjusting the partitions (by rotating and shifting hyperplanes)
2. Modifying the mapping from these partitions to outputs

This dual nature of learning helps explain why neural networks are so powerful yet sometimes challenging to train. We're not just learning a mapping – we're learning both the optimal way to partition the input space AND how to map these partitions to desired outputs.

## Modern Architecture Insights

In contemporary neural architectures, we often remove bias terms for normalization purposes. Geometrically, this constrains our hyperplanes to pass through the origin. While this might seem limiting, it actually provides beneficial regularization properties and simplifies optimization.

## Understanding LoRA

One interesting application of this geometric perspective comes in understanding low-rank adaptation methods like LoRA. This technique works by:

**LoRA (W + AB)x**:
- Focuses on efficiency through rank reduction
- Simple and effective for many tasks
- Does not explicitly prevent forgetting

Geometrically, this is equivalent to 
1. Updating the partitions only in a specific direction
2. Effective for tasks that are close to the pre-training distribution. Typically, LoRA does not result in new partitions as the hyperplane movements are severely constrained.
3. Note that the mapping in the partitions is changed, and thus, LoRA does not explicitly avoid forgetting. 

## Practical Implications

This geometric perspective has several practical applications:
1. Better understanding of model capacity and memorization
2. More intuitive approaches to model compression
3. Improved techniques for domain adaptation and transfer learning

## Looking Forward

This mental model opens up exciting possibilities for future research, particularly in:
- Understanding Transformer architectures (especially the interaction between attention and feed-forward layers)
- Developing better domain constraint mechanisms
- Improving model reasoning capabilities through geometric analysis

## Conclusion

Viewing MLPs as hashing functions provides a powerful mental model for understanding deep learning. By thinking about neural networks in terms of partitions and mappings, we can develop more intuitive approaches to architecture design, optimization, and adaptation.

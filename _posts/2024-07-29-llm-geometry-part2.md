---
title: "Part 2 - The Hidden Geometry of Large Language Models: A New Perspective on Reasoning"
date: 2024-07-29
excerpt: At Tenyx, we've delved into the intricate workings of Large Language Models (LLMs) to uncover the geometric structures underlying their reasoning capabilities. Our research provides new insights into how LLMs process information and the implications for improving their reasoning abilities.
permalink: /posts/2024/07/llm-geometry-part2/
tags:
  - LLM
  - reasoning
categories:
  - research
---

_Written for article published at Tenyx. Co-author: Romain Cosentino._

## Introduction

At Tenyx, we've delved into the intricate workings of Large Language Models (LLMs) to uncover the geometric structures underlying their reasoning capabilities. Our research provides new insights into how LLMs process information and the implications for improving their reasoning abilities. Look at our latest pre-print here: [Arxiv Page](https://arxiv.org/abs/2407.02678)

LLMs have revolutionized natural language processing, demonstrating remarkable abilities in tasks ranging from translation to complex problem-solving. However, the mechanisms behind their reasoning capabilities have remained largely obscure. This lack of understanding has posed challenges for improving LLM performance and ensuring their reliability in critical applications.

Our research takes a novel approach by examining LLMs through a geometric lens. We've developed a framework that allows us to analyze the intricate structures formed within these models as they process information.

‍<figure>
<a href="/images/llm_geometry/cpa.png"><img src="/images/llm_geometry/cpa.png" alt="Piecewise Affine Geometry"/></a>

</figure>

By focusing on concepts such as input space partitioning, intrinsic dimension, and the density of self-attention graphs, we've been able to draw connections between the prompt and its impact on reasoning abilities. Our findings not only provide deeper insights into how LLMs function but also suggest new avenues for enhancing their performance.

In the following, we delve into our key findings, exploring how the geometry of LLMs shapes their reasoning capabilities and what this means for the future of AI development.

## Key Findings

1. We establish a connection between an LLM's expressive power and the density of its self-attention graphs. This relationship is rooted in how MLPs partition their input space, creating regions where different affine transformations occur.

2. The intrinsic dimension of inputs to the multi-layer perceptron (MLP) blocks in LLMs plays a crucial role in their expressive capacity. Higher intrinsic dimension correlates with greater expressive power.

3. Increasing either the context length or the number of attention heads in an LLM can lead to higher intrinsic dimension of the MLP’s input.

4. Our experiments on the GSM8K-Zero dataset demonstrate that increases in intrinsic dimension, particularly in the final layers of an LLM, correlate with improved reasoning performance.

## Implications

We therefore posit that reasoning capabilities are tied to the expressive power induced by the MLPs. As we showed in this work, methods such as many-shot and chain-of-thought are exploiting such phenomena.

This research provides a new framework for understanding and potentially enhancing LLM reasoning abilities. By focusing on geometric properties like intrinsic dimension and input space partitioning, we may be able to design more efficient and capable language models without necessarily increasing model size.

## Future Directions

While our work reveals intriguing correlations between geometric properties and reasoning capabilities, many questions remain. How do these insights relate to LLM generalization? Can we leverage this understanding to create smaller models with comparable reasoning abilities to larger ones?

As we continue to explore these questions, we hope our geometric perspective will contribute to the development of more powerful and efficient language models, pushing the boundaries of what's possible in the realm of LLMs.

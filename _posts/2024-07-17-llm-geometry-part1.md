---
title: "Part 1 - The Hidden Geometry of Large Language Models: Implications on Safety & Toxicity‍"
date: 2024-07-17
excerpt: At Tenyx, we've spent countless hours peering into the intricate workings of Large Language Models (LLMs). Today, we're excited to share our research, in collaboration with Brown University, that sheds light on the geometric structures and transformations governing these models. Our work provides new insights into how LLMs process their inputs and the implications for AI safety in applications driven by LLMs.
permalink: /posts/2024/07/llm-geometry-part1/
tags:
  - LLM
  - safety
categories:
  - research
---

_Written for article published at Tenyx. Co-author: Romain Cosentino._

## Introduction

At Tenyx, we've spent countless hours peering into the intricate workings of Large Language Models (LLMs). Today, we're excited to share our research, in collaboration with Brown University, that sheds light on the geometric structures and transformations governing these models. Our work provides new insights into how LLMs process their inputs and the implications for AI safety in applications driven by LLMs.

## (Technical Aspect) Unpacking Transformers in LLM

<figure>
	<a href="/images/llm_geometry/attention_geometry.png"><img src="/images/llm_geometry/attention_geometry.png" alt="Attention Geometry"/></a>
	<figcaption> Figure 1: Illustration of LLM geometry at a single transformer layer for a 3-token input sequence. (Left) Convex hulls induced by two self-attention heads projected onto the output layer. (Middle) The combination of the heads induces a Minkowski sum of the single-head convex hulls. (Right) The output of the multi-head attention is mapped onto the unit circle, which is then partitioned by the continuous piecewise affine mapping. </figcaption>
</figure>

Our research focuses on two critical components of transformer layers in LLM: Multi-Head Attention (MHA) and Multilayer Perceptrons (MLPs). By developing mathematical tools to analyze these components, we've uncovered fundamental properties that enhance our understanding:

- The output of a MHA can be characterized as a Minkowski sum of convex hulls. This property gives us a precise understanding of how LLMs process relationships between words in a sentence.
- The expressivity of MLPs grows exponentially with the “intrinsic dimension” of the MHA output. This insight helps explain phenomena like chain-of-thought reasoning and in-context learning.

## A Surprising Vulnerability and Its Implications

<figure>
	<a href="/images/llm_geometry/rlhf_jailbreak.png"><img src="/images/llm_geometry/rlhf_jailbreak.png" alt="RLHF Jailbreak"/></a>
	<figcaption>Figure 2: The graph demonstrates an upward trend, with larger positive changes in ID correlating with higher RLHF bypass of Llama models. In our paper, we also propose quantitative experiments highlighting such phenomena.</figcaption>
</figure>

One of our most surprising findings is that our geometric understanding reveals a simple attack that can circumvent existing AI safety measures. We found that prompts—including random words—that increase the "intrinsic dimension" of the input can sometimes cause an LLM to generate toxic content, despite being trained to avoid such behavior using techniques like Reinforcement Learning from Human Feedback (RLHF).

This discovery highlights a significant challenge in AI safety. Current methods for making LLMs safer may not be as robust as previously thought when faced with longer inputs, be it via retrieval augmented generation or increased context via instructions and examples for agentic behaviors.
A New Approach to Toxicity Detection

On a positive note, our geometric insights led us to develop a highly effective method for detecting and intervening when this toxicity bypass occurs. We created a set of "spline” features that capture the geometric properties of how an LLM processes text.

Using these features, we achieved remarkable results, outperforming existing state-of-the-art toxicity detection systems by a significant margin. Our approach excels even with limited training data and can identify toxicity embedded even in a large context of input.

## Takeaways

- **Revealing Vulnerabilities**: Our research highlights shortcomings in current AI safety measures and suggests more robust approaches.
- **Improved Detection**: Our toxicity detection method is more accurate and faster than existing solutions.
- **Enhanced Understanding**: Our results improve the understanding of these complex systems through a geometric view.
- **New Analytical Framework**: The mathematical framework we've developed opens up new avenues for analyzing and improving LLMs.

## The Road Ahead

While our study focused on toxicity detection and generation, we're excited about the broader potential of this geometric approach to unlock many more insights into LLMs. As AI systems become increasingly integrated into our daily lives, understanding their inner workings is more crucial than ever.

Our work is a significant step towards making AI systems more transparent, reliable, and safe. As we continue to explore the capabilities of LLMs, we're committed to peeling back the complexity and revealing the simple mathematical structures that define these systems.

We look forward to seeing how other researchers and practitioners will build upon our findings. The journey to fully understand and harness the power of LLMs is far from over, but we believe our geometric approach provides a valuable new path forward.

Stay tuned for more updates on our research and discoveries as we continue to push the boundaries of AI understanding and safety.

—-

If you're interested in learning more about our work, you can read our paper here: [Openreview PDF](https://openreview.net/pdf?id=glfcwSsks8)

Attending ICML 2024? We'd love to chat! Feel free to reach out to us if you're interested in discussing our research or exploring potential collaborations. Our poster presentation is scheduled for Wednesday, July 24th, from 4:30 AM (6:00 AM PDT). It will be located in Hall C, section 4-9, at booth number 705.

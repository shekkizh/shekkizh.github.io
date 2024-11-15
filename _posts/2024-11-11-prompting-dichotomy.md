---
title: "Open-ended vs Descriptive Prompting: Finding the right balance in your AI use-cases"
date: 2024-11-15
excerpt: When working with language models, the way we phrase our prompts can dramatically affect the quality and usefulness of the responses we receive. In this post we explore the dichotomy in setting up prompts - being open-ended vs descriptive - and understand the implication of each.
permalink: /posts/2024/11/prompting-dichotomy/
categories:
  - development
tags:
  - LLM
  - prompting
---

When working with large language models (LLMs), the way we phrase our prompts can dramatically affect the quality and usefulness of the responses we receive. In this post we explore the dichotomy in setting up prompts - being open-ended vs descriptive - and understand the implications of each. The focus is to provide an intuition in terms of the underlying model rather than a set of prompt instructions (there are several out there already 😅).

## Understanding Transformers in LLM: Convex Polytopes + Hashing Functions

Before we get into the types of prompting, let's take a quick geometric detour on how transformers in LLMs process a sequence of text, i.e., prompt. A transformer is made up of two key components: Attention and Multi-Layer Perceptrons (MLPs).

In our previous post on [MLPs as Hashing Functions](/posts/2024/08/mlp-geometry/), we discussed how MLPs can be viewed as partitioning the input space and mapping functions. This view applies in the context of transformers as well (MLP here being 1-hidden layered) and completes half the picture of what happens geometrically. In fact, even though the input to the transformer is a sequence of text, the MLP processes this sequence independently as if they are unrelated data points. This should give you a sense of why increasing the size of tokenizers, the component that converts text into data points, can ease the learning process for the model. Well, that's a topic for another post!

_What's the catch in the above picture?_ The answer lies in the other half of transformers: Attention. Unlike the simple case of input data and partitions we think off with MLPs, attention dynamically modifies the location of the input data processed by the MLP. Figure 1. presents this idea visually.

<figure>
	<a href="/images/llm_geometry/attention_MLP.png"><img src="/images/llm_geometry/attention_MLP.png" alt="Attention + MLP Geometry"/></a>
	<figcaption> Figure 1: Illustration of attention mapping of an input (corresponding to the word "square") to different partitions in an MLP. The partitions do not change, however the space of partition in which the input data falls can change and lead to a different mapping. This means even though we have fixed tokenizer size, the number of data points processed by the MLP during training will exponentially increase with attention. </figcaption>
</figure>

Attention is the component in transformer which operates on the sequence, creating dependency among the input texts. You can think of _attention_ to be working on _representing_ the current text (given or to be generated) as a function of the texts that came before it (referred to as causal attention). Now, depending on how this representation turns out you can have different representation of the text as input to MLP, i.e, different sequence of texts lead to different versions of the same current text and consequently a different mapping function applied by the MLP.

<figure class="half">
	<a href="/images/llm_geometry/attention_poly4.png"><img src="/images/llm_geometry/attention_poly4.png" alt="Attention 4t"/></a>
   <a href="/images/llm_geometry/attention_poly5.png"><img src="/images/llm_geometry/attention_poly5.png" alt="Attention 5t"/></a>
	<figcaption> Figure 2: Space of existence for the current text (say t') given preceding text as a result of attention. An attention mapping represents a given text by a convex combination of the text that precede it. In the figure, each vertex corresponds to a preceding text. With 4 preceding texts (Left), t' will live in the volume of a tetrahedron (3-simplex). This will include the case where t' is represented in one of the faces, i.e., a subset of the 4 texts. However, having an additional text in the sequence for representation (Right) creates a larger space of existence for t'. Given MLP partitions are fixed, this means acess to larger set of function mappings for t'.</figcaption>
</figure>

Figure 2. illustrates geoemtrically the mapping defined by attention on a text. A key takeaway here is that having more **context** (preceding text) can lead to a larger space of existence and consequently more set of function mappings. This mental picture has often helped me in making sense of several research works on LLMs, be it few-shot prompting, chain-of-thought, or test-time compute to improve reasoning.

# Prompting

Finally, to prompting! The understanding above essentially boils down to this: when writing system instructions and prompts, you are addressing an attention mechanism that favors specific sequences in texts, i.e., the training corpus. By creating prompts and sequences that resemble text found during pre-training, the LLM will respond and follow instruction more accurately.

To become proficient at prompting, the best approach is to practice and experiment with different prompts, as various models integrate training data differently. However, the fundamental concept of the **internet** remains consistent, allowing skills learned with one model to be transferable to others, i.e, markdowns, HTML tags and so on. If you actively browse the texts in the internet, you are possibly in a good spot already when it comes to prompting.

## The Open-ended Approach

Open-ended prompting is one where you let the model do the work and you simply state what you're trying to achieve without much constraints. In this approach, it is important to ensure the model generates some context before answering your question. Note that when you are using ChatGPT or [Claude](https://docs.anthropic.com/en/release-notes/system-prompts#oct-22nd-2024), the application is already prompted with long context. This means the model is already in a state where it can generate answers. There is no escaping the requirement of context, provided or generated, if you want a smart chatbot.

The benefits of this approach include:

- Lower barrier to entry for newcomers. Easily transferable to other models.
- Opportunity for creative suggestions. The generation is constrained by the space of text the model generates rather than your text.

However, open-ended prompts can lead to:

- Inefficient for use-cases where speed is crucial.
- Multiple follow-ups. If not generating enough context, the model might fall short in answering and would require multiple steps before achieving required context to respond correctly.
- Hallucinated or unstructured responses. The initial text generated sets the stage for the future response. Consequently, this approach is often unpredictable.

## The Descriptive Approach

Descriptive prompting is like writing with a formal specification document. This approach includes attaching long text files and search based augmentation of user inputs. Through the description one is explicitly setting the space of response, allowing the model to respond with answer immediately.

Advantages:

- More precise and consistent outputs. Depending on the size of the context, the model is heavily constrained to the vocabulary in the context.
- Fewer iterations needed. There is usually less variability in the responses generated.
- Better for use-cases where speed to answer is critical.
- Ideally, you want to get to this state of prompt when building customer facing applications.

Drawbacks:

- Responses can feel mechanical or rigid. Moreover, things that are undesirable in generation would require a lot of effort to undo.
- Needs upfront investment. Demands careful planning and multiple refinements to get right.
- Requires expertise. Transferring the prompt for use with another model might require effort.

# Prompting in a Spectrum

The reality is that effective prompting isn't about choosing one approach over the other – it's about finding the right balance for your specific application. Start with one approach, observe the results, and adjust accordingly. Remember that the best prompting strategy is the one that gets you the results you need.

As technology continues to evolve, we may see even more sophisticated ways to interact with these systems. For now, creating a mental model of how different texts in your prompt affects the output you obtain is a powerful tool for consistently delivering results, current or future.

_Footnote: The technical content in the post makes several simplifying assumptions to present an easy to understand picture of transformers and its relationship with prompting. However, the message should remain the same for the general case without these assumptions._

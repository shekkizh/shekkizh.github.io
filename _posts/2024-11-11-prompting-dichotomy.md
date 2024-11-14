---
title: "Open-ended vs Descriptive Prompting: Finding the right balance in your AI use-cases"
date: 2024-08-15
excerpt: When working with language models, the way we phrase our prompts can dramatically affect the quality and usefulness of the responses we receive. In this post we explore the dichotomy in setting up prompts - being open-ended vs formal and descriptive - and understand the implication of each.
permalink: /posts/2024/11/prompting-dichotomy/
categories:
  - development
tags:
  - LLM
  - prompting
---

When working with large language models (LLMs), the way we phrase our prompts can dramatically affect the quality and usefulness of the responses we receive. In this post we explore the dichotomy in setting up prompts - being open-ended vs formal and descriptive - and understand the implications of each. The focus is to provide an intuition in terms of the underlying model rather than a concrete set of prompt instructions (there are several out there already 😅).

## Understanding Transformers in LLM: Convex Polytopes + Hashing Functions

Before we get into the types of prompting, let's take a quick geometric detour to what it means to prompt i.e., the sequence of text input to the LLM. At the heart of LLMs is the transformer architecture. Transformer is made up of two key components: Attention and Multi-Layer Perceptrons (MLPs).

In our previous post on [MLPs as Hashing Functions](/posts/2024/08/mlp-geometry/), we discussed how MLPs can be viewed as hashing out partitions of the input space and mapping functions on these partitions. This view applies in the context of Transformers as well (MLP here is always 1-hidden layered) and completes half the picture of what happens in the architecture. In fact, even though the input to the transformer is a sequence of text, the MLPs process this input independently as if they are unrelated data points in a high-dimensional space. This should give you a sense of why increasing the size of tokenizers, the component that converts text into data points, can ease the learning process for the model. Well, that's a topic for someother post!

What's the catch in the above picture? The answer lies in the other half of the picture: Attention. Unlike the simple case of input data and partitions we saw about MLPs, attention dynamically modifies the location of the input data processed by the MLP. Figure 1. presents this idea visually.

<figure>
	<a href="/images/llm_geometry/attention_MLP.png"><img src="/images/llm_geometry/attention_MLP.png" alt="Attention + MLP Geometry"/></a>
	<figcaption> Figure 1: Illustration of attention mapping of an input (corresponding to the word *square*) to different partitions in an MLP. The partitions do not change, however the space of partition in which the input data falls can change and lead to a different output. This means even though we have fixed tokenizer size, the number of data points processed by the MLP during training can exponentially increase due to attention. </figcaption>
</figure>

We got ahead of ourselves a bit. What is attention and how does it dynamically shift the input to MLP? Attention is the component in transformer which operates along the sequence dimension, creating dependency among the input texts. Mentally, you can think of attention to be working on **representing** the current text (given or to be generated) as a function of the texts that came before it (referred to as causal attention). Now, depending on how this representation turns out you can have different input of the current text to the MLP i.e, different sequence of text lead to different representations for the same current text and consequently a different input data point processed by the MLP.

<figure class="half">
	<a href="/images/llm_geometry/attention_poly4.png"><img src="/images/llm_geometry/attention_poly4.png" alt="Attention 4t"/></a>
   <a href="/images/llm_geometry/attention_poly5.png"><img src="/images/llm_geometry/attention_poly5.png" alt="Attention 5t"/></a>
	<figcaption> Figure 2: Space of existence for the current text (*t5*) given preceding text as a result of single attention. An attention mapping represents a given text by a convex combination of the preceding texts. In the figure each vertex corresponds to one of the preceding text. Consequently, with 4 preceding tokens (Left), *t5* can live in the volume of a tetrahedron (3-simplex). Note that this includes the case where *t5* is represented in one of the faces, corresponding to the polytope with a subset of the preceding text. On the flip side, having and additional text for representation (Right) creates a larger space of existence for *t5*. Given the partitions of the MLP are fixed, attention allows the an input to translate to different spaces with more preceding text providing for a bigger region of access to map into.</figcaption>
</figure>

Figure 2. illustrates geoemtrically the mapping defined by attention on a text. A key takeaway here is that having more **context** (preceding text) can lead to a larger space of existence and consequently more set of function mappings to output. Understanding this aspect of transformer has been instrumental for me in understanding several research works on LLMs, be it few-shot prompting, chain-of-thought, or test-time compute to improve reasoning.

# Prompting

Finally, to prompting! The mental model above essentially boils down to this when you're writing system instructions and prompts: you are writing them for something like the aggregated spirit of the training corpus which told attention this sequence of text corresponds to an input in a particular partition. If we write prompts that have similar sequence of text scraped from the internet, the model will comprehend and follow faithfully follow. This essentially means the best way to become good at prompting is to experiment and prompt more (different models incorporate the internet differently in their training). However, the general notion of the internet remains and skills gained with one model can be transferred to another. Also, if you are an active member of the internet, you probably are already at a good spot in terms of prompting.

## The Open-ended Approach

Think of open-ended prompting one where you let the model do the work for you. Instead of rigidly structuring your request, you simply state what you're trying to achieve. However, make sure to have the model generate a lot of text before answering your question. Note that when you are using ChatGPT or Claude, the application is already heavily prompted with long context. This means the model is already in a state where it can generate text answering your question. However, if you are building your own Claude, there is no escaping the need for long generation if you want a smart chatbot. For reference, take a look at the system prompt for [Claude](https://docs.anthropic.com/en/release-notes/system-prompts#oct-22nd-2024).

The benefits of this approach include:

- More natural, flowing dialogue where the model does the work for you.
- Opportunity for creative suggestions. The generation is constrained by the space of text the model generates rather than your text.
- Inefficient for use-cases where you want to get to an answer or solution quickly.
- Lower barrier to entry for newcomers. Easily transferable to other models.

However, open-ended prompts can lead to:

- Responses that miss crucial details or take a hallucinated path.
- Need for multiple follow-ups. If not generating enough text, the model might fall short of answering your question and would need more text to get to the desired response.
- The initial text generated sets the stage for the future response. This means the model can end up in unstructured or irrelvant response based on the context it set for itself.

## The Formal Descriptive Approach

Formal prompting is more like writing a detailed specification document. This includes attaching long text files and search results. In this scenario, you explicitly set the space of response allowing the model to possibly get to the answer immediately.

Advantages of formal prompting:

- More precise and consistent outputs. Depending on the size of the context, the model is heavily constrained to the vocabulary of the context.
- Fewer iterations needed. There is usually less variability in the responses generated when prompting with descriptive context.
- Better for use-cases where speed to answer is critical. In particular, for voice assistants, having enough context can let one respond to a user in a natural manner.
- Ideally, you want to get to this state when building customer facing applications.

Drawbacks:

- Responses can feel mechanical or rigid. Moreover, things that are undesirable in generation would now require a lot more effort to undo.
- Requires a lot of upfront effort and cost to setup the prompt. Several iterations are needed to identify gaps in the system and fixing them.
- Steeper learning curve. Will require some iterations in transferring the prompt for use with another model.

# Conclusion

The choice between open-ended and formal prompting isn't binary - it's a spectrum. The key is matching your prompting style to your specific needs and context. Start with one approach, observe the results, and adjust accordingly. Remember that the best prompting strategy is the one that gets you the results you need.

As AI technology continues to evolve, we may see even more sophisticated ways to interact with these systems. For now, creating a mental model of how different texts in your prompt affects the output you obtain is a powerful toolkit for getting the most out of language models, current or future.

_Footnote: This post takes a lot of liberties to simplify and present an easy to understand mental picture of transformers and its relationship with prompting. The general message will still apply albeit with technical complexities when accounting for details that are in-use with the complete transformer architecture._

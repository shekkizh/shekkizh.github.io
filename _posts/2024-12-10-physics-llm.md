---
title: Physics in Video Language Models
date: 2024-12-10
excerpt: In this post, we explore the physics behind text to video language models and how they can be used to generate realistic videos from text prompts.
permalink: /posts/2024/12/physics-llm/
categories:
  - research
tags:
  - LLM
  - video
---

This week, OpenAI released the public version of [Sora](https://openai.com/sora/), a video generation model that takes as input text, image, or even video and generates an output video. This post is largely based on a discussion I had while at ICML 2024, prompted by a recurring question: will just scale (compute, data, model) be sufficient to overcome limitations in video generation?

Skepticism from some quarters point to the fact that current video models still do not understand real-world physics, produce incoherent long samples, and generate objects that materialize or vanish spontaneously.
However, dismissing these models for such reasons mirrors early skepticism toward large language models (LLMs) and their ability to understand grammar. This post outlines why betting against tokenized video models might be short-sighted. It also highlights how data efficiency could become the most significant challenge to address, mirroring what we have come to expect from LLMs.

## The Nitty Gritty Details of Video Models

Video generation models, like Sora, are motivated from LLMs that acquire generalizable capabilities through large-scale training. The success of the paradigm is enabled by compute and architecture that allows for the use of tokens that unify diverse modalities (check out [previous blog on tokenization]({{ site.url }}/posts/2024/11/tokenization/)). Video, more specifically images, are processed by tokenizing the data into smaller visual patches, which are then arranged into sequences. Each patch becomes a token that the model predicts in succession, generating a coherent frame-by-frame video output. The figure below present the tokenization process in Sora model. In fact, the Sora report is a pretty easy read if you are wondering about the process of diffusion models with transformers -- see [Video generation as world simulators](https://openai.com/index/video-generation-models-as-world-simulators/).

<figure>
	<a href="/images/llm/sora_patches.webp"><img src="/images/llm/sora_patches.webp" alt="/images/llm/sora_patches.webp"/></a>
	<figcaption> Figure taken from Sora report. Illustration of how videos are converted into patches through space-time compression and sequentially tokenized for input to an LLM. </figcaption>
</figure>

This process is similar to how LLMs generate text, one token at a time. Just as GPT models predict the next word in a sentence, video models predict the next frame in a sequence. As seen with LLMs, increasing the data scale and training time often leads to emergent capabilities not explicitly programmed into the model. It is plausible that video models could achieve a similar conceptual leap, learning the "physics" of the world from the vast visual data they process.

## Physics Through Patterns, Not Equations

One of the most striking lessons from the success of LLMs is their ability to learn grammar and generate language without being explicitly taught. Early language models often had grammatical rules hard-coded into them. However, LLMs absorb grammar and structure through exposure to just text sequences. This implicit learning suggests that the models _can_ develop an internal representation or "world model" of complex systems.

A similar process could be at play in other modalities too. By exposing LLMs to several videos, they can recognize and internalize physical principles like motion, causality, and object permanence. For example, a video of a ball rolling down a hill teaches the model that objects on inclines tend to accelerate downward. The model doesn't "know" Newton's laws, but it infers similar relationships through pattern recognition.
Physics is about recognizing patterns in how the world behaves. Theorems and equations capture this behavior in a compact and deterministic form. However, data-driven modeling offers a different approach. Instead of relying on predefined equations, these models infer patterns from vast datasets, allowing them to identify relationships and predict outcomes without formalizing them into explicit rules. This shift reflects a growing realization that compact, deterministic representations may not be essential for effective modeling.

Having said that, _will the model understand the angle of the incline to change the speed of the ball in its generation?_ Maybe. But this might _emerge_ with enough training -- not necessarily through mere memorization.
When a model learns to generate a video of a bouncing ball, it isn't calculating trajectories using kinematic equations (it would be nice if it did). Instead, it possibly notices the visual cues that accompany bounces — deformation, direction change, and velocity shifts. Given enough data, the model infers these principles.

This shift in perspective — from explicit physics to learned physics — highlights a profound gap. These models don't need to "understand" physics as a physicist would; they only need to generate outputs that look plausible. If you thought hallucination was a problem with text generation, wait till we start seeing hallucination in videos.

By learning to simulate sequences, LLMs may indirectly capture the _physics_ that govern real-world behavior. This idea aligns with our Matrix view from previous blog where we argued for LLMs to be "world simulators" by the process of just sequencing with tokenization.

## The Question to ask: How much more data?

A key assumption above is the availability of data -- data that can teach the model to overcome the limitations in its current form. How much data do we need to train to generate a realistic video? The answer is not clear. The emergent properties discussed with LLMs used text, but will the same scaling laws hold for other modalities? How will the spatio-temporal tokenization of video affect the data efficiency of these models?

This data inefficiency problem, however, is not new. Early large language models (LLMs) faced a similar challenge. Initially, the cost of training these models was prohibitive, but optimizations in model architecture, loss functions, and pre-training strategies steadily reduced the data and compute required. This historical precedent suggests that we may follow a similar path of improvement.

However, video data is inherently more complex than text. While LLMs work with sequences of discrete tokens, video models must predict and generate spatial-temporal information across multiple frames. This complexity raises the bar for efficient learning. This issue is outlined in the [system card](https://openai.com/index/sora-system-card/) and that efforts are underway in optimizing architecture and loss functions, but it is likely that **video models will require new paradigms for data efficiency**.

A key insight from the evolution of LLMs is that betting against models due to early inefficiencies is often a mistake. In the past, critics claimed that models like GPT-2 and GPT-3 were computationally wasteful, only for those models to later demonstrate surprising and emergent abilities as training scaled up.

Moreover, alternatives to tokenized video models aren't clearly superior. Hand-coding physics into models is infeasible at scale, and hybrid approaches that combine symbolic physics engines with deep learning often end up limited in scope. Tokenized video models, with their capacity for generalization, seem better positioned to handle the infinite diversity of possible video scenes.

## Looking Ahead: World Simulators, Not Just Video Generators

The ultimate promise of LLMs extends beyond video or text generation. By learning to simulate reality itself, they become world simulators. Such models could power immersive virtual environments, predict complex real-world interactions, and serve as training grounds for AI agents. One direction that I would like to see flourish is world simulators through game engines and modeling sequences through the knowledge of these engines -- think tools in current language models based applications.

Self-driving cars or robotics systems are trained with simulated video environments. You would hardly see a car go through another in a game world. However -- can a video model guarantee this in its generation. We need an amalgamation of ideas and approaches that we have solved in the past to go over the barrier of data inefficiency.

Given how LLMs went from generating text to _reasoning_ about the world, it is reasonable to expect that video models will follow a similar path. The seeds of implicit physics are already present in the patterns these models learn. While today's video models may seem crude, they hint at the extraordinary potential for future systems. The question shouldn't be whether these models can understand physics, but how far/fast can we go while overcoming data and compute efficiency issues.

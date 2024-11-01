---
title: "Forgetting and Toxicity in LLMs: A Deep Dive on Fine-Tuning Methods"
tagline: Domain-specific fine-tuning of LLMs for enterprises comes at the cost of reduced compromised safety and general performance.
date: 2023-12-12
excerpt: Fine-tuning is a common procedure by which a pretrained language model is updated with training on a domain-specific dataset to improve performance in that domain (i.e. a chatbot to answer enterprise-specific Q&A, a hotel booking agent).  It has been known for some time (if not widely appreciated) that fine-tuning a model on new data degrades its performance on the initial pretraining dataset (the dreaded “catastrophic forgetting” problem in ML). But by how much? And do all fine-tuning methods degrade performance in the same ways, and to the same extent?
permalink: /posts/2023/12/forgetting-and-toxicity/
tags:
  - LLM
  - safety
categories:
  - research
toc: true
toc_sticky: true
---

_Written for article published at Tenyx. Co-authors: Romain Cosentino, Ron Chrisley._

## Introduction

Fine-tuning is a common procedure by which a pretrained language model is updated with training on a domain-specific dataset to improve performance in that domain (i.e. a chatbot to answer enterprise-specific Q&A, a hotel booking agent). It has been known for some time (if not widely appreciated) that fine-tuning a model on new data degrades its performance on the initial pretraining dataset (the dreaded “catastrophic forgetting” problem in ML). But by how much? And do all fine-tuning methods degrade performance in the same ways, and to the same extent?

Our research team sought to answer these questions by comprehensively evaluating several fine-tuning methods (pertaining to both public and private LLMs) in terms of their effects on proficiency with the new data, safety, and knowledge of the pre-trained data. Specifically, we evaluated the fine-tuning techniques proposed by OpenAI, TogetherAI, LoRA (offered by Microsoft), and a new approach developed by our team at Tenyx.

We found that the Tenyx fine-tuning method came out on top in terms of achieving the best performance while mitigating the risks.

In general, our investigations show that while fine-tuning in general improves the capability of the model on the new data distribution at hand (what we here call proficiency), it does so at the cost of:

- Removing the safety guardrails achieved – at great cost – via reinforcement learning from human feedback (RLHF), resulting in potentially unsafe model outputs (i.e. toxicity), and
- Degrading out-of-domain knowledge retrieval and reasoning (i.e. knowledge, forgetting effects).

We find that not all fine-tuning methods are the same with respect to these distortions. In particular, we show that the new Tenyx fine-tuning approach has comparatively better learning capabilities (proficiency), while at the same time alleviating toxicity by retaining RLHF-derived guardrails and minimizing the catastrophic forgetting problem.

## Measuring the learning vs forgetting tradeoff

We measure performance along three dimensions: proficiency with respect to the fine-tuned domain, safety, and retained general knowledge. We evaluate LLM performances before and after fine-tuning on clean, non-toxic, chat-based hotel room booking transcripts, which are prototypical of real enterprise datasets that companies are likely to fine-tune on.

We evaluate some of the most popular enterprise and open-source fine-tuning algorithms:

- OpenAI fine-tuning (Enterprise, base model: GPT 3.5 Turbo)
- Together AI fine-tuning (Enterprise, base model: RedPajama Incite Chat)
- Low-Rank Approximation (LoRA) fine-tuning, proposed by Microsoft (Open-source, base
  model: Llama2-7B)
- Tenyx Fine-Tuning: (Enterprise, base model: Llama2-7B)

Each of these fine-tuning methods are evaluated in standard fashion for each of the three following tasks:

1. Proficiency improvement: We measure the capability of both the base models and the fine-tuned versions to be able to behave as a hotel booking agent, i.e., how well the agent handles taking turns in a conversation with a customer that seeks to book a hotel room. The quality of the agent is captured by its capability at following the appropriate steps depending on both the customer utterance and the information already known. Comparing the proficiency before and after fine-tuning is a way to measure the degree to which the fine-tuning method promotes learning.
2. Safety retention: We measure how well the models react to toxic comments (from the Toxigen dataset), both before and after fine-tuning. Specifically, we measure how well the models’ outputs contradict the input toxic comment in a constructive manner.
3. Knowledge retention: We measure the capability of the models to answer general knowledge questions (from the Dolly Q&A dataset), both before and after fine-tuning.

For each task, we evaluate the response of each model, using GPT4, suitably prompted, for the benchmark.

The results of each of these evaluations are displayed, respectively, in figures 1 (proficiency), 2 (safety) and 3 (knowledge). Let’s look at each of these dimensions in turn.

### Proficiency (Learning)

<figure>
	<a href="/images/forgetting_llm/proficiency.jpeg"><img src="/images/forgetting_llm/proficiency.jpeg" alt="Proficiency"/></a>
	<figcaption>
		Figure 1: Learning Capability of Fine-tuning Approaches. Shown is the percentage correct on a hotel booking task before and after each of the four different methods of fine-tuning are applied. Percentage highlighted on top of each post fine-tuning bar reflects the net change in proficiency provided by that fine-tuning method.
	</figcaption>
</figure>

We observe that the model fine-tuned by the Tenyx method results in the highest-performing hotel booking agent (with the model fine-tuned by TogetherAI a close second). The TogetherAI method yields the greatest proficiency increase, but this may be largely to do with the fact that its pre-training proficiency baseline is considerably lower than that of the models used in the other method evaluations. Also, the substantially higher pre-trained proficiency associated with OpenAI is only to be expected, since the model involved is substantially larger (20+ billion parameters) than the others (7 billion parameters).

### Safety (Toxicity)

<figure>
	<a href="/images/forgetting_llm/safety.jpeg"><img src="/images/forgetting_llm/safety.jpeg" alt="Safety"/></a>
	<figcaption>
		Figure 2: Safety reduction induced by Fine-tuning Approaches Shown is the percentage of safe/appropriate responses to toxic inputs from the Toxigen dataset, before and after each of the four different methods of fine-tuning. Percentage highlighted on top of each post fine-tuning bar reflects the net change in performance provided by that fine-tuning method.
	</figcaption>
</figure>

Figure 2 illustrates the most striking results of our investigations. It shows how the fine-tuning approaches used by industry leaders, as well as the open-source one (LoRA), eliminate the safeguards obtained via the costly RLHF process. However, we also find that while all the current fine-tuning solutions lose some of this protective layer, the Tenyx approach maintains it best, resulting in the safest fine-tuning approach.

### Knowledge (Forgetting)

<figure>
	<a href="/images/forgetting_llm/knowledge.jpeg"><img src="/images/forgetting_llm/knowledge.jpeg" alt="Safety"/></a>
	<figcaption>
		Figure 3: Forgetting induced by Fine-tuning Approaches. Shown is the percentage correct on an open-source dataset (Dolly Q&A) before and after each of the four different methods of fine-tuning is applied. Percentage highlighted on top of each post fine-tuning bar reflects the net change in performance provided by that fine-tuning method.
	</figcaption>
</figure>

To measure the forgetting induced by each fine-tuning method, we compared each model’s performance on a domain-general dataset both before and following the fine-tuning of that model on our domain-specific dataset (hotel room booking). For the domain general dataset, we used Dolly Q&A, which consists of general knowledge questions covering a wide range of topics.
Our results are displayed in Figure 3. We found that the Tenyx fine-tuning method is the one that best mitigates the forgetting phenomena (with only a 3% loss of domain-general performance), while effectively retaining the knowledge of the base model. Again, the OpenAI model’s pre-fine-tuning performance is, as expected, significantly better than the others, which is explained by its much larger size.

## Safer, Smarter Fine-Tuning

The safety removal and knowledge loss observed above are a direct consequence of learning on a new domain through fine-tuning. But why does this happen?

Fine-tuning alters the pre-trained weights of the model – in particular, techniques such as LoRA update all weights across the layers to which it is applied. These perturbations typically distort the model outputs. This explains the general trend in the figures above: proficiency on the hotel booking use case increases after fine-tuning, yet general knowledge and safety capabilities are drastically reduced.

The Tenyx fine-tuning method, by contrast, minimally disturbs these pre-trained weights while still learning on the new data. Thus, while all the other assessed fine-tuning schemes achieve proficiency at the cost of knowledge and safety degradation, the Tenyx approach achieves the highest standards of proficiency while also inducing the least loss in knowledge and safety.

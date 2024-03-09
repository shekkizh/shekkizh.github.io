---
title: "Characterizing Large Language Model Geometry Solves Toxicity Detection and Generation
"
collection: publications
permalink: /publication/2023-12-04-lm-geometry
authors: 'R Balestriero, R Cosentino, S Shekkizhar'
excerpt: 'Large Language Models~(LLMs) drive current AI breakthroughs despite very little being known about their internal representations, e.g., how to extract a few informative features to solve various downstream tasks. To provide a practical and principled answer, we propose to characterize LLMs from a geometric perspective.'
date: 2023-12-04
venue: 'arXiv Preprints'
paperurl: 'https://arxiv.org/abs/2312.01648'
citation: '@article{balestriero2023characterizing,
  title={Characterizing large language model geometry solves toxicity detection and generation},
  author={Balestriero, Randall and Cosentino, Romain and Shekkizhar, Sarath},
  journal={arXiv preprint arXiv:2312.01648},
  year={2023}
}
'
---
Large Language Models~(LLMs) drive current AI breakthroughs despite very little being known about their internal representations, e.g., how to extract a few informative features to solve various downstream tasks. To provide a practical and principled answer, we propose to characterize LLMs from a geometric perspective. We obtain in closed form (i) the intrinsic dimension in which the Multi-Head Attention embeddings are constrained to exist and (ii) the partition and per-region affine mappings of the per-layer feedforward networks. Our results are informative, do not rely on approximations, and are actionable. First, we show that, motivated by our geometric interpretation, we can bypass Llama-2&apos;s RLHF by controlling its embedding&apos;s intrinsic dimension through informed prompt manipulation. Second, we derive 7 interpretable spline features that can be extracted from any (pre-trained) LLM layer, providing a rich abstract representation of their inputs. Those features alone (224 for Mistral-7B/Llama-2-7B and 560 for Llama-2-70B) are sufficient to help solve toxicity detection, infer the domain of the prompt, and even tackle the Jigsaw challenge, which aims at characterizing the type of toxicity of various prompts. Our results demonstrate how, even in large-scale regimes, exact theoretical results can answer practical questions in language models.

[Download paper here](https://arxiv.org/abs/2312.01648)

```
@article{balestriero2023characterizing,
  title={Characterizing large language model geometry solves toxicity detection and generation},
  author={Balestriero, Randall and Cosentino, Romain and Shekkizhar, Sarath},
  journal={arXiv preprint arXiv:2312.01648},
  year={2023}
}

```
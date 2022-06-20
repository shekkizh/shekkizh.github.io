---
title: 'Beyond accuracy: A data-driven approach to geometric understanding of deep learning'	
date: 2022-05-20
excerpt: 
permalink: /posts/2022/05/geometry-of-deep-learning/
tags:
 - deep learning
 - representation learning
categories:
 - research
---

In the last decade, deep neural networks~(DNN) have achieved unprecedented performance success in many application domains, largely thanks to three major trends: (i) easier algorithmic innovation owing to the modularity of model components, (ii) increased model capacity where the number of parameters far exceeds the training data size, and (iii) steady reductions in the cost of compute resources to train these models.
It is well understood that in this overparameterized regime, DNNs are highly expressive and have the capacity to (over)fit arbitrary training datasets including pure noise. This is troublesome since **not** all of these overparameterized models generalize (i.e., perform well in the real world). Such mysticism about the workings of DNN raises concerns about reliability and trustworthiness, especially for deployment in critical applications.
For example, DNN models are closely tied to training datasets and are often selected with significant manual engineering with subjective heuristics. Thus, it may not be known a priori whether a sufficiently large amount of training data has been used. Moreover, since the number of parameters is large, it is often difficult to obtain interpretable/verifiable solutions for the learning task of interest. Finally, small changes to the training data set, e.g., insertion or removal of a few samples, can lead to significant changes in the behavior of the learning algorithm.

Existing tools, which have typically claimed a “what you see is what you get” principle( i.e performance on unseen data will be similar to that on training data) are unable to account for the unique challenges of overparameterized DNN models. More recently, researchers have developed surrogate models that approximate the mappings of a DNN to tackle the shortcomings of the previous tools. However, these simplifications only provide a partial picture and do not adapt to new advances in DNNs (e.g., architectures, activation functions, optimization, loss functions). Thus, to develop reliable models that can overcome the aforementioned challenges, it is crucial to develop new theories and tools that are adaptable to the constantly evolving landscape of DNNs and are practical enough for use in a range of sectors and professions.

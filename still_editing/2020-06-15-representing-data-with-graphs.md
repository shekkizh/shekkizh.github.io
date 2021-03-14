---
title: 'Representing data using graphs: A sparse signal approximation view'	
date: 2020-06-15
excerpt: Graph driven machine learning has seen a surge of interest in the past few years with several applications in social sciences, biology, and network analysis, to name a few. However, in some scenarios, no graph is given a priori and one  one has to *infer and construct* a graph to fit the data given.
permalink: /posts/2020/06/representing-data-with-graphs/
tags:
 - graph construction
 - representation learning
categories:
 - research
---
## Why do we need to represent data using graphs?
Graph driven machine learning has seen a surge of interest in the past few years with several applications in social sciences, biology, and network analysis, to name a few. 
<!-- Graph neural networks are a particularly popular area of research where one learns parametric functions based on local connectivity in the graphs. -->

However, in some scenarios, no graph is given a priori and one has to *infer and construct* a graph to fit the data given. These graphs are useful for a few reasons: 
1. Unlike machine learning methods that learn a function to each point, one can leverage explicitly the information across points to obtain *better* functions over regions of space.
2. Allows one to characterize data under minimal assumptions for use in semi-supervised and unsupervised learning scenarios

In a typical graph learning problem, we are given *N* data points and the goal is to learn an *efficient* graph representation of the data. The keyword here is efficient: An efficient graph can be defined as one with number of edges of the same order as the number of nodes (*N*). Efficient graphs lead to faster downstream processing making them 

## A primer on sparse signal approximation


## Graph construction as sparse signal approximation


<figure class="half">
    <a href="/images/nnk_image_graph/knn_graph_gif.gif"><img src="/images/nnk_image_graph/knn_graph_gif.gif" alt="knn graph"/></a>
    <a href="/images/nnk_image_graph/NNK_graph_gif.gif"><img src="/images/nnk_image_graph/NNK_graph_gif.gif" alt="nnk graph"/></a>
    <figcaption>KNN (Left) vs NNK (Right) graph for different choices of K </figcaption>
</figure>
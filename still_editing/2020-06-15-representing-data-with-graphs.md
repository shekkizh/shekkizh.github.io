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
Graphs provide a generic setup to describe and analyze complex patterns in data where instead of observing data as isolated set of points, we can view them as network where data are entities/nodes with relationships/edges between them. 
Graph driven machine learning (Graph-ML) has seen a surge of interest in the past few years with several applications in social sciences, biology, and network analysis, to name a few. Unlike standard machine learning methods that learn a function to each data point (where locality and connectivity assumptions are implicit), graph-ML aims at leveraging explicitly the information across points to obtain *better* functions over regions of space. Further, by associating graphs to only the input data (without labels/task information) allows one to characterize data for use in semi-supervised and unsupervised learning scenarios.
<!-- Graph neural networks are a particularly popular area of research where one learns parametric functions based on local connectivity in the graphs. -->

A critical issue in applying graph based machine learning is the definition of graph itself. In some scenarios, a graph structure is intuitive and at times given alongside the data.
However, in most scenarios, no graph is given a priori and one has to *infer and construct* a graph to fit the data and the task to be solved. 

In a typical graph learning problem, we are given *N* data points and the goal is to learn an *efficient* graph representation of the data. The keyword here is **efficient**: An efficient graph can be defined as one with number of edges of the same order as the number of nodes (*N*). Efficient graphs lead to faster downstream processing making them 

## A primer on sparse signal approximation


## Graph construction as sparse signal approximation


<figure class="half">
    <a href="/images/nnk_image_graph/knn_graph_gif.gif"><img src="/images/nnk_image_graph/knn_graph_gif.gif" alt="knn graph"/></a>
    <a href="/images/nnk_image_graph/NNK_graph_gif.gif"><img src="/images/nnk_image_graph/NNK_graph_gif.gif" alt="nnk graph"/></a>
    <figcaption>KNN (Left) vs NNK (Right) graph for different choices of K </figcaption>
</figure>
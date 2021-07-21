---
title: 'Revisiting k-nearest neighbor benchmarks in self-supervised learning'	
date: 2021-07-21
excerpt: Standard protocols for benchmarking self-supervised models involve using a linear or k-nearest neighbor classification on frozen features of the learned model. However, both evaluations are sensitive to hyperparameters making the evaluation and comparison complicated. 
permalink: /posts/2021/06/revisiting-knn-with-nnk/
tags:
 - neighborhood methods
 - deep learning
categories:
 - experiments
---

## Self-Supervised Learning and KNN benchmarks
Deep learning has advanced performance in several machine learning problems throught the use of large *labeled* datasets. However, labels are expensive to collect and at times leads to biases in the trained model arising from the labeling of the data. One technique, that has gained interest in recent years, to solve these issues is self supervised learning (Self-SL). The goal of self-SL is to learn representations from data using the data itself as supervision (leveraging inductive biases that we assume on the system) i.e., a model is trained to produce representation such that the extracted features perform well on a artificially generated task for which ground truth is available. 

**How does one quantify the representations obtained?** 
Standard protocols for benchmarking self-SL models involve using a linear or weighted k-nearest neighbor classification (KNN) on features extracted from the learned model whose parameters are not updated.However, both these evaluations are sensitive to hyperparameters making the evaluation and comparison complicated. For e.g., in linear evaluations, one often applies *selected* augmentations to the input to train the linear classifier on top of the feature extractor in addition to hyperparameters used for training the classifier. A weighted k-nearest neighbor classifier, on the other hand, avoids data augmentations but still suffers from the selection of hyperparameter `k`. One observes large variance in accuracy in both these evaluation frameworks based on the hyperparameter/augmentations chosen making the comparison of feature extractors obscure. Ideally, one would want an evaluation protocol that does not require augmentations or hyperparameter tuning and can be run quickly given the features of the data. In this post, I hope to convince you with an alternate neighborhood based classifier that can satisfy these requirements exactly. In fact, we will see that not only is the proposed classifier robust but is also capable of performing better if not at par than the previous evaluation methods in terms of classification accuracy.

## Non Negative Kernel regression (NNK)
In [NNK]({{ site.url }}/posts/2020/06/representing-data-with-graphs/), neighborhood selection is formulated as a signal representation problem, where each data point is to be approximated using a dictionary formed by its neighbors. This problem formulation, for each data point, leads to an adaptive and principled approach to the choice of neighbors and their weights. 
While KNN is used as an initialization, NNK performs an optimization akin to orthogonal matching pursuit in kernel space resulting in a *robust* representation with a *geometric* interpretation. <!-- The Kernel Ratio Interval (KRI) theorem of NNK states, for a given data point `i` and similarity kernel ∈ [0,1]$, a necessary and sufficient condition 
for *both* `j` and `k` to be NNK neighbors of `i`:  -->
Geometrically, KRI reduces to a series of hyper plane conditions, one per NNK neighbor, which applied inductively lead to a convex polytope around each data point as show in Fig. below. In words, NNK ignores neighbors that are further away along a *similar* direction as an already chosen point and looks for neighbors in an *orthogonal* or *different* direction.
<figure class="half">
	<a href="/images/revisit_knn/NNK_decision_plane.png"><img src="/images/revisit_knn/NNK_decision_plane.png" alt="NNK_decision_plane"/></a>
	<a href="/images/revisit_knn/NNK_polytope.png"><img src="/images/revisit_knn/NNK_polytope.png" alt="NNK_polytope"/></a>
	<figcaption>
		Local geometry of NNK based on Kernel Ratio Interval (KRI). <br>
		<i>Left</i>: KRI plane (dashed orange line) corresponding to chosen neighbor `j`. Data points to the right of this plane will be not be selected by NNK as neighbors of `i`. <i>Right</i> KRI boundary obtained by inductive application of KRI plane and associated convex polytope formed by NNK neighbors at `i`.
	</figcaption>
</figure>

Note that, this perspective provides an alternative to the conventional thinking of local neighborhoods as hyperspheres or balls of certain radius in space. This is made possible in NNK, by taking into account the relative positions of nodes `j` and `k` using the metric on `(j,k)`, in addition to the metric on `(i,j)` and `(i,k)` that were previously used for the selection  and weighing of neighbors `j`,`k` to node `i`.

Application of NNK for classification is further interesting from a recent theoretical point of view: interpolative classifiers, namely classifiers with training error `0`, are capable of generalizing well to test data contrary to the conventional wisdom (interpolation ⇒ poor generalization). Note that overparameterized neural network models today are increasingly trained to zero training error and can be considered to fall under this category of interpolative classifiers. In the experiments that follow, we will use a normalized cosine kernel (cosine kernel shifted and scaled to have values between `0` and `1`) for NNK and KNN.  

## Self-SL evaluation with NNK

Table below lists Top-1 Linear, weighted KNN and NNK classification accuracy on ImageNet using a fixed bacbone architecture ResNet-50 that was trained using different self-SL training strategies. The evaluation protocol follows a standard setup where one evaluated performance on validation dataset based on labeled training dataset. The KNN and NNK evaluations were done using a self-SL  framework VISSL with officially released model weights and setting the parameter `k`, number of neighbors, to `50`. The results listed for linear evaluations are as reported on the corresponding self-SL papers and was not validated by us.


| Method | Linear | KNN | NNK |
| ------ | ---------- | --- | --- |
| Supervised | 76.1 | 74.5 | 75.4 |
| MoCo-v2 |  71.1 | 60.3 | 64.9 |
| DeepClusterV2|  75.2 | 65.8 | 70.7 |
| SwAV |  75.3 | 63.2 | 68.7 |
| DINO |  75.3 | 65.6 | 71.1 |
{: rules="groups"}


To evaluate the robustness of NNK relative to KNN we will use a recently introduced self-SL model, [DINO](https://arxiv.org/abs/2104.14294) (**di**stillation with **no** labels), as our baseline model and compare Top-1 accuracy on ImageNet for different values of `k`. As can be seen in Figure below, NNK not only consitently outperforms a weighted KNN classifer but does so in a robust manner. Further, unlike the KNN whose performance decreases as `k` increases, NNK improves with `k`. This can  be  explained  by  the  fact  that  NNK  accommodates  new neighbors only if they belong to a new direction in space that improves its interpolation whereas a KNN simply  interpolates  with all `k` neighbors.
<figure class="half">
	<a href="/images/revisit_knn/DINO_Evaluation_patch_8.png"><img src="/images/revisit_knn/DINO_Evaluation_patch_8.png" alt="DINO_Evaluation_patch_8"/></a>
	<a href="/images/revisit_knn/DINO_Evaluation_patch_16.png"><img src="/images/revisit_knn/DINO_Evaluation_patch_16.png" alt="DINO_Evaluation_patch_16"/></a>
	<figcaption> 
		KNN vs NNK evaluation of DINO self supervised model for different values of `k`.   
		The plot shows Top-1 accuracy on ImageNet for the base (B) and a distilled student (S) vision transformer models trained using DINO for two choices of patch sizes, $8$ (Left) and $16$ (Right). Note that NNK produces classification performance similar to that of the linear evaluations reported using DINO model.
	</figcaption>
</figure>

## Discussion 
Several machine learning methods leverage the idea of local neighborhood by using methods such as KNN, *∈*-neighborhood to better design and evaluate pattern recognition models. However, the choice of parameters such as `k` is often  made experimentally, e.g., via cross-validation, leading to local neighborhoods without a clear interpretation. NNK formulation allows us to overcome this shortcomings resulting in a superior framework that is adaptive to the local  distribution of samples. As show in this post and our related works, NNK does exhibit robust and superior performance relative to standard local methods. Ultimately, our goal is for the NNK framework to encourage and revisit the use of interpretable and robust neighborhood methods in machine learning - for e.g., consider the problem of [model distillation](https://arxiv.org/abs/2010.14713) or [clustering](https://arxiv.org/abs/2005.12320) where NNK could be used to enforce better local consistency regularization.

Source code for experiments in this post are available at [github.com/shekkizh/VISSL_NNK_Benchmark](https://github.com/shekkizh/VISSL_NNK_Benchmark){:.btn .btn--primary}

 

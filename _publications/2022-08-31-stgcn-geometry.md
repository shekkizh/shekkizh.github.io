---
title: "Towards a geometric understanding of Spatio Temporal Graph Convolution Networks"
collection: publications
permalink: /publication/2022-08-31-stgcn-geometry
authors: 'P. Das, S. Shekkizhar, A. Ortega'
excerpt: 'Spatio-temporal graph convolutional networks (STGCNs) have emerged as a desirable model for many applications including skeleton-based human action recognition. Despite achieving state-of-the-art performance, our limited understanding of the representations learned by these models  hinders their application in critical and real-world settings. '
date: 2022-08-31
venue: 'arXiv Preprints'
paperurl: 'https://arxiv.org/abs/2312.07777'
citation: '@misc{das2022geometry,
    title={Towards a geometric understanding of Spatio Temporal Graph Convolution Networks},
    author={Pratyusha Das, Sarath Shekkizhar, Antonio Ortega},
    year={2022},
}'
---
Spatio-temporal graph convolutional networks (STGCNs) have emerged as a desirable model for many applications including skeleton-based human action recognition. Despite achieving state-of-the-art performance, our limited understanding of the representations learned by these models  hinders their application in critical and real-world settings. 
In this paper, we first propose a data-driven  understanding of the embedding geometry induced at different layers of the STGCN using local neighborhood graphs constructed on the feature representation of input data at each layer. To do so, we develop a window based dynamic time warping~(DTW) to compute the distance between data sequences with varying temporal lengths. 
Secondly, we introduce a layerwise Spatio temporal Graph Gradient-weighted Class Activation Mapping for spatio-temporal data to visualize and interpret each layer of the STGCN network.
We characterize the functions learned by each layer of STGCN using the label smoothness of the representation and visualize using our GradCAM approach. 
We show that STGCN models learn representations that capture general human motion in their initial layers and are capable of discriminating different actions only in later layers.
This provides justification for experimental observations showing that fine-tuning of later layers works well for transfer between related tasks.  We also show that noise at the input has a limited effect on label smoothness, which can help justify the robustness of STGCNs to noise. 

[Download paper here](https://arxiv.org/abs/2312.07777)

```
@misc{das2022geometry,
    title={Towards a geometric understanding of Spatio Temporal Graph Convolution Networks},
    author={Pratyusha Das, Sarath Shekkizhar, Antonio Ortega},
    year={2022},
}
```
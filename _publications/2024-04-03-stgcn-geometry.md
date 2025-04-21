---
title: "Towards a geometric understanding of Spatio Temporal Graph Convolution Networks"
collection: publications
permalink: /publication/2024-04-03-stgcn-geometry
authors: 'P. Das, S. Shekkizhar, A. Ortega'
excerpt: 'Spatio-temporal graph convolutional networks (STGCNs) have emerged as a desirable model for many applications including skeleton-based human action recognition. Despite achieving state-of-the-art performance, our limited understanding of the representations learned by these models  hinders their application in critical and real-world settings. '
date: 2024-04-03
venue: 'IEEE Open Journal of Signal Processing'
paperurl: 'https://ieeexplore.ieee.org/iel7/8782710/9006934/10518107.pdf'
citation: '@article{das2024towards,
  title={Towards a geometric understanding of Spatiotemporal Graph Convolution Networks},
  author={Das, Pratyusha and Shekkizhar, Sarath and Ortega, Antonio},
  journal={IEEE Open Journal of Signal Processing},
  year={2024},
  publisher={IEEE}
}'
---
Spatio-temporal graph convolutional networks (STGCNs) have emerged as a desirable model for many applications including skeleton-based human action recognition. Despite achieving state-of-the-art performance, our limited understanding of the representations learned by these models  hinders their application in critical and real-world settings. In this paper, we first propose a data-driven  understanding of the embedding geometry induced at different layers of the STGCN using local neighborhood graphs constructed on the feature representation of input data at each layer. To do so, we develop a window based dynamic time warping~(DTW) to compute the distance between data sequences with varying temporal lengths. Secondly, we introduce a layerwise Spatio temporal Graph Gradient-weighted Class Activation Mapping for spatio-temporal data to visualize and interpret each layer of the STGCN network. We characterize the functions learned by each layer of STGCN using the label smoothness of the representation and visualize using our GradCAM approach. We show that STGCN models learn representations that capture general human motion in their initial layers and are capable of discriminating different actions only in later layers. This provides justification for experimental observations showing that fine-tuning of later layers works well for transfer between related tasks.  We also show that noise at the input has a limited effect on label smoothness, which can help justify the robustness of STGCNs to noise. 

[Download paper here](https://ieeexplore.ieee.org/iel7/8782710/9006934/10518107.pdf)

```
@article{das2024towards,
  title={Towards a geometric understanding of Spatiotemporal Graph Convolution Networks},
  author={Das, Pratyusha and Shekkizhar, Sarath and Ortega, Antonio},
  journal={IEEE Open Journal of Signal Processing},
  year={2024},
  publisher={IEEE}
}
```
---
title: "Channel redundancy and overlap in convolutional neural networks with Channel-wise NNK graphs"
collection: publications
permalink: /publication/2022-01-21-cw-nnk-redundancy
authors: 'D. Bonnet, A. Ortega, J.Ruiz-Hidalgo, S.Shekkizhar'
excerpt: 'Feature spaces in the deep layers of convolutional neural networks (CNNs) are often very high-dimensional and difficult to interpret. However, convolutional layers consist of multiple channels that are activated by different types of inputs, which suggests that more insights may be gained by studying the channels'
date: 2022-01-21
venue: 'In press, IEEE International Conference on Acoustics, Speech and Signal Processing (ICASSP)'
citation: '@inproceedings{bonet2022channel,
  title={Channel redundancy and overlap in convolutional neural networks with Channel-wise NNK graphs},
  author={Bonet, David and Ortega, Antonio and Ruiz-Hidalgo, Javier and Shekkizhar, Sarath},
  booktitle={IEEE International Conference on Acoustics, Speech and Signal Processing (ICASSP)}, pages={In press},
  year={2022}
}'
---
Feature spaces in the deep layers of convolutional neural networks (CNNs) are often very high-dimensional and difficult to interpret. However, convolutional layers consist of multiple channels that are activated by different types of inputs, which suggests that more insights may be gained by studying the channels and how they relate to each other. In this paper, we first analyze theoretically channel-wise non-negative kernel (CW-NNK) regression graphs, which allow us to quantify the overlap between channels and, indirectly, the intrinsic dimension of the data representation manifold. We find that redundancy between channels is significant and varies with the layer depth and the level of regularization during training. Additionally, we observe that there is a correlation between channel overlap in the last convolutional layer and generalization performance. Our experimental results demonstrate that these techniques can lead to a better understanding of deep representations. 

```
@inproceedings{bonet2022channel,
  title={Channel redundancy and overlap in convolutional neural networks with Channel-wise NNK graphs},
  author={Bonet, David and Ortega, Antonio and Ruiz-Hidalgo, Javier and Shekkizhar, Sarath},
  booktitle={IEEE International Conference on Acoustics, Speech and Signal Processing (ICASSP)}, pages={In press},
  year={2022}
}
```
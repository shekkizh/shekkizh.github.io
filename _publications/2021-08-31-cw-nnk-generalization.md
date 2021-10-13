---
title: "Channel-Wise Early Stopping without a ValidationSet via NNK Polytope Interpolation"
collection: publications
permalink: /publication/2021-08-31-cw-nnk-generalization
authors: 'D. Bonnet, A. Ortega, J.Ruiz-Hidalgo, S.Shekkizhar'
excerpt: 'Convolutional neural networks (ConvNets) comprise high-dimensional feature spaces formed by the aggregation of multiple channels, where analyzing intermediate data representations and the model&apos;s evolution can be challenging owing to the curse of dimensionality. We present channel-wise DeepNNK (CW-DeepNNK)'
date: 2021-08-31
venue: 'Asia Pacific Signal and Information Processing Association (APSIPA)'
citation: '@article{bonet2021channel,
  title={Channel-Wise Early Stopping without a Validation Set via NNK Polytope Interpolation},
  author={Bonet, David and Ortega, Antonio and Ruiz-Hidalgo, Javier and Shekkizhar, Sarath},
  journal={Asia-Pacific Signal and Information Processing Association Annual Summit and Conference (APSIPA ASC)},
  year={2021}
}'
---
State-of-the-art neural network architectures continue to scale in size and deliver impressive generalization results, although this comes at the expense of limited interpretability. In particular, a key challenge is to determine when to stop training the model, as this has a significant impact on generalization. Convolutional neural networks (ConvNets) comprise high-dimensional feature spaces formed by the aggregation of multiple channels, where analyzing intermediate data representations and the model&apos;s evolution can be challenging owing to the curse of dimensionality. We present channel-wise DeepNNK (CW-DeepNNK), a novel channel-wise generalization estimate based on non-negative kernel regression (NNK) graphs with which we perform local polytope interpolation on low-dimensional channels. This method leads to instance-based interpretability of both the learned data representations and the relationship between channels. Motivated by our observations, we use CW-DeepNNK to propose a novel early stopping criterion that (i) does not require a validation set, (ii) is based on a task performance metric, and (iii) allows stopping to be reached at different points for each channel. Our experiments demonstrate that our proposed method has advantages as compared to the standard criterion based on validation set performance.

```
@article{bonet2021channel,
  title={Channel-Wise Early Stopping without a Validation Set via NNK Polytope Interpolation},
  author={Bonet, David and Ortega, Antonio and Ruiz-Hidalgo, Javier and Shekkizhar, Sarath},
  journal={Asia-Pacific Signal and Information Processing Association Annual Summit and Conference (APSIPA ASC)},
  year={2021}
}
```
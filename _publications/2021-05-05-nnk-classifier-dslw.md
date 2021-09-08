---
title: "Revisiting local neighborhood methods in machine learning"
collection: publications
permalink: /publication/2021-05-05-nnk-classifier-dslw
authors: 'S. Shekkizhar, A. Ortega'
excerpt: 'Several machine learning methods leverage the idea of locality by using $k$-nearest neighbor (KNN) techniques to design better pattern recognition models.  However, the choice of KNN parameters such as $k$ is often  made experimentally, e.g., via cross-validation, leading to local neighborhoods without a clear geometric interpretation.'
date: 2021-05-05
venue: 'IEEE Data Science and Learning Workshop (DSLW)'
paperurl: 'https://ieeexplore.ieee.org/abstract/document/9523409'
citation: '@inproceedings{nonaka2020graph,
  title={Revisiting local neighborhood methods in machine learning},
  author={Shekkizhar, Sarath and Ortega, Antonio},
  booktitle={DSLW 2021-2021 IEEE Data Science and Learning Workshop (DSLW)},
  organization={IEEE}
}'
awards: 'Invited paper'
---
Several machine learning methods leverage the idea of locality by using $k$-nearest neighbor (KNN) techniques to design better pattern recognition models.  However, the choice of KNN parameters such as $k$ is often  made experimentally, e.g., via cross-validation, leading to local neighborhoods without a clear geometric interpretation. In this paper, we replace KNN with our recently introduced polytope neighborhood scheme - Non Negative Kernel regression (NNK). NNK formulates neighborhood selection as a sparse signal approximation problem and is adaptive to the local distribution of samples in the neighborhood of the data point of interest. We analyze the benefits of local neighborhood construction based on NNK. In particular, we study the generalization properties of local interpolation using NNK and present data dependent bounds in the non asymptotic setting. The applicability of NNK in transductive few shot learning setting and for measuring distance between two datasets is demonstrated. NNK exhibits robust, superior performance in comparison to standard locally weighted neighborhood methods. 

[Download paper here](https://ieeexplore.ieee.org/abstract/document/9523409)

```
@inproceedings{shekkizhar2021revisit,
  title={Revisiting local neighborhood methods in machine learning},
  author={Shekkizhar, Sarath and Ortega, Antonio},
  booktitle={DSLW 2021-2021 IEEE Data Science and Learning Workshop (DSLW)},
  organization={IEEE}
}
```

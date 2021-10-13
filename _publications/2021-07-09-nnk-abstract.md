---
title: "Revisiting nearest neighbors from a signal approximation perspective"
collection: publications
permalink: /publication/2021-07-09-nnk-abstract
authors: 'S. Shekkizhar, A. Ortega'
excerpt: 'NNK classification with features extracted from a self supervised model achieves 79.8% top-1 ImageNet accuracy, outperforming previous non parametric benchmarks while requiring no hyperparameter tuning or data augmentation. '
date: 2021-07-09
venue: 'Bay Area Machine Learning Symposium (BayLearn)'
citation: '@inproceedings{shekkizhar2021revisit,
  title={Revisiting local neighborhood methods in machine learning},
  author={Shekkizhar, Sarath and Ortega, Antonio},
  booktitle={DSLW 2021-2021 IEEE Data Science and Learning Workshop (DSLW)},
  organization={IEEE}
}'
---
Several machine learning methods leverage the idea of locality by using k-nearest neighbor or epsilon-neighborhood techniques to design pattern recognition models. However, the choice of parameters k/epsilon in these methods is often ad hoc and lacks a clear interpretation. We revisit the problem of neighborhood definition from a sparse signal approximation perspective and propose an improved approach, Non-Negative Kernel regression (NNK). NNK formulates neighborhood selection as a non negative basis pursuit problem and is adaptive to the local distribution of samples near the data point of interest. NNK neighbors are geometric, robust and exhibit superior performance in neighborhood based machine learning. We show that NNK classification with features extracted from a self supervised model achieves 79.8% top-1 ImageNet accuracy, outperforming previous non parametric benchmarks while requiring no hyperparameter tuning or data augmentation. 

```
@inproceedings{shekkizhar2021revisit,
  title={Revisiting local neighborhood methods in machine learning},
  author={Shekkizhar, Sarath and Ortega, Antonio},
  booktitle={DSLW 2021-2021 IEEE Data Science and Learning Workshop (DSLW)},
  organization={IEEE}
}
```
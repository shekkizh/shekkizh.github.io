---
title: "Data Sampling using Locality Sensitive Hashing for Large Scale Graph Learning"
collection: publications
permalink: /publication/2023-06-23-data-sampling-mlg
authors: 'S. Shekkizhar, N. Bulut, M. Farghal, S. Tavakkol, M. Bateni, A. Nandi'
excerpt: 'Recent works, such as GRALE, have focused on the semi-supervised setting to learn an optimal similarity function for constructing a task-optimal graph. However, in many scenarios with billions of data points and trillions of potential edges, the run-time and computational requirements for training the similarity model make these approaches impractical. In this work, we consider data sampling as a means to overcome this issue.'
date: 2023-06-23
venue: 'International Workshop on Mining and Learning with Graphs, Conference on Knowledge Discovery and Data Mining (KDD)
'
paperurl: 'https://www.mlgworkshop.org/2023/papers/MLG__KDD_2023_paper_2.pdf'
citation: '@inproceedings{mlg2023_2,
title={Data Sampling using Locality Sensitive Hashing for Large Scale Graph Learning},
author={Sarath Shekkizhar, Neslihan Bulut, Mohamed Farghal, Sasan Tavakkol, Mohammadhossein Bateni and Animesh Nandi},
booktitle={Proceedings of the 19th International Workshop on Mining and Learning with Graphs (MLG)},
year={2023}
}'
---
An important step in graph-based data analysis and processing is the construction of similarity graphs. Recent works, such as [7, 23 ], have focused on the semi-supervised setting to learn an optimal similarity function for constructing a task-optimal graph. However, in many scenarios with billions of data points and trillions of potential edges, the run-time and computational requirements for training the similarity model make these approaches impractical. In this work, we consider data sampling as a means to overcome this issue. Unlike typical sampling use-cases which only seek diversity, the similarity-learning for graph construction problem requires data samples that are both diverse and representative of highly similar data points. We present an efficient sampling approach by taking an adaptive partition view of locality sensitive hashing. Theoretically, we show that, though the samples obtained are correlated with sampling probabilities that do not sum to one, the training loss estimated for learning the graph similarity model using our approach is unbiased with a smaller variance compared to random sampling. Experiments on public datasets demonstrate the superior generalization of similarity models learned via our sampling. In a real large-scale industrial abuse-detection example, we observe ≈10× increase in identifying abusive items while having a lower false positive rate compared to the baseline.

[Download paper here](https://www.mlgworkshop.org/2023/papers/MLG__KDD_2023_paper_2.pdf)

```
@inproceedings{mlg2023_2,
title={Data Sampling using Locality Sensitive Hashing for Large Scale Graph Learning},
author={Sarath Shekkizhar, Neslihan Bulut, Mohamed Farghal, Sasan Tavakkol, Mohammadhossein Bateni and Animesh Nandi},
booktitle={Proceedings of the 19th International Workshop on Mining and Learning with Graphs (MLG)},
year={2023}
}
```
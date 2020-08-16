---
title: "Efficient graph construction for image representation"
collection: publications
permalink: /publication/2020-02-16-nnk-image-graph
authors: 'S. Shekkizhar, A. Ortega'
excerpt: 'Graphs are useful to interpret widely used image processing methods, e.g., bilateral filtering, or to develop new ones, e.g., kernel based techniques. However, simple graph constructions are often used, where edge weight and connectivity depend on a few parameters. In particular, the sparsity of the graph is determined by the choice of a window size.'
date: 2020-02-16
venue: 'arXiv Preprints (to be published at ICIP)'
paperurl: 'https://arxiv.org/abs/2002.06662'
citation: '@article{shekkizhar2020efficient,
  title={Efficient graph construction for image representation},
  author={Shekkizhar, Sarath and Ortega, Antonio},
  journal={arXiv preprint arXiv:2002.06662},
  year={2020}
}
'
---
Graphs are useful to interpret widely used image processing methods, e.g., bilateral filtering, or to develop new ones, e.g., kernel based techniques. However, simple graph constructions are often used, where edge weight and connectivity depend on a few parameters. In particular, the sparsity of the graph is determined by the choice of a window size. As an alternative, we extend and adapt to images recently introduced non negative kernel regression (NNK) graph construction. In NNK graphs sparsity adapts to intrinsic data properties. Moreover, while previous work considered NNK graphs in generic settings, here we develop novel algorithms that take advantage of image properties so that the NNK approach can scale to large images. Our experiments show that sparse NNK graphs achieve improved energy compaction and denoising performance when compared to using graphs directly derived from the bilateral filter. 

[Download paper here](https://arxiv.org/abs/2002.06662)
```
@article{shekkizhar2020efficient,
  title={Efficient graph construction for image representation},
  author={Shekkizhar, Sarath and Ortega, Antonio},
  journal={arXiv preprint arXiv:2002.06662},
  year={2020}
}
```
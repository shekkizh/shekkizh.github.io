---
title: "The geometry of self-supervised learning models and its impact on Transfer learning"
collection: publications
permalink: /publication/2022-05-19-ssl-geometry
authors: 'R. Cosentino, S. Shekkizhar, M. Soltanolkotabi, S. Avestimehr, A. Ortega'
excerpt: 'The recent popularity of SSL has led to the development of several models that make use of diverse training strategies, architectures, and data augmentation policies with no existing unified framework to study or assess their effectiveness in transfer learning.'
date: 2022-05-19
venue: 'arXiv Preprints'
paperurl: 'https://arxiv.org/abs/2209.08622v1'
citation: '@misc{shekkizhar2022sslgeometry,
    title={The geometry of self-supervised learning models and its impact on Transfer learning},
    author={Romain Cosentino, Sarath Shekkizhar, Mahdi Soltanolkotabi, Salman Avestimehr, Antonio Ortega},
    year={2022},
}'
---
Self-supervised learning~(SSL) has emerged as a desirable paradigm in computer vision due to the inability of supervised models to learn representations that can generalize in domains with limited labels. The recent popularity of SSL has led to the development of several models that make use of diverse training strategies, architectures, and data augmentation policies with no existing unified framework to study or assess their effectiveness in transfer learning.
We propose a data-driven geometric strategy to analyze different SSL models using local neighborhoods in the feature space induced by each. Unlike existing approaches that consider mathematical approximations of the parameters, individual components, or optimization landscape, our work aims to explore the geometric properties of the representation manifolds learned by SSL models.
Our proposed manifold graph metrics~(MGMs) provide insights into the geometric similarities and differences between available SSL models, their invariances with respect to specific augmentations, and their performances on transfer learning tasks. Our key findings are two fold: (i) contrary to popular belief, the geometry of SSL models is not tied to its training paradigm (contrastive, non-contrastive, and cluster-based); (ii) we can predict the transfer learning capability for a specific model based on the geometric properties of its semantic and augmentation manifolds.

[Download paper here](https://arxiv.org/abs/2209.08622v1)

```
@misc{shekkizhar2022sslgeometry,
    title={The geometry of self-supervised learning models and its impact on Transfer learning},
    author={Romain Cosentino, Sarath Shekkizhar, Mahdi Soltanolkotabi, Salman Avestimehr, Antonio Ortega},
    year={2022},
}
```
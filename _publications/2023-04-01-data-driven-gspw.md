---
title: "A data-driven graph framework for geometric understanding of deep learning"
collection: publications
permalink: /publication/2023-04-01-data-driven-gspw
authors: 'S. Shekkizhar, A. Ortega'
excerpt: 'Deep learning approaches have achieved unprecedented performance success in many application domains. In this work, we first present an empirical framework for studying deep learning by characterizing the geometry of the data manifold in the embedding spaces, using computationally efficient graph-based methods to learn manifold properties.'
date: 2023-04-01
venue: 'Graph Signal Processing Workshop'
citation: '@misc{shekkizhar2023data,
    title={A data-driven graph framework for geometric understanding of deep learning},
    author={Sarath Shekkizhar, Antonio Ortega},
    year={2023},
}'
---
Deep learning approaches have achieved unprecedented performance success in many application domains. One of the driving factors in their success is the use of massive models; often more parameters than the size of the training dataset. It is well understood that in this overparameterized regime, deep neural networks (DNNs) are highly expressive and have the capacity to (over)fit arbitrary training data and still exhibit good generalization, i.e., performance on unseen data. In this work, we first introduce an empirical framework for studying deep learning by characterizing the geometry of the data manifold in the embedding spaces, using computationally efficient graph-based methods to learn manifold properties. 

We then present a study, where we ask “what do bigger models achieve that smaller models do not?” in scenarios where both achieve zero classification error on the training dataset. Our analysis shows that there exist two distinct types of learned embedding spaces within the modern interpolative learning regimes. We observe that an increasing number of data are mapped to a local patch corresponding to the same class as the size of the model increases. We hypothesize that smaller models, which are still capable of achieving perfect classification, require a weighted averaging based on their neighborhood while larger models have local class homogeneity in the embedding space and can achieve perfect classification even with unweighted averaging.

```
@misc{shekkizhar2023data,
    title={A data-driven graph framework for geometric understanding of deep learning},
    author={Sarath Shekkizhar, Antonio Ortega},
    year={2023},
}
```
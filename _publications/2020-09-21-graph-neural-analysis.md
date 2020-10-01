---
title: "Graph-based Deep Learning Analysis and Instance Selection"
collection: publications
permalink: /publication/2020-09-21-graph-neural-analysis
authors: 'K. Nonaka, S. Shekkizhar, A. Ortega'
excerpt: 'While deep learning is a powerful tool for manyapplications, there has been only limited research about selectionof data for training, i.e., instance selection, which enhances deeplearning scalability by saving computational resources.'
date: 2020-09-21
venue: 'IEEE International Workshop on Multimedia Signal Processing (MMSP)'
paperurl: 'https://confcats-event-sessions.s3.amazonaws.com/mmsp20/papers/273.pdf'
citation: '@inproceedings{nonaka2020graph,
  title={Graph-based Deep Learning Analysis and Instance Selection},
  author={Nonaka, Keisuke and Shekkizhar, Sarath and Ortega, Antonio},
  booktitle={MMSP 2020-2020 IEEE International Workshop on Multimedia Signal Processing (MMSP)},
  organization={IEEE}
}'
---
While deep learning is a powerful tool for manyapplications, there has been only limited research about selectionof data for training, i.e., instance selection, which enhances deeplearning scalability by saving computational resources. This canbe attributed in part to the difficulty of interpreting deep learningmodels. While some graph-based methods have been proposed toimprove performance and interpret behavior of deep learning,the instance selection problem has not been addressed from agraph perspective. In this paper, we analyze the behavior of deeplearning outputs by using the K-nearest neighbor (KNN) graphconstruction. We observe that when a directed KNN graph isconstructed, instead of the more conventional undirected KNN, alarge number of instances become isolated nodes, i.e., they do notbelong to the directed neighborhoods of any other nodes. Basedon this, we propose two new instance selection methods, that bothlead to fewer isolated nodes, by either directly eliminating them(minimization approach) or by connecting them more stronglyto other points (maximization). Our experiments show that ourproposed maximization method leads to better performance thanrandom selection and recent methods for instance selection.

[Download paper here](https://confcats-event-sessions.s3.amazonaws.com/mmsp20/papers/273.pdf)
```
@inproceedings{nonaka2020graph,
  title={Graph-based Deep Learning Analysis and Instance Selection},
  author={Nonaka, Keisuke and Shekkizhar, Sarath and Ortega, Antonio},
  booktitle={MMSP 2020-2020 IEEE International Workshop on Multimedia Signal Processing (MMSP)},
  organization={IEEE}
}
```
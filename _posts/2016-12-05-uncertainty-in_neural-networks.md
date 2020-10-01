---
title: 'A notion of uncertainty in modern neural networks'	
date: 2016-12-5
excerpt: In this post, we will look at a particular view of uncertainty in modern deep learning systems using droput 
permalink: /posts/2016/12/uncertainty-neural-networks/
tags:
 - neural networks
 - deep learning
categories:
 - experiments	
---

# Uncertainty in Models
In this post, we look at an experiment based on the results published by Yarin et. al. on the interpretation of dropout as uncertainty in models. The central idea behind the paper is in interpreting uncertainty in models via dropout i.e By introducing dropout at test time we can draw mean and variance information over an input which helps us to concretely explain how are deep learning models interprets the input. Alternatively when we train a network with dropout, by the above explanation we are forcing the network  to learn under some uncertainty and hence the model is made to avoid over fitting.

Paper: [Dropout as a Bayesian Approximation](https://arxiv.org/abs/1506.02142)

## Results
The results below are obtained on MNIST with dropout in fully connected layer. The red line corresponds to inference with no dropout at test time. The blue dotted lines correspond to the mean and variance for inference over 100 iterations. 

The model architecture for the below results is 2 conv layers - fc layer with dropout - softmax layer. Training was done with dropout probability 0.1 - This means that at test time if we have the same dropout probability, the model should be fairly confident of it's inference. This can be seen in the below result.

![](https://raw.githubusercontent.com/shekkizh/neuralnetworks.thought-experiments/master/Uncertainty in Models/images/number6_test.png)

Now if we introduce higher dropout, the model should show signs of uncertainty as it is not trained to overcome this. Higher the dropout higher the uncertainty. Some examples of uncertain predictions that the model makes are as below.

![](https://raw.githubusercontent.com/shekkizh/neuralnetworks.thought-experiments/master/Uncertainty in Models/images/number5_uncertain2.png)
![](https://raw.githubusercontent.com/shekkizh/neuralnetworks.thought-experiments/master/Uncertainty in Models/images/number6_uncertain.png)
![](https://raw.githubusercontent.com/shekkizh/neuralnetworks.thought-experiments/master/Uncertainty in Models/images/number9_uncertain.png)

In the result below, we see the type of inputs where our model is uncertain and those were it is confident. This gives us valuable information on our model. Such insights gives us an idea of whether we need to train our model further, include more data and such.

![](https://raw.githubusercontent.com/shekkizh/neuralnetworks.thought-experiments/master/Uncertainty in Models/images/number7_uncertain.png)


## References
 - [Yarin Gal's blog post](http://mlg.eng.cam.ac.uk/yarin/blog_3d801aa532c1ce.html) 
 - [Video Presentation by author at MSR](https://www.youtube.com/watch?v=3ONLxYeM1Sc&index=14&list=WL&t=1030s)
 - [Tensorflow code for the experiment](https://github.com/shekkizh/TensorflowProjects/master/MNIST/Uncertainty_modelling.py)

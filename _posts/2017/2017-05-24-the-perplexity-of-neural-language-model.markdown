---
layout: "post"
title: "The Perplexity of Neural Language Model"
date: "2017-05-24 16:24"
comments: true
---


Given a list of word vectors: $x_1,\cdots,x_{t-1},x_t,x_{t+1},\cdots,x_T $,

$$\hat{y}_t=softmax(W h_t),
\hat{p}(x_{t+1}=v_j|x_t,\cdots,x_1) =\hat{y}_{t,j} $$

where $h_t$ is the hidden state output at time step $t$.

$ y \in R^{V}$ is a probability distribution over the vocabulary,

same cross entropy loss function but predicting words instead of classes:

$$J^{(t)}(\theta)=-\sum_{j=1}^{|V|}{y_{t,j}\log \hat{y}_{t,j}}$$

Evaluation could just be negative of average log probability over dataset of size (number of words) T:

$$\mathcal{L}=-\frac{1}{T}\sum_{t=1}^T\sum_{j=1}^{|V|}{y_{t,j}\log \hat{y}_{t,j}}$$

Perplexity: $\exp(\mathcal{L})$

Lower is better !

### Material
[cs224n-2017-lecture8](http://web.stanford.edu/class/cs224n/lectures/cs224n-2017-lecture8.pdf)

[CS 498: Introduction to Natural Language Processing](https://courses.engr.illinois.edu/cs498jh/Slides/Lecture04.pdf)

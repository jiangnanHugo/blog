---
layout: "post"
title: "Introduction to LSTM"
date: "2016-05-18 21:19"
comment: true
---
## Long short-term memory:

make that short-term memory last for a long time.


#### Paper Reference：
[A Critical Review of Recurrent Neural Networks for Sequence Learning](http://arxiv.org/pdf/1506.00019)

![LSTM Gate模型](http://deeplearning.net/tutorial/_images/lstm_memorycell.png)

## Three Types of Gate

### Input Gate:
Controls how much of the current input $x_t$ and the previous output $h_{t-1}$ will enter into the new cell.

$$i_t=\sigma(W^i x_t+U^i h_{t-1}+b^i)$$

### Forget Gate:
Decide whether to erase (set to zero) or keep individual components of the memory.

$$f_t=\sigma(W^f x_t+U^f h_{t-1}+b^f)$$

### Cell Update:
Transforms the input and previous state to be taken into account into the current state.

$$g_t=\phi(W^g x_t+U^g h_{t-1}+b^g)$$

### Output Gate:
Scales the output from the cell.

$$o_t=\sigma(W_o x_t+U^o h^{t-1}+b^o)$$

### Internal State update:
Computes the current timestep's state using the gated previous state and the gated input.

$$s_t=g_t\cdot i_t+s_{t-1}\cdot f_t$$

### Hidden Layer:
Output of the LSTM scaled by a $\tanh$ (squashed) transformations of the current state.

$$h_t=s_t\cdot \phi(o_t)$$

其中$\cdot$ 代表"element-wise matrix multiplication"(对应元素相乘)，$\phi(x)=\tanh(x),\sigma(x)=sigmoid(x)$

$$\phi(x)=\frac{e^x-e^{-x}}{e^x+e^{-x}},\sigma(x)=\frac{1}{1+e^{-x}}$$

## Parallel Computing

input gate, forget gate, cell update, output gate can be computed in parallel.

$$\begin{bmatrix} i^t\\ f^t\\g^t\\o^t \end{bmatrix} =\begin{bmatrix}\sigma\\ \sigma\\\phi\\\sigma\end{bmatrix}\times W\times[x^t,h^{t-1}]$$


## LSTM network for Semantic Analysis

![LSTM network for semantic analysis](http://deeplearning.net/tutorial/_images/lstm.png)

### Model Architecture
Model: LSTM layer --> Averaging Pooling --> Logistic Regession

#### Input sequence:

$$x_0,x_1,x_2,\cdots,x_n$$

#### representation sequence:

$$h_0,h_1,h_2,\cdots,h_n$$

This representation sequence is then averaged over all timesteps resulting in representation h:

$$h=\sum\limits_i^n{h_i}$$

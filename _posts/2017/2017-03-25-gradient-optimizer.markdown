---
layout: "post"
title: "gradient optimizer"
date: "2017-03-25 17:33"
comments: true
---

The equations of the momentum method

$$v(t)=\alpha v(t-1) -\epsilon \frac{\partial E}{\partial w} (t)$$

The effect of the gradient is to increment the previous velocity. The velocity also decays by $\alpha$ which is slight less than 1.

$$\delta w(t) = v(t) \\
 = \alpha v(t-1) -\epsilon \frac{\partial E}{\partial w} (t) \\
 = \alpha \delta w(t-1) -\epsilon \frac{\partial E}{\partial w} (t)$$

The weight change is equal to the current velocity.

The weight change ca be expressed in terms of the previous weight change and the current gradient.

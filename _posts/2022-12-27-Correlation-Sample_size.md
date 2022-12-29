---
title: 'Correlation and Sample Size Estimation'
date: 2022-12-27
permalink: /posts/2022/12/NewPost/
tags:
  - Correlation
  - Sample Size
  - loss functions
---

Consider the general scenario where we have variables X and Y which have a correlation $r$. We will use the standard definition of correlation for our discussion:
$$\text{Correlation} = \frac{Cov(X,Y)}{\sqrt{Var(X)Var(Y)}} = \frac{\mathbf{E}[XY] - \mathbf{E}[X]\mathbf{E}[Y]}{\sqrt{(\mathbf{E}[X^2]-\mathbf{E}[X]^2)(\mathbf{E}[Y^2] - \mathbf{E}[Y]^2)}}$$
$$=\frac{\sum_{i=1}^n(x_i-\bar{x})(y_i-\bar{y})}{\sqrt{\sum_{i=1}^n(x_i-\bar{x})^2\sum_{i=1}^n(y_i-\bar{y})^2}}$$

We want to find the number of measurements we need if we expect a correlation of $r$ and we have a type I error rate of $\alpha$ and type II error rate of $\beta$. Under these conditions, we can structure the hypothesis as:
$$ H_0: r \leq r_0$$
$$H_1: r > r_0 $$





This post will show up by default. To disable scheduling of future posts, edit `config.yml` and set `future: false`. 

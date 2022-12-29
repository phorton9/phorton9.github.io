---
title: 'Correlation and Sample Size Estimation'
date: 2022-12-27
permalink: /posts/2022/12/NewPost/
tags:
  - Correlation
  - Sample Size
---

Consider the general scenario where we have variables X and Y which have a correlation $r$. We will use the standard definition of correlation for our discussion:
$$\text{Correlation} = \frac{Cov(X,Y)}{\sqrt{Var(X)Var(Y)}} = \frac{\mathbf{E}[XY] - \mathbf{E}[X]\mathbf{E}[Y]}{\sqrt{(\mathbf{E}[X^2]-\mathbf{E}[X]^2)(\mathbf{E}[Y^2] - \mathbf{E}[Y]^2)}}$$
$$=\frac{\sum_{i=1} (x_i-\bar{x})(y_i-\bar{y})}{\sqrt{\sum_{i=1} (x_i-\bar{x})^2\sum_{i=1} (y_i-\bar{y})^2}}$$

We want to find the number of measurements we need if we expect a correlation of $r$ and we have a type I error rate of $\alpha$ and type II error rate of $\beta$. Under these conditions, we can structure the hypothesis as:
$$H_0: r \leq r_0 $$
$$H_1: r > r_0 $$

We setup this test to reject the null hypothesis that the correlation is under a threshold once we have sufficient data. We define $r'$ as the sample correlation, $r_0$ as the test correlation, and $r$ as the true correlation.
$$\beta = \text{P(Type II Error) = P(Fail to Reject } H_0 \mid H_0 \text{ is False})$$
$$=P(Z_0 \leq Z_\alpha \mid r > r_0) = P(\frac{atanh(r') - atanh(r_0)}{\sqrt{n-3}} \leq Z_\alpha)$$
$$= P(\frac{atanh(r') - atanh(r)}{\sqrt{n-3}} + \frac{atanh(r) - atanh(r_0)}{\sqrt{n-3}} \leq Z_\alpha) = P(Z \leq Z_\alpha + \frac{atanh(r) - atanh(r_0)}{\sqrt{n-3}})$$
$$\beta =P(Norm(0,1) \leq Z_\alpha + \frac{atanh(r) - atanh(r_0)}{\sqrt{n-3}}) = \Phi(Z_\alpha + \frac{atanh(r) - atanh(r_0)}{\sqrt{n-3}})$$



This post will show up by default. To disable scheduling of future posts, edit `config.yml` and set `future: false`. 
 

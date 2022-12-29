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
$$= P(\frac{atanh(r') - atanh(r)}{\sqrt{n-3}} + \frac{atanh(r) - atanh(r_0)}{\sqrt{n-3}} \leq Z_\alpha) = P(Z \leq Z_\alpha + \frac{atanh(r) - atanh(r_0)}{\sqrt{n-3}})$$$$


$$\beta =P(Norm(0,1) \leq Z_\alpha + \frac{atanh(r) - atanh(r_0)}{\sqrt{n-3}}) = \Phi(Z_\alpha + \frac{atanh(r) - atanh(r_0)}{\sqrt{n-3}})$$

Given by the Fisher's z-transformation where $atanh(r') = \frac{1}{2}\ln(\frac{1+r'}{1-r'})$ is normally distributed with mean $atanh(r)$ and variance $\frac{1}{n-3}$. We can then say:
$$-Z_\beta = \Phi^{-1}(\beta) = Z_\alpha + \frac{atanh(r) - atanh(r_0)}{\sqrt{n-3}}$$
$$\Phi(Z) = P(Norm(0,1)\leq Z) \text{ as the 1-pth quantile } Z_p \equiv \Phi^{-1}(1-p)$$

After re-arranging, we are left with:
$$n = \lceil \left(\frac{Z_\alpha + Z_\beta}{atanh(r) - atanh(r_0)}\right)^2 + 3 \rceil$$

Note - Due to observations being positive integers, we use the ceiling function to accomplish this.

We can consider the scenario where we expect the true value $r = 0.95$, we set our test value $r_0 = 0.90$. We want an $\alpha = 0.05$ (type I error rate) and $\beta = 0.1$ (type II error rate). The number of samples necessary for this setting:
$$n =  \lceil \left(\frac{1.645 + 1.282}{0.3596}\right)^2 + 3 \rceil = \lceil 69.3 \rceil \approx 70$$

We can also consider the case when $r_0 = 0$ where we want to show that a correlation is positive. We will keep $\alpha = 0.05$ and $\beta = 0.1$ but modify our expectation for the true correlation value to be $r = 0.5$. In this scenario, we have:
$$n = \lceil \left(\frac{1.645 + 1.282}{0.549}\right)^2 + 3 \rceil = \lceil 31.4 \rceil \approx 32$$

$$
\left(\begin{array}{cc} 
var(X_j) & cov(X_j,Y_j)\\
cov(Y_j,X_j) & var(Y_j)
\end{array}\right)
$$ 
$$
\left(\begin{array}{cc} 
\mathbf{E}[X_j]\\
\mathbf{E}[Y_j]
\end{array}\right)
$$

Now, consider the scenario where we have subgroups $j=1...K$ within a population that have covariance matrices $\Sigma_i = \begin{bmatrix}
    var(X_j) & cov(X_j,Y_j) \\
    cov(Y_j,X_j) & var(Y_j)
\end{bmatrix}$ and mean $\mu_j = \begin{bmatrix}
    \mathbf{E}[X_j] \\
    \mathbf{E}[Y_j]
\end{bmatrix}$. We have a two subgroup example shown in figure 1 below where:
This post will show up by default. To disable scheduling of future posts, edit `config.yml` and set `future: false`. 
 

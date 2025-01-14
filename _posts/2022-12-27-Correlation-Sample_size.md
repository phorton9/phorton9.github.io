---
title: 'Correlation and Sample Size Estimation'
date: 2022-12-27
permalink: /posts/2022/12/SampleSize/
tags:
  - Correlation
  - Sample Size
---
You will find correlations as a part of analyses in papers across all fields of research. They are simple ways to understand the relationship between variables. They can be put into matrix for all variables within a dataset and visualized such as in the heatmap below. An additional way to use correlations is in the planning stage of a study or trial. You can use the expected value of the correlation to determine the number of samples/observations you will need. In this post, I will describe a method for determining the number of samples you will need for a statistically significant correlation given a type I error rate $\left(\alpha\right)$ and type II error rate $\left(\beta\right)$. I will also discuss the implications for having subgroups within a population and the relationship they have to the combined sample correlation.

<p align="center">
  <br/><img src='/images/Correlation.png' width="300" alt="alt attribute goes here!" title="This is a Title">
</p>

Consider the general scenario where we have variables X and Y which have a correlation $r$. We will use the standard definition of the Pearson correlation for our discussion:
$$\text{Correlation} = \frac{Cov(X,Y)}{\sqrt{Var(X)Var(Y)}}$$

$$= \frac{\mathbf{E}[XY] - \mathbf{E}[X]\mathbf{E}[Y]}{\sqrt{(\mathbf{E}[X^2]-\mathbf{E}[X]^2)(\mathbf{E}[Y^2] - \mathbf{E}[Y]^2)}}$$

$$=\frac{\sum_{i=1} (x_i-\bar{x})(y_i-\bar{y})}{\sqrt{\sum_{i=1} (x_i-\bar{x})^2\sum_{i=1} (y_i-\bar{y})^2}}$$

Under these conditions, we can structure the hypothesis as:
$$H_0: r \leq r_0 $$

$$H_1: r > r_0 $$

We setup this test to reject the null hypothesis that the correlation is under a threshold once we have sufficient data. We define $r'$ as the sample correlation, $r_0$ as the test correlation, and $r$ as the true correlation. By definition, $\beta$ is the probability of committing a type II error or failing to reject the null hypothesis given that the null hypothesis is wrong. This leads us to derive:

$$\beta = \text{P(Type II Error) = P(Fail to Reject } H_0 \mid H_0 \text{ is False})$$

$$=P(Z_0 \leq Z_\alpha \mid r > r_0) = P(\frac{atanh(r') - atanh(r_0)}{1/\sqrt{n-3}} \leq Z_\alpha)$$

$$= P(\frac{atanh(r') - atanh(r)}{1/\sqrt{n-3}} + \frac{atanh(r) - atanh(r_0)}{1/\sqrt{n-3}} \leq Z_\alpha)$$

$$= P(Z \leq Z_\alpha - \frac{atanh(r) - atanh(r_0)}{1/\sqrt{n-3}})$$

$$= P(Norm(0,1) \leq Z_\alpha - \frac{atanh(r) - atanh(r_0)}{1/\sqrt{n-3}})$$

$$= \Phi(Z_\alpha - \frac{atanh(r) - atanh(r_0)}{1/\sqrt{n-3}})$$

Given by the Fisher's z-transformation where $atanh(r') = \frac{1}{2}\ln(\frac{1+r'}{1-r'})$ is normally distributed with mean $atanh(r)$ and variance $\frac{1}{n-3}$. We can then say:

$$-Z_\beta = \Phi^{-1}(\beta) = Z_\alpha - \frac{atanh(r) - atanh(r_0)}{1/\sqrt{n-3}}$$

$$\Phi(Z) = P(Norm(0,1)\leq Z) \text{ as the 1-pth quantile } Z_p \equiv \Phi^{-1}(1-p)$$

After re-arranging, we are left with:
$$n = \lceil \left(\frac{Z_\alpha + Z_\beta}{atanh(r) - atanh(r_0)}\right)^2 + 3 \rceil$$

Note - Due to observations being positive integers, we use the ceiling function to accomplish this.

We can consider the scenario where we expect the true value $r = 0.95$, we set our test value $r_0 = 0.90$. We want an $\alpha = 0.05$ (type I error rate) and $\beta = 0.1$ (type II error rate). The number of samples necessary for this setting:

$$n =  \lceil \left(\frac{1.645 + 1.282}{0.3596}\right)^2 + 3 \rceil = \lceil 69.3 \rceil \approx 70$$

We can also consider the case when $r_0 = 0$ where we want to show that a correlation is positive. We will keep $\alpha = 0.05$ and $\beta = 0.1$ but modify our expectation for the true correlation value to be $r = 0.5$. In this scenario, we have:

$$n = \lceil \left(\frac{1.645 + 1.282}{0.549}\right)^2 + 3 \rceil = \lceil 31.4 \rceil \approx 32$$

Now, consider the scenario where we have subgroups $j=1...K$ within a population that have covariance matrices

$$
\Sigma_i = \begin{bmatrix}{} 
var(X_j) & cov(X_j,Y_j)\\
cov(Y_j,X_j) & var(Y_j)
\end{bmatrix}
$$ 

$$
\mu_j = \begin{bmatrix}{} 
\mathbf{E}[X_j]\\
\mathbf{E}[Y_j]
\end{bmatrix}
$$

We have a two subgroup example shown in figure 2 below where:

$$
\Sigma_1 = \begin{bmatrix}{} 
1 & -0.8\\
-0.8 & 1
\end{bmatrix}       \hspace{2cm}
\mu_1 = \begin{bmatrix}
    1 \\
    4
\end{bmatrix}
$$ 

$$
\Sigma_2 = \begin{bmatrix}
    1 & 0.8 \\
    0.8 & 1
\end{bmatrix} \hspace{1cm}
\mu_2 = \begin{bmatrix}
    2 \\
    2
\end{bmatrix}
$$

<p align="center">
  <br/><img src='/images/Cor8-8MeanDif.png' width="300" alt="alt attribute goes here!" title="Correlation for Subgroups with Different Means">
</p>

Both subgroups have 100 samples and the combined sample correlation is -0.32. The correlation is driven by the difference in sample means between the two subgroups. If we standardize both subgroups where:

$$
\mu_1 = \begin{bmatrix}
    0 \\
    0
\end{bmatrix} \hspace{1cm}
\mu_2 = \begin{bmatrix}
    0 \\
    0
\end{bmatrix}
$$

We have sample correlation of 0. We did not need to standardize the variances since $var(X_1) = var(X_2) = var(Y_1) = var(Y_2) = 1$. 

With a standardized sample and subgroups, $\mathbf{E}[X] = \mathbf{E}[Y] = 0$ and the formula for the sample correlation becomes:

$$r = \frac{Cov(X,Y)}{\sqrt{Var(X)Var(Y)}}$$

$$= \mathbf{E}[XY] = \sum_{i=1}^n(x_i)(y_i) = \sum_{j=1}^K\sum_{i=1}^{n_j}(x_{ij})(y_{ij})$$

Where $x_{ij}$ and $y_{ij}$ are the $i-th$ observation from the $j-th$ subgroup. This is the weighted average of the covariance of the subgroups.

<p align="center">
    <br/><img align = "center" src='/images/Cor8-8MeanSame.png' width="300" alt="alt attribute goes here!" title="Correlation for Subgroups with Equal Means">
</p>

 

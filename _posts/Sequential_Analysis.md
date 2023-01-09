---
title: 'Sequential Analysis'
date: 2023-1-1
permalink: /posts/2022/12/NewPost/
tags:
  - Sequential Analysis
  - Hypothesis Testing
---

Sequential analysis is not a new topic but it is experiencing a renaissance with increasingly fast feedback for app developers. The roots of sequential analysis come from Abraham Wald focusing on Quality Control in manufacturing but tech companies are beginning to find these methods valuable. No longer do they have to plan for fixed length campaigns but rather can utilize dynamic sample sizes. Results for A/B testing can be available nearly instantly which facilitates shorter decision times and improved product performance. In this post, I will explain the advantages of using sequential analysis for hypothesis testing.

If you need a refresher on hypothesis testing, I suggest you review this video. Otherwise, I will assume you have a foundational knowledge of hypothesis testing.

Consider the scenario where an app developer (ADev) wants to experiment with a new feature to increase in-app purchases. Assume they can track the frequency of visits and amount purchased to calculate a metric Average Purchases per Visit (APV). The engineers decide to configure the experiment to show the new feature to a random 50% of the users while the remaining will continue to see the previous version. The team wants to show that the new feature improves APV and thus structures the hypothesis test as:
$$h_0: \mu_x \leq \mu_y$$
$$h_1: \mu_x > \mu_y$$
Here, the null hypothesis is that the feature has a negative or no effect on the the APV while the alternative hypothesis is that the feature improves APV. It is recognized that there are risks associated with making the wrong decision using statistical hypothesis testing. We will assume that the company is willing to accept a type I error rate of $\alpha = 0.05$ and type II error rate of $\beta = 0.05$.

We will assume the observations for the test group are $X_1, X_2, ... X_n \overset{\mathrm{iid}}{\sim} Norm(\mu_x, \sigma_x)$ and the observations from the control group are $Y_1, Y_2, ... Y_m \overset{\mathrm{iid}}{\sim} Norm(\mu_y, \sigma_y)$ where both $\sigma_x$ and $\sigma_y$ are unkown. We can use Welch's t-statistic $T_0 = \frac{\bar{X} - \bar{Y}}{\sqrt{\frac{S_x}{n}+\frac{S_y}{m}}} \approx t(v)$ which has an approximate t-distribution with $v$ degrees of freedom. The degrees of freedom are given by:
$$v \equiv \frac{(\frac{S_{x}^2}{n} + \frac{S_{y}^2}{m})^2}{\frac{(S_{x}^2 / n)^2}{n-1} + \frac{(S_{y}^2 / m)}{m-1}}$$

In this case, $t_\alpha$ and $t_\beta$ are dynamic and will update as you take more observations. You would also need at least $n\geq2$ and $m\geq2$ before being able to calculate this. Simpler alternatives to this method would be to assume that either:
1) The variance $\sigma$ is already known and will not change from the experiment
2) There are equal variances between the groups $\sigma_x = \sigma_y$

<p align="center">
  <br/><img src='/images/Sequence.png' width="300" alt="alt attribute goes here!" title="Sequential Test">
</p>


https://github.com/phorton9/BlogCode/blob/main/SequentialAnalysis.R

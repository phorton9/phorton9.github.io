---
title: 'Sequential Analysis'
date: 2023-1-1
permalink: /posts/2022/12/NewPost/
tags:
  - Sequential Analysis
  - Hypothesis Testing
---

Sequential analysis is not a new topic but it is experiencing a renaissance with increasingly fast feedback for app developers. The roots of sequential analysis come from Abraham Wald focusing on Quality Control in manufacturing but tech companies are beginning to find these methods valuable. No longer do they have to plan for fixed length campaigns but rather can utilize dynamic sample sizes. Results for A/B testing can be available nearly instantly which facilitates shorter decision times and improved product performance. In this post, I will explain the advantages of using sequential analysis for hypothesis testing.

If you need a refresher on hypothesis testing, I suggest you review this <a href="https://www.youtube.com/watch?v=VK-rnA3-41c">video</a>. Otherwise, I will assume you have a foundational knowledge of hypothesis testing.

Consider the scenario where an app developer (ADev) wants to experiment with a new feature to increase in-app purchases. Assume they can track the frequency of visits and amount purchased to calculate a metric Average Purchases per Visit (APV). The engineers decide to configure the experiment to show the new feature to a random selection of the users while the remaining will continue to see the previous version. Not all the users will login to see the feature at once so data will continue to stream in with the results. The team wants to show that the new feature improves APV and thus structures the hypothesis test as:
$$h_0: \mu_x \leq \mu_y$$
$$h_1: \mu_x > \mu_y$$
Here, the null hypothesis is that the feature has a negative or no effect on the the APV while the alternative hypothesis is that the feature improves APV. It is recognized that there are risks associated with making the wrong decision using statistical hypothesis testing. We will assume that the company is willing to accept a type I error rate of $\alpha = 0.05$ and type II error rate of $\beta = 0.05$.

We will assume the observations for the test group are $X_1, X_2, ... X_n \overset{\mathrm{iid}}{\sim} Norm(\mu_x, \sigma_x)$ and the observations from the control group are $Y_1, Y_2, ... Y_m \overset{\mathrm{iid}}{\sim} Norm(\mu_y, \sigma_y)$ where both $\sigma_x$ and $\sigma_y$ are unkown. We can use Welch's t-statistic $T_0 = \frac{\bar{X} - \bar{Y}}{\sqrt{\frac{S_x}{n}+\frac{S_y}{m}}} \approx t(v)$ which has an approximate t-distribution with $v$ degrees of freedom. The degrees of freedom are given by:
$$v \equiv \frac{(\frac{S_{x}^2}{n} + \frac{S_{y}^2}{m})^2}{\frac{(S_{x}^2 / n)^2}{n-1} + \frac{(S_{y}^2 / m)}{m-1}}$$

In this case, $t_\alpha$ and $t_\beta$ are dynamic and will update as you take more observations. You would also need at least $n\geq2$ and $m\geq2$ before being able to calculate this. Simpler alternatives to this method would be to assume that either:
1) The variance $\sigma$ is already known and will not change from the experiment
2) There are equal variances between the groups $\sigma_x = \sigma_y$

With the test set up this way, you will continue to taking observations until either $T_0 > t_\alpha$ or $T_0 < t_\beta$. If you terminate due to the former, you can reject the null hypothesis and conclude that the new feature improved the Average Purchases per Visit. If you terminate due to the latter, you can conclude that the new feature did not improve the APV.

For an example, I simulated data to replicate this scenario. I generated data for two normal distributions where $\mu_x = 10.25$, $\mu_y = 10$, $\sigma_x = 1$, $\sigma_y = 1$. You can see in the figure below that the test terminates after ~70 observations where we conclude that the new feature improved the APV.

<p align="center">
  <br/><img src='/images/Sequence.png' width="300" alt="alt attribute goes here!" title="Sequential Test">
</p>

If you are interested in the code for the simulation, you can find it here: https://github.com/phorton9/BlogCode/blob/main/SequentialAnalysis.R

This <a href="https://www.amazon.com/Sequential-Analysis-Abraham-Wald/dp/0486615790">book</a> is also a great resource to learn more about Sequential Analysis. 

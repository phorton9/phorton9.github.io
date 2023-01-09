---
title: 'Sequential Analysis'
date: 2023-1-1
permalink: /posts/2022/12/NewPost/
tags:
  - Sequential Analysis
  - Hypothesis Testing
---

Sequential analysis is not a new topic but it has experienced a renaissance with increasingly fast feedback for app developers. The roots of sequential analysis come from Quality Control in manufacturing but tech companies are beginning to find these methods valuable. No longer do they have to plan for fixed length campaigns but rather can utilize dynamic sample sizes. Results for A/B testing can be available nearly instantly which facilitates shorter decision times and improved product performance. In this post, I will explain the advantages of using sequential analysis for hypothesis testing.

If you need a refresher on hypothesis testing, I suggest you review this video. Otherwise, I will assume you have a foundational knowledge of hypothesis testing.

Consider the scenario where an app developer (ADev) wants to experiment with a new feature to increase in-app purchases. Assume they can track the frequency of visits and amount purchased to calculate a metric Average Purchases per Visit (APV). The engineers decide to configure the experiment to show the new feature to a random 50% of the users while the remaining will continue to see the previous version. The team wants to show that the new feature improves APV and thus structures the hypothesis test as:
$$h_0: \mu_x \leq \mu_y$$
$$h_1: \mu_x > \mu_y$$
Here, the null hypothesis is that the feature has a negative or no effect on the the APV while the alternative hypothesis is that the feature improves APV. It is recognized that there are risks associated with making the wrong decision using statistical hypothesis testing. We will assume that the company is willing to accept a type I error rate of $\alpha$ and type II error rate of $\beta$.

We will assume the observations for the test group are $X_1, X_2, ... X_n \overset{\mathrm{iid}}{\sim} Norm(\mu_x, \sigma_x)$ and the observations from the control group are $Y_1, Y_2, ... Y_m \overset{\mathrm{iid}}{\sim} Norm(\mu_y, \sigma_y)$ where both $\sigma_x$ and $\sigma_y$ are unkown. Our test statistic $T_0 = \frac{\bar{X} - \bar{Y}}{\sqrt{\frac{S_x}{n}+\frac{S_y}{m}}}$

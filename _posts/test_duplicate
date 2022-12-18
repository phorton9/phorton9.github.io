---
title: 'Risky Business'
date: 2022-12-01
permalink: /posts/2022/12/RiskyBusiness/
tags:
  - staitistical decision theory
  - risk functions
  - loss functions
---

Don’t be fooled by the title of my first blog post because I am not going to be reviewing any movies. Instead, I will explain risk functions and their role in statistical decision theory. Risk functions are a tool for determining under what conditions an estimator is better than another. The goal of machine learning algorithms is to minimize the risk (or expected loss), so it is an important concept to understand. In this post, I will start by describing the concept at a basic level and what you need to calculate the risk function, then I will show example risk functions, and finally I will cover admissibility and how it relates to this topic.

Consider the scenario where you have observed data $x_1...x_n$ from a given function $f(x|\theta)$ where the function is known but theta is unknown. You could have $x_1...x_n$ ~ $Norm(\theta,10)$ or another type of random variable. You want to use the data you have to determine the best estimator* of theta. Before even considering that, you must determine how you are going to measure the performance of the estimator which leads us to the concept of loss functions. 

*Note* I use the term estimator but others use the term procedure or decision rule. 

If you are familiar with regression, you have likely seen the squared error loss function $L(\theta, \delta) = (\theta – \delta)^2$. Here, theta what you are estimating and delta is the estimator. For the squared error loss, estimates further away from the actual value of theta incur a relatively larger penalty than estimates close to the true value. Another example of a loss function is the absolute loss $L(\theta, \delta) = |\theta – \delta|$ which has different characteristics than the squared error loss that are not so important for this post. To put it simply, the purpose of a loss function is to penalize bad guesses. There is no “right” answer for which loss function to chose as it is contextual and depends on the specific problem. 

Now that we have a way of measuring performance, we can talk about the risk function which is the way of quantifying the quality of an estimator. The risk function for an estimator and loss function is defined as the expected value of the loss function for a given theta:

$$R(\theta, \delta) = E_\theta[L(\theta, \delta(X)]$$

Ideally, you would have an estimator that has low risk for all values of theta but, like almost everything, there is a performance tradeoff. There is no estimator that is the best under all scenarios. 

For the squared error loss function, the expected value of the loss (risk) can be decomposed into two parts: bias and variance. You have possibly seen the definition of $var(x) = E[x^2] – E[x]^2$ which is what you have with this risk function given that theta is considered as a constant. If you rearrange that formula, you have $E[x^2] = var(x) + E[x]^2$. Replace x with $(\theta – \delta)$ and you have the bias $(E[\theta – \delta])$ and variance. Theta is constant so this becomes:

$$R_\delta(\theta) = (\theta – E[\delta])^2 + var(\delta)$$

Let’s revisit the original example where $x_1...x_n ~ Norm(\theta,10)$ where we are using a squared error loss function. We will evaluate the following estimators:

$$\delta_1 = \bar{x}$$

$$\delta_2 = 2$$

$$\delta_3 = 2\bar{x} + 1$$

The first estimator uses the mean of the observations, the second guesses 2 regardless of the observations, and the third uses a multiple of the mean with an added constant. The expected value of the mean for a $Norm(\theta,10)$ distribution is theta with variance 10/n. The expected value of $2*\bar{x}$ is $2\theta$ with variance 40/n given by the fact that var(2x) = 4*var(x). Therefore, the risk functions using these estimators are:

$$R1 = 10/n$$

$$R2 = (\theta – 2)^2$$

$$R3 = (\theta – 2\theta)^2 + 40/n = \theta^2 + 40/n$$

<br/><img src='/images/Risk.png'>

You can see there are values of $\theta$ for which $\delta_2$ is the best estimator and other values where $\delta_1$ is the best estimator. You should also notice that there are no values for which $\delta_3$ is the optimal estimator. In fact, it is universally worse than $\delta_1$ which brings me to the final part of this post – the concept of admissibility.

An estimator, $\delta’$, is considered inadmissible if there exists another estimator, $\delta*$, for which:

$a)	R_{\delta’}(\theta) >= R_{\delta*}(\theta) \hspace{2em} \forall \theta \in \Omega$

$b)	R_{\delta’}(\theta) > R_{\delta*}(\theta)$ for at least one $\theta \in \Omega$

You can also show that an estimator is admissible by showing it is Bayes optimal for a given prior but that is another topic for another time.




This post will show up by default. To disable scheduling of future posts, edit `config.yml` and set `future: false`. 

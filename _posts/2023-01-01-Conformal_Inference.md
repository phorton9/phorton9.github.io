---
title: 'Conformal Inference'
date: 2023-1-9
permalink: /posts/2022/12/NewPost/
tags:
  - Conformal Inference
  - Prediction Interval
  - Machine Learning
---
You are driving down the road during a thunderstorm. Your windshield wipers are old so it is difficult to see but you notice a sign in the distance. The color is not distinct and the shape is unclear through the rain. You decide to slow down because of the wet conditions and the uncertainty around the sign. As you approach, the red octagon becomes clear as do the other cars in the intersection. Fortunately, you used your uncertainty to guide your decision to be cautious so there was no accident. It is uncertainty (or confidence) that helps a decision maker take the best action and this is why quanitfying uncertainty has value for machine learning.

Decision making is built around uncertainty. You may be willing to undergo a surgical procedure if the doctor is confident in the diagnosis. If the doctor expresses more uncertainty, you may find the risk is not work taking and opt for other treatments. However, typically you will see output of predictive models as only a scalar value for regression or single class for a categorical problem. You might see the classification of an image as either "Cat" or "Dog". For binary classification, you can select a loss function to give a continuous value from 0-1 as a proxy for the confidence. Even linear regression models methods for prediction intervals. Now, conformal inference has emerged as a method for quantifying uncertainty without any restrictions on the distribution of data or the underlying model. In this post, I will describe why this is a promising application for statistical decision theory.

The main concept behind conformal inference is quantifying uncertainty while delivering a prediction interval that contains the true value with a $1-\alpha$ probability. What is powerful about conformal inference is that there are no assuptions about the distribution or underlying model. Top performing algorithms  built around neural networks and ensemble methods need an approach that can deliver this prediction interval since they have no requirements like the normality of data with linear regression. Early methods with this design required <a href="https://arxiv.org/pdf/2005.06095v1.pdf">exchangeable data</a>, a topic that deserves its own discussion, but new developments are branching beyond that. 

There are three (basic) steps to generating a conformal interval for a regression problem:
  1) Generate a predictive model using training data.
  2) Calculate the residuals relative to your prediction using the calibration data.
  3) Find the $1 - \alpha$ quantile of the residuals for your prediction interval.

Derivatives of this method include predicting the $\alpha / 2$ and $1-\alpha / 2$ quantiles in step 1 as opposed to the mean or median. Additionally, there are procedures which estimate a prediction interval for a single point using the rest of the data (full conformal) and others where data are initially split into roughly even training and calibration datasets (split conformal). 

I followed the steps outlined in <a href="https://proceedings.neurips.cc/paper/2019/file/5103c3584b063c431bd1268e9b5e76fb-Paper.pdf">this conformalized quantile regression paper</a> for a better perspective of how it works. I used a quantile random forest for my base model and generated synthetic data from the following distribution:

$$Y_i ∼ Pois(sin^2(X_i) + 0.1) + 0.01 \times X_i \epsilon_{1,i} + 25\times1{U_i < 0.01} \epsilon_{2,i}$$

Here, X is Uniform(1,5), both $\epsilon_{1,i}$ and $\epsilon_{2,i}$ are Normal(0,1) and U is Uniform(0,1). For a single run, I generated 2000 observations for the training set and 5000 for the calibration set. The following graph shows the calibration data along with the upper and lower bounds for the $1 - \alpha$ prediction interval with $\alpha = 0.1$.

<p align="center">
  <br/><img src='/images/DistributionWPI.png' width="300" alt="alt attribute goes here!" title="Calibration Data with Prediction Interval">
</p>

As outlined <a href="http://people.eecs.berkeley.edu/~angelopoulos/publications/downloads/gentle_intro_conformal_dfuq.pdf">here in section 3.3</a>, there are procedures for validating the correct implementation. One of which is take a number of trials and find the mean coverage value. I ran 100 trials and had an average coverage of 90.1% along with the following histogram of results where the percent outside the coverage interval roughly centered around 10%.

<p align="center">
  <br/><img src='/images/coverageHist.png' width="300" alt="alt attribute goes here!" title="Histogram of Coverage Results">
</p>

One interesting finding for me was that the initial prediction interval from the quantile random forest had greater than 90% coverage. The adjusted prediction interval was actually smaller after using the calibration set to compute residuals and compute Q.

If you are interested in my example code, you can find the file: https://github.com/phorton9/BlogCode/blob/main/ConformalQuantileRegression.R

Conformal inference originally was applicable to classification and regression problems but there are now extensions for <a href="http://proceedings.mlr.press/v139/xu21h.html?ref=https://codemonkey.link">time series data</a>, <a href="https://arxiv.org/pdf/2208.02814.pdf">segmentation</a>, <a href="https://arxiv.org/pdf/2208.02814.pdf"> data from changing distributions</a>, and <a href="https://arxiv.org/pdf/2104.08279.pdf">outlier detection</a>. It seems hard to see the end of the expansion of where conformal inference can be applied.

If you are interested in learning more, the following <a href="http://people.eecs.berkeley.edu/~angelopoulos/publications/downloads/gentle_intro_conformal_dfuq.pdf">paper</a> has a great (and much more thorough) introduction to the topic complete with a history that even has an accompanying <a href="https://www.youtube.com/watch?v=nql000Lu_iE">video</a>. 

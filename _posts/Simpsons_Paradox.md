---
title: 'Simpson Paradox'
date: 2023-1-23
permalink: /posts/2022/12/SimpsonsParadox/
tags:
  - Simpson's Paradox
  - Correlation
  - Pattern
---

No, this is not a post about the Simpson's episode where Homer visits the 3rd dimension. Simpson's paradox is a phenomenon where patterns or trends are different for subgroups compared to the entire sample. As data exploration is a critical component to any analysis, this is an important concept to have in mind to potentially prevent an erroneous conclusion from one view of the data.

The simplest way to understand this concept is through visualization. The following shows the correlation for two groups independently in black lines and then combined in the blue. What is worth noting is that, despite both subgroups having negative correlations, the relationship reverses when looking at the combined groups.

<p align="center">
  <br/><img src='/images/Neg_Pos.png' width="300" alt="alt attribute goes here!" title="Simpson's Paradox for Correlations">
</p>

We can attribute this reversal to the difference in means between the two subgroups for both of the random variables. As you may recall, the calculation for sample correlation is:
$$r =\frac{\sum_{i=1} (x_i-\bar{x})(y_i-\bar{y})}{\sqrt{\sum_{i=1} (x_i-\bar{x})^2\sum_{i=1} (y_i-\bar{y})^2}}$$
In the previous example, the two subgroups have negative correlations between variables $X$ and $Y$ of $\rho_1 = -0.8$ and $\rho_2 = -0.6$ respectively. However, they come from normal distributions with different means:

$$
\mu_1 = \begin{bmatrix}{} 
0\\
0
\end{bmatrix}
$$

$$
\mu_2 = \begin{bmatrix}{} 
6\\
6
\end{bmatrix}
$$

Both subgroups have the same number of samples so, when combined, the new sample average is:

$$
\bar{x}_{combined} = \begin{bmatrix}{} 
3\\
3
\end{bmatrix}
$$

One question that you might consider after the previous example is: What can you do to correct it? If you have read one of the other posts about sample size estimation, you will recall the effect that standardization has on the correlations of combined samples. 

<p align="center">
  <br/><img src='/images/Standardized.png' width="300" alt="alt attribute goes here!" title="Simpson's Paradox for Correlations">
</p>

With distance measurements, such as the distance from the sample mean or distance from the nearest neighbors in KNN, it is important to 

Another example of this phenomenon is the  <a href="https://homepage.stat.uiowa.edu/~mbognar/1030/Bickel-Berkeley.pdf ">paper on gender bias in admissions at UC Berkeley</a>. When compared strictly on the basis of gender, the authors found that women had a lower acceptance rate than men. However, when the authors divided the admissions data into departments, they found that women were more likely to apply to departments with lower average admission rates. This fact dragged on the overall admission rate for women and refuted the notion that women were being discriminated against.

One concept that this leads to is the importance of standardization. 

For more information <a href="https://plato.stanford.edu/entries/paradox-simpson/">link</a>

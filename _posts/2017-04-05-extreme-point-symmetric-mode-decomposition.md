---
layout: post
title: Extreme Point Symmetric Mode Decomposition
description: How to extract trend based on Extreme Point Symmetric Mode Decomposition
summary: How to extract trend based on Extreme Point Symmetric Mode Decomposition
author:
- Pavan Donthireddy
usemathjax: true
tags: [trend_extraction, EMD, ESMD]
---

<p align="justify">Considering the extraction methods of trend item, including the difference method, average slope method, moving average method, low pass filtering method, and least square fitting method, the type of trend term often needs to be presupposed. These methods are not suitable for processing the nonstationary signals with complex or random change trends.</p>

<p align="justify">According to previous studies, the wavelet transform-based method is required for preselecting the wavelet basis and decomposition levels. This method is influenced easily by
artificial factors and has no self-adaptability. </p>

<p align="justify">The method based on Empirical mode decomposition (EMD) can adaptively decompose non-stationary signals regardless of the type of trend term. But, EMD is affected by mode mixing and
end effect, causing the decomposed trend function is rough and the extraction accuracy is restricted. </p>

<p align="justify">Professor Wang et al. recently proposed a self-adaptive method called ESMD. The ESMD is a novel development derived from Hilbert Huang transform that can be used to process non-stationary signal. ESMD has been applied to many studies.</p>

## ESMD

- **Step 1:** Identify all local extreme points, including maxima and minima points, of the data $Y$. Mark them as $E_{i} (1 ≤ i ≤ n);$
- **Step 2:** Connect all adjacent Ei with line segments, and mark their midpoints as $F_{i} (1 ≤ i ≤ n-1);$
- **Step 3:** Add left and right boundary midpoints $F_{0}$ and $F_{n}$ using linear interpolation method;
- **Step 4:** Construct $p$ interpolating curves $L_{1}, L_{2},\dots L_{p} (p≥1)$ with all $n+1$ midpoints and calculate their mean value by using equation $L^{\ast}$.

$$
L^{*}= \frac{L_{1}+L_{2}+\dots + L_{p}}{p}
$$

- **Step 5:** Repeat steps $1$ to $4$ on $Y - L^{\ast}$ until $\|\|L^{\ast}\|\| \le \epsilon$ ($\epsilon$ is a permitted error), or until the sifting times attain a preset maximum number $K$. Then, the first mode $M_{1}$ is obtained.
- **Step 6:** Repeat steps $1$ to $5$ on the residual $Y - M_1$ and obtain $M_2, M_3 \dots$ until the last residual $R$ with no more than a certain number of extreme points.
- **Step 7:** Change the maximum number $K$ on a finite integer interval $[K_{min}, K_{max}],$ and repeat all previous steps. Calculate the variance $\sigma^2$ of $Y - R$ and plot a figure with $\frac{\sigma}{\sigma_{0}}$ and $K$, $\sigma_{0}$ is the standard deviation of $Y$. 

$$ 
\sigma^2 = \frac{1}{N}\sum_{i=1}^N(y_{i}-r_{i})^2
$$ 

$$ 
\sigma_{0}^2 = \frac{1}{N}\sum_{i=1}^N(y_{i}-\bar{Y})^2 
$$

- **Step 8 :** Identify the number $K_0$ which corresponds to the minimum  $\frac{\sigma}{\sigma_{0}}$  in $[K_{min}, K_{max}].$  Use this $K_{0}$ to repeat steps $1$ to $6$ and obtain the whole modes. Then last residual $R$ is an optimal Adaptive global mean (AGM) curve.


Based on the steps above, ESMD can decompose signal into limited intrinsic mode functions and a residual component. The residual component $R$ is an optimal AGM curve that can be considered as the trend term of the original signal.

<u>The extraction error of EMD is larger than that of ESMD. </u>

1. The EMD-based extraction method can adaptively extract the signal trend. Whereas, the extracted trend curve limits the number of its extreme points (no more than 1), and no optimal strategy to find it. Therefore, the extraction error of EMD is relatively larger than that of ESMD. 
2. The ESMD-based extraction method has commendable self-adaptability. It can obtain the signal trend with high precision using adaptive decomposition and optimization. The trend type of signal does not need to be preset. And, the extraction results of ESMD are better than that of EMD.

Reference: Adaptive extraction method for trend term of machinery signal based on
extreme-point symmetric mode decomposition - Yong Zhu, Wan-lu Jiang and Xiang-dong Kong

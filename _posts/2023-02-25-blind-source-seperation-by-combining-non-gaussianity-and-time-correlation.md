---
layout: post
title: Blind source separation for noisy time series by combining non-Gaussianity and time correlation
description: Blind source separation for noisy time series by combining non-Gaussianity and time correlation
summary: Blind source separation for noisy time series by combining non-Gaussianity and time correlation
author:
- Pavan Donthireddy
mathjax: true
tags: [BlindSourceSeperation, whitening, preprocessing]
original: zhang2008
---

## Abstract 

<p align="justify">This paper addressed the separation of noisy time series
(noisy signals with time structure). Based on the non-
Gaussianity of innovations, we first present an objective
function with negentropy forms about innovations of time
series. Furthermore, this criterion is extended for the noisy
time series separation through combing Gaussian moments
into it. Maximizing this objective function, a simple blind
source separation algorithm is presented.</p>

## Introduction

<p align="justify">Generally,
classical BSSmethods often utilize the non-Gaussianity as a
leading principle, which only use the marginal distributions
of the estimated signals and completely ignore any time
structure in their basic forms. However, in many applications,
what are mixed are not random variables but time signals,
or time series. Moreover, it has been shown interestingly
that under some restrictions, the time-dependency information
along is sufficient to estimated independent components
[5, 6, 7, 8]. Therefore, it would be most useful to
define a more general method that finds interesting projections
of time series using both the non-Guassianity and the
time structure of the projections.</p>

<p align="justify">Moreover, in many
cases we often assume that the innovations of the time series
are super-Gaussian, which seems to be the preponderant 
case in natural data. In this paper, we make
full use of the non-Gaussianity of the innovations to generate
the criterion based on the negentropy expression of the
innovations firstly. Furthermore, this criterion is developed
for the blind source separation of noisy time series. This
novel approaches combine the Gaussian moments and the
non-Gaussianity of the innovations, where Gaussian moments
are selected as the replacement of the nonquadratic
functions in negentropy expression. Maximizing this objective
function, a blind source separation algorithm is derived.
Experiments in the following show that in the separation
of noisy time series, the proposed algorithm outperforms
some existing algorithms, such as noise techniques–
the algorithm of [12] (simplified with ”NoisyCP”), the algorithm
in (called ”FastNoisyICA”), and noise-free
approach– GradCP algorithm.</p>


## Proposed algorithm

### Quasi-whitening

Denote the observed sensor signals $\mathrm{x}(t)=$ $\left(x_1(t), \cdots, x_m(t)\right)^T$ described by matrix equation
$$
\mathbf{x}(t)=\mathbf{A} \mathbf{s}(t)+\mathbf{n}(t)
$$
where $\mathbf{A}$ is an $m \times n$ unknown mixing matrix $(n \leq m)$, $\mathbf{s}(t)=\left(s_1(t), \cdots, s_n(t)\right)^T$ is a vector of unknown temporally correlated sources (zero-mean and unit-variance), $\mathbf{n}(t)=\left(n_1(t), \cdots, n_m(t)\right)^T$ is a vector of additive noise which is modeled as a stationary, temporally white, zeromean complex random process independent of the source signals, and whose covariance matrix is defined as $\boldsymbol{\Sigma}$ (that is, $\boldsymbol{\Sigma}=E\left\{\mathbf{n}(t) \mathbf{n}(t)^T\right\}$ ) and $t=1,2, \ldots, T$ is the time index. It is further assumed that the dimensions of $\mathrm{x}$ and $\mathrm{s}$ are equal, i.e. $m=n$ in this paper.

It must be noted, however, in the preliminary whitening, the effect of noise must be taken into account. This is quite simple if the noise covariance matrix $\Sigma$ is known or can be estimated. Provided that the measured sensor signals $\mathbf{x}(t)$ has the covariance matrix denoted by $\mathbf{C}=E\left\{\mathbf{x}(t) \mathbf{x}(t)^T\right\}$, the ordinary whitening should be changed into the following "quasi-whitening" operation
$$
\tilde{\mathbf{x}}(t)=(\mathbf{C}-\mathbf{\Sigma})^{-\frac{1}{2}} \mathbf{x}(t)
$$
In other words, the covariance matrix $(\mathbf{C}-\mathbf{\Sigma})$ of the noisefree data should be used in whitening instead of the covariance matrix $\mathbf{C}$ of the noisy data. The quasi-whiten data $\tilde{\mathbf{x}}$ follows a noisy ICA model as well, that is
$$
\tilde{\mathbf{x}}(t)=\mathbf{B s}(t)+\tilde{\mathbf{n}}(t)
$$
where $\mathbf{B}=(\mathbf{C}-\boldsymbol{\Sigma})^{-\frac{1}{2}} \mathbf{A}$ is an orthogonal mixing matrix, and noise $\tilde{\mathbf{n}}$ is a linear transform of the original noise, which having the following covariance matrix $[13,14]$
$$
\tilde{\mathbf{\Sigma}}=E\left\{\tilde{\mathbf{n}}(t) \tilde{\mathbf{n}}(t)^T\right\}=(\mathbf{C}-\mathbf{\Sigma})^{-\frac{1}{2}} \mathbf{\Sigma}(\mathbf{C}-\mathbf{\Sigma})^{-\frac{1}{2}}
$$
### Contrast function

Denote the noise-free data by $\mathbf{y}(t)=\mathbf{B s}(t)$, the basic idea in the complexity pursuit is to find projection $\mathbf{w}^T \mathbf{y}(t)$ such that the Kolmogoroff complexity of the projection is minimized. Similarly, we consider predictive coding of a scalar signal $z(t)=\mathbf{w}^T \mathbf{y}(t)(t=1, \ldots, T)$. Suppose the value of $z(t)$ is predicted from the preceding values by some function to be specified
$$
\hat{z}(t)=f(z(t-1), \ldots, z(1))
$$
To code the actual value $z(t)$, the innovation
$$
\delta z(t)=z(t)-\hat{z}(t)
$$
is coded by a scalar quantization method. Assuming that the innovation is stationary and ergodic and that the predictor uses a history of bounded length, and ignoring border effects. In practice, we need to fix the structure of the predictor $f$ and use a computationally simple predictor structure, given by a linear autoregressive model
$$
\hat{z}(t)=\sum_{\tau>0} \alpha_\tau z(t-\tau)
$$
Note that in [9] it has been pointed that minimizing the first term of their objective function amounts to finding direction in which the innovation is as non-Gaussianity as possible. In particular, in many cases we can assume that the innovations are super-Gaussian, which seems to be the preponderant case in natural data $[9,10,11]$. Therefore, the innovations can be considered as a random vector with non-Gaussianity. There also is a fact that the higher nonGaussianity of the innovations corresponds to the more sparseness of theirs and furthermore the better performance of source separations.

Actually, non-Gaussianity is of paramount importance in ICA estimation, which is a simple and intuitive principle for estimating ICs. The fourth-order cumulant, or kurtosis is the first practical measure of non-Gaussianity, however, it gives estimators that are very sensitive to outliers and have large mean square errors (at least for super-Gaussian data) $[4,13,14]$. Therefore, we use the information-theoretic quantity called negentropy as an alternative measure of innovations' non-Gaussianity, and derive the corresponding algorithms for this measure. Denote the contrast functions of the innovations $\delta z(t)$ as follows
$$
J_G(\delta z(t))=\left[E\{G(\delta z(t)\}-E\{G(\nu)\}]^2\right.
$$
where the function $G$ is a sufficiently regular nonquadratic function, $\nu$ is a standardized Gaussian variable, and innovations $\delta z(t)=\mathbf{w}^T \delta \mathbf{y}(t)$ are mutually statistically independent and have zero mean and unit variance, where $\delta \mathbf{y}(t)=\mathbf{y}(t)-\sum_{\tau>0} \alpha_\tau \mathbf{y}(t-\tau)$

### Gaussian moments

In formula (8), however, the noise term was not considered at all. Therefore, we might extend this formula to the case when noise is present. It must be pointed out that these approaches given in Section 2.2 could be used for noisy data, if only we were able to estimate $J_G(\delta z(t))$ of the noise-free data from the noisy observations $x$. The main point of this problem is to select some suitable measures, which are immune to Gaussian noise, or at least, whose values for the original data can be easily estimated from noisy observations. Denote by
$$
\varphi_c(x)=\frac{1}{c} \varphi\left(\frac{x}{c}\right)=\frac{1}{\sqrt{2 \pi} c} \exp \left(-\frac{x^2}{2 c^2}\right)
$$
the Gaussian density function of variance $c^2$, and by $\varphi_c^{(k)}(x)$ the $k$-th $(k>0)$ derivative of $\varphi_c(x)$. Denote further by $\varphi_c^{(-k)}(x)$ the $k$-th integral function of $\varphi_c(x)$, obtained by $\varphi_c^{(-k)}(x)=\int_0^x \varphi_c^{(-k+1)}(\xi) d \xi$, where we define $\varphi_c^{(0)}(x)=\varphi_c(x)$. Then we have the following theorem $[12,13,14]$

*<u>Theorem 1</u> Let $v$ be any non-Gaussian random variable, and denote by $n$ an independent Gaussian noise variable of variance $\sigma^2$. Define the Gaussian function $\varphi$ as in (9). Then for any constant $c>\sigma^2$, we have*
$$
E\left\{\varphi_c(v)\right\}=E\left\{\varphi_d(v+n)\right\}
$$
*with $d=\sqrt{c^2-\sigma^2}$. Moreover, (10) still holds when $\varphi$ is replaced $\varphi^{(k)}$ for any integer index $k$.*

This theorem means that we can estimate the ICs from noisy observations by maximizing a general contrast function of form (8), where the estimation of the statistics $E\{G(\delta z(t)\}$ of the noise-free data is made possible by using $E\left\{\varphi_c^{(k)}(\delta z(t)\}\right.$. The statistics of the form $E\left\{\varphi_c^{(k)}(\delta z)\right\}$ is called the Gaussian moments of the innovations $\delta z(t)$ $[12,13,14]$. Thus from (8) and (10), we can estimate the noisy model by maximizing, for the innovations of the quasi-whitened data $\tilde{\mathrm{x}}$, the following contrast function
$$
\max _{\|\mathbf{w}\|=1} \Phi\left(\mathbf{w}^T \delta \tilde{\mathbf{x}}(t)\right)=\left[E\left\{\varphi_{d(\mathbf{w})}^{(k)}\left(\mathbf{w}^T \delta \tilde{\mathbf{x}}(t)\right)\right\}-E\left\{\varphi_c^{(k)}(\nu)\right\}\right]^2
$$
where $\delta \tilde{\mathbf{x}}(t)=\tilde{\mathbf{x}}(t)-\sum_{\tau>0} \alpha_\tau \tilde{\mathbf{x}}(t-\tau), \mathbf{w}^T \delta \tilde{\mathbf{x}}(t)=$ $\delta z(t)+\mathbf{w}^T\left(\tilde{\mathbf{n}}(t)-\sum_{\tau>0} \alpha_\tau \tilde{\mathbf{n}}(t-\tau)\right)$, correspondingly, $d(\mathbf{w})=\sqrt{c^2-\left(1+\sum_{\tau>0} \alpha_\tau^2\right) \mathbf{w}^T \tilde{\mathbf{\Sigma}} \mathbf{w}}$

### Learning algorithm

Before we derive the learning algorithm, it is worth noting that the maxima of the approximation of the negentropy of the $\mathbf{w}^T \delta \tilde{\mathbf{x}}(t)$ are typically obtained at certain optima of $E\left\{\varphi_{d(\mathbf{w})}^{(k)}\left(\mathbf{w}^T \delta \tilde{\mathbf{x}}(t)\right)\right\}[4]$.
Note that
$$
\varphi_c^{(k)}(x)=\varphi^{(k)}\left(\frac{x}{c}\right) c^{(-k-1)}
$$
and denote as above
$$
\begin{aligned}
& d(\mathbf{w})=\sqrt{c^2-\left(1+\sum_{\tau>0} \alpha_\tau^2\right) \mathbf{w}^T \tilde{\mathbf{\Sigma}} \mathbf{w}} \\
& X=\mathbf{w}^T \delta \tilde{\mathbf{x}}(t), \\
& \tilde{d}=c^2-\left(1+\sum_{\tau>0} \alpha_\tau^2\right) \mathbf{w}^T \tilde{\mathbf{\Sigma}} \mathbf{w}
\end{aligned}
$$
Then the gradient of $\operatorname{term} \varphi_{d(\mathbf{w})}^{(k)}(X)$ with respect to $\mathbf{w}$ can be computed as
$$
\begin{aligned}
& \nabla_{\mathbf{w}} \varphi_{d(\mathbf{w})}^{(k)}(X)=\varphi_{d(\mathbf{w})}^{(k+1)}(X) \nabla_{\mathbf{w}} X-\frac{1}{2} d^{-2}(\mathbf{w}) \\
& \times\left(X \varphi_{d(\mathbf{w})}^{(k+1)}(X)+(k+1) \varphi_{d(\mathbf{w})}^{(k)}(X)\right) \nabla_{\mathbf{w}} \tilde{d} .
\end{aligned}
$$
To proceed, we use the lemma in [14] to imply
$$
\begin{aligned}
& d^{-2}(\mathbf{w})\left(X \varphi_{d(\mathbf{w})}^{(k+1)}(X)+(k+1) \varphi_{d(\mathbf{w})}^{(k)}(X)\right) \\
& =-\varphi_{d(\mathbf{w})}^{(k+2)}(X)
\end{aligned}
$$
This means the gradient in (16) can be expressed as
$$
\begin{aligned}
\nabla_{\mathbf{w}} \varphi_{d(\mathbf{w})}^{(k)}(X)= & \varphi_{d(\mathbf{w})}^{(k+1)}(X) \nabla_{\mathbf{w}} X \\
& +\frac{1}{2} \varphi_{d(\mathbf{w})}^{(k+2)}(X) \nabla_{\mathbf{w}} \tilde{d}
\end{aligned}
$$

That is
$$
\begin{aligned}
& \nabla_{\mathbf{w}} \varphi_{d(\mathbf{w})}^{(k)}\left(\mathbf{w}^T \delta \tilde{\mathbf{x}}(t)\right)=\varphi_{d(\mathbf{w})}^{(k+1)}\left(\mathbf{w}^T \delta \tilde{\mathbf{x}}(t)\right) \delta \tilde{\mathbf{x}}(t) \\
& -\left(1+\sum_{\tau>0} \alpha_\tau^2\right) \varphi_{d(\mathbf{w})}^{(k+2)}\left(\mathbf{w}^T \delta \tilde{\mathbf{x}}(t)\right) \tilde{\mathbf{\Sigma}} \mathbf{w} .
\end{aligned}
$$
Suppose $\delta s_i(t)=s_i(t)-\sum_{\tau>0} \alpha_\tau^i s_i(t-\tau)(i=1, \ldots, n)$ are mutually independent and have zero mean and unit variance (assume that $\alpha_\tau^i, i=1, \ldots, n$ are the known constants). Therefore, the equation giving the fixed-point algorithm was given just like in $[4,15,16]$ as
$$
\mathbf{w} \leftarrow E\left\{\nabla G\left(\mathbf{w}^T \delta \mathbf{y}(t)\right)\right\}-\mathbf{w} E\left\{G^{\prime \prime}\left(\mathbf{w}^T \delta \mathbf{y}(t)\right)\right\} .
$$
Choosing $G(u)=\varphi_c^{(k)}(u)$ and using the above derivation, we obtain the gradient part as (19). By Theorem 1, we have
$$
E\left\{G^{\prime \prime}\left(\mathbf{w}^T \delta \mathbf{y}(t)\right)\right\}=E\left\{\varphi_{d(\mathbf{w})}^{(k+2)}\left(\mathbf{w}^T \delta \tilde{\mathbf{x}}(t)\right)\right\} .
$$
Then we obtain
$$
\begin{aligned}
\mathbf{w} \leftarrow & E\left\{\nabla_{\mathbf{w}} \varphi_{d(\mathbf{w})}^{(k)}\left(\mathbf{w}^T \delta \tilde{\mathbf{x}}(t)\right)\right\} \\
& -\mathbf{w} E\left\{\varphi_{d(\mathbf{w})}^{(k+2)}\left(\mathbf{w}^T \delta \tilde{\mathbf{x}}(t)\right)\right\} .
\end{aligned}
$$
Thus we obtain the form of the fixed-point iteration for the innovations of the quasi-whitened data
$$
\begin{aligned}
& \mathbf{w} \leftarrow E\left\{\varphi_{d(\mathbf{w})}^{(k+1)}\left(\mathbf{w}^T \delta \tilde{\mathbf{x}}(t)\right) \delta \tilde{\mathbf{x}}(t)-\left(1+\sum_{\tau>0} \alpha_\tau^2\right)\right. \\
& \left.\times \tilde{\mathbf{\Sigma}} \mathbf{w} \varphi_{d(\mathbf{w})}^{(k+2)}\left(\mathbf{w}^T \delta \tilde{\mathbf{x}}(t)\right)\right\}-E\left\{\mathbf{w} \varphi_{d(\mathbf{w})}^{(k+2)}\left(\mathbf{w}^T \delta \tilde{\mathbf{x}}(t)\right)\right\} .
\end{aligned}
$$
Note that we could adapt parameter $c$ before every step so that $d(\mathbf{w})=\sqrt{c^2-\mathbf{w}^T \tilde{\mathbf{\Sigma}} \mathbf{w}}=1[13,14]$, and correspondingly choosing $G(u)=\varphi^{(k)}(u)$. Thus the learning rule is
$$
\begin{aligned}
\mathbf{w} \leftarrow & E\left\{( \tilde { \mathbf { x } } ( t ) - \sum _ { \tau > 0 } \alpha _ { \tau } \tilde { \mathbf { x } } ( t - \tau ) ) g \left(\mathbf{w}^T(\tilde{\mathbf{x}}(t)-\right.\right. \\
& \left.\left.\left.\sum_{\tau>0} \alpha_\tau \tilde{\mathbf{x}}(t-\tau)\right)\right)\right\}-\left(1+\sum_{\tau>0} \alpha_\tau^2\right) \tilde{\mathbf{\Sigma}} \mathbf{w} \\
& \times E\left\{g^{\prime}\left(\mathbf{w}^T\left(\tilde{\mathbf{x}}(t)-\sum_{\tau>0} \alpha_\tau \tilde{\mathbf{x}}(t-\tau)\right)\right)\right\} \\
& -\mathbf{w} E\left\{g^{\prime}\left(\mathbf{w}^T\left(\tilde{\mathbf{x}}(t)-\sum_{\tau>0} \alpha_\tau \tilde{\mathbf{x}}(t-\tau)\right)\right)\right\} \\
\mathbf{w} \leftarrow & \frac{\mathbf{w}}{\|\mathbf{w}\|},
\end{aligned}
$$
where $\tilde{\mathbf{\Sigma}}$ is given by (4) and the function $g$ is the derivative of $G, g^{\prime}$ corresponds to the derivative of $g$. Example of choice is $G(u)=\log \cosh (u)$, which is an approximation of $\varphi^{(-2)}$ and has been widely used in ICA $[1,2,12,13,14]$.
A simple special case of the method is obtained when the autoregressive model has just one predicting term [9]
$$
\hat{z}(t)=\alpha_1 z(t-1)
$$
The lag need not be equal to 1 , but this is the basic case. The parameter $\alpha_1$ in the algorithm can then be estimated simply by a least-squares method as [9]
$$
\hat{\alpha}_1=\mathbf{w}^T E\left\{\tilde{\mathbf{x}}(t) \tilde{\mathbf{x}}(t-1)^T\right\} \mathbf{w}
$$
### Simulations

In this section, extensive computer simulations were carried out to verify the validity of the proposed algorithm, which compared to the noise techniques- FastnoisyICA algorithm, NosiyCP algorithm and noise-free methodGradCP algorithm. In the comparisons, the quasi-whitening data were applied as the inputs of all the algorithms. The step sizes in GradCP algorithm and NoisyCP algorithm were taken equal to 1 , the time delays of GradCP, NoisyCP and our algorithm were 1 and the nonlinearity functions of all algorithms were chosen as $G(u)=\log \cosh (u)$. Note that in the simulations, the symmetric orthogonalization version of all algorithms for quasi-whitening data was used for estimating the weight vectors $\mathbf{w}_i$ in parallel. Moreover, the performance of algorithms to the estimated signal is measured by performance index (PI), which is defined as follows
$$
\begin{aligned}
\mathrm{PI}= & \frac{1}{n^2}\left\{\sum_{i=1}^n\left(\sum_{j=1}^n \frac{\left|p_{i j}\right|}{\max _k\left|p_{i k}\right|}-1\right)\right. \\
& \left.+\sum_{j=1}^n\left(\sum_{i=1}^n \frac{\left|p_{i j}\right|}{\max _k\left|p_{k j}\right|}-1\right)\right\},
\end{aligned}
$$
where $p_{i j}$ denotes the $i j$ th element of $n \times n$ matrix $\mathbf{P}=$ $\mathbf{W}^T \mathbf{B A}$, where $\mathbf{W}=\left(\mathbf{w}_1, \ldots, \mathbf{w}_n\right)$ is the demixing matrix, $\mathbf{B}$ corresponds to the orthogonal matrix in quasiwhitening operation and $\mathbf{A}$ is the mixing matrix. The larger value PI is, the poorer performance of the algorithm is. In the following experiments, we considered the separation of four signals using an AR(1) model, which have been applied in $[9,12]$. Signals 1 and 2 were created with superGaussian innovations and signals 3 and 4 with Gaussian innovations; all innovations had unit variance. Signals 1 and 3 had identical autoregressive coefficients $(0.25)$ and therefore identical autocovariances; signals 2 and 4 had identical coefficients $(0.5)$ as well. And here the sample size was 25000. The observations $\mathrm{x}$ with a white Gaussian noise (covariance $0.01 \mathrm{I}$ ) were generated by a $4 \times 4$ random mixing matrix. The performance was estimated as the average PI values of 50 independent trials. At every trial, four algorithms were run with 100 iterations respectively, which seemed to be always enough for convergence. Here $\mathbf{A}$ and W were initialized randomly. 
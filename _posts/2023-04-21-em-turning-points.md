---
layout: post
title: Expectation Maximization for Change Point Detection in Time Series
description: This article describes the Expectation Maximization algorithm for finding change points in time series data. The algorithm is explained for both batch and online mode, and Python implementation is provided.
summary: This article provides detailed explanations of the Expectation Maximization algorithm for finding change points in time series data, including batch and online modes, and includes Python implementation.
author: Pavan Donthireddy
usemathjax: true
original: new
tags: [Expectation_Maximization , turning_points , changepoint ]
---

## Introduction

Change point detection in time series data is a fundamental problem in statistics and machine learning. A change point is a time at which some property of the time series changes abruptly. For example, a change point in stock prices could indicate a shift in market trends or a significant world event. Change point detection is therefore useful in many applications such as finance, weather forecasting, and medical research.

One approach for detecting change points is the Expectation Maximization (EM) algorithm. The EM algorithm is a powerful tool for finding the underlying structure of data that has been generated from an unknown source. It works by iteratively fitting a statistical model to the data, estimating the parameters of the model, and then using those parameters to predict the underlying structure of the data.

In this article, we will start by introducing the EM algorithm and its basic principles. We will then explain how it can be used to detect change points in time series data. Finally, we will demonstrate the algorithm through a Python implementation.

## The Expectation Maximization Algorithm

The Expectation Maximization algorithm is a general algorithm for finding maximum likelihood estimates of parameters in statistical models with hidden variables. It is often used when there is missing or incomplete information in the data.

In essence, the algorithm works by iteratively updating two sets of variables: the "expectation" variables (E-step) and the "maximization" variables (M-step). The expectation variables represent the expected value of the hidden variables given the observed data and the current estimate of the model parameters. The maximization variables represent the parameter estimates that maximize the likelihood of the observed data given the current estimate of the hidden variables.

The EM algorithm can be summarized in the following steps:

1. Initialize the parameters of the model.
2. Compute the expectation variables given the current estimate of the parameters.
3. Compute the maximization variables by maximizing the likelihood function given the expectation variables.
4. Repeat steps 2 and 3 until convergence.

This algorithm is guaranteed to converge to a local maximum of the likelihood function. However, there is no guarantee that this maximum is the global maximum. Therefore, it is often run multiple times with different initial conditions to ensure that the global maximum is found.

## EM Algorithm for Change Point Detection

Now that we have covered the basic principles of the EM algorithm, let us explain how it can be used for change point detection in time series data.

Suppose we have a time series { $x_1$, $x_2$, ..., $x_n$ } and we would like to detect any change points in the data. The EM algorithm can be used to fit a statistical model to the data that assumes that there are a fixed number of segments with different means.

Let us assume that the data is generated from the following statistical model:

$$
x_i = \mu_{z_i} + \epsilon_i
$$

where $z_i$ is the segment index, $\mu_{z_i}$ is the mean of segment $z_i$, and $\epsilon_i$ is the noise term for observation $i$.

We can think of this statistical model as a hidden Markov model, where the segment index $z_i$ is the hidden state and the observation $x_i$ is the observed variable.

To apply the EM algorithm, we need to define the expectation and maximization steps. Let $\theta = \{ \mu_1, ..., \mu_k, \pi_1, ..., \pi_k \}$ be the set of parameters of the model, where $k$ is the number of segments in the data and $\pi_i$ is the probability of being in segment $i$.

### Batch Mode

In the batch mode of the EM algorithm, we assume that we have access to the entire time series data at once. The algorithm proceeds as follows:

#### Expectation Step:

We compute the probability of being in segment $i$ given the observed data and the current estimate of the parameters:

$$
\gamma_{i,j} = p(z_i = j \mid x_1, ..., x_n, \theta) = \frac{\pi_j f(x_i \mid \mu_j)}{\sum_{r=1}^k \pi_r f(x_i \mid \mu_r)}
$$

where $f(x_i \mid \mu_j)$ is the probability density function of a normal distribution with mean $\mu_j$ and variance $\sigma^2$, and $\sigma$ is assumed to be constant for all segments.

#### Maximization Step:

We update the parameters by maximizing the log-likelihood of the observed data given the expectation variables, subject to the constraint that the probabilities of being in the different segments add up to one:

$$
\begin{aligned}
\pi_j &= \frac{1}{n} \sum_{i=1}^n \gamma_{i,j} \\
\mu_j &= \frac{\sum_{i=1}^n \gamma_{i,j} x_i}{\sum_{i=1}^n \gamma_{i,j}}
\end{aligned}
$$

We repeat the expectation and maximization steps until convergence.

#### Interpretation:

The EM algorithm in batch mode provides us with the maximum likelihood estimates of the segment means and probabilities of being in each segment. We can use this information to identify the change points in the data. A change point is identified as the time where the segment mean changes.

### Online Mode

In the online mode of the EM algorithm, we assume that we have access to the time series data one observation at a time. We update the model parameters after each observation is received. The algorithm proceeds as follows:

#### Expectation Step:

The expectation step remains the same as in the batch mode:

$$
\gamma_{i,j} = p(z_i = j \mid x_1, ..., x_n, \theta) = \frac{\pi_j f(x_i \mid \mu_j)}{\sum_{r=1}^k \pi_r f(x_i \mid \mu_r)}
$$

#### Maximization Step:

We update the parameters after each observation by maximizing the log-likelihood of the observed data up to that point subject to the same constraint as in the batch mode:

$$
\begin{aligned}
\pi_{j}^{(t)} &= \pi_{j}^{(t-1)} + \alpha_j \gamma_{n,j} \\
\mu_{j}^{(t)} &= \mu_{j}^{(t-1)} + \beta_j \gamma _{n,j} (x_{n} - \mu_{j}^{(t-1)})
\end{aligned}
$$

where $t$ is the time step, $\alpha_j$ and $\beta_j$ are the learning rates for the mixture weight and the mean parameter respectively.

We repeat the expectation and maximization steps after each observation is received.

#### Interpretation:

The EM algorithm in online mode provides the same information as in batch mode. However, it is more useful in applications where online learning is critical. For example, in a stock trading application where stock prices change frequently and rapidly, online change point detection using the EM algorithm can help predict future trends and alter trading strategies on the fly.

## Python Implementation

We present a Python implementation of the EM algorithm for change point detection in time series data. The implementation is optimized for the batch mode of the algorithm.

```python
import numpy as np
from scipy.stats import norm

def em_cp_detection(X, K, max_iter=100, tol=1e-3):
    """
    Expectation Maximization algorithm for change point detection
    Args:
        X: 1D numpy array of observations
        K: int, number of segments to fit
        max_iter: int, maximum number of EM iterations
        tol: float, tolerance for convergence
    Returns:
        tuple of numpy arrays:
            * Z: 1D np array of segment assignments (length N)
            * mu: np array of segment means (length K)
            * pi: np array of segment probabilities (length K)
    """
    n = len(X)
    Z = np.zeros(n)
    mu = np.zeros(K)
    pi = np.ones(K) / K
    sig_sq = 1  # assume constant variance for all segments
    ll_old = -np.inf
    for _ in range(max_iter):
        # E-step
        for i in range(n):
            likelihood = pi * norm.pdf(X[i], mu, np.sqrt(sig_sq))
            Z[i] = np.argmax(likelihood)
        # M-step
        for j in range(K):
            mask = Z == j
            n_j = np.sum(mask)
            pi[j] = n_j / n
            if n_j > 0:
                mu[j] = np.sum(X[mask]) / n_j
        # Compute log-likelihood
        ll_new = 0
        for i in range(n):
            ll_new += np.log(np.sum(pi * norm.pdf(X[i], mu, np.sqrt(sig_sq))))
        # Check for convergence
        if np.abs(ll_new - ll_old) < tol:
            break
        ll_old = ll_new
    return Z, mu, pi
```

## Conclusion

The Expectation Maximization algorithm is a powerful tool for finding maximum likelihood estimates of parameters in statistical models with hidden variables. Its applicability in batch and online mode makes it useful in many applications, including change point detection in time series data.

In this article, we have presented the EM algorithm for change point detection in time series data. We have explained the algorithm in both batch and online mode, and provided a Python implementation for the batch mode. We hope that this article will serve as a useful reference for those interested in implementing the EM algorithm for change point detection.
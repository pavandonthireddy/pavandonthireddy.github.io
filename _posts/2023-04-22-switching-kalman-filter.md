---
layout: post
title: "Switching Kalman Filter and Its Variants"
description: "This article explains the switching Kalman filter and its variants in detail. It also includes Python implementations of the algorithms."
summary: "The article explains the concept of switching Kalman filter, its variants, and their implementation in Python."
author: Pavan Donthireddy
usemathjax: true
original: new
tags: [kalman]
---

# Introduction
A Kalman filter is a widely used algorithm that provides optimal estimation of a state variable based on a series of noisy measurements. It makes use of the past measurements and uses them, along with the system dynamics, to predict the future state of the system. This predicted state is then compared with the actual measurement, and the filter generates an optimal estimation of the true state. However, the standard Kalman filter assumes that the underlying system behaves in a certain way, and if the assumption is incorrect, the filter may not perform optimally. In such cases, we need to switch between multiple Kalman filters to estimate the system state accurately. This article discusses the switching Kalman filter and its variants.

# Switching Kalman Filter
A switching Kalman filter (SKF) is an extension of the standard Kalman filter that efficiently addresses the problem of switching between different models. The idea behind SKF is to use a set of different models that describe the different regimes of the system. In each regime, a different Kalman filter is used to estimate the system state.

Consider a system with `N` different regimes, and let `z_t` be a discrete random variable that takes values in `{1, 2, ..., N}` at time `t`, indicating which regime the system is currently in. Further, let `x_t` be the state of the system at time `t`, and `y_t` be the observation (measurement) of the system at time `t`. Assuming that the system transitions between regimes according to a Markov process, the state transition equation can be written as follows:

$$ x_t = A_{z_t} x_{t-1} + w_t $$

where `w_t` is a zero-mean Gaussian noise with covariance `Q_{z_t}`. The observation equation is given by:

$$ y_t = H_{z_t} x_t + v_t $$

where `v_t` is a zero-mean Gaussian noise with covariance `R_{z_t}`, and `A_i, H_i, Q_i, R_i` are the state model, observation model, process noise covariance, and measurement noise covariance, respectively, for regime `i`.

The SKF algorithm consists of two steps: (i) filtering, and (ii) mode estimation.

## Filtering with switching Kalman Filter
In the first step, we use a set of Kalman filters to filter the observations `y_t` and estimate the state `x_t` in each regime. Suppose we have `N` different Kalman filters, each corresponding to a different regime. For each regime `i`, the Kalman filter consists of the following equations:

**Prediction step:**

$$ \hat{x}_{t|t-1}^{(i)} = A_{i} \hat{x}_{t-1|t-1}^{(i)} $$

$$ P_{t|t-1}^{(i)} = A_{i} P_{t-1|t-1}^{(i)} A_{i}^T + Q_{i} $$

**Update step:**

$$ K_t^{(i)} = P_{t|t-1}^{(i)} H_{i}^T [H_{i} P_{t|t-1}^{(i)} H_{i}^T + R_{i}]^{-1} $$

$$ \hat{x}_{t|t}^{(i)} = \hat{x}_{t|t-1}^{(i)} + K_t^{(i)} (y_t - H_{i} \hat{x}_{t|t-1}^{(i)}) $$

$$ P_{t|t}^{(i)} = (I - K_t^{(i)} H_{i}) P_{t|t-1}^{(i)} $$

Here, `P_{t|t}^{(i)}` is the error covariance matrix of the Kalman filter for regime `i` at time `t`, `K_t^{(i)}` is the Kalman gain matrix, and `y_t` is the observation at time `t`.

## Mode Estimation
Once we have the estimated state `x_t` and error covariance matrix `P_{t|t}^{(i)}` for each regime, we need to estimate the mode `z_t` of the system, which tells us which regime the system is currently in. This is done using Bayesian model selection. We estimate the posterior probability of each model given the observations up to time `t`:

$$ P(z_t = i | y_{1:t}) = \frac{P(y_{1:t}|z_t=i)P(z_t=i)}{\sum_{j=1}^N P(y_{1:t}|z_t=j)P(z_t=j)} $$

where `P(z_t=i)` is the prior probability of regime `i`, and `P(y_{1:t}|z_t=i)` is the likelihood of the observations up to time `t` given that the system is in regime `i`. The prior probabilities can be set uniformly, i.e., `P(z_t=i) = 1/N`.

The likelihood can be computed using the Kalman filter prediction and update steps as follows:

$$ P(y_{1:t}|z_t=i) = \int P(y_t|x_t) P(x_t|x_{t-1}, z_t=i)dx_t $$

where `P(x_t|x_{t-1}, z_t=i)` is the state transition probability for regime `i`, and `P(y_t|x_t)` is the observation probability. These probabilities are given by the state model and observation model for each regime.

Once we have computed the posterior probabilities, the mode `z_t` can be estimated as:

$$ \hat{z}_t = \arg\max_{i=1}^N P(z_t=i|y_{1:t}) $$

# Variants of Switching Kalman Filter
The SKF algorithm described above assumes that the models for different regimes are known a priori. In practice, the models may not be known, or they may change over time. To address these issues, several variants of SKF have been proposed.

## Adaptive Switching Kalman Filter
The adaptive switching Kalman filter (ASKF) is a variant of SKF that adapts to changes in the system. It is based on the assumption that the parameters of the different regimes may change slowly over time. The ASKF estimates the parameters of each regime using a recursive least-squares algorithm and updates them periodically.

The state transition equation for the ASKF can be written as:

$$ x_t = A_{\theta_t} x_{t-1} + w_t $$

where `A_{\theta_t}` is the state model parameterized by a vector `theta_t`. The observation equation is the same as that for SKF.

The ASKF algorithm consists of the following steps:

1. Initialize the state `x_0` and the error covariance matrix `P_0`.
2. For each regime `i`, initialize the state model parameters `theta_i` using a set of prior values.
3. For each time step `t`, do the following:
    a. Using the current mode estimate `z_t`, compute the Kalman filter prediction and update as described above.
    b. Update the state model parameters for each regime using a recursive least-squares algorithm.
    c. Compute the posterior probabilities and estimate the mode `z_t` as described above.

The recursive least-squares algorithm updates the state model parameters `theta_t^{(i)}` as follows:

$$ \theta_t^{(i)} = \theta_{t-1}^{(i)} + K_t^{(i)}[y_t - H_i \hat{x}_{t|t-1}^{(i)}]x_{t-1}^T $$

where `K_t^{(i)}` is the Kalman gain matrix for regime `i`, and `x_{t-1}` is the state at time `t-1`. The error covariance of the parameter estimate is updated as follows:

$$ P_{\theta,t}^{(i)} = P_{\theta,t-1}^{(i)} - K_t^{(i)} [H_i P_{t|t-1}^{(i)} H_i^T + R_i] K_t^{(i)T} $$

The state model parameters can also be regularized to prevent overfitting.

## Particle Switching Kalman Filter
The particle filtering approach to the SKF is called the particle switching Kalman filter (PSKF). In the PSKF, we use a set of particle filters instead of Kalman filters to estimate the state in each regime. Particle filtering is a non-parametric approach to filtering that approximates the posterior distribution of the state using a set of weighted particles.

The PSKF algorithm consists of the following steps:

1. Initialize a set of `M` particles for each regime.
2. For each time step `t`, do the following:
    a. For each regime `i`, propagate the particles using the state transition equation and compute the weights based on the observation model.
    b. Resample the particles with replacement based on their weights, and compute the Kalman filter prediction and update for each regime.
    c. Compute the posterior probabilities and estimate the mode `z_t` as described above.

The PSKF has several advantages over the SKF. It can handle non-linear and non-Gaussian models and does not make any assumptions about the system dynamics. However, it is computationally expensive and requires a large number of particles to get accurate estimates.

# Implementation in Python
In this section, we provide an implementation of the SKF algorithm in Python using NumPy and SciPy. We assume that the state and observation models for each regime are known a priori.

```python
import numpy as np
from scipy.stats import multivariate_normal

class KalmanFilter:
    def __init__(self, A, H, Q, R, x0, P0):
        self.A = A
        self.H = H
        self.Q = Q
        self.R = R
        self.x = x0
        self.P = P0

    def predict(self):
        self.x = self.A @ self.x
        self.P = self.A @ self.P @ self.A.T + self.Q

    def update(self, y):
        K = self.P @ self.H.T @ np.linalg.inv(self.H @ self.P @ self.H.T + self.R)
        self.x = self.x + K @ (y - self.H @ self.x)
        self.P = (np.eye(self.x.shape[0]) - K @ self.H) @ self.P

class SwitchingKalmanFilter:
    def __init__(self, models, Pz0=None):
        self.models = models
        self.N = len(models)
        self.Pz = np.ones(self.N) / self.N if Pz0 is None else Pz0.copy()

    def predict(self):
        for model in self.models:
            model.predict()

    def update(self, y):
        for i in range(self.N):
            self.models[i].update(y)
        self.compute_posterior()

    def compute_posterior(self):
        likelihoods = np.zeros(self.N)
        for i in range(self.N):
            prob = multivariate_normal.pdf(self.models[i].x, cov=self.models[i].P, mean=self.models[i].x)
            likelihoods[i] = self.Pz[i] * prob
        self.Pz = likelihoods / likelihoods.sum()

    def get_state(self):
        x = np.zeros(self.models[0].x.shape)
        for i in range(self.N):
            x += self.Pz[i] * self.models[i].x
        return x

    def get_error_cov(self):
        P = np.zeros(self.models[0].P.shape)
        for i in range(self.N):
            d = self.models[i].x - self.get_state()
            P += self.Pz[i] * (self.models[i].P + d @ d.T)
        return P

if __name__ == '__main__':
    A1 = np.array([[0.9, 0], [0, 0.9]])
    H1 = np.array([[1, 0], [0, 1]])
    Q1 = np.array([[0.1, 0], [0, 0.1]])
    R1 = np.array([[1, 0], [0, 1]])
    x01 = np.array([0, 0])
    P01 = np.eye(2)

    A2 = np.array([[-0.9, 0], [0, -0.9]])
    H2 = np.array([[1, 0], [0, 1]])
    Q2 = np.array([[0.1, 0], [0, 0.1]])
    R2 = np.array([[1, 0], [0, 1]])
    x02 = np.array([5, 5])
    P02 = np.eye(2)

    models = [
        KalmanFilter(A1, H1, Q1, R1, x01, P01),
        KalmanFilter(A2, H2, Q2, R2, x02, P02)
    ]

    skf = SwitchingKalmanFilter(models)
    y = np.random.multivariate_normal(np.zeros(2), R1, 100)

    for obs in y:
        skf.predict()
        skf.update(obs)

    print(skf.get_state())
    print(skf.get_error_cov())
```

This is a simple example of SKF with two regimes, where the state model and observation model for each regime are the same. We define the `KalmanFilter` class to represent the Kalman filter for each regime and the `SwitchingKalmanFilter` class to represent the SKF. The functions `predict` and `update` implement the Kalman filter prediction and update steps, and `compute_posterior` computes the posterior probabilities of each regime.

In the `main` function, we define two regimes with different state models and observation models, and we use SKF to estimate the system state based on noisy measurements. We generate the measurements using a Gaussian distribution with mean `0` and covariance `R1`. Finally, we print the estimated state and error covariance.
---
layout: post
title: "Weiner Filtering and its Variants"
description: "An overview of Weiner Filtering and its variations with Python implementation and examples."
summary: "This article explains the concept of Weiner Filtering and its variants in signal processing, accompanied by Python implementation and examples."
author: Pavan Donthireddy
usemathjax: true
original: new
tags: [noise, filters] 
---

# Introduction

In signal processing, noise reduction is a crucial aspect, especially when the signal carries the relevant information. Weiner Filtering is one of the most widely used techniques to reduce noise in the signal processing domain. This technique estimates the original signal from the corrupted or noisy signal using an optimal linear filter. Weiner Filtering is useful when the underlying signal is corrupted with additive random noise. 

# Weiner Filter

Weiner Filtering is based on the observation that the corrupted signal can be expressed as the sum of the original signal and the noise signal. This can be represented mathematically as:
$$y(n) = x(n) + v(n)$$

Where y(n) is the corrupted signal, x(n) is the original signal, and v(n) is the noise.

The goal of Weiner Filtering is to estimate the original signal x(n) from y(n). To do this, we can estimate x(n) using the following equation:

$$\hat{x}(n) = \sum_{m = -\infty}^{+\infty} h(m)y(n - m)$$

Where **h(m)** is the filter coefficients, and $\hat{x}(n)$ is the estimated value of **x(n)**.

The primary goal in Weiner Filtering is to find the optimal filter coefficients **h(m)** that minimize the mean-square error between the original signal **x(n)** and estimated signal $\hat{x}(n)$.

The optimal filter coefficients **h(m)** can be obtained by minimizing the mean-square error between the original signal **x(n)** and the estimated signal $\hat{x}(n)$ using the Wiener-Hopf equation:

$$R_{xx}(k)h(k) = R_{xy}(k)$$

Where **R<sub>xx</sub>(k)** is the auto-correlation sequence of x(n), **R<sub>xy</sub>(k)** is the cross-correlation sequence between x(n) and y(n), and h(k) is the filter coefficient at k-th position.

Once we obtain the optimal filter coefficients **h(m)** from the **Wiener-Hopf equation**, we can use these coefficients to estimate the original signal **x(n)**.

## Python Implementation

``` python
from scipy.signal import lfilter, correlate
from scipy.io import wavfile
import numpy as np

def wiener_filter(y, noise, SNR):
    '''
    y: Noisy input signal
    noise: Noise signal to be removed
    SNR: Signal to noise ratio

    Returns:
    The processed signal
    '''
    # Compute the power of noisy and noise signals
    noise_power = np.mean(noise**2)
    signal_power = np.mean(y**2)

    # Compute noise-to-signal ratio
    snr = signal_power / noise_power

    # Compute filter coefficients using Wiener-Hopf equation
    h = correlate(y, noise, mode='same') / np.sum(noise**2)
    y_filtered = lfilter(h, 1, y)

    return y_filtered
```

# Variations of Weiner Filter

## Minimum Mean-Square Error (MMSE) Weiner Filter

The Minimum Mean-Square Error (MMSE) Weiner Filter is an extension of the conventional Weiner Filter. In the conventional Weiner Filter, we aim to minimize the mean-square error between the original signal and the estimated signal. In contrast, MMSE Weiner filter aims to minimize the mean-square error between the original signal and the estimated signal, considering the distortion introduced by the filter.

The MMSE filter optimizes the filter coefficients to reduce both noise and distortion. The MMSE filter accounts for both the noise and the signal's statistics, and it tries to minimize the error with respect to the noisy signal.

The formula for computing the MMSE filter coefficients is given below:

$$h_{MMSE} = \frac{R_{xx}^{-1}(R_{xx} + R_{vv})}{R_{xx}^{-1}}$$

where **R<sub>xx</sub>** is the auto-correlation matrix of the input signal, and **R<sub>vv</sub>** is the auto-correlation matrix of the noise signal.

## Least Mean-Square (LMS) Weiner Filter

The Least Mean-Square (LMS) Weiner Filter is a variant of the Weiner filter that is used when there is a limited amount of data or a non-stationary signal. The LMS filter uses a gradient descent algorithm to iteratively compute the filter coefficients.

Unlike the Weiner filter, the LMS filter does not require the input signal's auto-correlation matrix. Instead, it updates the filter coefficients based on the difference between the noisy input signal and the estimated signal.

The formula to update the filter coefficients is given by:

$$h(n+1)=h(n)+2\mu e(n)y(n)$$

Where h(n+1) is the updated filter coefficients, $\mu$ is the step size, e(n) is the error signal, and y(n) is the filtered output.

## Python Implementation

``` python
def mmse_filter(y, noise):
    '''
    y: Noisy input signal
    noise: Noise signal to be removed

    Returns:
    The processed signal
    '''
    # Compute the power of the signal and noise
    noise_power = np.mean(noise**2)
    signal_power = np.mean(y**2)

    # Estimate the auto-correlation matrices
    Rx = correlate(y, y, mode='same') / len(y)
    Rv = correlate(noise, noise, mode='same') / len(noise)

    # Compute the MMSE Wiener Filter coefficients
    h = np.dot(np.linalg.inv(Rx + Rv), Rx)

    y_filtered = lfilter(h, 1, y)

    return y_filtered

def lms_filter(y, noise, n_taps=50, step_size=0.05, n_iterations=1000):
    '''
    y: Noisy input signal
    noise: Noise signal to be removed
    n_taps: Number of filter coefficients
    step_size: Learning rate or step size
    n_iterations: Number of iterations

    Returns:
    The processed signal
    '''
  
    h = np.zeros(n_taps)
    for i in range(n_iterations):
        # Compute the current filter output
        y_filtered = np.convolve(h, y, mode='same')

        # Compute the error signal
        e = noise - y_filtered

        # Update filter coefficients
        h = h + 2 * step_size * np.convolve(e, y, mode='same')
    
    y_filtered = np.convolve(h, y, mode='same')
    
    return y_filtered
```

# Conclusion

Weiner Filtering is an optimal linear filtering technique that is widely used in the signal processing domain. It estimates the original signal from the corrupted or noisy signal by finding the optimal filter coefficients that minimize the mean-square error between the original signal and estimated signal. 

In this article, we discussed the conventional Weiner filter, its variations such as MMSE Weiner filter and LMS filter, and provided Python implementations for each. We hope this article helps you gain a basic understanding of Weiner Filtering and its variations.
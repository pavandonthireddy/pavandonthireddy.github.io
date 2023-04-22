---
layout: post
title: Matched Filters and their Variants
description: Understanding the working of Matched Filters and the different variants used for signal processing.
summary: This article discusses Matched Filters and their variants used for signal processing, including the working of Matched Filters, Matched Filter Banks, and Matched Subspace Filters.
author: Pavan Donthireddy
usemathjax: true
original: new
tags: [ filters , signal_detection ]
---

## Introduction

Matched Filters are a popular tool used for signal processing, primarily for detecting and extracting signals from noisy data. This article discusses the working of matched filters and their different variants. The variants covered in this article are Matched Filter Banks and Matched Subspace Filters.

## Matched Filters

Matched Filters are linear filters used for signal detection and extraction, where the filter output is maximized when the input signal matches a predefined template. The matched filter's advantage is that it maximizes the signal-to-noise ratio for the target signal while suppressing other noise sources.

Mathematically, a matched filter $h(t)$ for a signal $s(t)$ with energy $E_s$, is given as:

$$h(t) = \frac{s(T-t)}{E_s}$$

where T is the duration of the signal. The matched filter output $y(t)$ is the convolution of the input signal $x(t)$ with the matched filter $h(t)$:

$$y(t) = x(t) * h(t) = \int_{-\infty}^{\infty} x(\tau)h(t-\tau)d\tau$$

The output of the matched filter is proportional to the cross-correlation between the input signal and the template signal $s(t)$ shifted by a time lag $t$. Thus, the matched filter maximizes the detection probability of the target signal in the presence of noise.

The matched filter can be implemented using classical convolution, Fourier transform or digital filters. In digital implementation, input samples $x[n]$ are convolved with the matched filter impulse response $h[n]$:

$$y[n] = \sum_{k=0}^{N-1}x[n-k]h[k]$$

where $N$ is the length of the matched filter impulse response.

## Matched Filter Banks

Matched Filter Banks are used when there are multiple target signals at different frequencies or pulse durations. Instead of using a single matched filter for detecting all target signals, a bank of matched filters is used. Each filter in the bank is designed to detect a specific pulse duration or frequency.

A Matched Filter Bank for signals $\{s_1(t), s_2(t), \dots, s_N(t)\}$ is given as:

$$H(f) = \sum_{i=1}^{N}\frac{\bar{S_i(f)}}{E_{S_i}}S_i(f)$$

where $S_i(f)$ is the Fourier transform of $s_i(t)$ and $E_{S_i}$ is the energy of $s_i(t)$. The output of the Matched Filter Bank for an input signal $x(t)$ is given as:

$$Y(f) = X(f)H(f)$$

where $X(f)$ is the Fourier transform of $x(t)$.

In the digital domain, the matched filter bank is implemented using a filter bank consisting of multiple matched filters, with each filter covering a specific frequency band.

## Matched Subspace Filters

Matched Subspace Filters are used when the number of signal sources is unknown, and the signals are correlated. In such cases, a subspace containing the signals can be formed, and a matched filter is designed for extracting the signals from the subspace.

The input signal matrix $X$ can be represented as a sum of a subspace matrix $S$ containing the target signals and a noise matrix $N$:

$$X = S + N$$

The subspace matrix $S$ can be factorized using Singular Value Decomposition (SVD) as:

$$S = U\sum V^T$$

where $U$ and $V$ are unitary matrices, and $\sum$ is a diagonal matrix containing the singular values of $S$. A matched filter $h$ can be designed using the subspace matrix $S$ as:

$$h = \frac{\sum V^T}{\|\sum V^T\|}$$

The output of the matched filter bank is given as:

$$y(t) = h^Tx(t)$$

In Python, a matched filter can be easily implemented using the `scipy.signal` library. The `scipy.signal.correlate` function can be used to implement the matched filter, as shown below:

```python
import numpy as np
from scipy.signal import correlate

# Define the signal and template
signal = np.random.randn(100)
template = np.random.randn(10)

# Implement the matched filter
output = correlate(signal, template, mode='valid')

# Plot the output signal
import matplotlib.pyplot as plt
plt.plot(output)
plt.show()
```

## Conclusion

Matched Filters are a powerful tool used for signal detection and extraction in noisy data. Matched Filter Banks and Matched Subspace Filters are variants of the matched filter used for detecting multiple signals at different frequencies and extracting signals from a correlated subspace, respectively. In this article, we discussed the working of Matched Filters and their variants along with their mathematical formulations and Python implementations.
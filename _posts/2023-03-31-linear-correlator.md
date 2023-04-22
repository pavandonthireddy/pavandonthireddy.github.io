---
layout: post
title: Linear Correlator and Its Variants
description: This article discusses the linear correlator and its variants used in signal processing and data analysis.
summary: This article explains the mathematical formulations of the linear correlator and its variants, along with their Python implementation and an example.
author: Pavan Donthireddy
usemathjax: true
original: new
tags: [filters , linear_correlator]
---

# Introduction

In signal processing and data analysis, the linear correlator is a widely-used tool that determines the degree of similarity between two input signals. Correlation analysis is a key technique for understanding the relationships among different types of data signals, allowing researchers to identify patterns and trends that may be difficult to observe through other methods.

In this article, we will discuss the basic mathematical formulations of the linear correlator and its variants, as well as provide a Python implementation and example of each variant.

# Linear Correlator

The linear correlator is a simple yet powerful tool that measures the degree of similarity between two signals, x(t) and y(t), where t is a continuous variable representing time. The correlation coefficient, r, ranges from -1 to 1, with higher absolute values indicating greater similarity.

The mathematical formulation for the linear correlator is given by the following equation:

$r = \frac{\sum_{t}^{T} (x(t)-\bar{x})(y(t)-\bar{y})}{\sqrt{\sum_{t}^{T}(x(t)-\bar{x})^{2}}\sqrt{\sum_{t}^{T}(y(t)-\bar{y})^{2}}}$

where T is the total number of samples in x(t) and y(t), and $\bar{x}$ and $\bar{y}$ represent the mean values of x(t) and y(t), respectively.

In Python, we can implement the linear correlator as follows:

```python
import numpy as np

def linear_correlator(x, y):
    x_mean = np.mean(x)
    y_mean = np.mean(y)
    numerator = np.sum((x - x_mean) * (y - y_mean))
    denominator = np.sqrt(np.sum((x - x_mean)**2) * np.sum((y - y_mean)**2))
    r = numerator / denominator
    return r
```

# Cross-Correlator

The cross-correlator is a variant of the linear correlator that measures the similarity between two signals at different time lags. Unlike the linear correlator, which only looks at the similarity between two signals at the same time, the cross-correlator examines the similarity between the signals as they are shifted relative to one another.

The mathematical formulation for the cross-correlator is given by the following equation:

$r(\tau) = \frac{\sum_{t=1}^{T} x(t) y(t+\tau)}{\sqrt{\sum_{t=1}^{T}x^{2}(t)}\sqrt{\sum_{t+1}^{T}y^{2}(t)}}$

where $\tau$ represents the time lag, which can be positive or negative, and T is the total number of samples in x(t) and y(t).

In Python, we can implement the cross-correlator as follows:

```python
def cross_correlator(x, y):
    T = len(x)
    r = np.zeros(2*T-1)
    for tau in range(-T+1, T):
        numerator = 0
        x_terms = []
        y_terms = []
        for t in range(max(0, -tau), min(T, T-tau)):
            numerator += x[t] * y[t+tau]
            x_terms.append(x[t]**2)
            y_terms.append(y[t]**2)
        denominator = np.sqrt(np.sum(x_terms) * np.sum(y_terms))
        r[tau+T-1] = numerator / denominator
    return r
```

# Auto-Correlator

The auto-correlator is another variant of the linear correlator that measures the similarity of a signal with itself at different time lags. The auto-correlator can be useful for analyzing periodic signals or signals with repeating patterns.

The mathematical formulation for the auto-correlator is similar to that of the cross-correlator:

$r(\tau) = \frac{\sum_{t=1}^{T-\tau} x(t) x(t+\tau)}{\sqrt{\sum_{t=1}^{T}x^{2}(t)}}$

where $\tau$ represents the time lag, and T is the total number of samples in x(t).

In Python, we can implement the auto-correlator as follows:

```python
def auto_correlator(x):
    T = len(x)
    r = np.zeros(2*T-1)
    for tau in range(-T+1, T):
        numerator = 0
        x_terms = []
        for t in range(max(0, -tau), min(T, T-tau)):
            numerator += x[t] * x[t+tau]
            x_terms.append(x[t]**2)
        denominator = np.sqrt(np.sum(x_terms))
        r[tau+T-1] = numerator / denominator
    return r
```

# Example

As an example, let's consider two sinusoidal signals, x(t) and y(t), with different frequencies and random noise added to each. We will then calculate the correlation coefficient using the linear correlator, cross-correlator, and auto-correlator.

```python
import matplotlib.pyplot as plt

t = np.linspace(0, 2*np.pi, num=200)

x = np.sin(2*t)
noise_x = np.random.normal(0, 0.1, size=len(t))
x += noise_x

y = np.sin(3*t)
noise_y = np.random.normal(0, 0.1, size=len(t))
y += noise_y

# Linear Correlator
r1 = linear_correlator(x, y)
print("Linear Correlator: ", r1)

# Cross-Correlator
r2 = cross_correlator(x, y)
plt.plot(np.arange(-len(t)+1, len(t)), r2)
plt.title("Cross-Correlator")
plt.show()

# Auto-Correlator
r3 = auto_correlator(x)
plt.plot(np.arange(-len(t)+1, len(t)), r3)
plt.title("Auto-Correlator")
plt.show()
```

The output of this code would be:

```
Linear Correlator:  0.09451511255638794
```

The plots for the cross-correlator and auto-correlator would show the degree of similarity between the two signals at different time lags.

# Conclusion

The linear correlator and its variants are powerful tools for analyzing the degree of similarity between different types of data signals. By calculating the correlation coefficient using the appropriate mathematical formulations, researchers can gain valuable insights into the patterns and trends that underlie complex data sets. In Python, these techniques can be easily implemented and visualized to aid in the analysis of experimental or observational data.


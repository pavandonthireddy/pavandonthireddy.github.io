---
layout: post
title: Local Mean Decomposition
description: Local Mean Decomposition
summary: Local Mean Decomposition
author: Pavan Donthireddy
mathjax: true
original: new
tags: [signal_extraction] 
---



# Introduction to Local Mean Decomposition (LMD)

Local Mean Decomposition (LMD) is a signal decomposition algorithm used to filter out noise and extract meaningful information from signals. The main idea behind LMD is to decompose a signal into its local means, which can be used to identify the underlying components of the signal. LMD is used in a variety of applications, such as speech recognition, medical imaging, and signal processing. 

# Mathematical Formulation

The mathematical formulation of the LMD algorithm is defined as follows:

Given a signal $x(t)$, the local mean $m(t)$ at a given point $t$ is computed as follows:

$$m(t) = \frac{1}{N}\sum_{i=t-N}^{t+N} x(i)$$

where $N$ is the size of the local window.

The local mean residual is then computed as: 

$$r(t) = x(t) - m(t)$$

The LMD algorithm then recursively applies this process to the residuals, producing local means and residuals at each step: 

$$x_k(t) = r_{k-1}(t) - m_k(t)$$

where $k$ is the iteration step.

# Python Implementation 

The following is a Python implementation of the LMD algorithm:

```python
def lmd(x, N):
    # compute the local mean
    m = np.convolve(x, np.ones(N), 'same')/N
    
    # compute the local mean residual
    r = x - m
    
    # iteratively decompose the signal
    x_k = r
    for k in range(1, K):
        # compute the local mean
        m_k = np.convolve(x_k, np.ones(N), 'same')/N
        
        # compute the local mean residual
        r_k = x_k - m_k
        
        # update the signal for the next iteration
        x_k = r_k
    
    return m, r, x_k
```

# Example

Let's consider a signal consisting of a sinusoid and some noise:

```python
# generate the signal
t = np.arange(0, 10, 0.01)
x = np.sin(2*np.pi*t) + np.random.normal(0, 0.2, t.shape)
```

We can then apply the LMD algorithm to decompose the signal into its local means and residuals:

```python
# apply the lmd algorithm
N = 5
K = 3
m, r, x_k = lmd(x, N)
```


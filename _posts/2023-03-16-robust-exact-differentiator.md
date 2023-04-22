---
layout: post
title: Robust Exact Differentiator
description: Robust Exact Differentiator
summary: Robust Exact Differentiator
author:
- Pavan Donthireddy
usemathjax: true
tags: [numerical_differentiaton, trend_estimation, differentiator, loss_function]
original: new
---

A robust exact differentiator is a type of differentiation algorithm that provides an exact estimate of the derivative of a signal, while being robust to noise and outliers in the signal.

The basic idea behind a robust exact differentiator is to estimate the derivative of a signal by fitting a polynomial curve to the signal, and then differentiating the polynomial function. The order of the polynomial is chosen to match the degree of smoothness of the signal. For example, if the signal is a smooth curve, a low-order polynomial (such as a quadratic or cubic polynomial) may be used. If the signal has sharp edges or corners, a higher-order polynomial may be used.

The robustness of the algorithm comes from the use of a robust regression technique to fit the polynomial curve to the signal. Unlike ordinary least squares regression, which is sensitive to outliers, robust regression techniques are designed to downweight the influence of outliers on the fitting process, thus producing more accurate estimates of the underlying curve.

Examples of robust regression techniques that can be used for robust exact differentiation include the Huber loss function, the Tukey loss function, and the least trimmed squares method.

Overall, the robust exact differentiator is a powerful tool for accurately estimating the derivative of a signal in the presence of noise and outliers. However, it is computationally more expensive than some other differentiation techniques and requires careful selection of the polynomial order and regression technique to match the properties of the signal being analyzed.

## Mathematical Description:

Let `x` be the input signal, and `t` be the time vector corresponding to `x`. We wish to estimate the first derivative of `x` at each time point. We can do this by fitting a polynomial curve to `x` and then differentiating the polynomial function.

The general approach for a robust exact differentiator is as follows:

1. Choose a polynomial order `n` based on the degree of smoothness of the signal. A low-order polynomial (e.g., quadratic or cubic) may be appropriate for a smooth signal, while a higher-order polynomial may be needed for a signal with sharp edges or corners.
2. Use a robust regression technique (e.g., Huber loss, Tukey loss, least trimmed squares) to fit the polynomial curve to the signal.
3. Differentiate the polynomial function to obtain the estimated derivative of `x`.

Here is some example Python code that implements a robust exact differentiator using the Huber loss function:

```python
import numpy as np
from scipy.signal import savgol_filter
from scipy.interpolate import CubicSpline

def robust_differentiator(x, t, n, alpha):
    # Apply Savitzky-Golay filter to smooth the signal
    x_filtered = savgol_filter(x, 2*n+1, n)
    
    # Fit a polynomial to the filtered signal using the Huber loss function
    poly_coeffs = np.polynomial.polynomial.polyfit(t, x_filtered, n)
    poly_func = np.polynomial.polynomial.Polynomial(poly_coeffs)
    residual = x_filtered - poly_func(t)
    w = np.sqrt(np.maximum(1 - (residual/alpha)**2, 0))
    robust_poly_coeffs = np.polynomial.polynomial.polyfit(t, x_filtered, n, w=w)
    
    # Differentiate the polynomial to obtain the estimated derivative
    poly_deriv = np.polynomial.polynomial.Polynomial(robust_poly_coeffs).deriv()
    x_deriv = poly_deriv(t)
    
    # Interpolate the derivative to the original time points
    cs = CubicSpline(t, x_deriv)
    x_deriv_interp = cs(t)
    
    return x_deriv_interp
    ```



---
layout: post
title: Adaptive Wavelet Shrinkage Method and Its Variants
description: This article discusses the concept of the Adaptive Wavelet Shrinkage Method (AWSM) and its variants used in signal processing.
summary: The Adaptive Wavelet Shrinkage Method (AWSM) is a signal processing technique used to denoise and compress signals efficiently, without losing important features of the signal. This article explains the concept of AWSM and its variants.
author: Pavan Donthireddy
usemathjax: true
original: new
tags: [ wavelet , wavelet_thresholding , noise ]
---

# Adaptive Wavelet Shrinkage Method and Its Variants

The Adaptive Wavelet Shrinkage Method (AWSM) is a signal processing technique used to denoise and compress signals efficiently, without losing important features of the signal. In many signal processing applications, noise can be a major issue which affects the accuracy of the signal. The AWSM provides a solution to this issue by removing noise from the signal while preserving the important features.

The concept of AWSM was first introduced by Donoho and Johnstone in 1994 [1]. Since then, it has been widely used in various areas of signal processing such as data compression, image processing, speech processing, and many more.

## Wavelet Transform

The Wavelet Transform is a mathematical tool used to decompose a signal into wavelets. It is a time-frequency analysis technique that provides a multi-resolution analysis of the signal. The wavelet transform can be represented as:

$$
W(a,b) = \int x(t)\Psi_{a,b}(t)dt
$$
where, 

- $x(t)$ - Input signal
- $\Psi _{a,b}(t)$ - Wavelet function with scale $a$ and translation $b$.

The wavelet transform represents the signal $x(t)$ in terms of wavelets at different scales and positions. The wavelets form a set of basis functions that can capture the local features of the signal.

## Thresholding

Thresholding is a process where the coefficients of the wavelet transform are shrunk or thresholded. The thresholding process is done based on a threshold value, which determines which coefficients are retained and which are discarded.

## Hard Thresholding

Hard Thresholding is a thresholding technique where the coefficients below a certain threshold value are set to zero, and the coefficients above the threshold value are retained.

The hard thresholding operator $H_T$ can be represented as:

$$
y(t) = H_T[x(t)] = \sum_{j=1}^k x_j \Phi_j(t) + \sum_{j=k+1}^n \delta_j \Psi_j(t)
$$
where, 

- $k$ - The largest integer such that $|x_j|>T$
- $x_j$ - Wavelet coefficients
- $\Phi_j(t)$ - Scaling function
- $\Psi_j(t)$ - Wavelet function
- $\delta_j$ - The sign of $x_j$

## Soft Thresholding

Soft thresholding is a thresholding technique where the coefficients below a certain threshold value are set to zero, and the coefficients above the threshold value are shrunk towards zero.

The soft thresholding operator $S_T$ can be represented as:

$$
y(t) = S_T[x(t)] = \text{sign}(x)(|x| - T)_{+}
$$
where, 

- $|x|$ - Magnitude of the wavelet coefficients
- $\text{sign}(x)$ - Sign of the wavelet coefficients
- $T$ - Threshold value

## Adaptive Wavelet Shrinkage Method (AWSM)

The AWSM is a thresholding technique where the threshold value is adaptively determined. The threshold value is determined based on the statistics of the wavelet coefficients.

The AWSM has three main steps:

1. Decompose the signal using the wavelet transform
2. Estimate the noise level from the wavelet coefficients
3. Threshold the wavelet coefficients based on the estimated noise level.

### Estimation of Noise Level

The estimation of noise level is an important step in the AWSM. The noise level is estimated using the Median Absolute Deviation (MAD) of the wavelet coefficients. The MAD is a robust estimator of the noise level, which is less sensitive to outliers.

The MAD can be represented as:

$$
{\rm MAD} = {\rm median}(|x_i - {\rm median}(x_i)|)
$$
where, 

- $x_i$ - Wavelet coefficients

The noise level is estimated by multiplying the MAD with a scaling factor $1.4826$.

$$
\sigma = 1.4826 \times {\rm MAD}(x_i)
$$

### Thresholding the Coefficients

After estimating the noise level, the wavelet coefficients are thresholded using the soft thresholding operator. The threshold value is determined based on the noise level and a user-defined thresholding parameter $c$.

$$
T = c \times \sigma
$$

Where,

- $c$ - User-defined thresholding parameter
- $\sigma$ - Estimated noise level

The soft thresholding operator is applied to the wavelet coefficients to obtain the denoised signal.

$$
y(t) = S_T[x(t)]
$$

### Python Implementation

Here is an example implementation of AWSM in Python using the PyWavelets library:

```python
import numpy as np
import pywt

def awsm(signal, wavelet='db4', c=3.0):

    # Perform wavelet decomposition
    coeffs = pywt.wavedec(signal, wavelet)

    # Estimate noise level
    sigma = np.median(np.abs(coeffs[-1])) / 0.6745

    # Threshold the coefficients
    coeffs[1:] = [pywt.threshold(i, value=c*sigma, mode='soft') for i in coeffs[1:]]

    # Reconstruct the denoised signal
    denoised = pywt.waverec(coeffs, wavelet)

    return denoised
```

### Variants of AWSM

There are several variants of AWSM, which have been developed for specific signal processing applications. Some of the popular variants are:

- Bayesian Adaptive Wavelet Shrinkage (BAWS)
- Dual-Tree Complex Wavelet Transform (DT-CWT)
- Undecimated Wavelet Transform (UWT)

These variants have been developed to improve the performance of AWSM in specific signal processing applications.

## Conclusion

The Adaptive Wavelet Shrinkage Method (AWSM) is a powerful signal processing technique used to denoise and compress signals efficiently. The AWSM provides a solution to the issue of noise in the signal, while preserving the important features. Its variants, such as BAWS, DT-CWT, and UWT, have been developed to improve its performance in specific signal processing applications. The implementation of AWSM in Python is straightforward and can be easily integrated into any signal processing pipeline. 

## References

1. Donoho, D.L., & Johnstone, I.M. (1994). Ideal spatial adaptation by wavelet shrinkage. Biometrika 81(3), 425-455.
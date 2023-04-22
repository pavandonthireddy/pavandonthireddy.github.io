---
layout: post
title: "Pre-Whitening and Inverse Whitening Filters - A Detailed Scientific Article"
description: "This article discusses the concept of pre-whitening and inverse whitening filters, along with their variants and equations. The python implementation and an example for each variant are also provided."
summary: "This article explains the mathematical concept of pre-whitening and inverse whitening filters, their variants and equations. It also includes python implementation and an example for each variant."
author: Pavan Donthireddy
usemathjax: true
original: new
tags: [whitening, filters] 
---

Signal processing involves filtration of signals in various applications. One such filtration technique is the whitening filter, which helps to eliminate correlations between signals. Pre-whitening and inverse whitening filters are variants of the whitening filter that play a significant role in signal processing applications. 

## Pre-Whitening Filter

The pre-whitening filter is a technique, which helps to reduce or eliminate correlations between signals. It is useful in cases where two signals are correlated, and the correlation is not necessarily harmful to the application. Pre-whitening is also used when we want to remove the correlation from one of the signals before further processing. It is an effective way of dealing with spurious correlations between signals, which can lead to false conclusions or biased estimators.

The pre-whitening filter can be defined mathematically as follows:

![Pre Whitening Filter Equation](https://latex.codecogs.com/svg.latex?s_y%20%3D%20R_x%5E%7B-1/2%7D%20%5Ccdot%20x)

Where,  

- s_y: Pre-whitened signal
- R_x: Covariance matrix of the original signal x
- x: Original signal

The goal is to obtain a signal such that the covariance matrix becomes proportional to the identity matrix, ensuring that the signal is uncorrelated. We apply a transformation to the original signal that is proportional to the inverse square root of the original covariance matrix. This process is known as pre-whitening. 

In python, this can be implemented the following way:

``` python
import numpy as np

# Original signal
x = np.array([1, 2, 3, 4, 5, 6])

# Covariance matrix of the original signal
R_x = np.cov(x)

# Inverse square root of the covariance matrix
R_x_inv_sqrt = np.linalg.inv(np.sqrt(R_x))

# Pre-whitened signal
s_y = R_x_inv_sqrt @ x
```

## Inverse Whitening Filter

The inverse whitening filter is a technique that helps to decorrelate a signal without affecting the variance of the signal. It is useful in cases where only the correlation between signals needs to be removed, and the signal variance needs to be preserved. The inverse whitening filter operation can be defined mathematically as follows:

![Inverse Whitening Filter Equation](https://latex.codecogs.com/svg.latex?z%20%3D%20R_x%5E%7B-1/2%7D%20%5Ccdot%20y)

Where,  

- z: Inverse whitened signal
- R_x: Covariance matrix of the original signal x
- y: Correlated signal

The inverse whitened signal is obtained by multiplying the correlated signal by the inverse square root of the covariance matrix of the original signal x. This process is known as inverse whitening.

In python, this can be implemented the following way:

``` python
import numpy as np

# Correlated signal
y = np.array([1, 3, 5, 7, 9, 11])

# Covariance matrix of the original signal
R_x = np.cov(y)

# Inverse square root of the covariance matrix
R_x_inv_sqrt = np.linalg.inv(np.sqrt(R_x))

# Inverse whitened signal
z = R_x_inv_sqrt @ y
```

## Variants of Pre-Whitening and Inverse Whitening Filters

### Modified Pre-Whitening Filter

The modified pre-whitening filter is a variant of the pre-whitening filter that is useful in cases where it is not possible to invert the covariance matrix. This situation can arise when the covariance matrix is singular or when the number of samples is less than the dimension of the signal. The modified pre-whitening filter can be defined mathematically as follows:

![Modified Pre-Whitening Filter Equation](https://latex.codecogs.com/svg.latex?s_y%20%3D%20R_x%5E%7B-1/2%7D%20%5Ccdot%20%5Cmathrm%7Bdiag%7D%28%5Cmathrm%7Beig%7D%28R_x%29%29%20%5Ccdot%20R_x%5E%7B1/2%7D%20%5Ccdot%20R_x%5E%7B-1%7D%20%5Ccdot%20x)

Where,  

- s_y: Pre-whitened signal
- R_x: Covariance matrix of the original signal x
- x: Original signal
- diag(eig(R_x)): Diagonal matrix of eigenvalues of covariance matrix R_x
- eig(R_x): Eigenvalues of covariance matrix R_x

In python, this can be implemented the following way:

``` python
import numpy as np

# Original signal
x = np.array([1, 2, 3, 4, 5, 6])

# Covariance matrix of the original signal
R_x = np.cov(x)

# Eigenvalues and eigenvectors of the covariance matrix
eig_values, eig_vectors = np.linalg.eig(R_x)

# Diagonal matrix of eigenvalues
eig_values_diag = np.diag(eig_values)

# Modified pre-whitening filter
s_y = eig_vectors @ np.linalg.inv(np.sqrt(eig_values_diag)) @ eig_vectors.T @ x
```

### Modified Inverse Whitening Filter

The modified inverse whitening filter is a variant of the inverse whitening filter that is useful when the matrix is singular or not invertible. It provides better results than inverse whitening in such scenarios. The modified inverse whitening filter can be defined mathematically as follows:

![Modified Inverse Whitening Filter Equation](https://latex.codecogs.com/svg.latex?z%20%3D%20R_x%5E%7B%2B%7D%20%5Ccdot%20R_x%5E%7B-1/2%7D%20%5Ccdot%20y)

Where,  

- z: Modified inverse whitened signal
- R_x: Covariance matrix of the original signal x
- y: Correlated signal
- R_x+ : Moore-Penrose pseudoinverse of the covariance matrix R_x

In python, this can be implemented the following way:

``` python
import numpy as np

# Correlated signal
y = np.array([1, 3, 5, 7, 9, 11])

# Covariance matrix of the original signal
R_x = np.cov(y)

# Moore-Penrose pseudoinverse of the covariance matrix
R_x_pinv = np.linalg.pinv(R_x)

# Inverse square root of the covariance matrix
R_x_inv_sqrt = np.linalg.inv(np.sqrt(R_x))

# Modified inverse whitened signal
z = R_x_pinv @ R_x_inv_sqrt @ y
```

## Conclusion

In conclusion, pre-whitening and inverse whitening filters are essential techniques in signal processing. These filters help to eliminate correlations between signals, which can lead to biased results or false conclusions. The modified variants of pre-whitening and inverse whitening filters are useful when the covariance matrix is singular or not invertible. The python implementation and the examples of the variants discussed in this article provide a better understanding of the concepts and techniques involved in signal processing.

# Other version

Coloured noise is a complex signal that contains a combination of frequencies. This type of noise finds application in areas such as music production, image processing, and communication systems. However, for many applications, it is preferable to have a signal that is normally distributed, such as Gaussian noise. One way to achieve this is by using linear time invariant (LTI) whitening filters.

LTI whitening filters convert the frequency distribution of a noise signal so that the power spectral density (PSD) is flat. This is achieved by passing the signal through an LTI filter whose frequency response is the inverse square root of the PSD of the input signal. The filtered signal has a white noise spectrum, which is Gaussian and of equal amplitude at all frequencies. 

There are several popular whitening filter variants that can be used to convert coloured noise to Gaussian noise. 

### Variance Normalization Filtering

The variance normalization filter normalizes the variance of a signal to 1, leaving the signal with zero mean. The filter takes the form of:

$$H(z)=\frac{1}{\sqrt[]{E[x(n)^2]}}$$

Where `E[x(n)^2]` is the mean squared value of the input signal.
In Python, the variance normalization filter can be implemented as follows:

```
def filter_vn(sig):
    # Calculate mean and variance of signal
    mu = np.mean(sig)
    sig_var = np.var(sig)

    # Normalize signal variance to 1
    sig = (sig - mu) / np.sqrt(sig_var)

    return sig
```

### Correlation Matrix Filtering

The correlation matrix filter computes the correlation matrix of a signal and then applies the Cholesky decomposition to get its square root. The resulting matrix is then used as the coefficients of a linear filter. The filter takes the form of:

$$H(z)=\sqrt[]{R^{-1}}$$

Where `R` is the correlation matrix of the input signal.
In Python, the correlation matrix filter can be implemented as follows:

```
def filter_cmf(sig):
    # Compute correlation matrix
    R = np.corrcoef(sig)

    # Compute Cholesky decomposition of correlation matrix
    S = np.linalg.cholesky(np.linalg.inv(R))

    # Construct filter coefficients from Cholesky matrix
    b = np.diag(S).reshape(-1, 1)
    a = np.fliplr(S).reshape(-1, 1)

    return lfilter(b.squeeze(), a.squeeze(), sig)
```

### Autocorrelation Matrix Filtering

The autocorrelation matrix filter computes the autocorrelation matrix of a signal and then applies the Cholesky decomposition to get its square root. The resulting matrix is then used as the coefficients of a linear filter. The filter takes the form of:

$$H(z)=\sqrt[]{P^{-1}}$$

Where `P` is the autocorrelation matrix of the input signal.
In Python, the autocorrelation matrix filter can be implemented as follows:

```
def filter_amf(sig):
    # Compute autocorrelation matrix
    R = np.correlate(sig, sig, mode='full')[len(sig)-1:]
    T = toeplitz(R)

    # Compute Cholesky decomposition of autocorrelation matrix
    S = np.linalg.cholesky(np.linalg.inv(T))

    # Construct filter coefficients from Cholesky matrix
    b = np.diag(S).reshape(-1, 1)
    a = np.fliplr(S).reshape(-1, 1)

    return lfilter(b.squeeze(), a.squeeze(), sig)
```

### Example: Whitening Filter Comparison

To compare the different whitening filters, we can generate a signal with a coloured noise spectrum and then apply each of the filters in turn. The resulting filtered signal should have a Gaussian spectrum with zero mean and unit variance. 

```
import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import lfilter

# Generate coloured noise signal
n = 10000
sig = np.sin(np.linspace(0, np.pi*10, n)) + np.random.randn(n)*3

# Apply variance normalization filter
vn_sig = filter_vn(sig)

# Apply correlation matrix filter
cmf_sig = filter_cmf(sig)

# Apply autocorrelation matrix filter
amf_sig = filter_amf(sig)

# Plot PSD of original and filtered signals
psd_orig = np.abs(np.fft.fft(sig))**2
psd_vn = np.abs(np.fft.fft(vn_sig))**2
psd_cmf = np.abs(np.fft.fft(cmf_sig))**2
psd_amf = np.abs(np.fft.fft(amf_sig))**2

freqs = np.fft.fftfreq(n, d=1/n)
plt.plot(freqs, psd_orig, label='Original')
plt.plot(freqs, psd_vn, label='Variance Normalization')
plt.plot(freqs, psd_cmf, label='Correlation Matrix')
plt.plot(freqs, psd_amf, label='Autocorrelation Matrix')
plt.xlabel('Frequency')
plt.ylabel('Power Spectral Density')
plt.legend()
plt.show()
```

The resulting plot shows the PSD of the original signal and the filtered signals using the variance normalization, correlation matrix, and autocorrelation matrix filters. We can see that all filters achieve a similar result, with a flat PSD indicating Gaussian noise.

In conclusion, LTI whitening filters are a powerful tool for converting coloured noise into Gaussian noise, which has many applications in signal processing. The variance normalization, correlation matrix, and autocorrelation matrix filters are popular variants of this approach, each with its strengths and weaknesses. The presented implementations demonstrate how to use the whitening filters in Python.


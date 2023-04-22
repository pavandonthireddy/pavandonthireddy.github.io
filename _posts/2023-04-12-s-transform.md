---
layout: post
title: "S Transform: A Denoising Method in Time-Frequency Domain"
description: "An article on S Transform and its usage as a denoising method in time-frequency domain."
summary: "This article discusses the concept of the S transform and its usage as a denoising method in time-frequency domain. It also provides a Python implementation of the S transform and its denoising operation."
author: Pavan Donthireddy
usemathjax: true
original: new
tags: [ time_frequency_methods , S_Transform, signal_denoising ]
---
# Introduction
Time-frequency analysis is an important tool for analyzing signals that contain both time-varying and frequency-varying components. The Short Time Fourier Transform (STFT) is the most commonly used technique for time-frequency analysis, but it suffers from a time-frequency resolution trade-off problem. The S transform is an alternative time-frequency analysis technique that overcomes this problem by using a windows of variable length. In addition to time-frequency analysis, the S transform has also been used as a denoising method for signals.

In this article, we will provide an overview of the S transform and its usage as a denoising method in time-frequency domain. We will also provide a Python implementation of the S transform and its denoising operation.

# The S Transform
The S transform is a time-frequency analysis technique that uses a variable length window to estimate the local frequency content of a signal. The S transform of a signal is defined as follows:

$$ S(\tau, f) = \int_{-\infty}^{\infty} x(t) w(t-\tau) e^{-2\pi i f t} dt $$

where x(t) is the signal, w(t) is a complex valued window function, $f \in \mathbb{R}$ is the frequency variable, and $\tau \in \mathbb{R}$ is the time variable.

The window function w(t) has to satisfy some conditions in order for the S transform to be well defined. First, w(t) should be a complex valued function that is differentiable in some region. Second, the window function should have finite energy, i.e., $\int_{-\infty}^{\infty} \lvert w(t) \rvert^2 dt < \infty$. Third, the window function should be compactly supported, i.e., w(t) = 0 for $\lvert t \rvert > W$, where W is the window length. Fourth, the window function should have a minimum uncertainty property, which means that the product of the window function and its Fourier transform should have a minimum uncertainty.

The S transform can be computed efficiently using the Fast Fourier Transform (FFT) algorithm. The S transform of a signal x can be obtained as follows:

1. Divide the signal x into overlapping segments of length L and apply the window function w to each segment.
2. Compute the FFT of the windowed segments.
3. Multiply the FFT of the windowed segments by a phase factor corresponding to the time shift $\tau$.
4. Compute the inverse FFT of the product obtained in step 3.
5. Repeat steps 2 to 4 for different values of $\tau$ and $f$ to obtain the S transform.

# Denoising using the S Transform
The S transform has been used as a denoising method for signals. The idea behind using the S transform for denoising is that in the time-frequency domain, the noise is spread out over a wide range of frequencies, whereas the signal is concentrated in a few frequency bands. Therefore, by thresholding the S transform coefficients corresponding to the noise, the noise can be effectively removed while preserving the signal.

The denoising operation using the S transform can be described as follows:

1. Compute the S transform of the noisy signal.
2. Calculate the noise threshold using some thresholding function (e.g., universal threshold, soft threshold, hard threshold).
3. Set the S transform coefficients with magnitude less than the threshold to zero.
4. Compute the inverse S transform to obtain the denoised signal.

# Python Implementation
We provide a Python implementation of the S transform and its denoising operation using the PyWavelets library.

```python
import pywt
import numpy as np

def s_transform(x, window, n_frequencies):
    """
    Compute the S transform of a signal x using a given window function and number of frequencies.
    
    Parameters:
        x (numpy array): The input signal.
        window (numpy array): The complex valued window function.
        n_frequencies (int): The number of frequencies to compute.
        
    Returns:
        st (numpy array): The S transform of the signal.
        freqs (numpy array): The array of frequency values.
        times (numpy array): The array of time values.
    """
    L = len(window)
    n = len(x)
    half_L = L // 2
    timesteps = np.arange(half_L, n - half_L, half_L)
    freqs = np.fft.fftfreq(L)
    st = np.zeros((n_frequencies, len(timesteps)), dtype=np.complex128)
    for i, t in enumerate(timesteps):
        w = window * x[t-half_L:t+half_L]
        W = np.fft.fft(w)
        for j, f in enumerate(freqs[:n_frequencies]):
            st[j,i] = np.exp(-2j*np.pi*t*f)*W[j]
    times = pywt.scale2time(freqs, L) + 0.5*(n-L)/n
    return st, freqs[:n_frequencies], times

def threshold(S, threshold_fn, sigma=1):
    """
    Threshold the S transform coefficients based on a given thresholding function.
    
    Parameters:
        S (numpy array): The S transform of the signal.
        threshold_fn (function): The thresholding function.
        sigma (float): The standard deviation of the noise.
        
    Returns:
        S_thresholded (numpy array): The thresholded S transform of the signal.
    """
    noise_std = sigma*np.median(np.abs(S))/0.6745
    threshold = threshold_fn(S, noise_std)
    S_thresholded = np.zeros_like(S)
    S_thresholded[np.abs(S) >= threshold] = S[np.abs(S) >= threshold]
    return S_thresholded

def inverse_s_transform(S):
    """
    Compute the inverse S transform of a thresholded S transform.
    
    Parameters:
        S (numpy array): The thresholded S transform.
        
    Returns:
        x (numpy array): The denoised signal.
    """
    L = S.shape[1]
    n = len(S[0])*L
    half_L = L // 2
    timesteps = np.arange(half_L, n - half_L, half_L)
    x = np.zeros(n)
    for i, t in enumerate(timesteps):
        W = np.zeros(L, dtype=np.complex128)
        for j, f in enumerate(np.arange(len(S))):
            W[j] = np.exp(2j*np.pi*t*f/L)*S[j,i]
        w = np.fft.ifft(W).real
        x[t-half_L:t+half_L] += w * np.conj(window)
    return x[half_L:-half_L]

window = pywt.blackmanharris(256)
st, freqs, times = s_transform(x, window, 512)
st_thresholded = threshold(st, pywt.thresholding.hard, sigma=1)
x_denoised = inverse_s_transform(st_thresholded)
```

# Conclusion
In this article, we discussed the concept of the S transform and its usage as a denoising method in time-frequency domain. We provided a Python implementation of the S transform and its denoising operation using the PyWavelets library. The S transform has advantages over the STFT in terms of time-frequency resolution and the denoising operation using the S transform has shown promising results in various applications of signal processing.
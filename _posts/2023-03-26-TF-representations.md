
---
layout: post
title: Time Frequency Representations and Its Variants
description: This article explains the concept of time frequency analysis, along with its variants and their implementation in Python.
summary: The article provides an introduction to time frequency analysis, discussing the need and significance of time frequency representations. It explains the variants of time frequency representations, namely Short-Time Fourier Transform (STFT), Continuous Wavelet Transform (CWT), Empirical Mode Decomposition (EMD), and Cohen's Class, providing a theoretical understanding of each. Python implementation and examples are also provided.
author: Pavan Donthireddy
mathjax: true
original: new
tags: time_frequency_methods , representation, STFT , EMD 

---

## Introduction 
Time-frequency analysis (TFA) is a technique that allows us to analyze signals in both time and frequency domains. Traditional Fourier analysis assumes that the signal is stationary over time, i.e., the frequency content of the signal is constant. However, in real-world applications, such as speech and music signal processing, the stationary assumption does not hold. TFA provides time-frequency representations of non-stationary signals, enabling us to study signal dynamics with changing frequency behavior. 

## Time Frequency Representations
Time-frequency representations can be classified into four groups: Short-Time Fourier Transform (STFT), Continuous Wavelet Transform (CWT), Empirical Mode Decomposition (EMD) and Cohen's class. 

### Short-Time Fourier Transform (STFT)
STFT is a standard technique for time-frequency analysis that computes the Fourier transform of signal segments over time. The analysis window of a fixed-length is used to break down the signal into overlapping segments. An STFT of size $N$ applied to the signal $x(n)$ gives:

$$\begin{equation}
X_{m,k} = \sum^{N-1}_{n=0}x(n+mH)w(n)e^{-j2\pi kn/N}
\end{equation} $$



where $H$ is the hop-size between window frames, $w(n)$ is the analysis window, $m$ denotes the window frame number, and $k$ is the frequency index. The STFT is characterized by the window shape and length, as well as the hop size.

Python Implementation of STFT:
```python
import numpy as np
from scipy.signal import get_window
from scipy.fftpack import fft

def stft(x, win, hop):
    nx = len(x)
    nwin = len(win)
    nfft = int(2**np.ceil(np.log2(nwin)))
    nframes = int(np.ceil((nx-nwin)/hop)+1)
    
    x = np.pad(x, int(nwin//2), mode='reflect')
    frames = np.lib.stride_tricks.as_strided(x, shape=(nwin, nframes),
                                             strides=(x.itemsize, hop*x.itemsize))
    frames = frames * win[:, None]
    spectrum = fft(frames, axis=0)[:nfft//2]
    return spectrum
```

### Continuous Wavelet Transform (CWT)
CWT finds the time-frequency decomposition of the signal by using a time-varying window, or wavelet. The wavelet is scaled and shifted over time to obtain the distribution of the frequency and its variations with time. The CWT of a signal $x(t)$ with wavelet $\psi(t)$ is given by:

$$\begin{equation}
W_x(a,b) = \int^{+\infty}_{-\infty}\psi^*(t)\frac{1}{\sqrt{|a|}}x(t)\exp{\bigg(\frac{i}{a}bt\bigg)}dt
\end{equation}$$

where the wavelet $\psi(t)$ is scaled by a factor $a$ and shifted by $b$. CWT requires the selection of a suitable wavelet that is appropriate for the application.

Python Implementation of CWT:
```python
import pywt

def cwt(x, wavelet):
    scales = np.arange(1, 64)
    coef, freqs = pywt.cwt(x, scales, wavelet, sampling_period=1/1000)
    return coef
```

### Empirical Mode Decomposition (EMD)
EMD is a data-driven, adaptive time-frequency decomposition method that decomposes a signal into Intrinsic Mode Functions (IMFs), resulting in a time-frequency representation. IMFs are the low-frequency components of the signal, and they represent the signal's local characteristics. 

Python Implementation of EMD:
```python
import emd

def emd(x):
    emd_result = emd.sift.sift(x)
    imfs = emd_result[:-1]
    return imfs
```

### Cohen's Class
Cohen's class is a generalization of the STFT that allows the window function to vary over time. This generalization allows the use of different window functions that change over time. The Cohen's Class of a signal $x(t)$ with a window function $g(t,\tau)$ is given by:

$$\begin{equation}
C_{g}(s, \tau) = \int_{-\infty}^{\infty}x(t)g^*(t, \tau)\exp(-j2\pi st)dt
\end{equation}$$

where $g(t,\tau)$ is a time-varying window function dependent on a continuous parameter $\tau$.

Python Implementation of Cohen's Class:
```python
import pandas as pd
from pyct import saa

def cohens_class(x):
    sst, result = saa.s_transform(x)
    return pd.DataFrame(result)
```
# Time Frequency Representations

In signal processing, it is often necessary to analyze signals in both time and frequency domains. However, traditional Fourier analysis is not sufficient as it only analyzes the frequency components and completely ignores the variations in time. This limitation led to the development of time frequency representations (TFRs) that analyze the frequency components of a signal at different points in time.

TFRs are important in many fields of signal processing, including speech processing, radar signal analysis, biomedical engineering, and image processing. There are many different types of TFRs, each with its own strengths and weaknesses.

## Wigner Distribution Function

The Wigner distribution function (WDF) is a widely used TFR that was introduced in the 1930s by Eugene Wigner. It provides a joint time-frequency analysis and gives an estimate of the local energy density of a signal in time and frequency domains.

The WDF has several advantages. Firstly, it can accurately detect time-varying frequencies and phase information, making it useful for analyzing non-stationary signals. Secondly, it has good resolution properties and can distinguish between closely spaced frequency components. However, the WDF has some limitations. It has a high computational complexity and can produce negative values, making interpretation difficult.

## Modified Distribution Functions

Modified distribution functions (MDFs) are a family of TFRs that include smoothed WDFs, spectrograms, and scalograms. Spectrograms are the most widely used MDFs and provide a frequency-time representation of a signal. They use a window function to obtain a smoothed version of the WDF and have a low computational complexity.

Scalograms are a type of MDF that uses wavelet transforms to analyze signals. They have good time-frequency resolution and can capture both high and low-frequency components of a signal. However, they have limited resolution in time and frequency if the wavelet basis function is not chosen properly.

## Table comparing TFRs

| TFR            | Pros                                                                      | Cons                                                                                                      |
|----------------|---------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------|
| Wigner         | Accurate frequency and phase information. Good frequency resolution.    | High computational complexity. Can produce negative values, making interpretation difficult.              |
| Spectrogram    | Low computational complexity. Good frequency resolution.                 | Limited time and frequency resolution.                                                                     |
| Scalogram      | Good time and frequency resolution. Can capture both high and low frequencies. | Limited resolution in time and frequency if the wavelet basis function is not chosen properly. |

In conclusion, TFRs are an essential tool in signal processing as they allow for a joint analysis of the time and frequency domains. The choice of TFR will depend on the specific requirements of the analysis, including the complexity of the signal and the desired resolution in time and frequency.

## Conclusion
Time-frequency analysis is a powerful technique for signal processing, especially when analyzing non-stationary signals. The article provided an introduction to TFA, discussing time-frequency representations and the need for them. Additionally, it explained the four main types of time-frequency representations and their working principles. Python implementations of Short-Time Fourier Transform (STFT), Continuous Wavelet Transform (CWT), Empirical Mode Decomposition (EMD), and Cohen's Class were also provided as examples.
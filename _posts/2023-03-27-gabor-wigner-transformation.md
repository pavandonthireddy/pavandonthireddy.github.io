---
layout: post
title: "Gabor Wigner Transform and Its Variants"
description: "This article introduces the Gabor Wigner transform and its variants along with the python implementation of each variant with code examples."
summary: "Learn about Gabor Wigner transform and its variants with python implementation of each variant with code examples."
author: Pavan Donthireddy
usemathjax: true
original: new
tags: GWT, time_frequency_methods , representation 
---

# Introduction
The Gabor Wigner Transform (GWT) is a technique used in signal processing to analyze time-varying signals. It is based on the Short-Time Fourier Transform (STFT), which allows the analysis of signals in the time-frequency domain. The GWT extends the STFT by considering the Wigner distribution, which is a time-frequency distribution with desirable mathematical properties.

# Gabor Wigner Transform
Let x(t) be a continuous-time signal, and g(t) be a window function. The Gabor Wigner Transform of x(t) is defined as follows:

$$GW_x(t, \omega) = \int_{-\infty}^\infty x(\tau)g(\tau - t)e^{-j\omega \tau}d\tau.$$

The GWT represents the time-frequency content of x(t) as a two-dimensional function, where the vertical axis represents frequency and the horizontal axis represents time.

# Variants of Gabor Wigner Transform

## Complex Gabor Wigner Transform
The Complex Gabor Wigner Transform (CGWT) is an extension of the GWT that uses complex window functions. The CGWT is defined as follows:

$$CGW_x(t, \omega) = \int_{-\infty}^\infty x(\tau)g(\tau - t)e^{-j\omega \tau}d\tau + i\int_{-\infty}^\infty x(\tau)h(\tau - t)e^{-j\omega \tau}d\tau,$$

where g(t) and h(t) are complex window functions. The CGWT allows the phase information of the signal to be retained in the time-frequency domain.

### Python Implementation
```python
import numpy as np

def cgwt(x, g, h, fs, fmin, fmax, nfreq, nfft):
    tfr = np.zeros((nfreq, x.size), dtype=np.complex)
    freqs = np.linspace(fmin, fmax, nfreq)
    t = np.arange(x.size) / fs
    for i, f in enumerate(freqs):
        kernel = g(t) * np.exp(-1j * 2 * np.pi * f * t) + h(t) * np.exp(1j * 2 * np.pi * f * t)
        s = np.fft.fft(x * kernel, nfft)
        tfr[i] = np.fft.ifft(s)
    return tfr, freqs
```

## Wavelet Gabor Wigner Transform
The Wavelet Gabor Wigner Transform (WGWT) is another variant of GWT that uses wavelet functions as the window functions. The WGWT is defined as follows:

$$WGW_x(t, \omega) = \int_{-\infty}^\infty x(\tau)g_{a,b}(\tau - t)e^{-j\omega \tau}d\tau,$$

where g_{a,b}(t) is a wavelet function with scale a and shift b.

### Python Implementation
```python
import numpy as np
import pywt

def wgwt(x, wavelet, scales, fmin, fmax, nfreq, nfft):
    tfr = np.zeros((nfreq, x.size), dtype=np.complex)
    freqs = np.linspace(fmin, fmax, nfreq)
    for i, scale in enumerate(scales):
        w = pywt.cwt(x, scale, wavelet)
        for j, f in enumerate(freqs):
            tfr[j] += w[0] * np.exp(-1j * 2 * np.pi * f * w[1])
    tfr /= len(scales)
    return tfr, freqs
```

## Multi-Window Gabor Wigner Transform
The Multi-Window Gabor Wigner Transform (MWGWT) uses multiple window functions with different time-frequency resolutions. The MWGWT is defined as follows:

$$MWG_x(t, \omega) = \sum_i \int_{-\infty}^\infty x(\tau)g_i(\tau - t)e^{-j\omega \tau}d\tau.$$

### Python Implementation
```python
import numpy as np
from scipy import signal

def mwgwt(x, windows, freqs, nfft, fs):
    tfr = np.zeros((len(freqs), x.size), dtype=np.complex)
    for i, f in enumerate(freqs):
        for j, w in enumerate(windows):
            tfr[i] += np.abs(signal.spectrogram(x, fs, w, fs/8, fs/4, nfft)[2])**2 * np.exp(-1j * 2 * np.pi * f * i / len(freqs))
    return tfr, freqs
```

# Conclusion
The Gabor Wigner Transform and its variants are useful techniques for analyzing time-varying signals in the time-frequency domain. The CGWT allows the phase information of the signal to be retained, while the WGWT uses wavelet functions for better time-frequency resolution. The MWGWT combines multiple window functions to achieve a balance between time and frequency resolutions. All of these variants can be easily implemented in Python, making them accessible to a wider audience.
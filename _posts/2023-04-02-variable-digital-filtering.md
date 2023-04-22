---
layout: post
title: Variable Digital Filtering and its Variants
description: This article explains the concept of Variable Digital Filtering and its variants using equations, Python implementation, and examples.
summary: This article covers the basics of Variable Digital Filtering, its variants, equations, Python implementation, and an example of each variant.
author: Pavan Donthireddy
usemathjax: true
original: new
tags: noise , filters 

---

# Introduction

Digital Signal Processing techniques have revolutionized the field of signal processing. Among various techniques, Digital Filtering plays a crucial role. Digital Filters are Linear Time-Invariant (LTI) Systems that process a discrete-time signal in the digital domain. Digital filters can be classified into two categories: Finite Impulse Response (FIR) and Infinite Impulse Response (IIR) filters. FIR filters are commonly used as they possess certain advantages over IIR filters such as linear-phase property, easy implementation, and stability. FIR filters also have a unique property of Variable Digital Filtering.

# Variable Digital Filtering

Variable Digital Filtering is a technique where the filter coefficients vary with time or frequency. The FIR filter coefficients involved in variable digital filtering are time-varying which leads to the ability to tune the filter parameters to match the characteristics of the input signal. The Variable Digital Filter applies an impulse response that varies over time. The coefficients of the filter are a function of time or frequency, depending on the type of variable filter used.

## Types of Variable Digital Filtering

There are two variants of Variable Digital Filters based on the variation of their filter coefficients:

1. Time-varying Digital Filters
2. Frequency-varying Digital Filters

### Time-varying Digital Filters

Time-varying digital filters are those filters that change their filter coefficients over time. These filters are typically used when the characteristics of the input signal change over time. The time variation can be either discrete or continuous.

#### Python Implementation

```python
import numpy as np
import scipy.signal as sig

def time_varying_filter(signal, filter_coeffs):
	"""
	Applies a time-varying filter to a given signal.
	
	Args:
	signal (array): Input signal to be processed.
	filter_coeffs (array): Array of filter coefficients.
	
	Returns:
	output (array): Filtered signal.
	"""
	output = np.zeros(len(signal))
	for i in range(len(signal)):
		output[i] = np.sum(signal[i:i+len(filter_coeffs)] * filter_coeffs)
		filter_coeffs = filter_coeffs + 0.01  # Increase filter coefficients over time
	return output
```

#### Example

Let us consider a signal that is a linear chirp. A linear chirp is a signal whose frequency changes linearly with time. We will apply a time-varying digital filter to this signal. 

```python
import matplotlib.pyplot as plt

# Generate linear chirp signal
t = np.linspace(0, 2*np.pi, num=1000)
linear_chirp = sig.chirp(t, f0=1.0, f1=10.0, t1=np.pi, method='linear')

# Generate filter coefficients
filter_coeffs = np.random.rand(11)

# Filter the linear chirp signal using time-varying filter
output = time_varying_filter(linear_chirp, filter_coeffs)

# Plot the results
fig, axes = plt.subplots(nrows=2, ncols=1, figsize=(10, 10))
axes[0].plot(t, linear_chirp)
axes[0].set_title('Linear Chirp Signal')
axes[0].set_xlabel('Time')
axes[0].set_ylabel('Amplitude')
axes[1].plot(t, output)
axes[1].set_title('Filtered Signal')
axes[1].set_xlabel('Time')
axes[1].set_ylabel('Amplitude')
plt.show()
```

The above code snippet generates a linear chirp signal, generates random filter coefficients and applies a time-varying digital filter to the signal. 

### Frequency-varying Digital Filters

Frequency-varying digital filters are those filters that change their filter coefficients with frequency. These filters are typically used when the input signal contains frequency components that vary over time.

#### Python Implementation

```python
import numpy as np
import scipy.signal as sig

def freq_varying_filter(signal, filter_coeffs):
	"""
	Applies a frequency-varying filter to a given signal.
	
	Args:
	signal (array): Input signal to be processed.
	filter_coeffs (array): Array of filter coefficients.
	
	Returns:
	output (array): Filtered signal.
	"""
	freqs = np.fft.fftfreq(len(signal), d=1/len(signal))
	f = np.fft.fft(signal)
	filter_curve = 1 - np.abs(freqs)/np.max(np.abs(freqs))
	filter_curve = filter_curve ** 2
	filtered = f * filter_curve
	output = np.real(np.fft.ifft(filtered))
	return output
```

#### Example

Let us consider a signal that is a sum of two sine waves: one with a frequency of 20 Hz and another with a frequency of 50 Hz. We will apply a frequency-varying digital filter to this signal.

```python
import matplotlib.pyplot as plt

# Generate the signal
t = np.linspace(0, 2*np.pi, num=1000)
sig1 = np.sin(2*np.pi*20*t)
sig2 = np.sin(2*np.pi*50*t)
signal = sig1 + sig2

# Generate filter coefficients
filter_coeffs = np.random.rand(11)

# Filter the signal using frequency-varying filter
output = freq_varying_filter(signal, filter_coeffs)

# Plot the results
fig, axes = plt.subplots(nrows=2, ncols=1, figsize=(10, 10))
axes[0].plot(t, signal)
axes[0].set_title('Input Signal')
axes[0].set_xlabel('Time')
axes[0].set_ylabel('Amplitude')
axes[1].plot(t, output)
axes[1].set_title('Filtered Signal')
axes[1].set_xlabel('Time')
axes[1].set_ylabel('Amplitude')
plt.show()
```

The above code snippet generates a signal with two sine waves of frequencies 20 Hz and 50 Hz, generates random filter coefficients, and applies a frequency-varying digital filter to the signal. The filtered signal is plotted against the original signal in the below graph.


# Conclusion

Variable Digital Filtering is a technique that is useful in several applications where the input signal characteristics vary with time. Time-varying and frequency-varying digital filters are the two variants of variable digital filters, and both are useful in various applications. This article provides a basic understanding of variable digital filters, their equations, Python implementation, and an example of each variant.

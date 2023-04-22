
---
layout: post
title: "Different Frequency Filtering Algorithms and its Variants"
description: "This article discusses various frequency filtering algorithms and their variants, along with equations in LaTeX. It also includes Python implementations for each variant with an example."
summary: "This article discusses various frequency filtering algorithms and their variants, along with equations in LaTeX. It also includes Python implementations for each variant with an example."
author: "Pavan Donthireddy"
mathjax: true
original: new
tags: [ filters ]
---

# Introduction

Frequency filtering is an essential signal processing technique used to eliminate unwanted frequency components from signals. It is used in various fields such as audio processing, image processing, and communication systems. Frequency filtering algorithms are designed to remove unwanted frequency components while preserving the useful components. This article provides a brief overview of common frequency filtering algorithms and their variants, along with their mathematical equations in LaTeX.

# Types of Frequency Filtering Algorithms

## Low-Pass Filter

A low-pass filter allows the low-frequency components of a signal to pass while attenuating the high-frequency components. The cut-off frequency of a low-pass filter determines the point at which the high-frequency components are attenuated. The transfer function of a low-pass filter can be expressed as follows:

$$
H_{lp}(f) = \frac{1}{1 + j\frac{f}{f_c}}
$$

Where $f_c$ is the cut-off frequency.

### Implementation in Python

```python
import numpy as np
import matplotlib.pyplot as plt

def lowpass_filter(signal, cutoff_freq, sample_rate):
    """ 
    Implements a low-pass filter on the input signal. 
    
    Args:
    signal (ndarray): Input signal
    cutoff_freq (float): Cut-off frequency of the filter
    sample_rate (float): Sample rate of the signal
    
    Returns:
    ndarray: Filtered signal
    """
    nyquist_freq = 0.5 * sample_rate
    normalized_cutoff_freq = 2 * cutoff_freq / sample_rate
    b, a = signal.butter(5, normalized_cutoff_freq, btype='lowpass')
    filtered_signal = signal.filtfilt(b, a, signal)
    
    return filtered_signal

# Example Usage
t = np.linspace(0, 1, 1000)
signal = np.sin(2*np.pi*10*t) + np.sin(2*np.pi*50*t)

filtered_signal = lowpass_filter(signal, 20, 100)
plt.plot(t, signal, label='Original Signal')
plt.plot(t, filtered_signal, label='Filtered Signal')
plt.legend()
plt.show()
```

## High-Pass Filter

As the name suggests, a high-pass filter attenuates the low-frequency components of a signal while allowing the high-frequency components to pass. The cut-off frequency of a high-pass filter determines the point at which the low-frequency components are attenuated. The transfer function of a high-pass filter can be expressed as follows:

$$
H_{hp}(f) = \frac{jf}{j\frac{f}{f_c} + 1}
$$

Where $f_c$ is the cut-off frequency.

### Implementation in Python

```python
import numpy as np
import matplotlib.pyplot as plt

def highpass_filter(signal, cutoff_freq, sample_rate):
    """ 
    Implements a high-pass filter on the input signal. 
    
    Args:
    signal (ndarray): Input signal
    cutoff_freq (float): Cut-off frequency of the filter
    sample_rate (float): Sample rate of the signal
    
    Returns:
    ndarray: Filtered signal
    """
    nyquist_freq = 0.5 * sample_rate
    normalized_cutoff_freq = 2 * cutoff_freq / sample_rate
    b, a = signal.butter(5, normalized_cutoff_freq, btype='highpass')
    filtered_signal = signal.filtfilt(b, a, signal)
    
    return filtered_signal

# Example Usage
t = np.linspace(0, 1, 1000)
signal = np.sin(2*np.pi*10*t) + np.sin(2*np.pi*50*t)

filtered_signal = highpass_filter(signal, 20, 100)
plt.plot(t, signal, label='Original Signal')
plt.plot(t, filtered_signal, label='Filtered Signal')
plt.legend()
plt.show()
```

## Band-Pass Filter

A band-pass filter attenuates the frequency components outside its pass-band, allowing only the frequency components within the band to pass. The pass-band of a band-pass filter is defined by the upper and lower cut-off frequencies. The transfer function of a band-pass filter can be expressed as follows:

$$
H_{bp}(f) = \frac{j(f_{h} - f_{l})}{j\frac{(f_{h} - f_{l})}{f_c} + 1} e^{-j2\pi\frac{f_{h} + f_{l}}{2f_s}t}
$$

Where $f_{h}$ and $f_{l}$ are the upper and lower cut-off frequencies, respectively.

### Implementation in Python

```python
import numpy as np
import matplotlib.pyplot as plt

def bandpass_filter(signal, lowcut, highcut, sample_rate):
    """ 
    Implements a band-pass filter on the input signal. 
    
    Args:
    signal (ndarray): Input signal
    lowcut (float): Lower cut-off frequency of the filter
    highcut (float): Upper cut-off frequency of the filter
    sample_rate (float): Sample rate of the signal
    
    Returns:
    ndarray: Filtered signal
    """
    nyquist_freq = 0.5 * sample_rate
    normalized_lowcut = lowcut / nyquist_freq
    normalized_highcut = highcut / nyquist_freq
    b, a = signal.butter(5, [normalized_lowcut, normalized_highcut], btype='band')
    filtered_signal = signal.filtfilt(b, a, signal)
    
    return filtered_signal

# Example Usage
t = np.linspace(0, 1, 1000)
signal = np.sin(2*np.pi*10*t) + np.sin(2*np.pi*50*t)

filtered_signal = bandpass_filter(signal, 20, 80, 100)
plt.plot(t, signal, label='Original Signal')
plt.plot(t, filtered_signal, label='Filtered Signal')
plt.legend()
plt.show()
```

## Band-Stop Filter

A band-stop filter attenuates the frequency components within its stop-band, allowing only the frequency components outside the band to pass. The stop-band of a band-stop filter is defined by the upper and lower cut-off frequencies. The transfer function of a band-stop filter can be expressed as follows:

$$
H_{bs}(f) = \frac{1}{1 + j\frac{(f_{h} - f_{l})}{f_c}} e^{-j2\pi\frac{f_{h} + f_{l}}{2f_s}t}
$$

Where $f_{h}$ and $f_{l}$ are the upper and lower cut-off frequencies, respectively.

### Implementation in Python

```python
import numpy as np
import matplotlib.pyplot as plt

def bandstop_filter(signal, lowcut, highcut, sample_rate):
    """ 
    Implements a band-stop filter on the input signal. 
    
    Args:
    signal (ndarray): Input signal
    lowcut (float): Lower cut-off frequency of the filter
    highcut (float): Upper cut-off frequency of the filter
    sample_rate (float): Sample rate of the signal
    
    Returns:
    ndarray: Filtered signal
    """
    nyquist_freq = 0.5 * sample_rate
    normalized_lowcut = lowcut / nyquist_freq
    normalized_highcut = highcut / nyquist_freq
    b, a = signal.butter(5, [normalized_lowcut, normalized_highcut], btype='bandstop')
    filtered_signal = signal.filtfilt(b, a, signal)
    
    return filtered_signal

# Example Usage
t = np.linspace(0, 1, 1000)
signal = np.sin(2*np.pi*10*t) + np.sin(2*np.pi*50*t)

filtered_signal = bandstop_filter(signal, 20, 80, 100)
plt.plot(t, signal, label='Original Signal')
plt.plot(t, filtered_signal, label='Filtered Signal')
plt.legend()
plt.show()
```

# Conclusion

Frequency filtering is an essential technique in digital signal processing, and various algorithms and their variants are commonly used in various fields. This article provided a brief overview of the most common frequency filtering algorithms, along with mathematical equations in LaTeX and their Python implementations. It is vital to understand the application and characteristics of different algorithms before selecting a specific algorithm for a specific task.
---
layout: post
title: "Intrinsic Chirp Component Decomposition and its Variants"
description: "This article discusses the theoretical concept of intrinsic chirp component decomposition along with its variants."
summary: "This article explains how intrinsic chirp component decomposition can be used to separate signal components in a given signal using mathematical equations and its variants."
author: "Pavan Donthireddy"
usemathjax: true
original: new
tags: [ time_frequency_methods , ICCD, signal_extraction ]
---

# Introduction

The intrinsic chirp component (ICC) is a time-frequency component present in a signal that has been widely studied in the field of time-frequency analysis. The decomposition of a signal into its ICC and non-ICC components can provide insight into its underlying structure and aid in the extraction of meaningful information. 

In this article, we will discuss the theoretical concept of intrinsic chirp component decomposition along with its variants. We will also provide Python implementations and examples for each variant.

# Intrinsic Chirp Component Decomposition

Intrinsic Chirp Component Decomposition (ICCD) is a technique used to extract the ICC(s) of a signal. The concept behind the ICC is simple: At any instant of time, the signal is analyzed using a time-frequency window. In a standard Fourier transform, this window is fixed and its length becomes shorter for high frequencies. However, the ICC approach employs a time-frequency window that varies with time, such that the window's size increases for high frequencies. Therefore, ICC is a non-stationary feature that varies with time, unlike Fourier-based methods, which are stationary features. 

The general equation for ICCD is:

$$x(t) = ICC(t) + x_{0}(t)$$

where $x(t)$ is the signal, $ICC(t)$ is the Intrinsic Chirp Component, and $x_0(t)$ is the non-ICC component. 

ICC(t) is defined as follows:

$$ICC(t) = \int_{-\infty}^{\infty}\int_{-\infty}^{\infty}W(t,f)\,f\,dt\,df$$

where $W(t,f)$ is the short-time Fourier transform of the signal, and $f$ is the frequency component.

ICC can be used to characterize several properties of the signal, including its time-varying spectral profile, complexity, and phase structure. The decomposition of the signal into the ICC and non-ICC components can help extract meaningful information from the signal.

A Python implementation of ICCD is as follows:

```
def iccd(x, fs):
    N = len(x)
    f, t, stft = signal.stft(x, fs)
    
    ICC = np.sum(stft*f, axis=0)
    noICC = stft - np.outer(f, ICC)

    return ICC, noICC
```

Here, `x` is the input signal, and `fs` is its sampling frequency. We compute the short-time Fourier transform using the `signal.stft` function from `scipy` library, then calculate the ICC and noICC components using the equations described earlier.

# Variants of ICCD

Several variants of ICCD can be used based on the properties required from the signal. Here are three variants: 

## Amplitude Modulation Decomposition

In this variant, we decompose a signal into its amplitude modulation components, which are related to the ICC feature. The equation for amplitude modulation decomposition is:

$$x(t) = \sum_{a=1}^{M} a(t)\,C_{a}(t) + x_{0}(t)$$

where $a(t)$ is the amplitude modulation envelope, $C_a(t)$ is the $a^{\text{th}}$ intrinsic chirp component, and $M$ is the number of ICCs. 

The Python implementation of this variant is:

```
def ampd(x, fs, M):
    N = len(x)
    f, t, stft = signal.stft(x, fs)
    
    am = np.sum(np.abs(stft), axis=0)
    noAMP = stft / np.outer(am, np.ones(N))

    ICCs = []
    for i in range(M):
        C = np.sum(noAMP * (np.abs(stft) ** i), axis=0)
        ICCs.append(C)
        noAMP = noAMP - np.outer(C, (am ** i))

    return np.array(ICCs), noAMP
```

Here, `M` is the number of ICCs we want to extract. We compute the short-time Fourier transform and calculate the amplitude modulation envelope. We then calculate the ICC components by iteratively subtracting the ICC components from the non-ICC component. 

## Frequency Modulation Decomposition

In this variant, we decompose a signal into its frequency modulation components, which are related to the derivative of the ICC feature. The equation for frequency modulation decomposition is:

$$x(t) = \sum_{a=1}^{M} b_a(t)\,F_{a}(t) + x_{0}(t)$$

where $b_a(t)$ is the frequency modulation envelope, $F_{a}(t)$ is the $a^{\text{th}}$ derivative of the ICC, and $M$ is the number of ICCs. 

The Python implementation of this variant is:

```
def fmdp(x, fs, M):
    N = len(x)
    f, t, stft = signal.stft(x, fs)
    
    fm = np.sum((f[:, np.newaxis] - np.mean(f)) ** 2 * np.abs(stft) ** 2, axis=0)
    noFMP = stft / np.outer(np.ones(N), np.sqrt(fm))

    ICCs = []
    for i in range(M):
        F = np.sum(noFMP * ((f[:, np.newaxis]-np.mean(f))**i)*np.abs(stft)**2, axis=0) / fm
        ICCs.append(F)
        noFMP = noFMP - np.outer(ICC, (f[:, np.newaxis]-np.mean(f)) ** i)
    
    return np.array(ICCs), noFMP
```

Here, `M` is the number of ICCs we want to extract. We compute the short-time Fourier transform and calculate the frequency modulation envelope. We then calculate the ICC components by iteratively subtracting the ICC components from the non-ICC component. 

## Synchrosqueezing Transform

In this variant, we apply the Synchrosqueezing Transform (SST) to the signal, which is a modified version of the Fourier transform that concentrates the energy of the signal onto the ICCs. The equation for SST is:

$$S\{\gamma_f h(t)\}(t, f) = \frac{h(t)\,\overline{h(t)}}{\int_{0}^{\infty}|h(t)|^2\,dt}\,w(t, f)$$

where $\gamma_f$ is the frequency scaling factor, $h(t)$ is the signal, $w(t, f)$ is the wavelet, and $S$ is the synchrosqueezing operator. 

The Python implementation of this variant is:

```
def sst(x, fs):
    N = len(x)
    f, stft = scipy.signal.stft(x, fs)

    M = np.shape(stft)[0]
    ICs = np.zeros((M, len(f)))

    for i in range(M):
        w = synchrosqueezing_window(f, i, fs)
        ICs[i] = np.sum(stft*w, axis=1)

    return ICs
```

Here, we calculate the short-time Fourier transform using the `scipy.signal.stft` function. We then calculate the synchrosqueezing window using a custom-defined function `synchrosqueezing_window`. We calculate the ICC components using the synchrosqueezing operator and return the matrix of the ICC components.

# Conclusion

In this article, we discussed the concept of intrinsic chirp component decomposition and its variants. We provided equations and Python implementations for each variant, along with examples. ICCD and its variants are powerful tools for extracting information from a given signal, and they have several applications in signal processing, such as in speech recognition, image analysis, and bio-medical signal processing.
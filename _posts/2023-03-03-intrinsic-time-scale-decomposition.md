---
layout: post
title: The De-noising Algorithm Based on Intrinsic Time-scale Decomposition
description: The De-noising Algorithm Based on Intrinsic Time-scale Decomposition
summary: The De-noising Algorithm Based on Intrinsic Time-scale Decomposition
author:
- Pavan Donthireddy
usemathjax: true
tags: [signal_denoising, ITD, multiresolution]
original: zeng2011
---

## Abstract

<p align="justify">A new de-noising algorithm based on Intrinsic Time-scale Decomposition (ITD) is
proposed after analyzing the statistical characteristics of additional Gaussian white noise decomposed
by ITD. Compared with the Wavelet Threshold De-noising(WTD) and de-noising algorithms based
on empirical mode decomposition (EMD), the numerical simulation results show that this algorithm
has comparable performance with the de-noising based on EMD and the WTD, and it is no need for
spline interpolation, iterative sifting and selection of the wavelet base. It is a new adaptive de-noising
algorithm.
</p>

## About ITD

Intrinsic Scale Decomposition (ISD) is a signal processing technique that aims to decompose a given signal into a set of intrinsic scales or frequency bands, each of which captures different patterns and features of the signal.

ISD is based on the idea of multiresolution analysis, which involves analyzing a signal at multiple scales or resolutions to extract different levels of detail. However, unlike traditional multiresolution analysis techniques such as wavelet transforms or Fourier transforms, ISD uses an adaptive and data-driven approach to identify the intrinsic scales of the signal.

The basic idea behind ISD is to iteratively decompose a signal into two parts: a smooth part and a fluctuation part. The smooth part represents the low-frequency components of the signal, while the fluctuation part captures the high-frequency components. This decomposition is repeated at each scale, with the smooth part of the previous scale serving as the input for the next scale.

The ISD algorithm typically involves the following steps:

1.  Define an initial scale and compute the mean and standard deviation of the signal at that scale.
2.  Decompose the signal into a smooth part and a fluctuation part at that scale, using the mean and standard deviation as thresholds.
3.  Repeat the decomposition process at successively higher scales, using the smooth part of the previous scale as the input for the next scale.
4.  Stop the decomposition process when the remaining signal has a small amplitude or when a predefined number of scales have been reached.
5.  Reconstruct the signal by summing up the smooth parts of each scale.

The resulting decomposition provides a set of intrinsic scales or frequency bands that capture different patterns and features of the signal. These scales can be used for various signal processing tasks such as denoising, feature extraction, and pattern recognition.

ISD has been applied in various fields such as biomedical signal processing, image processing, and audio processing. However, it's worth noting that the effectiveness of ISD depends on the specific characteristics of the signal being analyzed and the choice of parameters used in the algorithm. Therefore, careful parameter tuning and validation are necessary to ensure the reliability and accuracy of the results.

```
import numpy as np

def intrinsic_scale_decomposition(signal, num_scales):
    """
    Perform intrinsic scale decomposition on a given signal.
    
    Args:
        signal (array_like): The input signal to be decomposed.
        num_scales (int): The number of scales to decompose the signal into.
        
    Returns:
        smooth (array_like): The smooth part of the signal at each scale.
        fluctuation (array_like): The fluctuation part of the signal at each scale.
    """
    
    # Define an initial scale and compute the mean and standard deviation of the signal
    scale = 0
    mean = np.mean(signal)
    std = np.std(signal)
    
    # Initialize arrays to store the smooth and fluctuation parts of the signal
    smooth = np.zeros((num_scales, len(signal)))
    fluctuation = np.zeros((num_scales, len(signal)))
    
    # Perform ISD at each scale
    for i in range(num_scales):
        # Decompose the signal into a smooth part and a fluctuation part
        threshold = std * 2**(scale/2)
        smooth[i] = np.where(abs(signal - mean) < threshold, signal, mean)
        fluctuation[i] = signal - smooth[i]
        
        # Update the mean and standard deviation for the next scale
        mean = np.mean(smooth[i])
        std = np.std(fluctuation[i])
        
        # Increment the scale for the next iteration
        scale += 1
    
    return smooth, fluctuation

```


Here's a brief explanation of the steps involved in the algorithm:

1.  The input signal is decomposed into a set of scales, with the number of scales specified by the `num_scales` parameter.
2.  The mean and standard deviation of the signal are computed at the initial scale.
3.  For each scale, the signal is decomposed into a smooth part and a fluctuation part using a threshold based on the standard deviation and the current scale.
4.  The mean and standard deviation are updated for the next scale using the smooth and fluctuation parts of the previous scale.
5.  The process is repeated for the specified number of scales.
6.  The output of the algorithm is a set of arrays containing the smooth and fluctuation parts of the signal at each scale.

Note that this is just one possible implementation of ISD, and there are many variations and extensions of the algorithm that can be used depending on the specific requirements of the application.

See [[2023-05-14-ITD]]


## Introduction

<p align="justify">In this paper,we impose a new signal analysis method,called intrinsic time-scale decomposition
(ITD),that was first introduced by G. Frei Mark and Ivan Osorio in 2006.This method is specifically
proposed for application to non-stationary and nonlinear signals in nature and obtained from complex
systems with underlying dynamics that change on multiple time-scales simultaneously.The ITD
algorithm has the adavantages of low computation complexity, small edge effects and fast processing
speed, and avoids wavelet base seletion compared with decomposition algorithms based on EMD and
wavelet.According to direct extraction of the signal energy associated with various intrinsic time
scales,the ITD decomposes an input signal into a set of proper rotation components and a residual
signal.And the proper rotations may be applied to analyse the instantaneous information.Based on the
statistic features of uniformly distributed white noise using the ITD, an adaptive denoising algorithm
based on ITD is proposed.Compared with the de-noising based on wavelet threshold and EMD,the
simulation results show that the ITD algorithm has a good de-noising properties.</p>

### Intrinsic Time-scale Decomposition

The purpose of the intrinsic time-scale decomposition is to decompose the signal into a series of proper rotation components and a monotonous trend component,in ordor to obtain meaningful instantaneous frequency and amplitude information.

A real-valued signal $\left\{X_t, t \geq 0\right\}$ is given, and we define an operator $L$, which decomposes the signal $X_t$ into the baseline signal and a proper rotation. The $X_t$ can be expressed as

$$
X_t=L X_t+(1-L) X_t=L_t+H_t
$$
Where $L_t=L X_t$ is the baseline signal and $H_t=(1-L) X_t$ is a proper rotation. $\left\{\tau_k, k=1,2, \ldots\right\}$ is the local extrema of $X_t$, and especially define $\tau_0=0$. To simplify notation,let $X_k=X\left(\tau_k\right)$ and $L_k=L\left(\tau_k\right)$

Provided that $X_t$ is known for $\left[0, \tau_{k+2}\right]$ and that $L_t$ and $H_t$ have been given on $\left(0, \tau_k\right]$. Then the baseline signal $L_t$ can be defined on the interval $\left(\tau_k, \tau_{k+1}\right]$ between the continuous extrema as follows:
$$
L X_t=L_t=L_k+\left(\frac{L_{k+1}-L_k}{X_{k+1}-X_k}\right)\left(X_t-X_k\right), t \in\left(\tau_k, \tau_{k+1}\right] .
$$
Where
$$
L_{k+1}=L_t=\alpha\left(X_k+\left(\frac{\tau_{k+1}-\tau_k}{\tau_{k+2}-\tau_k}\right)\left(X_{k+2}-X_k\right)\right)+(1-\alpha) X_{k+1}
$$
$\alpha$ acts as a linear gain on the amplitude of the proper rotation component.And $0<\alpha<1$ is typically fixed with $\alpha=0.5$. The proper rotation $H_t$ can also be defined, as
$$
H X_t=H_t=(1-L) X_t=X_t-L_t
$$
The rotation signal, $H_t$, indicates the highest relative frequency of the input signal. And the baseline signal, $L_t$, indicates the lowest relative frequency of the input signal. The baseline signal is then treated as new input signal. The process continues until a monotonic trend is reached. This decomposes the input signal into a sequence of proper rotations of successively decreasing instantaneous frequency at each subsequent level of the decomposition. So the decomposition of $X_t$ can be written as
$$
\begin{aligned}
& X_t=H X_t+L X_t=H X_t+(H+L) L X_t \\
& =\left(H+H L+L^2\right) X_t \\
& =\left(H+H L+(H+L) L^2\right) X_t \\
& =\left(H+H L+H L^2+L^3\right) X_t \\
& =\ldots \ldots=\left(H \sum_{k=0}^{p-1} L^k+L^p\right) X_t
\end{aligned}
$$
Where $H L^k X_t$ is the $(k+1)$ st level proper rotation and $L^p X_t$ is either the residual signal or the lowest frequency baseline signal before the monotonic trend is obtained. Here the formula, $H+L=1$, is defined, and we also apply for the compression sum formula : $1-L^p=(1-L)\left(1+L+\ldots+L^{p-2}+L^{p-1}\right)$

Once the input signal has been decomposed into a set of proper rotations and a residual signal by the ITD, we are able to analysis the proper rotations to extract the instantaneous amplitude, phase and frequency.

### Denoising Principle Based on the ITD

The numerical experiments are made to study the characteristics of white noise using the ITD. The results show that each proper rotation of the ITD is a normal distribution with mean 0 and variance $\delta^2$, that $\delta^2$ is variance of each rotation; and all the Fourier spectra except the first one have nearly the same shapes in terms of the semi-logarithmic scale. At the same time, we can obtain a simple equation that presents the relation of the energy density $E_n$ and the averaged period $\overline{T_n}$, i.e.
$$
\begin{aligned}
& E_n \overline{T_n}=\text { const } \\
& \ln E_n+\ln \overline{T_n}=\text { const }
\end{aligned}
$$
Where $E_n=\frac{1}{N} \sum_{i=1}^n\left[C_n(i)^2\right]$ is the energy density of the $n$th proper rotation with the data length of $\mathrm{N}$, and $\bar{T}_n=N / N_{\max }$ is the averaged period of the $n$th proper rotation with $N_{\max }$ standing for the number of the maximum extrema in $C_n$. If a white-noise series is normalized, the constant in equation (6) is unity. Therefore, the constant of equation (7) is zero, i.e.
$$
\ln \overline{E_n}+\ln \overline{T_n}=0
$$
Where $\overline{E_n}$ is the mean of $E_n$ when $n$ approaches infinity. Based on the probability density function theory, the energy density is the $\chi^2$ distribution for the time series is a normal distribution. The degrees of the $\chi^2$ distribution should be the mean of the energy.

The verification of equation (8) is given in figure 1 . The random dataset is $10^6$ data points divided into 1000 samples with an identical length of 1000 data points. From Fig. 1, we can get the conclusion that the energy density and the averaged period of the proper rotations could deviate from the standard line, but this is very small.

Having determined the distribution function of the energy of the Gaussian white noise, we will discuss spread of the confidence levels of the energy of white-noise samples. The spread of the confidence levels of the energy is the range of the energy distribution with the upper-energy side and lower-energy side.

First, we define a new variable $\mathrm{y}$, as $y=\ln E_n$. The spread line can be defined as
$$
y=\ln E_n \pm k \sqrt{\delta^2}=-\ln T_n \pm k \sqrt{2 / N} \cdot \sqrt{T_n}=-\ln T_n \pm k \sqrt{2 / N} \cdot e^{\ln T_n / 2}
$$
Where
$$
x=\ln T_n
$$
So
$$
y=-x \pm k \sqrt{2 / N} e^{x / 2}
$$
Here $\mathrm{k}$ is a constant determined by the confidence levels. For example, we will have $\mathrm{k}$ equal to $-2.326,-0.675,-0.0,0.675$ and 2.326 for the first, 25 th, 50 th, 75 th and 99 th percentiles, respectively. The spread lines of the confidence level based on equation (11) are plotted in Fig. 2 with the first (the lower side) and 99th (the upper side) percentiles. The bold blue lines are the first (the lower side) and 99th (the upper side) percentiles.

Based on the statistical characteristics of white noise, we put forward a method, to extract the used information of a dataset with unknown noise. Specifically, we need to find which rotations from the noisy dataset include information, and which rotations are purely noise. We introduce $x(t)=s(t)+n(t)$, where $s(t)$ is the used information and $n(t)$ is the white-noise with mean 0 and variance 1 . 

The specific steps are as follows.
(1) decompose $x(t)$ into the proper rotations basing on the ITD.
(2) caculate the energy density and the averaged period of each rotation.
(3) determine the spread of confidence level of an artifical white-noide as a reference.
(4) compare the energy density for the rotations of $x(t)$ with the spread functions of the reference noise; the rotations that locate in the bound of the spread of the confidence level of the reference noise are considered to be the noise. And the corresponding rotations are subtracted from the original siganl to get the de-noising signal.


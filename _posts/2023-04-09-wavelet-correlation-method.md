---
layout: post
title: "Wavelet Correlation Method and Its Variants"
description: "Exploring the principles and applications of wavelet correlation method and its various forms."
summary: "This article aims to provide a comprehensive overview of wavelet correlation method and its variants, highlighting their significance and advantages in various scientific applications."
author: Pavan Donthireddy
usemathjax: true
original: new
tags: [ wavelet , preprocessing , signal_denoising ]
---

# Introduction

Wavelet Correlation Method (WCM) is a powerful mathematical tool used in signal processing and data analysis. It is a technique that helps detect and measure correlations between two signals or data sets. With the help of WCM, researchers can precisely identify co-occurring events in different data sets and study the relationship between two time series or multi-dimensional signals.

The wavelet transform is a mathematical tool used to analyze the frequencies present in a signal. It decomposes a signal into a set of wavelets, which are localized in both time and frequency domains. Wavelet correlation method leverages this feature of wavelets to evaluate the similarity between two signals over different frequency scales.

In this article, we will provide an overview of the WCM approach and its various forms. We will discuss its significance in scientific research and practical implementations using Python.

# Wavelet Correlation Method

The core idea behind WCM is to decompose two signals, x(t) and y(t), using wavelet transforms and then measure the similarity between the resultant wavelet coefficients at different scales. The wavelet correlation coefficient (WCC) is defined as follows:

$$WCC(a,b) = \sum_{i=-\infty}^\infty x_iy_i^*, 
$$
where

- x_i = a-th scale wavelet coefficient of signal x(t) at time i
- y_i = b-th scale wavelet coefficient of signal y(t) at time i
- a and b are scales at which wavelet transforms are performed
- * represents the complex conjugate.

The wavelet correlation coefficient quantifies the degree of similarity between the two signals at different frequency scales. WCC can be seen as a measure of cross-correlation between two signals, but with a better frequency resolution. 

Using WCM, one can identify the time points where the two signals are highly correlated, thereby helping to detect the joint occurrences of events in the two signals. This feature has been widely used in several research domains, including neuroscience, climatology, and genetics.

# Variations of Wavelet Correlation Method

Several variations of the WCM approach have been proposed in the literature, each catering to specific research domains and signal types. In this section, we will discuss some of the most commonly used variants of the WCM approach.

## Phase-Slope Index

Phase-Slope Index (PSI) is a variant of WCM that is widely used in neuroscience research. PSI is a measure of phase lag between two signals, evaluated at different frequency scales. PSI is defined as follows:




$$\text{PSI}(a,b) = \frac{\sum_{i,j} \Delta\varphi_{ij} \cdot \Delta\log{s_{x,i}} \cdot \Delta\log{s_{y,j}}}{\sum_{i,j}\Delta\log{s_{x,i}} \cdot \Delta\log{s_{y,j}}},
$$




where

- Δϕ_ij = the phase difference between the a-th scale wavelet coefficient of signal x and the b-th scale wavelet coefficient of signal y
- Δlog(s_x,i) and Δlog(s_y,j) are the differences in logarithm of scales s used for the wavelet transforms.

PSI takes both the phase difference and the scale difference between two signals into account while quantifying their similarity. PSI is used to measure the connectivity between different brain regions and identify the source of neuronal oscillations.

## Wavelet Coherence

Wavelet Coherence is another variation of WCM that is used to assess the coherence between two signals over different frequency scales. It quantifies the degree of power correlation between two signals at different frequency scales.

Wavelet Coherence (WC) is defined as follows:

$$\text{WC}(a,b) = \frac{|\text{WCC}(a,b)|^2}{\text{Power}(a,\text{x})\text{Power}(b,\text{y})},$$

where

- Power(a,x) and Power(b,y) are the wavelet power of x(t) and y(t) at scales a and b, respectively.

Wavelet coherence is used in several domains such as financial risk analysis, biomedical engineering, and geophysics. 

## Weighted Average Wavelet Coefficient

Weighted Average Wavelet Coefficient (WAWC) is a variant of WCM used to quantify the correlation between a single signal and a group of signals. WAWC is defined based on the weighted average of wavelet coefficients, where the weights are determined by the degree of similarity between the signals.

$$WAWC(a) = \frac{\sum_{j=1}^N w_j(a) \cdot x_j(a)}{\sum_{j=1}^N w_j(a)},$$

where

- xj(a) is the a-th scale wavelet coefficient of j-th signal
- wj(a) is the weight assigned to the j-th signal at the a-th scale

WAWC finds applications in several domains, including climatology and finance.

# Python Implementation

Python provides several libraries to perform wavelet transform and implement WCM. Two of the most commonly used libraries are PyWavelets and Wavelets.

First, let us install PyWavelets using pip:

```
$ pip install PyWavelets
```

Consider two signals, x(t) and y(t), represented as arrays. To perform wavelet correlation between them, we can use the following code:

```python
import pywt

def WCC(a, b, x, y):
    c_1 = pywt.wavedec(x, 'db1', mode='per') # wavelet decomposition of x
    c_2 = pywt.wavedec(y, 'db1', mode='per') # wavelet decomposition of y
    
    sum_WCC = 0
    
    for i in range(len(c_1[a])):
        sum_WCC += c_1[a][i] * c_2[b][i].conjugate()
        
    WCC = sum_WCC.real
    
    return WCC
```

The above code snippet computes the wavelet correlation coefficient between two signals at scales a and b. We can use this as a building block to implement various variants of WCM such as PSI, Wavelet Coherence, and WAWC.

# Conclusion

Wavelet Correlation Method and its variants are powerful mathematical tools used for signal processing and data analysis. They enable researchers to precisely identify co-occurring events and link them between different signals. In this article, we provided an overview of the WCM approach and discussed its significance in various scientific domains. We also discussed some of the most commonly used variants of WCM and their practical implementations using Python.

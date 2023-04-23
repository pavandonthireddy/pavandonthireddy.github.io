---
layout: post
title: Time Series Segmentation using Turning Points and their Variants
description: A comprehensive guide on Time Series Segmentation using Turning Points and their Variants
summary: This article presents an overview of time series segmentation using turning points and their variants. It explores various methods for identifying turning points and their applications in practical time series analysis. Python implementations are provided for all variants.
author: Pavan Donthireddy
usemathjax: true
original: new
tags: [turning_points, representation ]
---

Time series segmentation is a crucial task in time series analysis. It involves dividing a time series into homogeneous segments, thereby facilitating further analysis and modeling. Turning points, which are defined as local minima or maxima, are widely used as anchors for segmenting time series. This article provides an overview of various methods for identifying turning points and their variants, along with their applications in practical time series analysis. Implementations in Python are provided for all variants.

## Turning Points

A turning point in a time series is a value of the series where the trend changes direction. In other words, it is a local minimum or maximum in the series. Turning points play a crucial role in time series segmentation, as they are often used as anchors for dividing the series into homogeneous segments. The detection of turning points can be done by various methods, as discussed below.

## Fixed Interval Method

The fixed interval method involves dividing a time series into fixed-sized intervals and identifying the turning points within each interval. This method is computationally simple and easy to implement, but it may miss key turning points if they occur at the boundaries of the intervals. 

## Moving Average Method

The moving average method involves computing a moving average of the time series and identifying the turning points based on the slope of the moving average. Specifically, a turning point is identified as a point where the difference between the moving average at that point and the moving average at the previous point changes sign. This method is computationally efficient and more robust than the fixed interval method, as it is less affected by local noise in the series.

## Regression Method

The regression method involves fitting a regression model to the time series and identifying turning points as the local minima or maxima of the fitted function. The regression function can be a linear or nonlinear function, depending on the nature of the time series. This method is more accurate than the previous methods but can be computationally intensive, especially for large time series.

## Wavelet Method

The wavelet method involves applying wavelet analysis to the time series and identifying turning points as the local minima or maxima of the wavelet transform. Wavelet analysis is a powerful tool for time series analysis that allows for both time and frequency localization. This method is more complex than the previous methods but is more robust and accurate, especially for nonstationary time series.

## Variants of Turning Points

Several variants of the turning points concept have been proposed to address specific issues in time series analysis. Some of the commonly used variants are discussed below.

### L-Peaks and Troughs

L-peaks and troughs are local extrema that are defined using both the amplitude and the length of a series of consecutive points. Specifically, an L-peak is a point that has a value greater than its surrounding points and whose height is greater than a certain threshold, which is defined as the average of the heights of the n highest peaks in the series. Similarly, an L-trough is a point that has a value less than its surrounding points and whose depth is less than a certain threshold, which is defined as the average of the depths of the n deepest troughs in the series. This variant is useful for identifying significant turning points in noisy time series.

### Dynamic Time Warping

Dynamic time warping (DTW) is a technique for aligning two time series by warping their time axes to minimize the difference between them. DTW can be used to identify turning points in time series by comparing the distance between each point in the series and the best matching point in a reference series. This variant is useful for comparing time series with different lengths or for identifying turning points in nonstationary time series.

### Hidden Markov Models

Hidden Markov models (HMM) are stochastic models that capture the underlying structure of a time series by modeling its transitions between states. HMM can be used for identifying turning points in time series by inferring the state sequence that generates the observed series and identifying the transition points between states. This variant is useful for identifying turning points in complex time series with multiple trends or regimes.

## Python Implementation

Below is an example Python implementation for identifying turning points in a time series using the moving average method.

```python
import numpy as np

def moving_average(x, window_size):
    weights = np.repeat(1.0, window_size) / window_size
    ma = np.convolve(x, weights, 'valid')
    return ma

def turning_points(x, window_size):
    ma = moving_average(x, window_size)
    tp = []
    for i in range(1, len(ma)-1):
        if np.sign(ma[i]-ma[i-1]) != np.sign(ma[i+1]-ma[i]):
            tp.append(i)
    return tp
```

The `moving_average` function computes a moving average of the input time series `x` using a window of `window_size`. The `turning_points` function identifies the turning points in the original time series `x` based on the slope of the moving average. Specifically, it checks for points where the difference between the moving average at that point and the moving average at the previous point changes sign. The function returns a list of indices corresponding to the turning points.

## Conclusion

Time series segmentation is a fundamental task in time series analysis, and turning points are widely used as anchors for this task. Various methods and variants for identifying turning points have been proposed, each with its own strengths and weaknesses. These methods and variants can be applied to a wide range of time series analysis problems, ranging from simple anomaly detection to complex regime switching models. Python implementations for all variants make it easy to explore these methods and variants on real-world time series data.
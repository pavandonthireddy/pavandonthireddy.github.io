---
layout: post
title: PCA-ICA-for-fault-detection-1d-timeseries
description: How to apply ICA, PCA for fault detection from single sensor?
summary: How to apply ICA,PCA for fault detection from single sensor?
author:
- Pavan Donthireddy
usemathjax: true
tags: [ICA, faultdetection, wavelet, PCA, sensors, preprocessing]
---

### Idea
<p align="justify">Principal component analysis (PCA) isa method that transforms multiple data series into uncorrelated data series. Independent component analysis (ICA) is a method that separates multiple data series into independent data series. Both methods have been used in fault detection. However, both require signals from at least two separate sensors. To overcome this requirement and utilize the fault detection capability of ICA and PCA, we propose to use wavelet transform to pre-process the data collected from a single sensor and then use the coefficients of the wavelet transforms at different scales as input to ICA and PCA. </p>


<p align="justify">Independent components analysis (ICA) requires little prior knowledge about the components to be isolated; however, at least two sensors must be available for signal collection and the number of sensors must be at least equal to the number of sources to be separated and this method cannot be applied directly when there is only one sensor collecting signals.</p>

<p align="justify">Principal component analysis (PCA) is a multivariate data analysis technique that transforms a set of correlated variables into a set of uncorrelated variables. Each member of the resulting set of uncorrelated variables is called a principal component. We are interested in determining its suitability for fault detection because one of the identified principal components may reveal the signature of a hidden fault. As with ICA, however, this method cannot be applied directly when only a single variable is observed.</p>

Wavelet transform may be considered as a series of band pass filters when applied to the data
collected from a single sensor. The results of the transform, which exist in different frequency
regions, say $N$ regions, may be considered as different mixtures of the sources that have
generated the collected signals.These $N$ groups of data can then be used as input to ICA or PCA
for identification of the hidden sources.


### ICA and PCA

ICA is a technique for separating independent sources linearly mixed in signals. Suppose that
there are $N$ independent sources of vibration, and $N$ sensors at different locations are used to
record vibration signals. The signals recorded by each sensor come from different sources with
different mixing ratios. Let $s_{1}(t),s_{2}(t),  \dots ,s_{N}(t)$ be the signals produced by the $N$ independent
sources and $x_{1}(t),x_{2}(t),  \dots ,x_{N}(t)$ be the observations from the $N$ sensors. The sensors record these signals simultaneously. The task of ICA is to estimate the mixing ratios of the source signals in the collected signals and obtain the independent source signals.

<p align="justify">To identify the independent components successfully, we need a rule for evaluating the
independency of the identified components. According to the Central Limit Theorem, the
distribution of the sum of a large number of independent random variables tends to a Gaussian
distribution. Since the collected signals are weighted sums of the independent sources, the sources
to be isolated must have less Gaussianity than the collected signals. Thus, non-Gaussianity can be
used for separating independent components. Hyvarinen and Oja proposed to use negentropy
to evaluate the non-Gaussianity of the separated components so as to evaluate separation
performance. With this concept, we can seek the separation that provides the least Gaussianness of the separated components. The popular FastICA algorithm proposed by Havarinen and Oja
isoften used to carry out the ICA procedure.</p>

PCA is a technique that obtains linear transformations of a group of correlated variables such
that the transformed variables are uncorrelated. For example, consider two variables, $x_{1}$ and
$x_{2}$. For each variable, we have obtained the following $N$ observations:
$$x_{11}, x_{12}, \dots , x_{1N}; x_{21}, x_{22}, \dots; x_{2N}$$
where $x_{1i}$ and $x_{2j}$ denote the $i^{th}$ and the $j^{th}$ observations of variables $x_{1}$ and $x_{2}$, respectively. The PCA method seeks two new axes, D1 and D2, that make the projectionsof the collected data onto
D1 have the largest variability and at the same time, the projections of the collected data onto D2
have the smallest variability. This way, we have expressed the collected data as their two principal
components. Most of the variation in the original data is explained by the first principal
component, D1, and the remaining variation in the original data isexplained by the second
principal component, D2.
<p align="justify">
ICA renders the separated components independent of one another while PCA rendersthe
separated components uncorrelated with one another. PCA separates the components based only
on the second-order cumulant while ICA separates the components on high-order cumulants.
Therefore, ICA can be considered a generalization of PCA.</p>

### Method of preprocessing to apply ICA or PCA on 1D Time series

The available data is a single time series. To apply ICA or PCA for feature extraction, we need
to have more than one time series. A method to generate multiple time series from the single available time series is given below.

Wavelet transform decomposes a signal series in the time domain into a two-dimensional
function in the time-scale (frequency) plane. The wavelet coefficients measure the time-scale (frequency) content in a signal indexed by the scale parameter and the translation parameter. Let
$\varphi(t)$ be the mother wavelet. The wavelet family consists of a series of daughter wavelets that are
generated by dilation and translation from the mother wavelet $\varphi(t)$

$$
\varphi_{a, b}(t)=\sqrt{|a|} \varphi[(t-b) / a]
$$

where $a$ is the scale parameter, $b$ isthe location parameter, and $\sqrt{  |a|}$
isused to guarantee energy preservation. The wavelet transform of signal $x(t)$ isdefined as the inner product of $\varphi_{a, b}(t)$ and $x(t)$ in the Hilbert space of $L^2$ norm defined as:

$$
W(a, b)=\left\langle\varphi_{a, b}(t), x(t)\right\rangle=\int x(t) \varphi_{a, b}^*(t) \mathrm{d} t
$$

where the symbol * stands for the complex conjugate.

Wavelet transform can be thought of as a series of band pass filters. The results of the
transform, which exist in different frequency regions, may be thought of as different mixtures of the independent sources. These different mixtures may be considered to be signals collected at
different ‘‘locations’’, or more accurately, through different ‘‘sensors’’ with different frequency
ranges. This way, the one-dimensional signal is transformed into multidimensional data
that satisfy the requirements of ICA and PCA. The preprocessing of the one-dimensional data with wavelet transform makes ICA and PCA usable for identification of a hidden
source.

![Flowchart](/assets/snips/img1.png)

### Reference :
Feature separation using ICA for a one-dimensional time series and its application in fault detection - Ming J. Zuo, Jing Lin, Xianfeng Fan
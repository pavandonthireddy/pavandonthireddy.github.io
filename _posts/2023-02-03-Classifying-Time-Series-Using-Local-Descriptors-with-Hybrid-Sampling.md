---
layout: post
title: Classifying Time Series Using Local Descriptors with Hybrid Sampling
description: Classifying Time Series Using Local Descriptors with Hybrid Sampling
summary: Classifying Time Series Using Local Descriptors with Hybrid Sampling
author:
- Pavan Donthireddy
usemathjax: true
tags: [classification, timeseries, GMM, representation]
original: zhao2016
---

## Abstract

<p align="justify">Time series classification (TSC) arises in many fields and has a wide range of applications. Here, we adopt the bag-ofwords
(BoW) framework to classify time series. Our algorithm first samples local subsequences from time series at feature-point
locations when available. It then builds local descriptors, and models their distribution by Gaussian mixture models (GMM), and at last it
computes a Fisher Vector (FV) to encode each time series. The encoded FV representations of time series are readily used by existing
classifiers, e.g., SVM, for training and prediction. In our work, we focus on detecting better feature points and crafting better local
representations, while using existing techniques to learn codebook and encode time series. Specifically, we develop an efficient and
effective peak and valley detection algorithm from real-case time series data. Subsequences are sampled from these peaks and
valleys, instead of sampled randomly or uniformly as was done previously. Then, two local descriptors, Histogram of Oriented Gradients
(HOG-1D) and Dynamic time warping-Multidimensional scaling (DTW-MDS), are designed to represent sampled subsequences. Both
descriptors complement each other, and their fused representation is shown to be more descriptive than individual ones. We test our
approach extensively on 43 UCR time series datasets, and obtain significantly improved classification accuracies over existing
approaches, including NNDTW and shapelet transform.</p>

## Introduction

A typical BoW framework consists of three major steps:

1. local feature points detection and description, 
2. codebook generation and 
3. signal encoding.

Afterwards, any classifier can be trained on signal encodings to do the final classification. 

The performance of a BoW framework implementation depends on all steps. In the computer vision community, many efforts have been made to improve each step.

Regarding local feature detection and description, successful feature extractors (e.g., SIFT, Space Time Interest Points (STIPs)) have been developed to detect local feature points, and manually-crafted descriptors (e.g., Histogram of Gradients, Motion Boundary Histogram (MBH))
have been invented to represent local 2D image patches and 3D visual cuboid patterns around feature points. 

However, as reviewed below, fewer developments have been made with 1D time series descriptors. The next step, codebook generation, attempts to model the local descriptor space and to provide a partition in that space. Two typical ways are K-means and Gaussian Mixture Models (GMM). For the
last step, encoding, there is a large family of research studies; several representative encoding methods are vector quantization (hard voting) , sparse coding and Fisher Vector encoding . 

In this work, we adopt the BoW pipeline: we focus on improving the first step: designing better
local feature extractors and descriptors, while using existing techniques for the second and third steps; specifically, GMM is used to produce the codebook and Fisher Vector is employed to encode the time series.

While local feature extractors are well studied in the computer vision community, in the time series community, no widely used extractors exist yet, such that most methods sample feature points either uniformly or randomly. In this paper, we introduce an efficient and effective feature point
extractor, which detects all peaks and valleys, termed as landmarks, from time series. Afterwards, subsequences centered on landmarks are sampled. Landmark-based sampling gives deterministic and phase-invariant subsequences, while uniformor random sampling are affected by the phase of the time series. 

<p align="justify">Due to the observation that dense sampling outperforms sparse interest-points sampling in image classification and activity recognition, in experiments, we
adopt a hybrid sampling strategy: first sample subsequences
from landmarks, then sample uniformly in “flat” featureless
regions of the signal. In this way, information from both feature-
rich and feature-less intervals is incorporated in the
sampled subsequences. We show experimentally that this
new hybrid sampling strategy outperforms both uniform
and random sampling significantly.</p>
<p align="justify">To the best of our knowledge, little recent literature on
time series classification is focused on developing better
local descriptors for local time series subsequences. Commonly
used local features are often simple, including mean,
variance and slope. However, statistical features
like mean and variance cannot characterize local segment
shapes well. </p>

<p align="justify">Although slope incorporates shape information,
it will underfit the shape of local subsequences if the
interval (here, a subsequence is divided into equal-length
non-overlapping temporal intervals and represented as a
sequence of slopes of intervals) is too long, and becomes sensitive
to noise if the interval is too short. Symbolic Aggregate
approXimation (SAX) is shown be a good representation
for time series, however, its usage in a BoW framework
creates a large codebook, resulting in high-dimensional
encoding vectors for time series, which inevitably enburdens
downstream classifier training and prediction. </p>
<p align="justify">
Other widely
used and somewhat older time series representations
include Discrete Fourier Transform (DFT) coefficients, Discrete
Wavelet Transform (DWT), piecewise linear approximation
(PLA), etc. It is important to clarify that SAX, DFT,
DWT and PLA have been used in general to represent the
whole time series, instead of local subsequences.</p>

<p align="justify">In our work, we propose two new local descriptors,
namely Histogram of Oriented Gradients (HOG) of 1D time
series (HOG-1D) and Dynamic time warping-multidimensional
scaling (DTW-MDS), which are shown experimentally
to be quite descriptive of local subsequence shapes.
These two descriptors have individual advantages: HOG-
1D consists of statistical histograms, therefore is robust to
noise. Moreover, HOG-1D is invariant to y-axis magnitude
shift. While DTW-MDS is sensitive to noise and magnitude
shift, it is more invariant to stretching, contraction and
temporal shifting. Two descriptors thus complement
each other. By fusing them into a single descriptor, the
fused one, HOG-1D+DTW-MDS, combines the benefits of
both descriptors, becomes more descriptive of subsequences,
and thus is more discriminative for classification tasks.</p>

<p align="justify">Experimental results show that our fused descriptor outperforms
existing descriptors, such as DFT, DWT and Zhang’s significantly on 43 UCR datasets for time series
classification. Here DFT, DWT and Zhang’s are used to represent
local subsequences, instead of the whole time series.
All local descriptors, including our fused one, work under
the same classification pipeline: (1) feature points extraction,
(2) local subsequence representation, (3) time series encoding
by Fisher Vector, (4) linear kernel SVM classification. In
addition, we compare TSC performance of our fused
descriptor with two state-of-the-art algorithms, NNDTW
and shapelet transform, on 41 UCR datasets, and ours
achieves the best performance on 22 of them (including
ties).</p>


<p align="justify">Wilcoxon signed rank test on relative accuracy boost shows our fused descriptor
improves relative classification accuracies significantly compared
to NNDTW (p < 0.0017) and shapelet transform
(p < 0.0452). Our algorithm performs well on UCR datasets,
which have fixed length time series instances, however,
our algorithm is also applicable to datasets with variable
length time series instances, since Fisher Vector is essentially
a normalized encoder, making encodings largely
invariant to time series length.
</p>

<p align="justify">Our contributions are several fold: (1) we introduce a
simple but effective feature point extractor, which detects a
set of landmarks from time series; (2) we explicitly design
two local subsequence descriptors, namely HOG-1D and
DTW-MDS, which are descriptive of local shapes and complement
each other; (3) we obtain significantly improved
classification accuracies using our fused descriptor when
compared with two competing state-of-the-art TSC algorithms,
NNDTW and shapelet transform, and three existing
descriptors, DFT, DWT and Zhang’s, on 43 UCR datasets.</p>



2 PREVIOUS WORK
Time series classification methods can be categorized into
instance-based, shapelets, feature-based and pattern frequency
histogram methods.
Instance-based methods predict labels of test time series
based on their similarity to the training instances. The most
popular similarity metrics include euclidean distance and
elastic distances, e.g., the dynamic time warping (DTW)
distance. Using a single nearest neighbor, with euclidean
distance (NNEuclidean) or DTW distance (NNDTW), has
demonstrated successful time series label prediction. DTW
allows time series to be locally shifted, contracted and
stretched, and lengths of time series hence need not be the
same. Therefore, DTW usually gives a better similarity
measurement than Euclidean distance, and NNDTW has
been shown to be very hard to beat on many datasets [11].
A number of more complex elastic distance measures have
been proposed, including longest common subsequences
(LCSS) [27], Edit distance with Real Penalty (ERP) [28]
and edit distance on Real Sequence (EDR) [29]. However,
in [30], the authors claimed that no other elastic distance
measure outperforms DTW by a statistically significant
amount, and DTW is the best measure. Instance-based
approaches, like NN-euclidean and NNDTW, are accurate,
but they are less interpretable, since they are based on
global matching and provide limited insights into the temporal
characteristics.





---
layout: post
title: Whitening and Quasi Whitening
description: Whitening and Quasi Whitening
summary: Whitening and Quasi Whitening
author:
- Pavan Donthireddy
usemathjax: true
tags: [BlindSourceSeperation, whitening, preprocessing]
original: new
---

## Quasi-Whitening of Sensor Matrices

In signal processing and machine learning, sensor matrices are often used to represent high-dimensional data collected from sensors. These matrices can be analyzed using techniques such as independent component analysis (ICA) or principal component analysis (PCA), but these methods often assume that the samples are uncorrelated and have unit variance. Quasi-whitening is a preprocessing technique that can transform a given sensor matrix into a form that has these desirable statistical properties.

The goal of quasi-whitening is to transform the sensor matrix in such a way that the samples become uncorrelated and have unit variance. This can help improve the performance of algorithms that rely on these statistical properties. The term "quasi" refers to the fact that the transformed matrix is not perfectly whitened, meaning that the samples are not completely uncorrelated and do not have exactly unit variance. However, the transformation is still useful because it can significantly reduce the correlation among the sensor samples, making them more suitable for subsequent analysis.

One common technique for quasi-whitening a sensor matrix is to use a preprocessing step called "decorrelation," which involves applying a matrix transformation to the original sensor matrix to eliminate correlations among the samples. After decorrelation, the transformed matrix can be further scaled so that each sample has unit variance.

The decorrelation transformation can be achieved using the following equation:

$$X' = DX$$

where $X$ is the original sensor matrix, $D$ is a decorrelation matrix, and $X'$ is the transformed matrix. The decorrelation matrix $D$ is typically computed using the eigenvalue decomposition of the sample covariance matrix of $X$. Specifically, if the sample covariance matrix of $X$ is denoted by $C$, then $D$ can be computed as:

$$D = C^{-1/2}$$

where $C^{-1/2}$ is the matrix inverse square root of $C$. This transformation has the property that the transformed matrix $X'$ has a sample covariance matrix that is approximately equal to the identity matrix.

After decorrelation, the transformed matrix $X'$ can be further scaled so that each sample has unit variance. This is achieved using the following equation:

$$X'' = \frac{X'}{\sqrt{\mathrm{diag}(X'^TX')}}$$

where $\mathrm{diag}(A)$ denotes the diagonal elements of matrix $A$. This transformation scales each sample so that it has unit variance, while preserving the decorrelation achieved by the earlier transformation.

In summary, quasi-whitening is a useful preprocessing technique for improving the performance of signal processing and machine learning algorithms that rely on uncorrelated and unit variance samples. By decorrelating and scaling the sensor matrix, quasi-whitening can reduce the impact of correlations among the samples and make them more suitable for subsequent analysis.


# Whitening for Blind Source Signal Separation

In many applications such as speech recognition and biomedical signal processing, it is common to encounter signals that are mixtures of multiple sources. Blind source separation (BSS) is the problem of separating these sources from their mixture without any prior knowledge of the sources or the mixing process. One technique used for BSS is whitening, which transforms the mixture to a new space where the sources are uncorrelated and have unit variance. 

## Whitening

Whitening is a linear transformation that maps a random vector $\mathbf{x} \in \mathbb{R}^n$ with covariance matrix $\mathbf{\Sigma}$ to a new vector $\mathbf{y} \in \mathbb{R}^n$ with identity covariance matrix, i.e.,

$$\mathbf{y} = \mathbf{W} \mathbf{x},$$

where $\mathbf{W}$ is a square matrix such that $\mathbf{W}\mathbf{\Sigma}\mathbf{W}^T = \mathbf{I}$, where $\mathbf{I}$ is the identity matrix.

To see why this is useful for BSS, consider a mixture of $m$ sources:

$$\mathbf{x}(t) = \sum_{i=1}^m s_i(t) \mathbf{a}_i,$$

where $\mathbf{a}_i$ is the mixing matrix for the $i$th source, and $s_i(t)$ is the signal of the $i$th source at time $t$. We assume that the sources are statistically independent and have zero mean and unit variance. The covariance matrix of $\mathbf{x}$ is then

$$\mathbf{\Sigma}_x = \mathbb{E}[\mathbf{xx}^T] = \sum_{i=1}^m \mathbf{a}_i \mathbf{a}_i^T.$$

To separate the sources, we want to find a matrix $\mathbf{B}$ such that

$$\mathbf{y}(t) = \mathbf{B} \mathbf{x}(t) = \sum_{i=1}^m b_i s_i(t) \mathbf{e}_i,$$

where $\mathbf{e}_i$ is the $i$th canonical basis vector. The covariance matrix of $\mathbf{y}$ is then

$$\mathbf{\Sigma}_y = \mathbb{E}[\mathbf{yy}^T] = \mathbf{B} \mathbf{\Sigma}_x \mathbf{B}^T.$$

If we choose $\mathbf{B} = \mathbf{W}^{-1}$, then we have

$$\mathbf{\Sigma}_y = \mathbf{W}^{-1} \mathbf{\Sigma}_x (\mathbf{W}^{-1})^T = \mathbf{W}^{-1} \mathbf{W} \mathbf{\Sigma}_s \mathbf{W}^T (\mathbf{W}^{-1})^T = \mathbf{I},$$

where $\mathbf{\Sigma}_s$ is the diagonal matrix of the variances of the sources.

Thus, by whitening the mixture with $\mathbf{W}$, we transform the problem of BSS into a problem of finding a linear transformation that makes the sources uncorrelated.


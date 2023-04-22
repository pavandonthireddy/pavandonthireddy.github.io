---
layout: post
title: A Blind Source Separation Method Based on the Time Delayed Correlations and the Wavelet Transform
description:  A Blind Source Separation Method Based on the Time Delayed Correlations and the Wavelet Transform
summary:  A Blind Source Separation Method Based on the Time Delayed Correlations and the Wavelet Transform
author:
- Pavan Donthireddy
usemathjax: true
tags: [BlindSourceSeperation, wavelet]
original: zhao2006
---

## Abstract

<p align="justify">Blind source separation method based on
generalized eigendecomposition of time delayed
correlation matrices in the wavelet domain is proposed.
The wavelet domain algorithm can separate the
mixtures when the number of the sources is more than
three, while the time domain algorithm can’t. The
proposed method is a fast, stable and easy to
implement algorithm. The computer simulations
results demonstrate the correctness and effectiveness
of the proposed algorithm.
</p>

Blind source separation(BSS) addresses the problem of recovering a set of source signals( $\mathbf{s})$ from sensor signals $(\mathbf{x})$ only with the assumption that the source signals are mutually statistically independent. When the sensor signals are assumed to follow a linear mixture model, i.e., $\mathbf{x}=\mathbf{A s}$, where $\mathbf{A}$ is the mixing matrix, the problem is to find a separation matrix to estimate the source signals. Here assume that the number of sensor signals is equal to the number of source signals. The BSS problem has been paid wide attention in various fields such as signal analysis and processing of speech, image and biomedical signals, especially, signal extraction, enhancement and denoising problems.

One of the solutions for the blind source separation problem is based on the generalized eigendecomposition(GED) of a matrix pencil $\left(\mathbf{R}_{x 1}, \mathbf{R}_{x 2}\right)$ formed with correlation matrices $\mathbf{R}_{x i}$, $i=1,2$, computed with the sensor signals, the transpose of the eigenvector matrix is the estimation of the separation matrix. There are many different approaches to compute the correlation matrices. Souloumiac considers two segments of sensor signals with distinct energy, Molgedey and Tomé consider filtered versions of the sensor signals to compute the correlation matrices, while Schuster and Chang et al. compute time delayed correlation matrices. In this paper we study a BSS algorithm based on the generalized eigendecomposition of the matrix pencil computed with time delayed correlation matrices in the wavelet domain. The gaussianity of the signals in the wavelet domain is weaker than that in the time domain, so the performance of the BSS algorithm in the wavelet domain is better than that in the time domain algorithm.

### The generalized eigendecomposition

The solution for the blind source separation problem is based on the generalized eigendecomposition of the matrix pencil $\left(\mathbf{R}_{x 1}, \mathbf{R}_{x 2}\right)$.The generalized eigendecomposition statement of the sensor pencil reads
$$
\mathbf{R}_{x 2} \mathbf{E}=\mathbf{R}_{x 1} \mathbf{E} \mathbf{D}
$$
where $\mathbf{E}$ is the eigenvector matrix and $\mathbf{D}$ is a diagonal matrix with the eigenvalues of the sensor pencil. $\mathbf{E}$ will be unique if $\mathbf{D}$ has distinct eigenvalues. Otherwise the eigenvectors which correspond to the same eigenvalue might be substituted by their linear combinations without affecting the previous equality. So, supposing that the diagonal elements of $\mathbf{D}$ are all distinct.
The sensor pencil is related to a pencil $\left(\mathbf{R}_{s 1}, \mathbf{R}_{s 2}\right)$ computed with the source signals via the mixing matrix as described by the following relations
$$
\mathbf{R}_{x 1}=\mathbf{A} \mathbf{R}_{s 1} \mathbf{A}^T \text { and } \mathbf{R}_{x 2}=\mathbf{A} \mathbf{R}_{s 2} \mathbf{A}^T
$$
According to Parlett ,two pencils related as described by Eq.(2) are called congruent pencils if $\mathbf{A}$ is an invertible matrix, then

*Proposition.* The eigenvectors of the source pencil are related to the eigenvectors of the sensor pencil by the mixing matrix,
$$
\mathbf{E}_s=\mathbf{A}^T \mathbf{E}
$$
where $\mathbf{E}_s$ is the eigenvector matrix of the source pencil. We can see from Eq.(3) that the transpose of the eigenvector matrix of the sensor pencil $\mathbf{E}^T$ forms the separation matrix, i.e.,
$$
\hat{\mathbf{S}}=\mathbf{W} \mathbf{X}=\mathbf{E}^T \mathbf{X}
$$
if $\mathbf{E}_s$ is a diagonal or permutation matrix. Then $\hat{\mathbf{S}}$ will be an estimation of the source signals except for the usual scaling and ordering indeterminacies.

Similar results are achieved if the number of mixtures is higher than the number of sources.
There are different suggestions to compute the sensor matrix pencil. It can be shown that a pencil of correlation matrices computed with different time delay of the sensor signals has a congruent pencil in source domain as described by Eq.(2). Let $\mathbf{X}$ be a $m \times N$ matrix containing a segment with $N$ samples of each of $m$ sensor signals. The time delayed correlation matrix is the correlation of the delayed data with the original data ${ }^{[2]}$, then $\mathbf{R}_{x i}$ for a delay $d_i$ can be written as
$$
\mathbf{R}_{x i}=\frac{1}{N-d_i} \mathbf{X H}^T \mathbf{X}^T
$$
where $\mathbf{H}$ has only one nonzero diagonal which is the $d_i$ th diagonal lower than the main diagonal, if $d_i=0, \mathbf{H}$ will be the identity matrix. The corresponding time delayed correlation matrix of the source signals is
$$
\mathbf{R}_{s i}=\frac{1}{N-d_i} \mathbf{S H}^T \mathbf{S}^T
$$
Substituting $\mathbf{x}=$ As in Eq. (5)
$$
\mathbf{R}_{x i}=\frac{1}{N-d_i} \mathbf{A} \mathbf{S} \mathbf{H}^T \mathbf{S}^T \mathbf{A}^T
$$
It is easy to see from Eqs.(6) and (7) that the sensor pencil $\left(\mathbf{R}_{x 1}, \mathbf{R}_{x 2}\right)$ is congruent to the source pencil $\left(\mathbf{R}_{s 1}, \mathbf{R}_{s 2}\right)$ as defined in Eq.(2). The pair of matrices computed for different time delays forms a pencil whose eigenvalues are distinct.
3. Bss algorithm based on the wavelet transform

The wavelet transform maps a signal from the time domain to the time-scale domain. The transformation makes the gaussianity of the signals become weaker, and it is very useful for blind source separation problem, as will be analyzed in the next section. A basic wavelet function is defined, called the mother wavelet, which is translated and dilated, resulting in a set of orthonormal wavelet basis functions ${ }^{[6]}$.Then, the wavelet transform of a signal is given by the inner product of the signal with each of the basis function. Discrete wavelets are defined as
$$
\psi_{j, q}(k)=2^{-j / 2} \psi\left(2^{-j} k-q\right)
$$
where $j, q \in \mathrm{Z}$, and $\mathrm{Z}$ denotes the field of integers, and the wavelet transform of a signal $x(k)$ is given by
$$
c_{j, A}=\left(x(k), \psi_{j, A}(k)\right)
$$
where $c_{j, q}$ denotes the transform coefficients, and $(\cdot, \cdot)$ represents the inner product. Denote $W\{\}$ and $W^{-1}\{\}$ the forward and reverse discrete wavelet


transform(DWT) operators. Taking the wavelet transform of the vector of the sensor signals, then the wavelet coefficients matrix $\mathbf{C}_x$ of the sensor signal $\mathbf{X}$ is given by
$$
\mathbf{C}_x=W\{\mathbf{X}\}
$$
so, each row of $C_x$ is the wavelet coefficients of the corresponding row of $\mathbf{X}$. Then the correlation matrix of the time delay of the wavelet coefficients is
$$
\mathbf{R}_{c_x}=\frac{1}{N-d_i} \mathbf{C}_x \mathbf{H}^T \mathbf{C}_x^T
$$
Using the linearity property of the inner $\operatorname{product}^{[7]}$
$$
\begin{gathered}
((x(k)+z(k)), y(k))=(x(k), y(k))+(z(k), y(k)) \\
(\alpha x(k), y(k))=\alpha(x(k), y(k))
\end{gathered}
$$
when the mixing matrix $\mathbf{A}$ is real and time-invariant, the wavelet transform of the $i$ th sensor signal $x_i(k)$ in $\mathbf{x}=$ As is given by
$$
\begin{gathered}
W\left\{x_i(k)\right\}=W\left\{\sum_{l=1}^m a_{i l} s_l(k)\right\} \\
\left(x_i(k), \psi_{j, q}(k)\right)=\sum_{l=1}^m a_{i l}\left(s_i(k), \psi_{j, q}(k)\right)
\end{gathered}
$$
So, we obtain, in matrix form
$$
\mathrm{C}_x=\mathrm{AC}_s
$$
where $C_s$ is the wavelet coefficients matrix of the source signal, Eq.(16) has the same formulation with $\mathbf{x}=\mathbf{A s}$. So, it is easy to prove that the pencil $\left(\mathbf{R}_{c_{11}}, \mathbf{R}_{c_{12}}\right)$ has a congruent pencil $\left(\mathbf{R}_{c_{11}}, \mathbf{R}_{c_{12}}\right)$, as described by Eq.(2), where the pencil ( $\left.\mathbf{R}_{c_{t 1}}, \mathbf{R}_{c_{t 2}}\right)$ is computed by the wavelet coefficients of source signals. The generalized eigendecomposition of the pencil $\left(\mathbf{R}_{c_{x 1}}, \mathbf{R}_{c_{x 2}}\right)$ is
$$
\mathbf{R}_{c_{x 2}} \mathbf{E}_c=\mathbf{R}_{c_{x 1}} \mathbf{E}_c \mathbf{D}_c
$$
The transpose of the eigenvector matrix $\mathbf{E}_c{ }^T$ is an estimation of the separation matrix. So, the estimation of the wavelet coefficients of the independent components is
$$
\hat{\mathbf{C}}_s=\mathbf{E}_c^T \mathbf{C}_x
$$
The inverse wavelet transform of $\hat{C}_s$ represents the estimation of the source signals
$$
\hat{\mathbf{S}}=W^{-1}\left\{\hat{\mathbf{C}}_s\right\}
$$

## Note

To blind source separation problem, we can obtain the estimation of the source signals by making linear transformation to $x$ to maximize the non-gaussianity of each column of $x$. We use kurtosis as the measure of non-gaussianity of a random variable
$$
\operatorname{kurt}(x)=E\left\{x^4\right\}-3\left(E\left\{x^2\right\}\right)^2
$$
Where $E\{\}$ is the mean, the further away the probability density function of a random variable is from the Gaussian distribution, the further away is its kurtosis from zero. The kurtosis of the sensor signals and their wavelet coefficients are given in Table 4. It can be seen from Table 4 that the non-gaussianity of the sensor signals is weaker than that of its wavelet coefficients. So the separation performance of the wavelet domain algorithm is better than that of the time domain algorithm. This property is especially outstanding when the number of source signals is more than three.
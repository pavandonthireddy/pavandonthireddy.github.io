---
layout: post
title: SSA and its variants
description: SSA and its variants
summary: SSA and its variants
author:
- Pavan Donthireddy
usemathjax: true
tags: [SSA]
original: new
---

<p align="justify">Singular Spectrum Analysis (SSA) has proven to be a flexible
method for the analysis of time-series data. Applications are
reported in diverse areas such as climate change and geophysical
phenomena [13], mineral processing [4] and telecommunication
applications [5,6]. The basic SSA method has been combined with
the maximum entropy method (MEM) [7] and with multi-taper
methods [8] to enhance the spectral analysis of data. Extensions to
cope with missing data [9] and multi-scale applications have also
been developed [10].</p>

<p align="justify">The basic elements of SSA were first reported in [11,12].
Widespread use of SSA followed a series of papers by Vautard
and Ghil [2] and Vautard et al. [3]. The monograph by Golyandina
et al. [13] describes the basic algorithm plus a number of variations.</p>


## Basic SSA and some variations

### Basic SSA algorithm

The basic SSA algorithm consists of the following steps.
1. Choose an embedded dimension $K$ and define $L=N+1-K$, where $N$ is the number of observations in the time series.
2. Form the $L \times K$ Hankel matrix $\boldsymbol{A}$ using mean-corrected data, $y_t, t=1,2, \ldots, N$.
$$
\begin{aligned}
\boldsymbol{A} & =\left[\boldsymbol{y}_1, \boldsymbol{y}_2, \boldsymbol{y}_3, \ldots, \boldsymbol{y}_K\right] \\
& =\left[\begin{array}{cccccc}
y_1 & y_2 & y_3 & \cdots & \cdots & y_K \\
y_2 & y_3 & y_4 & \cdots & \cdots & y_{K+1} \\
y_3 & y_4 & y_5 & \cdots & \cdots & y_{K+2} \\
\vdots & \vdots & \vdots & & & \vdots \\
y_L & y_{L+1} & y_{L+2} & \cdots & \cdots & y_{K+L-1}
\end{array}\right]
\end{aligned}
$$

where $\boldsymbol{y}_i=\left(y_i, y_{i+1}, \ldots, y_{i+\mathrm{L}-1}\right)^T$. This matrix $\boldsymbol{A}$ is often referred to as the trajectory matrix. In most applications of SSA, $L>K[2,13]$
3. Determine the eigenvalues and eigenvectors of $A^T A$. Denote the eigenvalues by $\lambda_1 \geq \lambda_2 \geq \cdots \geq \lambda_K \geq 0$. For each eigenvalue $\lambda_i$ there is a corresponding eigenvector $v_i$.
$$
\left(A^T A\right) v_i=\lambda_i v_i
$$
4. Define $K$ new series, $\boldsymbol{w}_i=A v_i, i=1,2, \ldots, K$. Each series is of length $L$. Once the new series are constructed, the analysis then focuses on the new series, which are sometimes referred to as the latent variables. The individual series may be analyzed, or subsets may be grouped together.


The utility of the method is derived from the following properties and interpretations of the eigenvalue analysis:

(a) The eigenvectors $v_i$ are orthonormal, i.e., $v_i^T v_j=0(i \neq j)$ and $\boldsymbol{v}_i^T \boldsymbol{v}_i=1$.
(b) The latent variables $w_i$ are orthogonal, and
$$
\begin{aligned}
\left\|\boldsymbol{w}_i\right\|^2 & =\boldsymbol{w}_i^T \boldsymbol{w}_i=\left(\boldsymbol{A} \boldsymbol{v}_i\right)^T A \boldsymbol{v}_i=\boldsymbol{v}_i^{\mathrm{T}}\left(A^T A\right) v_i \\
& =\boldsymbol{v}_i^T \lambda_i v_i=\lambda_{\mathrm{i}} .
\end{aligned}
$$
(c) Consequently,
$$
\sum_{i=1}^K \boldsymbol{w}_i^T \boldsymbol{w}_i=\sum_{i=1}^K \boldsymbol{w}_i^T \sum_{i=1}^K \boldsymbol{w}_i=\sum_{i=1}^K \lambda_i .
$$
Often, the interesting features of a time series are found by analyzing the first few latent variables. A number of methods have been proposed to choose the number of latent variables for analysis. Most often, the construction of a scree plot [18], which is a plot of $\lambda_i$ versus $i$, will indicate a knee or bend. This can be used to select the number of latent variables. Other methods have been proposed when the break points are not clear [19].

Scree plots are also useful for identifying harmonics in the data. As discussed in $[2,12,14]$, if $N$ and $L$ are large enough, each harmonic results in two eigenvalues that are closely paired for a purely harmonic series. A harmonic component may produce a periodic component in the autocorrelation and partial autocorrelation function. However, the number of periodic components cannot be easily extracted from these functions. In addition, a slowly decreasing sequence of eigenvalues can be produced by a pure noise series $[13,14]$. These two observations suggest that a break or knee in the scree plot can be used to separate the signals that arise from harmonics and signals from noise or aperiodic components [13].

The eigenvalues of $A^T A$ are most often calculated by undertaking a singular value decomposition (SVD) of $A$. The right singular vectors of $A$ are identical with the eigenvectors of $A^T A$ and the eigenvalues of this latter matrix are the squares of the corresponding singular values of $\boldsymbol{A}[13]$.

### Variation: Toeplitz approximation to $A^T A$

$A^T A$ is symmetric and positive semi-definite. It can be written as
$$
A^T A=\left[\begin{array}{cccc}
y_1^T y_1 & y_1^T y_2 & \cdots & y_1^T y_K \\
y_2^T y_1 & y_2^T y_2 & \cdots & y_2^T y_K \\
\vdots & \vdots & & \vdots \\
y_K^T y_1 & y_K^T y_2 & \cdots & y_K^T y_K
\end{array}\right] \text {. }
$$
In situations when $L \gg K$, we have $$
\begin{aligned}
& \frac{1}{L} \boldsymbol{y}_1^T \boldsymbol{y}_1 \simeq \frac{1}{L} \boldsymbol{y}_2^T \boldsymbol{y}_2 \simeq \frac{1}{L} y_3^T y_3 \simeq \cdots \simeq \frac{1}{L} y_K^T y_K \simeq \frac{1}{N} \sum_{t=1}^N y_t^2=c_0 \\
& \frac{1}{L} \boldsymbol{y}_1^T \boldsymbol{y}_2 \simeq \frac{1}{L} y_2^T \boldsymbol{y}_3 \simeq \cdots \simeq \frac{1}{L} y_{K-1}^T y_K \simeq \frac{1}{N-1} \sum_{t=1}^{N-1} y_t y_{t-1}=c_1 \\
& \vdots \\
& \frac{1}{L} \boldsymbol{y}_1^T \boldsymbol{y}_K=\frac{1}{L} \sum_{t=1}^L y_t y_{t-(K-1)}=c_{K-1}
\end{aligned}
$$
where $c_i$ is the sample autocovariance at lag $i$ (we have previously assumed that the data have been mean corrected). Consequently
$$
\frac{A^{\mathbf{T}} A}{L} \simeq \boldsymbol{C}=\left[\begin{array}{cccc}
c_0 & c_1 & \cdots & c_{K-1} \\
c_1 & c_0 & \cdots & c_{K-2} \\
\vdots & \vdots & & \vdots \\
c_{K-1} & c_{K-2} & \cdots & c_0
\end{array}\right]
$$
where $C$ is the sample covariance matrix of the observations. The sample autocorrelation matrix $R=C / c_0$ is often used instead of $C$ for analysis. This is appropriate when the data have been centered and normalized $[12,20]$.

### Variation: Hankel approximation and diagonal averaging

A singular value decomposition of the matrix is undertaken
$$
\boldsymbol{A}=\sum_{i=1}^\mu \boldsymbol{X}_i=\sum_{i=1}^\mu \sqrt{\lambda_i} \boldsymbol{u}_i \boldsymbol{v}_i^T
$$
where $\mu=\min (L, K), \lambda_i$ and $v_i$ are the eigenvalues and eigenvectors of $A^T A$ as described in Eq. (1), and $\boldsymbol{u}_i$ are the eigenvectors of $A A^T$, i.e., the solution to $[21]$
$$
\left(\boldsymbol{A} \boldsymbol{A}^{\boldsymbol{T}}\right) \boldsymbol{u}_i=\lambda_i \boldsymbol{u}_i
$$
The orthogonal vectors $\boldsymbol{u}_i$ and $\boldsymbol{v}_i$ are related by
$$
A v_i=\sqrt{\lambda_i} \boldsymbol{u}_i, \quad i=1,2, \ldots, \mu
$$
where the singular values of $A$ are $\sqrt{\lambda_i}$, i.e., the square root of the eigenvalues of $A^T A$. Clearly, $u_i=w_i / \sqrt{\lambda_i}$.

Each of the $X_i$ in Eq. (4) is of rank 1 . A new series $x_i$ of length $N$ is reconstructed by averaging each of the $N$ anti-diagonals in $X_i$. Attention is then focused on the new series $x_i$, or groupings of these series. Guidelines for grouping of variables are typically based on the clustering and separation of the eigenvalues. A 'separability index' has been proposed in [14] to assist with grouping.

This diagonal averaging is computationally equivalent to calculating $x_i$ using [22]
$$
\boldsymbol{x}_i=\mathbf{D}^{-1} W_i v_i
$$
where

$$
W_i=\left(\begin{array}{cccccc}
w_1 & 0 & \cdots & \cdots & \cdots & 0 \\
w_2 & w_1 & 0 & \cdots & \cdots & 0 \\
w_3 & w_2 & w_1 & 0 & \cdots & 0 \\
\vdots & & \vdots & \vdots & & \vdots \\
w_{K-1} & \cdots & w_3 & w_2 & w_1 & 0 \\
w_K & \cdots & \cdots & w_3 & w_2 & w_1 \\
w_{K+1} & \cdots & \cdots & \cdots & w_3 & w_2 \\
\vdots & & & & & \vdots \\
w_{\mathrm{L}-1} & w_{\mathrm{L}-2} & \cdots & \cdots & \cdots & w_{\mathrm{L}-K} \\
w_{\mathrm{L}} & w_{\mathrm{L}-1} & w_{\mathrm{L}-2} & \cdots & \cdots & w_{\mathrm{L}-K+1} \\
0 & w_{\mathrm{L}} & w_{\mathrm{L}-1} & w_{\mathrm{L}-2} & \cdots & w_{\mathrm{L}-K+2} \\
\vdots & & \vdots & \vdots & & \vdots \\
0 & \cdots & 0 & w_{\mathrm{L}} & w_{\mathrm{L}-1} & w_{\mathrm{L}-2} \\
0 & \cdots & \cdots & 0 & w_{\mathrm{L}} & w_{\mathrm{L}-1} \\
0 & \cdots & \cdots & \cdots & 0 & w_{\mathrm{L}}
\end{array}\right)
$$
and $D$ is an $N \times N$ diagonal matrix, whose diagonal elements are
$\left(\begin{array}{lllllllllll}1 & 2 & \cdots & \mu-1 & \mu & \cdots & \mu & \mu-1 & \cdots & 2 & 1\end{array}\right)$
and $\boldsymbol{w}_i=\left(\begin{array}{llll}w_1 & w_2 & \cdots & w_L\end{array}\right)^T=A \boldsymbol{v}_i$, and $\boldsymbol{v}_i$ is one of the eigenvectors. To simplify the nomenclature, double subscripting on $w_i$ has been avoided. It is understood that the elements of this vector depend upon the specific eigenvector used in the reconstruction.
Recall that $N=L+K-1$ and $\mu=\min (L, K)=K$ in most SSA applications. Then there are $N-2(K-1)=2 L-N$ 'complete' rows with diagonal elements $\mu$ in $D$. The matrix $W_i$ is of dimension $N \times K$. The first and last $K-1$ rows are 'incomplete', which leaves $N-2(K-1)$ 'complete' rows.

The latent variables $w_i$ are orthogonal, and have squared norm $\left\|w_i\right\|_2^2=\lambda_i$. The squared norm of a reconstructed series using diagonal averaging is
$$
\begin{aligned}
\left\|\boldsymbol{x}_i\right\|_2^2 & =\left\|\boldsymbol{D}^{-1} \boldsymbol{W}_i \boldsymbol{v}_i\right\|_2^2 \\
& \leq\left\|D^{-1}\right\|_2^2 \cdot \operatorname{trace}\left(\boldsymbol{W}_i^{\mathrm{T}} \boldsymbol{W}_i\right) \\
& =K\left\|\boldsymbol{D}^{-1}\right\|_2^2 \cdot\left\|\boldsymbol{w}_i\right\|_2^2 \\
& =K \lambda_i\left\|D^{-1}\right\|_2^2 \\
& =\frac{K \lambda_i}{2\left(1+1 / 4+1 / 9+\cdots 1 /(K-1)^2\right)+(2 L-N) / K^2} \\
& \simeq \frac{K}{\pi^2 / 3+(2 L-N) / K^2} \lambda_i, \quad L \gg K
\end{aligned}
$$
and
$$
\left\|\sum_{i=1}^d \boldsymbol{x}_i\right\|_2^2 \neq \sum_{i=1}^d\left\|\boldsymbol{x}_i\right\|_2^2 \text {. }
$$
Calculations indicate that the upper bound may be quite conservative. The reconstructed series $\boldsymbol{x}_i$ are not orthogonal making it impossible to calculate the variance of grouped variables from the variance of the individual reconstructed series.

The use of reduced-rank approximations to assist in the extraction of harmonic signals from additive noise has been considered extensively in the signal processing literature. The trajectory matrix has a central role in these algorithms. Extensive research indicates that extraction of these signals is considerably enhanced when the trajectory matrix is replaced by a structured low-rank approximation. 

The SVD leads to an unstructured approximation, because the $X_i$ are not Hankel. A structured approximation is obtained when the trajectory matrix is calculated using the reconstructed series (or groupings of variables). While the SVD does not preserve the Hankel structure, the Hankel matrix constructed from the reconstructed series does not preserve the rank property. Cadzow developed a simple iterative algorithm to preserve both the rank and Hankel structure. He has shown that this iteration will converge to reduced-rank approximation that has the Hankel structure for certain classes of signals including sinusoids and damped sinusoids corrupted by white noise. The reconstruction of the $\boldsymbol{x}_i$ corresponds to one iteration of Cadzow's algorithm. Other approaches for obtaining reduced-rank approximations with appropriate structure involve the use of structured total least squares. These methods are computationally intense, requiring the use of a nonlinear optimizer in high dimension.



# Variants

SSA, or Singular Spectrum Analysis, is a time-series analysis technique that decomposes a time series into several components, such as trend, seasonal, and noise. Here are some variants or extensions of SSA:

1.  Multichannel SSA (M-SSA): This variant of SSA applies the decomposition to multivariate time series data, where each component is represented as a matrix.
    
2.  Ensemble SSA (ESSA): ESSA applies SSA to multiple time series data sets, with the goal of finding common patterns and extracting signals that are common across the ensemble.
    
3.  Spatial SSA (SpaSSA): This variant of SSA is used to analyze spatial data, such as satellite imagery or climate data, where each observation corresponds to a location in space.
    
4.  Complex SSA (CSSA): CSSA is used to analyze complex-valued time series data, where the components can have both real and imaginary parts.
    
5.  Local SSA (L-SSA): This approach applies SSA to a local region or window of a time series, instead of analyzing the entire time series. It can be useful for detecting local trends and patterns.
    
6.  Multilevel SSA (ML-SSA): ML-SSA decomposes a time series into multiple levels, each with a different time scale, allowing for the detection of patterns at different scales.
    
7.  Nonlinear SSA (NSSA): This approach applies SSA to nonlinear time series data, which can exhibit complex patterns and behaviors.
    

These variants of SSA can be used in different applications, depending on the nature of the data and the research question.
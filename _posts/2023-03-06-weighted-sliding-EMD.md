---
layout: post
title: Weighted Sliding Empirical Mode Decomposition for Online Analysis of Biomedical Time Series 
description: Weighted Sliding Empirical Mode Decomposition for Online Analysis of Biomedical Time Series 
summary: Weighted Sliding Empirical Mode Decomposition for Online Analysis of Biomedical Time Series
author:
- Pavan Donthireddy
usemathjax: true
tags: [EMD, online_algorithms]
original: zeiler2012
---

## Abstract 

<p align="justify">Biomedical signals are in general non-linear and non-stationary. empirical mode
decomposition in conjunction with a Hilbert-Huang Transform provides a fully adaptive and
data-driven technique to extract intrinsic mode functions. The latter represent a complete set
of locally orthogonal basis functions to represent non-linear and non-stationary time series.
Large scale biomedical time series necessitate an online analysis, which is presented in this
contribution. It shortly reviews the technique of EMD and related algorithms, discusses the
recently proposed weighted sliding EMD algorithm (wSEMD) and, additionally, proposes a
more sophisticated implementation of the weighting process. As an application to biomedical
signals we will show that wSEMD in combination with mutual information could be used to
detect temporal correlations of arterial blood pressure and intracranial pressure monitored at
a neurosurgical intensive care unit.We will demonstrate that the wSEMD technique renders
itself much more flexible than the Fourier based method used in Faltermeier et al.</p>


## Introduction
<p align="justify">
Recently an empirical nonlinear analysis tool for complex, non-stationary time series has
been pioneered by Huang et al. [6]. It is commonly referred to as empirical mode decomposition
(EMD) and if combined with Hilbert spectral analysis it is called Hilbert-Huang
Transform (HHT). It adaptively and locally decomposes any non-stationary time series into a
sum of intrinsic mode functions (IMF) which represent zero-mean amplitude and frequency
modulated (AM–FM) oscillatory components. The EMDrepresents a fully data-driven, unsupervised
signal decomposition technique and does not need any a priori defined basis system.
The empirical nature of EMD offers the advantage over other empirical signal decomposition
techniques like exploratory matrix factorization (EMF) [8] of not being constrained
by conditions which often only apply approximately. Especially with biomedical signals
one often has only a rough idea about the underlying modes and mostly their number is
unknown. Furthermore, large scale biomedical time series recorded over days necessitate an
online analysis [13], while EMD can analyze data only globally so far. This contribution
will review the technique of EMD and its recent extensions, propose an online EMD variant
called weighted sliding EMD (wSEMD) and discuss some biomedical applications related
to neuromonitoring. In the following we will denote by N the total number of time samples
tn in the time series, by M the size of a segment, by S the total number of segments and by
L the total number of IMFs into which the time series is decomposed in every segment.</p>

## Sliding EMD

### The Principle

This new technique presents an improved EMD algorithm which is suitable for online processing of non-stationary time series. Sliding $\operatorname{EMD}$ (SEMD) $[3,4]$ offers a robust and easy -to-implement solution to the problem of dealing with e.g. biomedical time series which often are recorded over long time spans with high sampling rate.
Using Sliding EMD the recorded time series is split into segments which can be analyzed with EMD. The segment size $M$ has to be a multiple of the step size $K$ with which the segments are shifted relative to each other. Thus, if $\frac{M}{K} \in \mathbb{N}$ holds, neighboring segments can be joined without resulting discontinuities or boundary artifacts. With this choice, every sample is represented equally often, i.e. $E=\frac{M}{K}$-times, in the overlapping segments for a later estimation of the corresponding mean sample value. The time series in every segment $s$ is decomposed by EMD into $L$ IMFs $x_{l, s}(t)$ and a local residuum $x_{L+1, s}(t) \equiv r_s(t)$ according to
$$
x_s(t)=\sum_{l=1}^L x_{l, s}(t)+r_s(t)
$$
whereby the number of sifting steps $L_s$ is kept equal in all segments $s$. Resulting IMFs are collected in a matrix with corresponding sample points forming a column of the matrix with $E=\frac{M}{K}$ entries. Only columns which contain an identical number of entries are used to estimate average IMF amplitudes at every time point $t_n$ in each segment. Consequently, the first and last $M$ samples of the time series are omitted. This finally yields:
For $t_n>M$ and $h=\left\lfloor\frac{t_n-M}{K}\right\rfloor+2:$
with $h \in \mathbb{N}$. By construction SEMD fulfills the condition to be complete, much as EMD does. Except for the stopping criterion, which here amounts to keeping the number of sifting steps $L_S$ constant, any EMD algorithm can be applied. Furthermore the number of IMFs has to be kept constant in every window e.g. according to $L=\left\lfloor\log _2 N\right\rfloor$. A schematic diagram of the SEMD procedure is presented in Fig. 1.

![[wsEMD.png]]

### Properties of SEMD

Because of the segmentation involved, contrary to global EMD the local residua estimated with SEMD for every segment when joined together may result in low-frequency oscillations instead in an average global residuum, as the residuum is only monotonous in every single window, but not in the resulting global residuum. By choosing the segment size properly, it may be determined which oscillations should appear as distinct IMFs and which should be absorbed as apparent local trends into the respective residua. 

<p align="justify">These apparent local trends,
which combine to low-frequency oscillations in the final average global residuum, may be
down-sampled, because of the high sampling rate, to a useful time resolution and subsequently
analyzed with SEMD again. This process can be repeated until finally a truly monotonous
trend remains. Hence, this cascaded application of SEMD acts as a low-frequency filter for
long-term oscillations and trends in biomedical time series.</p>


<p align="justify">Similar to ensemble empirical mode decomposition (EEMD) [11], also with Sliding EMD
an averaging over differently decomposed data sets is achieved. While due to added noise,
with EEMD a given sample is associated with different amplitudes, with sliding EMD the
same amplitude is associated with different samples in different shifted segments. This latter
behavior alleviates effects related with a non-unique data decomposition via EMD. Furthermore,
artifacts resulting from end effects loose their impact via averaging. Finally note that
while local IMFs fulfill all defining conditions, this is not necessarily true for the resulting
average IMFs though the related deviations should always be small.</p>

### weighted SEMD

Despite the averaging operations involved inSEMD,reconstruction errors due to the boundary
effects remain to be observed in SEMD.In order to diminish the impact of the latter, awSEMD
was developed recently. Every value of the ensemble of samples E, whose average
forms the final time series, is weighted by a coefficient drawn from a predefined distribution
of weights. These coefficients become larger when the estimated data point origins from
the middle of the window, and smaller when it is located near one of the boundaries. The
coefficients are assumed to form a discrete Gaussian distribution $p_{G}(E) (te)$ with E samples $e = 1, . . . , E$. Using such weights, boundary effects are strongly suppressed.

![[wsEMDex.png]]

### Improvement of the weighting process

In this subsection we consider an alternative way of applying weights to the time series to suppress boundary artifacts. It amounts to applying a weight to every sample of a window rather than weighting the estimates. Thus every window of the resulting IMFs and the residuum is multiplied by the weighting function. The latter, again, is assumed to form a discrete Gaussian distribution $p_G^{(M)}\left(t_m\right)$. But instead of weighting the estimates, every sample point inside the window is weighted according to its distance to the closest border of the window, which effectively suppresses samples near the boundaries. Therefore, the weighting function consists of $M$ samples, instead of $E$. Furthermore, the Gaussian distribution is shifted along the ordinate via $p_G^{(M)}\left(t_m\right)-p_G^{(M)}\left(t_1\right)$, so that $p_G^{(M)}\left(t_1\right)=0$ and $p_G^{(M)}\left(t_M\right)=0$, respectively.

This technique produces a more sophisticated and precise weighting of the estimates as several similar distributions $p_G^{(M)}\left(t_{m, e}\right), t_{m, e} \in[1, M]$ with $e=1, \ldots, E$ are utilized to weight the estimates. After the calculation of the ensemble mean of $K$ data points, every sample position $t_m, m=1, \ldots, M$, and therefore point of the weighting function of the window $p_G^{(M)}\left(t_m\right)$, has been used exactly once for averaging, as $K=\frac{M}{E}$ (see scheme in Fig. 3).

Hence $K$ shorter and slightly different distributions $p_G^{(M, i)}\left(t_{m, e}\right), i=1, \ldots, K$ are picked out of the weighting function and are used to weight the estimates, whereas all picked out samples for one ensemble weighting function have a distance of $K$ points respectively. The $K$ different distributions $p_G^{(M, i)}\left(t_{m, e}\right)$ can be described as 'part' of $p_G^{(M)}\left(t_m\right)$ using the following set of samples:
$$
\left\{p_G^{(M, i)}\left(t_{m, e}\right) \mid t_{m, e}=i+0 K, i+1 K, \ldots, i+(E-1) K\right\}
$$
To calculate the final result for a specific sample of an IMF or the residuum, the sum over $E$ estimates multiplied by $E$ weighting coefficients is computed and the value is normalized by the reciprocal sum of all used weights for that particular data point, so that the amplitude of the signal is preserved. For a step size of $K=1$ both methods, the weighted estimates and the weighted window SEMD, are the same, as $E=M$. Otherwise both approaches differ in that a specific set of weights for one data point is repeatedly used again-and only again-after $K$ samples. In the following, the improved wSEMD will be used for the further analyses.




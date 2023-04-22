---
layout: post
title: Adaptive Wavelet Packet thresholding with iterative kalman filter
description: Adaptive Wavelet Packet thresholding with iterative kalman filter
summary: Adaptive Wavelet Packet thresholding with iterative kalman filter
author:
- Pavan Donthireddy
usemathjax: true
tags: [wavelet,kalman, preprocessing, wavelet_thresholding]
original: zhao2017
---


## Abstract

<p align="justify">In this paper, we propose an adaptive wavelet packet (WP)
thresholding method with iterative Kalman filter (IKF) for
speech enhancement. The WP transform is first applied to
the noise corrupted speech on a frame-by-frame basis, which
decomposes each frame into a number of subbands. For each
subband, a voice activity detector (VAD) is designed to detect
the voiced/unvoiced parts of the speech. Based on the
VAD result, an adaptive thresholding scheme is then utilized
to each subband speech to obtain the pre-enhanced speech.
To achieve a further level of enhancement, an IKF is next
applied to the pre-enhanced speech. The proposed method
is evaluated under various noise conditions. Experimental results
are provided to demonstrate the effectiveness of the proposed
method as compared to some previous works in terms
of segmental SNR and perceptual evaluation of speech quality
(PESQ) as two well-known performance indexes</p>

## Introduction 

<p align="justify">Wavelet Packet (WP), as a well-known powerful method,
is used in several signal processing applications including
speech enhancement. Based on an adaptive thresholding in
wavelet packets, a speech enhancement approach is proposed
in [3], where a subband thresholding is applied to detect the
voice/noise frames. The criterion used in [3] to determine
voiced and noise frames is to compare the frame energy with
a constant threshold. Namely, a voiced frame is detected if
the frame energy exceeds the constant threshold. Otherwise,the frame is decided as noise. In practice, however, such an
energy-based decision making would fail to identify all voice
or noise frames. To increase the detection accuracy, other
frame characteristics need to be considered.</p>

<p align="justify">The authors in [4] proposed an iterative Kalman filter
(IKF) approach for speech enhancement, where the linear
prediction coefficients (LPCs) and the noise variance are estimated
directly from the noisy speech, which decreases the
accuracy of IKF approach to a certain degree. In [5], another
IKF-based approach is proposed along with a subband processing,
where the noisy speech is decomposed into a number
of subbands followed by Kalman Filtering (KF) on each subband.
The method, however, demands a large amount of computational
resource for the implementation of KF at all the
subbands. More recently, a subband IKF method with partial
reconstruction is proposed in [6], where the noisy speech is
first decomposed into a set of subbands, and then a partial
reconstruction scheme is used to reconstruct the subbands
into high-frequency and low-frequency subband speeches. In
this context, the IKF is employed only in the high-frequency
subband. Since the low-frequency subband is not filtered by
the IKF, this method offers limited enhancement performance
for noisy speeches which contain non-negligible noises in lowfrequency
region.</p>

<p align="justify">In order to address the aforementioned limitations, in this
paper we propose an improved thresholding scheme with the
IKF for speech enhancement on a frame-by-frame basis. The
noisy speech is first decomposed into a number of subbands
with the WP. The VAD is then applied to each subband frame
to determine whether the frame is voice or noise. In contrast
to most existing works where only a single parameter is employed
for voice/noise frame detection, our method makes use
of two measurements in the VAD stage. i) frame energy and ii)
spectral flatness. A VAD based adaptive thresholding scheme
is then proposed for speech enhancement in accordance with
each subband frame activity. Finally, an IKF is used for further
noise reduction, which is followed by reconstruction of
the full-band speech from the enhanced subband speeches.</p>
## Iterative Kalman Filter

Here, the pre-enhanced full-band speech signal $\hat{y}(k)$ is further processed by an IKF as modelled below
$$
\begin{aligned}
& \hat{y}(k)=\boldsymbol{H} \boldsymbol{x}(k)+w(k), \\
& \boldsymbol{x}(k)=\boldsymbol{F} \boldsymbol{x}(k-1)+\boldsymbol{G} u(k),
\end{aligned}
$$
with $\boldsymbol{H}=\boldsymbol{G}^T=[1, \ldots, 1] \in \mathbb{R}^{1 \times p}, \boldsymbol{x}(k)=[s(k-p+1), \ldots, s(k)]$. The term $\boldsymbol{F}$ denotes the $p \times p$ state transition matrix represented as LPCs estimation based on Modified Yule-Walker equations $[10]$
$$
\boldsymbol{F}=\left[\begin{array}{ccccc}
-a_1 & -a_2 & \cdots & -a_{p-1} & -a_p \\
1 & 0 & \cdots & 0 & 0 \\
0 & 1 & \cdots & 0 & 0 \\
\vdots & \vdots & \ddots & \vdots & \vdots \\
0 & 0 & \cdots & 1 & 0
\end{array}\right]
$$
The number of iterations is usually set to 2 or 3 . The operation principle of the IKF includes a prediction step and a measurement update step. In the prediction step, the IKF predicts the state vector and parameter covariance by using the previous samples of the state-space model. The estimate of clean speech $\hat{x}(k)$ and the posteriori estimation error covariance $P(k \mid k)$ are predicted from time step $(k-1)$ to step $k$ (the status are $\hat{x}(k \mid k-1) / P(k \mid k-1)$ ),
$$
\begin{aligned}
\hat{\boldsymbol{x}}(k \mid k-1) & =\boldsymbol{F} \hat{\boldsymbol{x}}(k-1 \mid k-1), \\
P(k \mid k-1) & =\boldsymbol{F} P(k-1 \mid k-1) \boldsymbol{F}^T+G \sigma_u{ }^2 G^T .
\end{aligned}
$$
In the measurement update step, the Kalman Gain and state vectors are updated by
$$
\begin{aligned}
\boldsymbol{K}(k) & =P(k \mid k-1) \boldsymbol{H}^T\left(\boldsymbol{H} P_{(k \mid k-1)} \boldsymbol{H}^T+\sigma_w{ }^2\right)^{-1}, \\
\hat{\boldsymbol{x}}(k \mid k) & =\hat{\boldsymbol{x}}(k \mid k-1)+\boldsymbol{K}(k)(y(k)-\boldsymbol{H} \hat{\boldsymbol{x}}(k \mid k-1)), \\
P(k \mid k) & =(\boldsymbol{I}-\boldsymbol{K}(k) \boldsymbol{H}) P(k \mid k-1),
\end{aligned}
$$
where $\boldsymbol{I}$ denotes the identity matrix.


## Comparison

<p align="justify">Three existing methods namely, adaptive threshold (AT) [9],
iterative Kalman filter (IKF) [4] and subband iterative
Kalman filter (S-IKF) [6], are compared with the proposed
adaptive threshold iterative Kalman filter (AT-IKF) method.
Standard objective metrics, i.e., segmental SNR and PESQ,
are applied for performance evaluations. From Fig. 4, it is
observed that in non-stationary noise environment the proposed
method achieves the same performance as compared
with the IKF and S-IKF methods in terms of segmental
SNR. However, the experimental results shown in Fig. 5
demonstrate a performance improvement in terms of PESQ.
Moreover, as shown in Fig. 6 and Fig. 7, the proposed scheme
outperforms the other methods both in terms of segmental
SNR and PESQ.</p>








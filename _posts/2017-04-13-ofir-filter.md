---
layout: post
title: Optimal Finite Impulse Response (OFIR) Filter
description: Optimal Finite Impulse Response (OFIR) Filter
summary: Optimal Finite Impulse Response (OFIR) Filter
author:
- Pavan Donthireddy
usemathjax: true
tags: [filters, OFIR, FIR, IIR, kalman]
---

<p align="justify">The Kalman filter (KF) is the
most widely used real-time optimal estimator. However, the KF is a
Bayesian estimator and its recursive algorithm has the infinite impulse
response (IIR), owing to which the KF often suffers of insufficient robustness. Better robustness is inherent to finite memory filters and to filters with finite impulse response (FIR).</p>

Unlike the KF, the FIR filter utilizes measurements on an interval of
N most recent neighbouring points called horizon. Compared to the KF,
FIR filters demonstrate many useful properties such as the bound input/
bound output (BIBO) stability, higher robustness against temporary
model uncertainties and round-off errors , and
lower sensitivity to noise. 


### Preliminaries

Consider a general class of discrete-time linear systems represented in state-space with time-variant coefficients as

$$x_{k}=A_{k} x_{k-1}+B_{k} w_{k} \tag{1}$$

$$y_{k}=C_{k} x_{k}+v_{k}\tag{2}$$
in which $k$ is the discrete time index, $x_{k} \in \mathbb{R}^{n}$ is the state vector, $y_{k} \in \mathbb{R}^{p}$ is the measurement vector, and $A_{k} \in \mathbb{R}^{n \times n}, B_{k} \in \mathbb{R}^{n \times u}$, and $C_{k} \in \mathbb{R}^{p \times n}$ are time-variant matrices. Here, $w_{k} \in \mathbb{R}^{u}$ and $v_{k} \in \mathbb{R}^{p}$ are additive process and measurement noise sources with known covariances 

$Q_k=\E ( w_k w_{k}^{T} ) $ and $R_{k}=\mathbb{E}( v_{k} v_{k}^{T})$, respectively. We suppose that $w_{k}$ and $v_{k}$ are zero mean, white, and mutually uncorrelated; that is, $\mathbb{E}( w_{k})=0$, $\mathbb{E}( v_{k})=0, \mathbb{E}(w_{k} w_{j}^{T})=0$ and $\mathbb{E}( v_{k} v_{j}^{T})=0$ for all $k$ and $j \neq k$, and $\mathbb{E}( w_{k} v_{j}^{T})=0$ for all $k$ and $j$.

The FIR filter requires simultaneously $N$ data points taken from the horizon $[l=k-N+1, k]$. Therefore, (1) and (2) need to be extended on $[l, k]$. That can be done if to use the recursively computed forward in-time solutions and write

$$X_{k, l}=A_{k, l} x_{l}+B_{k, l} W_{k, l}\tag{3}$$

$$Y_{k, l}=C_{k, l} x_{l}+H_{k, l} W_{k, l}+V_{k, l} \tag{5}$$


where the extended vectors are $X_{k, l}=\left[x_{k}^{T}, x_{k-1}^{T}, \ldots, x_{l}^{T}\right]^{T} \in \mathbb{R}^{N n \times 1}$, $Y_{k, l}=\left[y_{k}^{T}, y_{k-1}^{T}, \ldots, y_{l}^{T}\right]^{T} \in \mathbb{R}^{N p \times 1}, W_{k, l}=\left[w_{k}^{T}, w_{k-1}^{T}, \ldots, w_{l}^{T}\right]^{T} \in \mathbb{R}^{N u \times 1}$, and $V_{k, l}=\left[v_{k}^{T}, v_{k-1}^{T}, \ldots, v_{l}^{T}\right]^{T} \in \mathbb{R}^{N p \times 1}$. The extended $k$ - and $N$-variant matrices $A_{k, l} \in \mathbb{R}^{N n \times n}, B_{k, l} \in \mathbb{R}^{N n \times N u}, C_{k, l} \in \mathbb{R}^{N p \times n}$, and $H_{k, l} \in \mathbb{R}^{N p \times N u}$ can be represented as, respectively,

$$A_{k, l}=\left[\mathscr{A}_{k, l+1}^{T}, \mathscr{A}_{k-1, l+1}^{T}, \ldots, \mathscr{A}_{l+1, l+1}^{T}, I\right]^{T}$$
$$B_{k, l}=\left[\begin{array}{ccccc}B_{k} & \mathscr{A}_{k, k} B_{k-1} & \cdots & \mathbf{A}_{k, l+2} B_{l+1} & \mathscr{A}_{k, l+1} B_{l} \\ 0 & B_{k-1} & \cdots & \mathscr{A}_{k-1, l+2} B_{l+1} & \mathscr{A}_{k-1, l+1} B_{l} \\ \vdots & \vdots & \cdots & \vdots & \vdots \\ 0 & 0 & \cdots & B_{l+1} & \mathscr{A}_{l+1, l+1} B_{l} \\ 0 & 0 & \cdots & 0 & B_{l}\end{array}\right]$$
,

$$C_{k, l}=\bar{C}_{k, l} A_{k, l}$$

$$H_{k, l}=\bar{C}_{k, l} B_{k, l}$$


where

$$\bar{C}_{k, l}=\operatorname{diag}\left(C_{k} C_{k-1} \cdots C_{l}\right)$$

$$\mathbf{A}_{i, j}=\prod_{r=0}^{i-j} A_{i-r}=A_{i} A_{i-1} \ldots A_{j}$$

At the initial horizon point, (3) becomes $x_{l}=x_{l}+B_{l} w_{l}$ that is uniquely satisfied if $w_{l}$ is zero-valued, provided that $B_{l}$ is not zeroth. That means that the initial state must be known in advance or estimated optimally. 

The FIR filtering estimate can be obtained at $k$ via (4) using the discrete convolution as

$$\hat{x}_{k \mid k}=K_{k} Y_{k, l} \tag{5}$$

where $x_{t \vert r} $ means the estimate at $t$ via measurements from the past to and including at $r$ and $K_{k}$ is the FIR filter gain, which needs to be defined to obey some cost function. Note that the aforementioned inherent properties of FIR filtering are associated with the fact that measurements prior to $l$ are discarded in (5) and thus do not affect the estimate unlike in the KF which has IIR. It is also necessary to emphasize that when the system considered is time-invariant, the FIR estimate (5) will becomes $x_{k \mid k}=K_{N} Y_{k, l}$, which means that the filter gain $K_{N}$ is time-invariant and can be determined off-line once the horizon length $N$ is available. In this case, $K_{N}$ is not necessarily to be realized into iterative computation structure.

The optimal gain $K_{k}$ can be obtained for (5) in the minimum MSE sense by minimizing the trace of the MSE as

$$\hat{K}_{k}=\underset{K_{k}}{\arg \min } E\left\{\operatorname{tr}\left(e_{k} e_{k}^{T}\right)\right\}$$

where $e_{k}=x_{k}-x_{k \mid k}$ is the estimation error. Provided $x_{k \mid k}$ via (5), the one-step prediction required by feedback control and associated with receding horizon filtering can be formed as $x_{k+1 \mid k}=A_{k+1} x_{k \mid k}$, similarly to the KF.


### OFIR algorithm

Given the model (1) and (2) with white and mutually uncorrelated noise processes $w_{k}$ and $v_{k}$ which have covariances $Q_{k}$ and $R_{k}$, respectively. The iterative form for OFIR estimate (10) with gain (16) is the following,

$$
\begin{aligned}
\Xi_{i}= & A_{i} \Xi_{i-1} A_{i}^{T}+B_{i} Q_{i} B_{i}^{T}-A_{i} \Xi_{i-1} C_{i-1}^{T} \\
& \times\left(R_{i-1}+C_{i-1} \Xi_{i-1} C_{i-1}^{T}\right)^{-1} C_{i-1} \Xi_{i-1} A_{i}^{T} \\
G_{i}= & \Xi_{i} C_{i}^{T}\left(R_{i}+C_{i} \Xi_{i} C_{i}^{T}\right)^{-1}
\end{aligned} \tag{6}
$$


$$\hat{x}_{i \mid i}=A_{i} \hat{x}_{i-1 \mid i-1}+G_{i}\left(y_{i}-C_{i} A_{i} \hat{x}_{i-1 \mid i-1}\right)\tag{7}$$

where $i$ ranges from $l+1$ to $k$ and the output is taken when $i=k$. The initial state $x_{l \vert l}$ is given and the initial prior error $\Xi_{i}$ is provided at l by

$\Xi_{l}=\Theta_{x, l}+B_{l} Q_{l} B_{l}^{T}$

where $\Theta_{x, l}$ is given.

As can be seen (7), is the Kalman-like recursion in which $A_{i} x_{i-1 \mid i-1}$ predicts the state from $i-1$ to $i$ and the bias correction gain (6) corrects the prediction for the residual. Although the KF and OFIR filter both minimize the MSE, $G_{i}$ is not the Kalman gain, because the KF has IIR. However, an increase in the horizon length $N$ reduces the estimation error and makes it such that the OFIR estimate converges to the KF estimate: the estimates become practically equal when $N>N_{\mathrm{opt}}$ . In this sense, the KF can be considered as a special case of a more general OFIR filter when $N=\infty$, provided the initial conditions. Another difference is that $N$ measurements are processed by the OFIR filter simultaneously at each time index $k$, while only one measurement is processed by the KF at $k$. That means that the computational complexity of OFIR filter $\mathcal{O}(N)$ is $N$ times larger than $\mathcal{O}(1)$ of the KF. On the other hand, the iterative algorithm reduces essentially the computational complexity $\mathcal{O}\left(N^{2}\right)$ of the batch OFIR form.
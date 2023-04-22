---
layout: post
title: Time Frequency Bandpass Filter with Nonstationary Signal Decomposition Application
description: Time Frequency Bandpass Filter with Nonstationary Signal Decomposition Application
summary: Time Frequency Bandpass Filter with Nonstationary Signal Decomposition Application
author:
- Pavan Donthireddy
usemathjax: true
tags: [ filters , time_frequency_methods ]
original: Yu_2021_J._Phys.__Conf._Ser._1880_012003
---

## Abstract 

<p align="justify">In various applications such as speech processing, underwater sound, radar application
and mechanical fault diagnosis, there are large number of nonstationary signals. In order to
achieve nonstationary signal decomposition, the instantaneous frequency ridge is extracted
through interactive mode, and a time-frequency bandpass filter (TFBPF) method is proposed.
This method is the modified version of Intrinsic Chirp Component Decomposition (ICCD) and
has the physical essence of time-frequency domain bandpass filter. The superiority and
application potential of TFBPF in complex engineering signal decomposition are demonstrated
through two numerical examples. In the first one, we prove that TFBPF can decompose the weak
signal component directly through analyzing the vibration signal of hydraulic turbine; While in
the second one, we prove that TFBPF can effectively overcome the drawbacks of ICCD through
analyzing the vibration signal during the speed-up process of a complex equipment. TFBPF is
still very effective even for complex signal decomposition in a strong noise environment.</p>


## Introduction

There are large number of nonstationary signals. Such signals usually
exhibit amplitude modulation and frequency modulation characteristics, which can be modeled as
amplitude-modulated and frequency-modulated signals[5].

<p align="justify">In order to effectively extract the basic components of signal, signal decomposition has gradually
become a hot spot in the field of signal processing. However, signals in nature and engineering usually
exhibit strong time-varying nonlinear frequency modulation characteristics and often contain strong
background noise, which brings great challenges to the decomposition of signal components.
The Empirical Mode Decomposition (EMD) proposed by Huang et al. [6] is the most classical
nonstationary signal decomposition method. However, EMD has a series of problems such as boundary
effect, mode aliasing, sensitivity to noise, and lack of mathematical theoretical support.</p>

<p align="justify">Therefore, Smith
proposed Local Mean Decomposition (LMD)[7], Frei proposed Intrinsic Time-Scale Decomposition
(ITD)[8], which decomposes the signal into several product functions or rotation components, and the
calculation efficiency and accuracy are improved compared with EMD. In addition, relative scholars
proposed Iterative Filtering Decomposition (IFD) and its variants[9,10], which use low-pass filtering
method to obtain the average of signal, and have been successfully used in the field of power grid data analysis and rotating machinery fault diagnosis. However, the above iterative decomposition method has poor noise resisting ability, or cannot decompose overlapping and cross components, which limited their application.</p>

<p align="justify">Frequency domain filtering methods represented by Variational Mode Decomposition (VMD)[11] and Empirical Wavelet Transform (EWT)[12] essentially obtain signal components with high SNR by constructing different optimal filters, and have been widely used in finance, seismic data analysis[13,14] and medical disease monitoring[15]. But they will all suffer in decomposition of nonlinear frequency-modulated signal with broadband overlapping components.
Time-frequency domain reconstruction methods represented by Synchrosqueezing Transform (SST)[16,17] achieve signal decomposition based on the reversibility of time-frequency transform, which overcomes the above problems, but they will produce large instantaneous frequency estimation error and signal reconstruction error when decomposing strong time-varying frequency modulation signals.</p>

<p align="justify">Yang proposed general parameterized time-frequency transform[18], which can effectively obtain the time-frequency characterization of strong time-varying frequency modulation signals with high concentration. Chen solves the linear system on this basis, then proposes Intrinsic Chirp Component Decomposition (ICCD)[19] and Ridge Path Regrouping (RPRG)[20], which can effectively realize the decomposition of strong time-varying frequency modulation and even cross signal components. However, due to such methods extract instantaneous frequency ridges by iteratively detecting peaks in time-frequency diagram, they cannot decompose signal components with weak energy directly, and usually combine two uncorrelated signal components into a false signal component. The above shortcomings make them lack flexibility in complex signal decomposition problems.</p>

<p align="justify">In this paper, the instantaneous frequency ridge is extracted through interactive mode, and a time-frequency bandpass filter (TFBPF) method is proposed to overcome the above-mentioned problems of ICCD. We proved that the physical essence of the proposed TFBPF method is time-frequency domain bandpass filter, and demonstrate the effectiveness of this method through two numerical examples.</p>

## Method

The arbitrary component $s_i(t)$ of signal $s(t)$ can be expressed in the form of frequency modulation component:
$$
s_i(t)=a(t) \cos \left[2 \pi \int_0^t f_i(\tau) d \tau+\theta_0\right]
$$
where, $f_i(t)$ represents the instantaneous frequency of $s_i(t), t=t_0, t_1, \cdots t_{N-1}$ represents sampling time, $N$ is the number of sampling points. In order to eliminate the nonlinear effect of the initial phase, the above equation can be rewritten as:
$$
s_i(t)=u(t) \cos \left[2 \pi \int_0^t f_i(\tau) d \tau\right]+v(t) \sin \left[2 \pi \int_0^t f_i(\tau) d \tau\right]
$$
where, $u(t)$ and $v(t)$ are the amplitude functions of the signal components, which are described by the Fourier series model as follows:
$$
\begin{aligned}
& u(t)=u_0^{(i)}+\sum_{l=1}^L\left[u_l^{(i)} \cos \left(2 \pi l F_0 t\right)+\bar{u}_l^{(i)} \sin \left(2 \pi l F_0 t\right)\right] \\
& v(t)=v_0^{(i)}+\sum_{l=1}^L\left[v_l^{(i)} \cos \left(2 \pi l F_0 t\right)+\bar{v}_l^{(i)} \sin \left(2 \pi l F_0 t\right)\right]
\end{aligned}
$$
where, $L$ represents the order of the Fourier model, $\left\{u_0^{(i)}, \cdots, u_L^{(i)}, \bar{u}_1^{(i)}, \cdots \bar{u}_L^{(i)}\right\}$ and $\left\{v_0^{(i)}, \cdots, v_L^{(i)}, \bar{v}_1^{(i)}, \cdots \bar{v}_L^{(i)}\right\}$ represent the Fourier coefficients to be estimated; The frequency resolution of the Fourier model is $F_0=f_s / Q N, Q \in N^*, f_s$ is the sample frequency of signal. In this paper, the redundant Fourier model is obtained through $Q=2$, which can describe more complex functions [21].
The instantaneous frequency $f_i(t)$ of the signal component is usually a function that changes continuously with time, so it can also be approximated by the Fourier series model, namely:
$$
f_i(t)=f_c^{(i)}+\sum_{m=1}^M\left[b_m^{(i)} \cos \left(2 \pi m F_0 t\right)+\bar{b}_m^{(i)} \sin \left(2 \pi m F_0 t\right)\right]
$$



where, $f_c^{(i)}$ represents the carrier frequency of signal component, $M$ represents the order of the Fourier model, $\left\{b_1^{(i)}, \cdots, b_M^{(i)}, \bar{b}_1^{(i)}, \cdots, \bar{b}_M^{(i)}\right\}$ is the parameter set of the Fourier model, make $F_0=f_s /(2 N)$ to obtain the redundant Fourier model.

In the above signal model, there is linear relationship between the amplitude function and the instantaneous frequency. Therefore, the instantaneous frequency parameters can be estimated first, then the amplitude parameters can be estimated by solving the linear system, and finally the frequency modulation component can be reconstructed to realize signal decomposition. In ICCD, the instantaneous frequency is estimated by parameterized time-frequency transformation, which lacks flexibility in complex signal decomposition problems. Therefore, TFBPF uses interactive selection and interpolation to achieve instantaneous frequency estimation.

### Instantaneous frequency estimation

For the nonstationary signal to be analyzed, the time-frequency distribution can be obtained through Short Time Fourier Transform first:
$$
\operatorname{STFT}(t, f)=\int_{-\infty}^{+\infty} s(\tau) h(\tau-t) e^{j 2 \pi f \tau} d \tau
$$
where, $h(t)$ is window function. In the calculated time-frequency distribution diagram, the instantaneous frequency feature point set $\left(t_i^{(j)}, f_i^{(j)}, f_i^{(j)^{\prime}}\right), j=0,1,2 \cdots, n$ can be obtained interactively, where $t_i^{(j)}$ is the corresponding $j$-th time period of $i$-th signal component, $f_i^{(j)}$ is the instantaneous frequency at the corresponding time, and $f_i^{(j)^{\prime}}$ is the derivative of $f_i^{(j)}$.
The instantaneous frequency ridge $f_i(t)$ is estimated by piecewise cubic Hermite interpolation:
$$
f_i^{(j)}\left(t_j\right)=f_i^{(j)} \alpha_i\left(t_i\right)+f_i^{(j+1)} \alpha_{i 1}\left(t_i\right)+f_i^{(j)^{\prime}} \beta_i\left(t_i\right)+f_i^{(j+1)^{\prime}} \beta_{i 1}\left(t_i\right), t_j \in\left[t_i^{(j)}, t_i^{(j+1)}\right]
$$
Where
$$
\begin{gathered}
\alpha_i\left(t_j\right)=\left(1-2 \frac{t_i-t_i^{(j)}}{t_i^{(j)}-t_i^{(j+1)}}\right)\left(\frac{t_i-t_i^{(j+1)}}{t_i^{(j)}-t_i^{(j+1)}}\right)^2, \alpha_{i 1}\left(t_i\right)=\left(1-2 \frac{t_i-t_i^{(j+1)}}{t_i^{(j+1)}-t_i^{(j)}}\right)\left(\frac{t_i-t_i^{(j)}}{t_i^{(j+1)}-t_i^{(j)}}\right)^2 \\
\beta_i\left(t_i\right)=\left(t_i-t_i^{(j)}\right)\left(\frac{t_i-t_i^{(j+1)}}{t_i^{(j)}-t_i^{(j+1)}}\right)^2, \beta_{i 1}\left(t_i\right)=\left(t_i-t_i^{(j+1)}\right)\left(\frac{t_i-t_i^{(j)}}{t_i^{(j+1)}-t_i^{(j)}}\right)^2
\end{gathered}
$$
therefore:
$$
f_i(t)=\left\{\begin{array}{cc}
f_i^{(0)}\left(t_i\right), & t_i \in\left[t_i^{(0)}, t_i^{(1)}\right] \\
f_i^{(1)}\left(t_i\right), & t_i \in\left[t_i^{(1)}, t_i^{(2)}\right] \\
\vdots \\
f_i^{(n-1)}\left(t_i\right), & t_i \in\left[t_i^{(n-1)}, t_i^{(n)}\right]
\end{array}\right.
$$
Then the instantaneous frequency ridge can be fitted by the Fourier series model to obtain an instantaneous frequency estimate.

### Amplitude estimation

In order to estimate the amplitude parameters, the signal model is written in the form of multi-component matrix:
where, $\boldsymbol{s}=\left[s\left(t_0\right) \cdots s\left(t_{N-1}\right)\right]^T, \boldsymbol{r}=\left[r\left(t_0\right) \cdots r\left(t_{N-1}^K\right)\right]^T \mathbf{H}_i \boldsymbol{y}_i+\boldsymbol{r}$ represents error, $\boldsymbol{y}_i$ is the column vector of the $i$-th signal component composed of the corresponding amplitude parameters. When only one of the signal components is considered, $K=1$. The expression of $\boldsymbol{y}_i$ is as follows:
$$
\begin{gathered}
\boldsymbol{y}_i=\left[\left(y_i^u\right)^T \quad\left(y_i^v\right)^T\right]^T \\
y_i^u=\left[u_0^{(i)}, \cdots, u_L^{(i)}, \bar{u}_1^{(i)}, \cdots \bar{u}_L^{(i)}\right]^T \\
y_i^v=\left[v_0^{(i)}, \cdots, v_L^{(i)}, \bar{v}_1^{(i)}, \cdots \bar{v}_L^{(i)}\right]^T
\end{gathered}
$$
where superscript $T$ represents matrix transpose. For convenience, $\phi_i(t)=2 \pi \int_0^t f_i(\tau) d \tau$, then the form of matrix $\mathbf{H}_i$ is as follows:
$$
\begin{gathered}
\mathbf{H}_i=\left[\begin{array}{ll}
\mathbf{H}_i^c & \mathbf{H}_i^s
\end{array}\right] \\
\mathbf{H}_i^c=\operatorname{diag}\left[\cos \phi_i\left(t_0\right) \cdots \cos \phi_i\left(t_{N-1}\right)\right] \mathbf{F} \\
\mathbf{H}_i^s=\operatorname{diag}\left[\sin \phi_i\left(t_0\right) \cdots \sin \phi_i\left(t_{N-1}\right)\right] \mathbf{F}
\end{gathered}
$$
where diag [.] represents the diagonal matrix. $\mathbf{F}$ is an $N \times(2 L+1)$ Fourier model matrix:
$$
\mathbf{F}=\left[\begin{array}{ccccccc}
1 & \cos \left(2 \pi F_0 t_0\right) & \cdots & \cos \left(2 \pi L F_0 t_0\right) & \sin \left(2 \pi F_0 t_0\right) & \cdots & \sin \left(2 \pi L F_0 t_0\right) \\
\vdots & \vdots & \cdots & \vdots & \vdots & \cdots & \vdots \\
1 & \cos \left(2 \pi F_0 t_{N-1}\right) & \cdots & \cos \left(2 \pi L F_0 t_{N-1}\right) & \sin \left(2 \pi F_0 t_{N-1}\right) & \cdots & \sin \left(2 \pi L F_0 t_{N-1}\right)
\end{array}\right](18)
$$
The above formula shows that for $i$-th signal component there is a linear relationship between $\boldsymbol{y}_i$ and $\mathbf{H}_i$, while the matrix $\mathbf{H}_i$ is determined by the instantaneous frequency $f_i(t)$. Therefore, under the condition that $\mathbf{H}_i$ is known, the amplitude parameter vector $\boldsymbol{y}_i$ can be estimated by solving an ill-posed inverse problem of linear system, which can be achieved through Tikhonov regularization:
$$
\tilde{\boldsymbol{y}}_i=\arg \min _{\boldsymbol{y}_i}\left\{\left\|\boldsymbol{s}-\mathbf{H}_i \boldsymbol{y}_i\right\|_2^2+\lambda_1\left\|\boldsymbol{y}_i\right\|_2^2\right\}
$$
where, $\|\cdot\|_2$ represents $l_2$ norm; $\lambda_1>0$ represents regularization parameter, and can be selected by generalized cross validation (GCV) method. The analytical solution of the above formula is given by the following expression:
$$
\tilde{\boldsymbol{y}}_i=\left(\mathbf{H}_i^T \mathbf{H}_i+\lambda_1 \mathbf{I}\right)^{-1} \mathbf{H}_i^T \boldsymbol{s}
$$
where, I represents the identity matrix. Based on the obtained amplitude parameters the corresponding signal component can be reconstructed:
$$
\tilde{\boldsymbol{s}}_i=\mathbf{H}_i \tilde{\boldsymbol{y}}_i
$$
All of the signal components can be decomposed and reconstructed by repeating the above process. The proposed method is called Time-Frequency Bandpass Filter (TFBPF).

## Physical essence

In this section, we explain that the proposed method can essentially be regarded as a time-frequency band pass filter. The signal model can be organized as:
$$
\begin{aligned}
& s(t)=\sum_{i=1}^K\left\{A_{i 0}^{u v} \sin \left[\phi_i(t)+\varphi_{i 0}^{u v}\right]+\sum_{l=1}^L \frac{A_{i l}^{u \bar{u}}}{2}\left\{\sin \left[\phi_i(t)+2 \pi l F_0 t+\varphi_{i l}^{u \bar{u}}\right]-\sin \left[\phi_i(t)-2 \pi l F_0 t-\right.\right.\right. \\
& \left.\left.\left.\varphi_{i l}^{u \bar{u}}\right]\right\}+\sum_{l=1}^L \frac{A_{i l}^{v v}}{2}\left\{\cos \left[\phi_i(t)-2 \pi l F_0 t-\varphi_{i l}^{v \bar{v}}\right]-\cos \left[\phi_i(t)+2 \pi l F_0 t+\varphi_{i l}^{v \bar{v}}\right]\right\}\right\}+r(t) \\
& \text { where, } \phi_i(t)=2 \pi \int_0^t f_i(\tau) d \tau, A_{i l}^{c d}=\left(\left(c_l^{(i)}\right)^2+\left(d_l^{(i)}\right)^2\right)^{1 / 2}, \varphi_{i l}^{c d}=\arctan \frac{c_l^{(i)}}{d_l^{(i)}}, i=1, \cdots, K, l=
\end{aligned}
$$
$0, \cdots, L, c d$ represents $u v, u \bar{u}$ or $v \bar{v}$. The above formula shows that each signal component is composed of a series of harmonic components with the instantaneous frequency range of $\left[f_i(t)-L F_0, f_i(t)+L F_0\right]$. Therefore, TFBPF can be regarded as a time-frequency bandpass filter with center frequency $f_i(t)$, of which bandwidth is:
$$
B W=2 L F_0=\frac{L f_s}{N}
$$


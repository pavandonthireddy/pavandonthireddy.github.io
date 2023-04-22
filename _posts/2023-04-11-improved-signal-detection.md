---
layout: post
title: Improved signal detection using efficient time–frequency de-noising technique and Pre-whitening filter
description: Improved signal detection using efficient time–frequency de-noising technique and Pre-whitening filter
summary: Improved signal detection using efficient time–frequency de-noising technique and Pre-whitening filter
author:
- Pavan Donthireddy
usemathjax: true
tags: [ signal_detection , signal_denoising  , time_frequency_methods, trend_estimation , trend_detection  ]
original: Yousifal-aboosi 2017
---


## Abstract

<p align="justify">In the present study, the proposed Gaussian noise injection
detector (GNID) represents a complete detection system. This
detector is developed to improve the probability of detection (PD)
using a pre-whitening filter, a time–frequency de-noising algorithm
based on S-transform, and an inverse whitening filter. Stransform
is used in the de-noising process to overcome the limitations
and poor performance of de-noising using the wavelet
transform [25]. The UWAN used for the validation of the system
is sea-truth data, which are collected at the Desaru Beach on the
eastern shore of Johor in Malaysia using broadband hydrophones.
The performance results of the proposed detector are compared
with other nonlinear detectors, namely, locally optimal (LO), sign
correlation (SC), and conventional LC.</p>

## Signal detection problem

In this section, a known signal is to be detected in an additive noise channel representing a common problem in communication, radar, and sonar systems, that is, where the noise follows a Student's t-distribution and the noise samples are uncorrelated.
2.1. Signal model
The signals used are single-frequency sinusoidal and linear frequency modulated (LFM) signals. These signals represent the fixed frequency and time-varying signals that can be encountered in practical situations. An arbitrary sinusoidal signal can be defined as follows:
$$
\begin{aligned}
s(n) & =A \cos (\alpha(n)) & & 0 \leqslant n \leqslant N-1 \\
& =0 & & \text { elsewhere }
\end{aligned}
$$
where $N$ is the signal duration in the samples, $A$ is signal amplitude, and $\alpha(n)$ is the instantaneous phase. For a fixed-frequency signal, the instantaneous phase is defined as
$$
\alpha(n)=2 \pi f_m n T_s
$$
where $f_m$ is signal frequency, and $T_s$ is the sampling period. The instantaneous phase for the LFM signal is
$$
\alpha(n)=2 \pi\left(f_m+\frac{\varphi}{2} n T_s\right) n T_s
$$
where $\varphi$ is the frequency defined as $\varphi=f_{B W} / N T_S$, where $f_{B W}$ is the signal bandwidth.

Given the combined influences of the internal measurement system and the external environmental factors, measured signals are often contaminated with noise. Thus, the received signal can be defined as follows:
$$
x(n)=s(n)+v(n)
$$
where $s(n)$ is the signal of interest, and $v(n)$ is the UWAN. The assumption of a Gaussian distribution for UWAN is explained in [26]. However, recent studies have suggested that UWAN follows a t-distribution [27] and a stable alpha distribution [11]. Therefore, the purpose of de-noising is to reduce the degree of corruption on $s(n)$ by $v(n)$

The main idea of detection is to determine the presence of a signal in the noise. Given an observation vector $x$ and several hypotheses $\mathrm{H} i$, the aim is to find the data set that matches a hypothesis. Although the number of hypotheses can be arbitrary,
the case of having two hypotheses, $\mathrm{H}_0$ and $\mathrm{H}_1$, is considered applicable to communication, radar, and sonar systems [8]. If the pdf for each hypothesis is assumed to be completely known, then the hypothesis-testing problem is formulated as follows:
$H_0($ Null hypothesis $): y(n)=v(n) n=0,1, \ldots, N-1$
$H_1$ (Alternative hypothesis) : $x(n)=s(n)+v(n) n=0,1, \ldots, N-1$
Neyman-Pearson (NP) and Bayesian methods are primarily used for hypothesis testing. Method selection depends on the availability of prior probability. Although digital communication and pattern recognition systems use the Bayes risk [28], the NP criterion is employed for radar and sonar systems. Furthermore, the derivation of optimal detectors depends on the assumption about the noise [8]. Given that UWAN is frequency dependent [1,29], the assumption of AWGN is invalid, and UWAN is more appropriately modelled as colored noise $[12,13,30]$. The power spectrum of the colored noise is defined as $[31,32]$
$$
S_{V V}\left(e^{j 2 \pi f}\right)=\frac{1}{f^\delta} \quad \delta>0, \quad \frac{-f_s}{2} \leqslant f \leqslant \frac{f_s}{2}
$$
AWGN has a delta autocorrelation function, that is, the adjacent samples are independent and identically distributed. Conversely, $\frac{1}{f^\delta}$ noise has a $\operatorname{sinc}()$ autocorrelation function $[28,31]$. Unlike AWGN, the samples of $\frac{1}{f^s}$ noise are correlated.

## Complete detection system

Since the UWAN is colored with a non-Gaussian distribution, the proposed detection system is a GNID, which is shown in Fig. 5. The complete detection system based on the noise models consists of the broadband hydrophone, pre-whitening filter, time-frequency distribution, de-noising method, inverse whitening filter, and detection stage. In this section, the performance of the GNID is compared with three other linear and nonlinear detectors.

### Signal detection in the t-distributed noise using GNID

For non-Gaussian detection, linear and nonlinear detectors demonstrate optimal or at least near-optimal performance. In this study, the performances of four detectors for the detection of a known signal in additive UWAN are compared: LO, SC, and LC detectors, and the proposed GNID.

In the presence of a Gaussian noise, the LC detector is optimal for detecting a known signal. Many communication systems use this detector as a matched filter. The test statistic for the matched filter is given by [8]
$$
T(x)=\sum_{n=0}^{N-1} x[n] s[n]
$$
where $s(n)$ is the signal to be detected (reference signal) and $x(n)$ denotes the observed data. The expected value $\left(E\left\{T ; H_i\right\}\right.$ for $i=0$, 1) and the variance of the test statistic $\left(\operatorname{Var}\left\{T ; H_i\right\}\right.$ for $\left.i=0,1\right)$ are $T(x)= \begin{cases}N\left(0, v \operatorname{var}(v) \cdot E_s\right) & \text { under } H_0 \\ N\left(E_s, \operatorname{var}(v) \cdot E_s\right) & \text { under } H_1\end{cases}$
where $E_s$ is the energy of the signal, and $\operatorname{var}(v)$ is the variance of the noise that follows the $t$-distribution defined in Eq. (7). The false alarm probability $\left(P_{F A}\right)$ is defined as

$$
\mathrm{P}_{F A}=\mathrm{P}\left(\mathrm{H}_1 ; \mathrm{H}_0\right)=P_r\left\{x[0]>\gamma ; H_0\right\}=Q\left(\frac{\gamma}{\left(\operatorname{var}(v) \cdot E_s\right)^{1 / 2}}\right)
$$
where $\gamma$ is the threshold value for a given $P_{F A}$, and this threshold value is determined using
$$
\gamma=Q^{-1}\left(P_{F A}\right) \cdot\left(\operatorname{var}(v) \cdot E_s\right)^{1 / 2}
$$
The $P_D$ is defined as
$$
P_D=P\left(H_1 ; H_1\right)=P_r\left\{x[0]>\gamma ; H_1\right\}=Q\left(\frac{\gamma-E_s}{\left(v \operatorname{var}(v) \cdot E_s\right)^{1 / 2}}\right)
$$
By using Eqs. (9) and (11) in Eq. (12), we obtain the following equation [8]:
$$
P_D=Q\left[Q^{-1}\left(P_{F A}\right)-\sqrt{\frac{E_S}{\operatorname{var}(v)}}\right]
$$
As mentioned in the previous section, the LC detector shows performance degradation in the presence of non-Gaussian noise. Furthermore, nonlinear detectors have several limitations when used for non-Gaussian detection. For example, the LO detector is used for the detection of weak signals by introducing a nonlinear transfer function before a standard LC detector. The test statistic for the LO detector is given by [8-11]
$$
T(x)=\sum_{n=0}^{N-1} g(x[n]) s[n]
$$
where $g(x[n])$ is the nonlinear transfer function that can be determined from the noise pdf:
$$
g(x)=-\frac{1}{\rho(x)} \frac{d \rho(x)}{d x}
$$
where $\rho(x)$ is the pdf for a $t$-distribution defined in Eq. (7).
Another nonlinear detector is the SC detector, which is a nonparametric detector designed without predetermining the exact distribution of noise. Although the aforementioned feature of the SC detector can be considered advantageous, a negative effect on the performance may result from the lack of detailed information on noise distribution. The test statistic for the SC detector is as follows
$$
T(x)=\sum_{n=0}^{N-1} \operatorname{sgn}(x[n]) s[n]
$$
In this paper, we propose a GNID based on a noise-enhanced signal detection [14] using an S-transform de-noising method and prewhitening filter to ensure that the noise follows a Gaussian distri-bution and overcome the limitations of nonlinear detectors exclusively used for non-Gaussian detection. The basic idea of this proposed method is to insert a Gaussian noise to the UWAN that follows a t-distribution and convert that UWAN into a noise following a Gaussian distribution, which has a lighter tail than a t-distribution [15]. Given that the noise power has increased because of the insertion process, a de-noising algorithm using the S-transform is required before performing matched-filter detection, as shown in Fig. 5.

The sum of two independent random variables $X$ and $Y$, whose pdfs are $\rho_X(x)$ and $\rho_Y(y)$, respectively, produces a random variable $Z$ whose pdf $\rho_Z(z)$ is
$$
\rho_Z(z)=\rho_X(x) * \rho_Y(y)=\int_{-\infty}^{\infty} \rho_Y(y) \rho_X(z-x) d y
$$
The expression in Eq. (17), is a convolution integral. The distribution of the sum of two independent Gaussian and Student's $t$ (for three degrees of freedom) spherical random variables was studied in [15]. Two random variables $X$ and $Y$ are considered. $X$ is a Gaussian random variable with mean $\bar{X}$, variance $\sigma_v^2$, and pdf $\rho_X(x) ; Y$ is a $t$-distributed random variable with $v$-degrees of freedom, mean $\mu_v$, variance $\operatorname{var}(v)$, and pdf $\rho_y(y)$ [15]. The pdf for the sum of the random variables is [35]
$$
f_Z(z)=\frac{\Gamma\left(\frac{d+1}{2}\right)}{\sqrt{2 \pi} \sigma_v \Gamma\left(\frac{d}{2}\right)} \cdot \Psi\left(\frac{1}{2}, 1-\frac{d}{2} ; \frac{d}{2 \sigma_v^2}\right) \cdot e^{-\frac{z^2}{2 \sigma_v^2}}
$$
where $|z| \leqslant \infty, v>0$, and $\sigma_v>0 ; \Psi($.$) denotes the Kummer's$ hypergeometric function. By substituting $v=1$ and using the relationship between Kummer's hypergeometric function and the complementary error function [36], the following equation is obtained: $\operatorname{erfc}(x)=\frac{1}{\sqrt{\pi}} \cdot e^{-x^2} \cdot \Psi\left(\frac{1}{2}, \frac{1}{2} ; x^2\right)$


Subsequently, Eq. (19) is substituted into Eq. (18) to obtain
$$
f_z(z)=\frac{1}{\sqrt{2 \pi} \sigma_v} \cdot e^{\frac{1}{2 \sigma_v^2}} \cdot \operatorname{erfc}\left(\frac{1}{\sqrt{2} \sigma_v^2}\right) \cdot e^{-\frac{z^2}{2 \sigma_v^2}}
$$
Eq. (20) shows that the function approaches a Gaussian distribution as the variance or the degrees of freedom increases. A normality test, such as the Lilliefors test, is performed to determine if the pdf of the sum of the random variables is approximately Gaussian [37,38]. If the degree of freedom is greater than 1, the pdf in Eq. (20) is approximately Gaussian. The threshold derived from the $P_{F A}$ can be calculated by Eq. (11). The $P_D$ can be calculated by the threshold defined in Eq. (13).

![[gnid.png]]

### Whitening process and inverse whitening filter

The colored noise can be transformed into white by passing into a linear time invariant (LTI) whitening filter $[28,39]$. The prediction error filter (PEF) with transfer function $H_p(z)$ is used for this purpose $[32,40]$. The output of the PEF is used as the difference between the estimate of the linear predictor and the actual sequence. The transfer function of the PEF can be expressed as
$$
H_p(z)=1+a_1 z^{-1}+a_2 z^{-2}+\ldots+a_p z^{-p}
$$
where $\mathrm{p}$ is the length of the forward predictor filter, and $a_p(n)$ is the filter coefficients and depends on the UWAN data recording. If the order $p$ of the PEF is sufficiently large, then the forward prediction error is orthogonal with constant variance; thus, the output of filter is similar to AWGN [32]. Selecting the model order to use for the pre-whitening and the inverse pre-whitening filters is done using several standard order selection techniques. These methods include Akaike's information criterion (AIC), Rissanen's minimum description length, and maximum a posteriori probability [32,41,42]. The AIC provides a distinct minimum at the optimum model order $P$
and is the criteria selected for deciding the pre-whitening filter model order in this study.

The output of the PEF is referred to as $x_w(n)$ and represents the convolution process between the input noisy signal $x(n)$ and the impulse response of the whitening filter $h_w(n)$. Thus, the resulting PEF is the transform of the signal with the AWGN, which is expressed as follows
$$
x_w(n)=x(n) * h_w(n)=s(n) * h_w(n)+v(n) * h_w(n)
$$

After the filter coefficients are determined, the de-noising process minimizes the noise term $v(n) * h_w(n)$ to produce a clean estimate of the transform signal, which can be obtained as follows
$$
\hat{s}_w(n)=s(n) * h_w
$$
The original signal $s(n)$ can be recovered with an inverse whitening filter [43] with impulse response $h_{I W F}(n)$ and transfer function $1 / H_p(z)$. The estimate of the original signal is

$$
\hat{s}(n)=\hat{s}_w(n) * h_{I W F}(n)=s(n) * h_w(n) * h_{I W F}(n)
$$
In the z-domain, the estimation of the original signal can be expressed as
$$
\hat{S}(z)=S(z) \cdot H_P(z) \cdot \frac{1}{H_P(z)}=S(z)
$$
### Time-frequency de-noising process based on the S-transform

The S-transform is used for the signal transformation in the denoising process, as shown in Fig. 6. S-transform can be considered a special case of the short-time Fourier transform); the window function is replaced with a frequency-dependent Gaussian window $[44,45]$. The Gaussian window width is inversely proportional to the frequency, and its height is scaled linearly with the frequency. Given this window scaling behaviour, the S-transform possesses a good time resolution for high-frequency components and a good frequency resolution for low-frequency components. Thus, the S-transform is suitable to use for signal de-noising in underwater applications because the underwater acoustic signals are mostly in the $0-2500 \mathrm{~Hz}$ frequency band that represents low-frequency signals [46]. The S-transform can be expressed as [44]
$$
X(t, f)=\int_{-\infty}^{\infty} x(\tau) \cdot g(\tau-t, f) \cdot e^{-j 2 \pi f \tau} d \tau
$$
where $x(t)$ is the signal, and $g(t, f)$ is the frequency-dependent Gaussian window, which is expressed as follows [44]:
$$
g(t, f)=\frac{|f|}{\sqrt{2 \pi}} e^{\left(\frac{t^2 f^2}{2}\right)}
$$
The presence of the variable $f$ renders the frequency-dependent window spread. Given that $X(t, f)$ is a complex value, the modulus $|X(t, f)|$ is usually plotted in practice to construct a time-frequency representation. The S-transform represents the local spectrum; thus, averaging the local spectrum over time generates the Fourier spectrum, which can be expressed as follows [44]:
$$
\int_{-\infty}^{\infty} X(t, f) d t=X(f)
$$
The signal in time representation $x(t)$ is exactly recoverable from $X(t, f)$ based on the following expression $[44,47]$ :
$$
x(t)=\int_{-\infty}^{\infty}\left\{\int_{-\infty}^{\infty} X(t, f) d t\right\} e^{j 2 \pi f t} d f
$$
In this study, de-noising is performed in the time-frequency representation, and the signal is recovered from the noise using Eq. (29).
The discrete S-transform is used in this study to allow the processing in the continuous S-transform. Let $x(n), n=0,1, \ldots(N-1)$ denote a discrete time series corresponding to $x(t)$ with a time sampling interval of $T_s$. The S-transform of the discrete time series $x(n)$ is expressed as:

$$
X(n, k)=\sum_{m=0}^{N-1} x(m-n) e^{\frac{-2 \pi^2 m^2}{k^2}} e^{\frac{-j 2 \pi m k}{N}}
$$
The inverse of the discrete S-transform is expressed as follows [48]: $x(n)=\frac{1}{N} \sum_{k=0}^{N-1}\left\{\sum_{n=0}^{N-1} X(n, k)\right\} e^{\frac{i 2 \pi n k}{N}}$

In this study, a de-noising method based on a time-frequency analysis is proposed, with the S-transform used as an alternative to the wavelet transform. A key feature of the S-transform is its capacity to uniquely combine a frequency-dependent resolution with the simultaneously localizing real and imaginary spectra [49]. In contrast

to the wavelet approach, the S-transform provides a frequency invariant amplitude response. Moreover, the S-transform uses a time-frequency axis rather than a time-scale axis, which is used in the wavelet transform. Therefore, the interpretation of the frequency information in the S-transform is more straightforward than that in the wavelet approach. Furthermore, the use of the S-transform is beneficial to the removal of noises for all frequency components [50].
The de-noising process using the S-transform is described as follows:
1. A discrete S-transform using Eq. (30) is applied to noisy signals (signals that are corrupted by UWAN and defined in Eqs. (1-4)), as shown in Fig. 7. Based on the properties of the discrete Fourier transform and convolution theorem, the S-transform in Eq. (30) can be considered a convolution process in the frequency domain between the signal $X(k)$ and the localizing scalable Gaussian window ( $k$. The S-transform can be expressed as
$$
\begin{aligned}
X(n, k) & =\sum_{m=0}^{N-1} x(m-n) e^{\frac{-2 \pi^2 m^2}{k^2}} e^{\frac{-j 2 \pi m k}{N}}=\sum_{m=0}^{N-1} x(m-n) w(m) e^{\frac{-j 2 \pi m k}{N}} \\
& =X(k) * W(k) e^{-j \frac{2 \pi n k}{N}}
\end{aligned}
$$
(k)
If the signal is considered in terms of real and imaginary components, Eq. (31) can be written as
$$
X(n, k)=\left[X_{r e}(k)+j X_{i m}(k)\right] * \quad W(k) e^{-j \frac{j \pi n k}{N}}
$$
$(k)$
$$
=\left[\begin{array}{cc}
X_{r e}(k) * W(k) e^{-j \frac{2 \pi n k}{N}}+j X_{i m}(k) * W(k) e^{-j \frac{2 \pi n k}{N}} \\
(k) & (k)
\end{array}\right]
$$
The complex exponential denoted by $\left(e^{-j \frac{2 \pi n k}{N}}\right)$ represents the shift of the window in the time domain.
2. A pre-whitening transform is applied to the input data before generating the time-frequency representation of noisy signals. The output of the pre-whitening filter is a colored version of the signal in additive white noise, as shown in Fig. 8.
3. After a pre-whitening transform is applied to the input data, de-noising is performed using soft thresholding by adaptive universal threshold estimation. Subsequently, a pre-whitening filter, which alleviates the need to calculate a separate threshold for every scale, is used. The use of a pre-whitening transform produces better results than that of applying level-wise thresholding on the data that was proposed in [51]. The threshold value applied to the time-frequency coefficients estimated by adaptive universal threshold estimation [52] is expressed as:
$$
\lambda=c \cdot \sigma_v \sqrt{2 \log (N)}
$$
where $N$ is the signal length, $\sigma_v$ is the noise standard deviation estimated for the first voice [53], and $c$ is the adaptive universal threshold factor $0<c<1$. The noise standard deviation for each voice is $\sigma_v=\frac{\operatorname{median}(|X(n, k)|)}{0.6745}$
where $X(n, k)$ represents all the coefficients for the first voice [51].
The threshold value $\lambda$ is used to remove noise and recover the original signal efficiently. The adaptive threshold factor $c$ is introduced to enhance the de-noising performance further [54]. The value of $c$ is determined by gradually changing it in increments of 0.1 for each voice to find the best results at the highest SNR.
According to Eq. (33), thresholding for both real and imaginary components of the spectrum should be performed in the

de-noising process in the frequency domain. Thus, the adaptive universal threshold estimation described in Eq. (34) should include both real and imaginary components. The threshold value is obtained as follows
$$
\begin{aligned}
& \lambda_{r e}=c . \sigma_{v, r e} \sqrt{2 \log (N)} \\
& \lambda_{i m}=c \cdot \sigma_{v, i m} \sqrt{2 \log (N)}
\end{aligned}
$$
where $\sigma_{v, k, r e}$ and $\sigma_{v, k, i m}$ are the noise standard deviations for the real and imaginary components, respectively. The $k$-th noise standard deviations are calculated as
$$
\begin{aligned}
\sigma_{v, r e} & =\frac{\operatorname{median}\left(\left|X_{r e}(n, k)\right|\right)}{0.6745} \\
\sigma_{v, i m} & =\frac{\operatorname{median}\left(\left|X_{i m}(n, k)\right|\right)}{0.6745}
\end{aligned}
$$
After the threshold values $\lambda_{k, r e}$ and $\lambda_{k, i m}$ are determined for the real and imaginary components, respectively, the time-frequency representations of the real and imaginary components after hard thresholding are
$$
\begin{aligned}
& X_{\lambda, r e}(n, k)=\left\{\begin{array}{l}
X_{r e}(n, k) i f\left|X_{r e}(n, k)\right|>\lambda_{r e} \\
0 i f\left|X_{r e}(n, k)\right| \leqslant \lambda_{r e}
\end{array}\right. \\
& X_{\lambda, i m}(n, k)=\left\{\begin{array}{l}
X_{i m}(n, k) i f\left|X_{i m}(n, k)\right|>\lambda_{i m} \\
0 i f\left|X_{i m}(n, k)\right| \leqslant \lambda_{i m}
\end{array}\right.
\end{aligned}
$$
Alternatively, the time-frequency representations of the real and imaginary components after soft thresholding are
$$
\begin{aligned}
& X_{\lambda, r e}(n, k)=\left\{\begin{array}{l}
\operatorname{sgn}\left(X_{r e}(n, k)\right)\left(\left|X_{r e}(n, k)\right|-\gamma_{k, r e}\right) i f\left|X_{r e}(n, k)\right|>\lambda_{r e} \\
0 i f\left|X_{r e}(n, k)\right| \leqslant \lambda_{r e}
\end{array}\right. \\
& X_{\lambda, i m}(n, k)=\left\{\begin{array}{l}
\operatorname{sgn}\left(X_{i m}(n, k)\right)\left(\left|X_{i m}(n, k)\right|-\gamma_{k, i m}\right) i f\left|X_{i m}(n, k)\right|>\lambda_{i m} \\
0 i f\left|X_{i m}(n, k)\right| \leqslant \lambda_{i m}
\end{array}\right.
\end{aligned}
$$
The time-frequency representation obtained by combining the real and imaginary components is
$$
X_\lambda(n, k)=X_{\lambda, r e}(n, k)+j X_{\lambda, i m}(n, k)
$$
4. The de-noised signal $x(n)$ in the time representation can be recovered using the inverse discrete S-transform in Eq. (31). The time-frequency representation of the noisy signal after the de-noising process and inverse whitening filter is shown in Fig. 9.

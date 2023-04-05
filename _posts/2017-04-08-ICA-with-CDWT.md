---
layout: post
title: ICA with CDWT 
description: ICA with CDWT 
summary: ICA with CDWT 
author:
- Pavan Donthireddy
usemathjax: true
tags: [BlindSourceSeperation, ICA, CDWT, STFT, DWT, wavelet, whitening, ICAissues]
---

<p align="justify">It is well known that if the original sounds are mixed in
the real environment (in the time domain) then the observed
sounds are a convolution mixture between the original
sounds with a delay and a reverberation. In order to simplify
this convolution mixture, it is a good idea to convert the
signal from the time domain into the time–frequency
domain and transform the convolution mixture into the
linear mixture by a time–frequency analysis method. By
doing this the drawback of poor performance with unsteady
sounds of the ICA also can be improved.</p>

<p align="justify">The time-frequency analysis method is usually a
combination of the [[ICA|ICA]], the Short Time Fourier Transform
(STFT) and the Discrete Wavelet Transform (DWT).</p>

<p align="justify">The STFT is probably the most common approach for
time–frequency analysis. It subdivides the signal into short
time segments (it is the same as using a small window to
divide the signal), and a discrete Fourier transform is
computed for each of these. For each frequency component,
however, the window length is fixed. So it is impossible to
choose an optimal window for each frequency component,
that is, the short time Fourier transform is unable to obtain
optimal analysis results for individual frequency
components.</p>

<p align="justify">On the other hand, the DWT that was
carried out by Mattal’s fast algorithm also has a drawback
of lacking shift invariance although it can solve the problem
of the window width and obtain optimal frequency
resolution for each frequency component. Fortunately,
in order to improve the fault, a Complex Discrete Wavelet
Transform (CDWT) was proposed and it has been applied
widely to signal and image analysis</p>

## ICA and CDWT for blind source seperation

In this method, the signals first were transformed from the time–domain into the
time–frequency domain by using the CDWT and then the ICA was carried out in the time–frequency domain. As in traditional methods, such as the STFT + ICA and the DWT + ICA, the following two problems when the ICA processing was carry out in the time–frequency domain
occurred. 
	1. Scaling problem: the signal’s amplitude and phase obtained by the ICA was changed, 
	2. Permutation problem: the separated signals are replaced at every frequency level mutually. 

This method discuss the technique for solving the scaling and the permutation problems. Finally, the separated signals are obtained by the inverse CDWT.

![ICA_CDWT](/assets/snips/ica_cdwt.png)


Here, the case of two sound sources and two mikes has been considered for simplicity. First of all,
the two sound signals $x_n(t) (n=1,2,$ where $n$ is the number of channels and $t$ is the time) were observed by mikes from two sound sources $s_{i}(t) ( i =1, 2)$. The relation between the observed signal $x_n(t)$ and the sound source $s_{i}(t)$ is as follows:

$$
x_{n}(t) = \mathbf{A_{n,i}}(t) \ast  S_{i}(t) \tag{1}
$$

where $\ast$ denotes convolution, the $\mathbf{A_{n,i}}(t)$ , is the impulse response that is from the sound sources to the mikes and can be shown as the following equation:

$$
\mathbf{A_{n,i}}(t) = \begin{bmatrix} 
a_{11}(t) & a_{12}(t)\\ a_{21}(t) & a_{22}(t)\\
\end{bmatrix}, n,i = 1,2 
$$

If one transforms the signal $x_{n}(t)$ from the time domain to the time–frequency domain by the CDWT then the (1) can be expressed as (2), in which the convolution of the sound source and the impulse response was changed to simple multiplication.

$$
x_{n}(\omega , T) = \mathbf{A_{n,i}}(\omega) S_{i}(\omega,T) \tag{2}
$$

where, $\omega$ is the frequency and $T$ the time in the time–frequency domain.

Next, whitening of the observed signal was carried out as follows:

$$
\hat{x}_{n}(\omega , T) = Q(\omega) x_{n}(\omega,T) \tag{3}
$$

where $\hat{x}_{n}(\omega ,T)$ 

is a whitened signal matrix and $Q(\omega)$ a whitened mixture, which can be obtained from the observed mixture signal $x_{n}(\omega , T)$ in each frequency.

Finally, the ICA was carried out by using the whitened signal matrix $\hat{x}_{n}(\omega , T)$ 

, in which the separation matrix $W(\omega)$ can be presumed. As a result, the separated signal $u_{i}(\omega , T)$ shown in (4) can be obtained.

$$
u_{i}(\omega , T) = W(\omega) \hat{x}_{n}(\omega,T) \tag{4}
$$

The convolution mixture signal $x_{n}(t)$  shown in (1) can be transformed into the linear mixture signal
$x_{n}(\omega, T)$ shown in (2) by using the CDWT which simplifies the preprocessing of the ICA. A complex wavelet like, RI-Daubechies 6 wavelet can be applied as the mother wavelet.

## Problem and correction rule of ICA processing

The ICA is a technique for presuming the sound source $s_{i}(\omega,T)$  and the inverse matrix of $A_{ni}(\omega)$ from statistics without any former information of the observed signal. In this case, the amplitude of the separated signal $u_{i}(\omega,T)$ is a constant times the amplitude of the sound source $s_{i}(\omega,T)$ and a correction is needed.

<p align="justify">In this method, a similar amplitude change at each frequency level also occurred in the preprocessing by CDWT introduced. This phenomenon is called a scaling irregularity. Furthermore,
same as in the traditional method, it is also possible that the separated sound is replaced with noise at every frequency
level mutually. This phenomenon is called the permutation
problem. Therefore, after these two problems are solved, the
inverse complex discrete wavelet transform is performed,
and it is necessary to restore the sound signal observed with
each mike.</p>

### Scaling problem and correction rule

Not only the amplitude of the restored signal but the phase also differs depending on the frequency by making for signal whitening (making no correlation). To take an arbitrary complex value by processing, this is caused. In order to solve the scaling irregularity problem, a method has
been proposed by Murata that uses the independent element $u_{i}(\omega,T)$ , which is obtained at each frequency and divides the spectrum. In this study, the method of correcting scaling is adopted from the divided spectrum and can be shown as follows:

$$
v_{1}(\omega,T)=\begin{bmatrix}
v_{11}(\omega,T)\\ v_{12}(\omega,T)
\end{bmatrix} = (W(\omega)Q(\omega))^{-1}\begin{bmatrix}
u_{1}(\omega,T) \\
0
\end{bmatrix}
$$

$$
v_{2}(\omega,T)=\begin{bmatrix}
v_{21}(\omega,T)\\ v_{22}(\omega,T)
\end{bmatrix} = (W(\omega)Q(\omega))^{-1}\begin{bmatrix} 0 \\
u_{2}(\omega,T) 
\end{bmatrix}
$$

where $v_{11}(\omega,T),v_{22}(\omega,T)$ are divided spectrums. If the sum $v_{1}(\omega,T)+v_{2}(\omega,T)$ is calculated then the sum $v_{11}(\omega,T)+v_{21}(\omega,T)$ is the mixture signal $x_{1}(\omega,T)$ and the sum $v_{11}(\omega,T)+v_{22}(\omega,T)$ is the mixture signal $x_{2}(\omega,T)$

### Permutation problem and correction rule

<p align="justify">The complex Fast-ICA performs separation based on
non-Gaussian characteristics. Therefore, the possibility of
the separating signal with higher non-Gaussian
characteristics being output as the first channel is very high.
However, the height of the frequency is not determined and
noise with low non-Gaussian characteristics might also be
output. </p>

Therefore, there is a possibility that the output of each frequency level is separated without being united by the sound. The separated signal $u_{1}(\omega,T), u_{2}(\omega,T)$ of the 1st and 2nd channel without permutation is shown as follows.

$$
u_{1}(\omega ,k) \approx s_{1}(\omega,T) \tag{5} ; u_{2}(\omega ,k) \approx s_{2}(\omega,T) 
$$

The above expression can be shown as the following equation by using the divided spectrum of the scaling correction.

$$
\begin{bmatrix}
v_{11}(\omega,T)\\ 
v_{22}(\omega,T)
\end{bmatrix} = \begin{bmatrix}
g_{11}(\omega,T)u_{1}(\omega,T) \\
g_{21}(\omega,T)u_{1}(\omega,T)
\end{bmatrix}
$$

$$
\begin{bmatrix}
v_{21}(\omega,T)\\ 
v_{22}(\omega,T)
\end{bmatrix} = \begin{bmatrix}
g_{12}(\omega,T)u_{2}(\omega,T) \\
g_{22}(\omega,T)u_{2}(\omega,T)
\end{bmatrix}
$$

On the other hand, when permutation occurs, (5) becomes the next expression

$$
u_{1}(\omega ,k) \approx s_{2}(\omega,T) \tag{6} ; u_{2}(\omega ,k) \approx s_{1}(\omega,T) 
$$

$$
\begin{bmatrix}
v_{11}(\omega,T)\\ 
v_{22}(\omega,T)
\end{bmatrix} = \begin{bmatrix}
g_{12}(\omega,T)u_{2}(\omega,T) \\
g_{22}(\omega,T)u_{2}(\omega,T)
\end{bmatrix}
$$

$$
\begin{bmatrix}
v_{21}(\omega,T)\\ 
v_{22}(\omega,T)
\end{bmatrix} = \begin{bmatrix}
g_{11}(\omega,T)u_{1}(\omega,T) \\
g_{21}(\omega,T)u_{1}(\omega,T)
\end{bmatrix}
$$

From these, we can know that the divided spectrum can be shown as a multiplication of the separated signal $u_{i}(\omega,T)$ and the transfer function $g_{ni}(\omega)$ , which is from the sound source to the mike.

The separation matrix $W(\omega)$ and the whitening matrix $Q(\omega)$ presumed by the ICA processing are used and the next equation can be obtained.

$$
D = (W(\omega)Q(\omega))^{-1} = \begin{bmatrix}
g_{11}(\omega) & g_{12}(\omega) \\
g_{21}(\omega) & g_{22}(\omega)
\end{bmatrix} = e\begin{bmatrix}
a_{11}(\omega) & a_{12}(\omega) \\
a_{21}(\omega) & a_{22}(\omega)
\end{bmatrix} = eA_{ni}(\omega), e \in \mathbb{R}
$$

## Conclusion

CDWT +Complex Value Fast ICA outperforms, STFT+ Complex value Fast ICA and DWT+Real Value Fast ICA

Reference : BLIND SOURCE SEPARATION BY COMBINING INDEPANDENT COMPONENT ANALYSIS WITH COMPLEX DISCRETE WAVELET TRANSFORM ZHONG ZHANG , TAKESHI ENOMOTO , TETSUO MIYAKE , TAKASHI IMAMURA
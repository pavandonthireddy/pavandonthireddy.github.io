---
layout: post
title: ON WHITENING FOR KRYLOV-PROPORTIONATE NORMALIZED LMS ALGORITHM
description: ON WHITENING FOR KRYLOV-PROPORTIONATE NORMALIZED LMS ALGORITHM 
summary: ON WHITENING FOR KRYLOV-PROPORTIONATE NORMALIZED LMS ALGORITHM
author:
- Pavan Donthireddy
usemathjax: true
tags: [adaptive_filtering, feedback, subspace_methods]
original: yukawa2008
---

## Introduction

<p align="justify">The tradeoffproblem between convergence speed and computational
complexity has been the most important and challenging issue in
adaptive filtering [1]. Since the birth of the classical least mean
square (LMS) algorithm, a variety ofalgorithms have been proposed,
such as the normalized LMS (NLMS) algorithm [2], the affine projection
algorithm (APA) [3,4], and the adaptive parallel subgradient
projection (PSP) algorithm [5].</p>

<p align="justify">Recently, the Krylov-proportionate normalized least-meansquare
(KPNLMS) algorithm has been proposed [6], which extends
the well-known (sparsity-based) proportionate normalized leastmean-
square (PNLMS) algorithm [7, 8] to a nonsparse estimandum
(system to be estimated). Here, sparse means that most components
have negligibly small magnitudes. The KPNLMS algorithm
constructs a set of orthonormal basis vectors, with which the estimandum
has sparse coefficients, by using a certain Krylov subspace,
and utilizes the sparsity for raising the speed of convergence. The
gain offered by KPNLMS depends on the energy ofthe estimandum
in the Krylov subspace.</p>

## PRELIMINARIES

### Problem Formulation

We consider a simple linear system model:
$$
d_k:=\boldsymbol{u}_k^T \boldsymbol{h}^*+n_k, k \in \mathbb{N}
$$
where $u_k:=\left[u_k, u_{k-1}, \cdots, u_{k-N+1}\right]^T \in \mathbb{R}^N$ is the input vector at time $k$ with the input process $\left(u_k\right)_{k \in \mathbb{N}}, \boldsymbol{h}^* \in \mathbb{R}^N$ the estimandum, $\left(d_k\right)_{k \in \mathbf{N}}$ the output process, and $\left(n_k\right)_{k \in \mathbf{N}}$ the noise process $\left(N \in \mathbb{N}^*:=\mathbb{N} \backslash\{0\}\right)$. Assume that the input and output data are available. An adaptive filter $\left(\boldsymbol{h}_k\right)_{k \in \mathrm{N}}$ is controlled in a recursive way for minimizing the mean-square error (MSE):
$$
\operatorname{MSE}(\boldsymbol{h}):=E\left\{e_k^2(\boldsymbol{h})\right\}, \boldsymbol{h} \in \mathbb{R}^N \text {. }
$$
Here, $E\{\cdot\}$ denotes expectation and $e_k: \mathbb{R}^N \rightarrow \mathbb{R}, \boldsymbol{h} \mapsto \boldsymbol{u}_k^T \boldsymbol{h}-d_k$, the error function at time $k$. The filter $\boldsymbol{h}_{\text {MMSE }} \in \mathbb{R}^N$ minimizing (2) is called the minimum MSE (MMSE) filter, characterized by the the so-called Wiener-Hopf equation: $\boldsymbol{R} \boldsymbol{h}_{\mathrm{MMSE}}=\boldsymbol{p}$, where $\boldsymbol{R}:=$ $E\left\{\boldsymbol{u}_k \boldsymbol{u}_k^T\right\} \in \mathbb{R}^{N \times N}$ and $\boldsymbol{p}:=E\left\{\boldsymbol{u}_k d_k\right\} \in \mathbb{R}^N$. The matrix $\boldsymbol{R}$ is mostly positive definite due to the presence of noise, and in this case, the MMSE filter is uniquely given by $\boldsymbol{h}_{\mathrm{MMSE}}=\boldsymbol{R}^{-1} \boldsymbol{p}$. In the following, the MMSE filter is denoted by $\boldsymbol{h}^*$, because $\boldsymbol{h}_{\mathrm{MMSE}}=\boldsymbol{h}^*$ under the natural assumption $E\left\{\boldsymbol{u}_k n_k\right\}=0$, where 0 denotes the zero vector.
### Brief Review of the KPNLMS Algorithm

The update equation of the KPNLMS algorithm is given as [6]
$$
\boldsymbol{h}_{k+1}=\boldsymbol{h}_k-\lambda_k e_k\left(\boldsymbol{h}_k\right) \frac{\boldsymbol{\Omega}_k \boldsymbol{u}_k}{\boldsymbol{u}_k^T \boldsymbol{\Omega}_k \boldsymbol{u}_k}, k \in \mathbb{N}
$$
Here, $\lambda_k \in[0,2]$ is the step size, and the matrix $\boldsymbol{\Omega}_k:=\boldsymbol{U} \boldsymbol{\Lambda}_k \boldsymbol{U}^T \in$ $\mathbb{R}^{N \times N}, k \in \mathbb{N}$, is positive definite with the orthogonal matrix $U \in$ $\mathbb{R}^{N \times N}$ and the positive diagonal matrix $\Lambda_k \in \mathbb{R}^{N \times N}, k \in \mathbb{N}$. The key is how to construct $\boldsymbol{U}$ and $\boldsymbol{\Lambda}_k$.

To explain the construction of the matrix $\boldsymbol{U}$, let us define, for a given $(N \geq) D \in \mathbb{N}^*$, a matrix-valued function $\boldsymbol{K}_D: \mathbb{R}^{N \times N} \times$ $\mathbb{R}^N \rightarrow \mathbb{R}^{N \times D}$ as
$$
\boldsymbol{K}_D(\boldsymbol{A}, \boldsymbol{b}):=\left[\boldsymbol{b}, \boldsymbol{A} \boldsymbol{b}, \cdots, \boldsymbol{A}^{D-1} \boldsymbol{b}\right], \forall \boldsymbol{A} \in \mathbb{R}^{N \times N}, \boldsymbol{b} \in \mathbb{R}^N .
$$
Then,
$$
\mathcal{K}_D(\boldsymbol{A}, \boldsymbol{b}):=\mathcal{R}\left\{\boldsymbol{K}_D(\boldsymbol{A}, \boldsymbol{b})\right\} \subset \mathbb{R}^N
$$
is called the $D$ th Krylov subspace associated with $\boldsymbol{A}$ and $\boldsymbol{b}$, where $\mathcal{R}\{\cdot\}$ stands for range.

The matrix $U \in \mathbb{R}^{N \times N}$ is constructed by orthogonalizing the columns of $\boldsymbol{K}_N(\widehat{\boldsymbol{R}}, \widehat{\boldsymbol{p}})$, where $\widehat{\boldsymbol{R}} \in \mathbb{R}^{N \times N}$ and $\widehat{\boldsymbol{p}} \in \mathbb{R}^N$ are estimates of $\boldsymbol{R}$ and $\boldsymbol{p}$, respectively. The construction of $\boldsymbol{\Lambda}_k$ borrows the idea of the PNLMS algorithm $[7,8]$. If the improved PNLMS (IPNLMS) algorithm [11] is adopted, the diagonal matrix is given as
$$
\boldsymbol{\Lambda}_k:=\operatorname{diag}\left\{\boldsymbol{\theta}^{(k)}\right\} \in \mathbb{R}^{N \times N}, k \in \mathbb{N}
$$
with
$$
\begin{aligned}
\boldsymbol{\theta}^{(k)} & :=\frac{1-\eta}{N} \mathbf{1}_N+\frac{\eta}{\left\|\tilde{\boldsymbol{h}}_k\right\|_1+\varepsilon}\left|\tilde{\boldsymbol{h}}_k\right| \in \mathbb{R}^N, k \in \mathbb{N}, \\
\tilde{\boldsymbol{h}}_k & :=\boldsymbol{U}^T \boldsymbol{h}_k \in \mathbb{R}^N, k \in \mathbb{N}, \\
\mathbf{1}_N & :=[1,1, \cdots, 1]^T \in \mathbb{R}^N .
\end{aligned}
$$
Here, $|\cdot|$ and $\|\cdot\|_1$ denote the elementwise absolute-value operation and 1-norm, respectively, $\eta \in(0,1)$ a parameter to control the amount of proportionality in the update, and $\varepsilon>0$ a small positive constant for regularization. If $\boldsymbol{U}=\boldsymbol{I}(\boldsymbol{I}$ : identity matrix), then KPNLMS coincides with PNLMS.

It should be mentioned that another key point of KPNLMS is simplification to keep $O(N)$ computational complexity per iteration, which is practically important but is omitted in this paper for conciseness (see [6]). Moreover, an extension of KPNLMS to complexvalued signals and its application to wireless communication systems will be presented at this workshop [12], in which the whitening is not used because the correlation of the input signals is fairly low.

## WHITENING IN THE KPNLMS ALGORITHM

The KPNLMS algorithm realizes fast convergence when
$$
\tilde{\boldsymbol{h}}^*:=\boldsymbol{U}^T \boldsymbol{h}^* \in \mathbb{R}^N
$$
is sparse; the sparsity is measured by a certain energy. In [6], only an intuitive discussion is given about the motivation for whitening in case of highly colored input signals.


### On Whitening for KPNLMS

Let $\boldsymbol{V} \in \mathbb{R}^{N \times N}$ (or $\boldsymbol{V} \in \mathbb{C}^{N \times N}$ ) be a prespecified orthogonal (or unitary) matrix, such as the DCT (discrete cosine transform) or the DFT (discrete Fourier transform) matrix. For simplicity, $\boldsymbol{V}$ is assumed to be real-valued in the following (an extention to the complex-valued case is straightforward). As in TDAF, the diagonal matrix is defined as
$$
\boldsymbol{D}_k:=\operatorname{diag}^{-1}\left\{\sigma_1^{(k)}, \sigma_2^{(k)}, \cdots, \sigma_N^{(k)}\right\}, k \in \mathbb{N}
$$
where, for given initial estimates $\sigma_n^{(0)}>0, n=1,2, \cdots, N$, $\sigma_n^{(k)}:=\zeta \sigma_n^{(k-1)}+(1-\zeta)\left[\boldsymbol{V} \boldsymbol{u}_k\right]_n^2>0, k \in \mathbb{N}$, with the forgetting factor $\zeta \in(0,1)$. Here, $[\cdot]_n$ is the $n$th element of a vector. Then, the whitened input vector is generated as
$$
\phi_k:=\boldsymbol{\Phi}_k^{1 / 2} \boldsymbol{u}_k \in \mathbb{R}^N, k \in \mathbb{N}
$$
with $\boldsymbol{\Phi}_k:=\boldsymbol{V}^T \boldsymbol{D}_k \boldsymbol{V} \in \mathbb{R}^{N \times N}, k \in \mathbb{N}$. The standard NLMS algorithm with the whitened input $\phi_k$ tracks the modified solution $\boldsymbol{\omega}^*$ characterized by $\boldsymbol{R}_\phi \boldsymbol{\omega}^*=\boldsymbol{p}_\phi\left(\Leftrightarrow \boldsymbol{R} \boldsymbol{\Phi}_k^{1 / 2} \boldsymbol{\omega}^*=\boldsymbol{p}\right)$, where $\boldsymbol{R}_\phi:=E\left\{\phi_k \phi_k^T\right\} \in \mathbb{R}^{N \times N}$ and $p_\phi:=E\left\{\phi_k d_k\right\} \in \mathbb{R}^N$. Hence, for letting the algorithm track the original solution $\boldsymbol{h}^*$, the update equation (12) with $\boldsymbol{v}_k=\phi_k\left(\boldsymbol{G}_k=\boldsymbol{\Phi}_k\right)$ should be left-multiplied by $\boldsymbol{\Phi}_k^{1 / 2}$, leading to
$$
\boldsymbol{h}_{k+1}=\boldsymbol{h}_k-\lambda_k e_k\left(\boldsymbol{h}_k\right) \frac{\boldsymbol{\Phi}_k \boldsymbol{u}_k}{\boldsymbol{u}_k^T \boldsymbol{\Phi}_k \boldsymbol{u}_k}, k<K_0,
$$
where $\boldsymbol{h}_k:=\boldsymbol{\Phi}_k^{1 / 2} \boldsymbol{w}_k ;$ (16) is nothing but (11) for $\boldsymbol{G}_k=\boldsymbol{\Phi}_k$. Once obtaining adequate estimates of $\boldsymbol{R}_{\boldsymbol{\phi}}$ and $\boldsymbol{p}_\phi$, we can construct the orthogonal matrix $\boldsymbol{U}$ as in the original KPNLMS algorithm.
Next is the construction of the diagonal matrix $\boldsymbol{\Lambda}_k$. Note that
1. $\boldsymbol{h}_k$ tracks $\boldsymbol{h}^*$;
2. (not the original solution $\boldsymbol{h}^*$ but) the modified solution $\boldsymbol{\omega}^*(=$ $\left.\boldsymbol{\Phi}_k^{-1 / 2} \boldsymbol{h}^*\right)$ tends to have large energy in $\mathcal{K}_D\left(\boldsymbol{R}_\phi, \boldsymbol{p}_\phi\right)$.
Thus, $\boldsymbol{\Lambda}_k$ should be constructed according, instead of $\tilde{\boldsymbol{h}}_k$, to
$$
\ddot{\boldsymbol{h}}_k:=\boldsymbol{U}^T \boldsymbol{\Phi}_k^{-1 / 2} \boldsymbol{h}_k
$$
The final and important point is how to combine $\boldsymbol{\Phi}_k$ and $\boldsymbol{\Omega}_k$. The original KPNLMS algorithm can be viewed as follows: (i) the input is modified by $\Omega_k^{1 / 2}$, and then (ii) the update equation (12) is left-multiplied by $\Omega_k^{1 / 2}\left(=G_k^{1 / 2}\right)$ for tracking the original solution $h^*$. In case that whitening is involved, the input $\phi_k$ is further modified by $\boldsymbol{\Omega}_k^{1 / 2}\left(=\boldsymbol{U} \boldsymbol{\Lambda}_k^{1 / 2} \boldsymbol{U}^T\right)$, implying that the solution $\boldsymbol{\omega}^*$ is also modified further by $\Omega_k^{1 / 2}$. Therefore, for tracking $\boldsymbol{h}^*$, the update equation with the doubly-modified input $\boldsymbol{v}_k=\Omega_k^{1 / 2} \boldsymbol{\phi}_k$ should be left-multiplied by $\boldsymbol{\Phi}_k^{1 / 2} \boldsymbol{\Omega}_k^{1 / 2}$, leading to
$$
\boldsymbol{h}_{k+1}=\boldsymbol{h}_k-\lambda_k e_k\left(\boldsymbol{h}_k\right) \frac{\boldsymbol{\Pi}_k \boldsymbol{u}_k}{\boldsymbol{u}_k^T \boldsymbol{\Pi}_k \boldsymbol{u}_k}, k \geq K_0,
$$
where $\boldsymbol{h}_k:=\boldsymbol{\Phi}_k^{1 / 2} \boldsymbol{\Omega}_k^{1 / 2} \boldsymbol{w}_k$ and $\boldsymbol{\Pi}_k:=\boldsymbol{\Phi}_k^{1 / 2} \boldsymbol{\Omega}_k \boldsymbol{\Phi}_k^{1 / 2}$. Simplification is possible to attain $O(N)$ complexity by following the way in [6].




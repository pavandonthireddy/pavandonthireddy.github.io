---
layout: post
title: A new approach to numerical differentiation
description:  A new approach to numerical differentiation
summary:  A new approach to numerical differentiation
author:
- Pavan Donthireddy
usemathjax: true
tags: [numerical_differentiation]
original: zhao2009
---


## Abstract

<p align="justify">In this paper we consider the numerical differentiation of functions specified by noisy data.
A new approach, which is based on an integral equation of the first kind with a suitable
compact operator, is presented and discussed. Since the singular system of the compact
operator can be obtained easily, TSVD is chosen as the needed regularization technique
and we show that the method calls for a discrete sine transform, so the method can be
implemented easily and fast.</p>

## Introduction

Numerical differentiation is a problem to determine the derivative of a function from the values on an interval or some scattered points. It arises from many scientific researches and applications, e.g., the identification of the discontinuous points in an image process [1]; the problem of solving the Abel integral equation [2]; the problem of determining the peaks in chemical spectroscopy [3] and some inverse problems in mathematical physical equations [4]. The main difficulty is that it is an ill-posed problem, which means that small errors in the measurement of a function may lead to large errors in its computed derivatives [5,4]. A number of techniques have been developed for numerical differentiation [6-8,4,9]. One type of method is to transform the differentiation problem into an operator equation of the first kind. In fact, for given $g(t) \in H^1[0,1]$, to find $f=D g=g^{\prime}$ is equivalent to solve the Volterra integral equation of the first kind
$$
\left(K_1 f\right)(s)=\int_0^s f(t) \mathrm{d} t=g(s)-g(0), \quad s \in[0,1] .
$$
In this paper we will point out the disadvantage of operator $K_1$ and a new operator which is a modified form of $K_1$ will be presented. Since a singular system of the new operator can be obtained easily, it seems natural to use the TSVD method for this problem and good results may be expected. A convergence result, analogous to the literature [4], will be obtained by our method. Comparing with the Tikhonov regularization method used in [4], the regularization parameter can be obtained easily by TSVD method. Moreover, it is well known that the Tikhonov method has a finite saturation index, which means that it is impossible to improve the convergence rates of the regularization solution with increasing smoothness assumption of exact solutions. But for TSVD method this disadvantage will be overcome. Moreover, we will point out that our method calls for a discrete sine transform when the noisy values of the function to be differentiated at the nodes are given, so the method can be implemented easily and fast.


## Numerical Implementation

In practical problem, the perturbed data of functions is usually given at nodes. In this case, our approach naturally calls for a discrete sine transform(DST) of the data.
Give $N+1$ knots
$$
t_j=j h, \quad h=\frac{1}{N}, j=0,1, \ldots, N
$$
and the noisy vector $\mathbf{g}^\delta=\left(\mathbf{g}_0^\delta, \mathbf{g}_1^\delta, \ldots, \mathbf{g}_N^\delta\right)$ of the vector $\mathbf{g}=\left(\mathbf{g}_0, \mathbf{g}_1, \ldots, \mathbf{g}_N\right)=\left(g\left(t_0\right), g\left(t_1\right), \ldots, g\left(t_N\right)\right)$ is given, and the condition
$$
\left\|\mathbf{g}^\delta-\mathbf{g}\right\| \leq \delta
$$
is assumed. Then we let $\overline{\mathbf{g}}=\left(\overline{\mathbf{g}}_0, \overline{\mathbf{g}}_2, \ldots, \overline{\mathbf{g}}_{N-1}\right)$, where,
$$
\overline{\mathbf{g}}_i=\mathbf{g}_i^\delta+(i-N) h \mathbf{g}_1^\delta+i h \mathbf{g}_N^\delta, \quad i=0,1, \ldots, N-1 .
$$
Then the expansion
$$
\overline{\mathbf{g}}_i=\sum_{k=1}^N C_k \sin (k \pi \mathrm{i} h)
$$
can be obtained, where the coefficients
$$
C_k=\frac{2}{N} \sum_{j=1}^N \mathbf{g}_j^\delta \sin (k \pi j / N), \quad k=1,2, \ldots, N .
$$
We let
$$
\mathbf{r}^n=\left(\mathbf{r}_0^n, \mathbf{r}_1^n, \ldots, \mathbf{r}_{N-1}^n\right)
$$
where
$$
\mathbf{r}_j^n=\sum_{k=n}^N C_k \sin (k \pi \mathrm{i} h)
$$


then we can give the approximate derivative of function $g$
$$
f^\delta(t)=\sum_{k=1}^m C_k k \pi \cos (k \pi t)
$$
where $m$ is determined by the discrepancy principle
$$
\left\|\mathbf{r}^{m+1}\right\| \leq \tau \widehat{\delta}<\left\|\mathbf{r}^m\right\|
$$
where
$$
\widehat{\delta}= \begin{cases}\delta, & \mathbf{g}_0^\delta=g(0), \mathbf{g}_N^\delta=g\left(t_N\right) \\ \tilde{\delta}, & \text { other cases. }\end{cases}
$$
In the following, we present numerical results of some examples. In all the cases, $N=2048$. The perturbed discrete data are given by
$$
\mathbf{g}_i^\delta=g\left(t_i\right)+\epsilon_i, \quad\left|\epsilon_i\right|<\delta_1
$$


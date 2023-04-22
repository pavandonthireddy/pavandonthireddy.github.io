---
layout: post
title: Signal Subspace low rank plus sparse decomposition
description:  Signal Subspace low rank plus sparse decomposition
summary:  Signal Subspace low rank plus sparse decomposition
author:
- Pavan Donthireddy
usemathjax: true
tags: [signal_enhancement, subspace_methods]
original: yuan2017
---

## Abstract

<p align="justify">In this paper, a new subspace speech enhancement method using low-rank and sparse decomposition is
presented. In the proposed method, we firstly structure the corrupted data as a Toeplitz matrix and estimate its effective
rank for the underlying human speech signal. Then the low-rank and sparse decomposition is performed with the
guidance of speech rank value to remove the noise. Extensive experiments have been carried out in white Gaussian
noise condition, and experimental results show the proposed method performs better than conventional speech
enhancement methods, in terms of yielding less residual noise and lower speech distortion.</p>

<p align="justify">In this paper, we propose a new subspace-based method
for speech enhancement based on the principle of low-rank
and sparse decomposition (LSD). The main idea behind our
method is motivated by the recent development of lowrank
and sparse theory [16]. According to this theory, if a
given corrupted data matrix Y has an underlying low-rank
structure, yet corrupted by sparse additive noises. The
underlying low-rank component L can be effectively
recovered by solving a convex optimization problem, even
if the noise is arbitrary in magnitude. In the time domain,
owing to the short-time stability of human speech, speech
signals can be assumed to have a low-rank structure. On
the other hand, due to the randomness of noise, background
noise is more variable and thus can be viewed as sparse and
high-rank. Thus LSD theory can be exploited to recover the
underlying speech from corrupted speech signals.</p>





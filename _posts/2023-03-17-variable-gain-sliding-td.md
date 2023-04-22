---
layout: post
title: A Variable Gain Sliding Mode Tracking Differentiator for Derivative Estimation of Noisy Signals
description: A Variable Gain Sliding Mode Tracking Differentiator for Derivative Estimation of Noisy Signals
summary: A Variable Gain Sliding Mode Tracking Differentiator for Derivative Estimation of Noisy Signals
author:
- Pavan Donthireddy
usemathjax: true
tags: [numerical_differentiaton, trend_estimation, tracking, differentiator]
original: yu2020
---

## Abstract

<p align="justify">Estimating reliable signal component and its derivatives from noisy feedback signal is
important in control systems. Toward this problem, this article presents a new model-free variable gain
sliding mode tracking differentiator for derivative estimation of noisy signals by modifying a Levant and Yu's
sliding mode tracking differentiator. Specically, different from Levant and Yu's TD, the new TD employs
an additional variable that contributes to overshoot reduction. In addition, the new TD adaptively changes
its gains for improving the tracking and ltering performances. Moreover, the new TD only uses previous
output values and it does not require input signal model in advance. The advantages of the new TD over
previous TDs are conrmed through numerical examples.</p>

## Introduction

<p align="justify">Estimating reliable signal component and its derivatives from
noisy feedback signal is important in control systems. Tra-
ditional linear lters [1] are simple in structure and low in
computational cost, and thus they are often the rst option.
However, in the case of strong noise reduction, a linear lter
introduces a signicant phase lag in the output. In addition,
a linear lter proportionally transfers any signal component
into the output. These problems of linear lters may cause
instability of the controlled system in the case where system
hardware generates signicant phase lag and noise compo-
nent has high amplitude.</p>

<p align="justify">Sliding mode tracking differentiators are studied for avoid-
ing the disadvantages of linear lters. For example, Han and
Wang [2] proposed a sliding mode tracking differentiator
(TD [2]), of which the sliding surface takes a parabolic
curve-like shape. One major advantage of TD [2] is that it
realizes minimum-time convergence. Because of its effective-
ness, TD [2] has been applied in many applications, such as
The associate editor coordinating the review of this manuscript and
approving it for publication was Geng-Ming Jiang .
vehicle suspension system [3], induction motor system [4]
and wind turbine system [5].</p>

<p align="justify">However, TD [2] is prone to
overshoot during convergence. Jin et al. [6] presented a mod-
ication of TD [2] by introducing a multi-level set-valued
mapping (TD [6]). It is reported that, compared with TD [2],
TD [6] is less prone to overshoot, and it produces smaller
phase lag. After that, extensions of TD [6] are reported in the
literature [7][10]. However, this class of tracking differentia-
tors is limited to estimations of the input and its the 1st-order
derivative.</p>

<p align="justify">Another class of sliding mode tracking differentiators that
proposed by Levant and his colleagues received consider-
able attention in recent years. Specically, in [11], Lev-
ant proposed 2nd-order tracking differentiator (TD [11])
that effectively estimates useful signal component and its
1st-order derivative from the input. Due to simple structure,
easy design procedure and high tracking accuracy, TD [11]
has been widely applied in control systems [12][14]. How-
ever, TD [11] is also limited to 1st-order derivative.
Toward the problem of high-order derivative estimation,
in a subsequent study [15], Levant presented a TD [11]'s
extension (TD [15]) that realizes the estimation of arbitrary</p>
<p align="justify">order derivative of the input. In addition, TD [15] can effec-
tively remove small magnitude noise contained in the input,
and it can reduce the chattering phenomenon by increasing
the system order. After that, in [16], Levant and Yu proposed
a TD [15]'s modication (TD [16]) that provides better track-
ing accuracy and ltering performance than TD [15] does.
However, the performance of TD [16] is still not satisfactory
enough in the cases where the magnitude of noise is high and
the frequency range of the input is board. Moreover, TD [16]
and its predecessors produce signicant overshoot during the
convergence.
</p>


<p align="justify">Some variable gain techniques can be applied for improv-
ing the performance of Levant and his colleagues' tracking
differentiators. For example, in [17], a method of constructing
adaptive variable gains is presented. Although the method
improves the tracking performance, but the variable gains
are constructed based on the input signal model, which can-
not be always obtained in advance. As another example,
in [18][21], state-norm observer based adaptive variable
gain techniques are introduced for improving tracking per-
formance. </p>

<p align="justify">However, the construction of state-norm observer
requires lower and upper bounds for the parameters of the
system dynamic model as well as the noise source.
This article presents a new model-free variable gain sliding
mode tracking differentiator for derivative estimation of noisy
signals (new TD), which is an improvement of TD [16].
Concretely, different from TD [16], the new TD employs
an additional variable that contributes overshoot reduction.
In addition, the new TD adaptively changes its gains for
improving the tracking and ltering performances. Moreover,
the new TD only uses previous output values, and it does not
require input signal model in advance. 
</p>


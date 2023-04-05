---
layout: post
title: ICA 
description: Blind source seperation based on ICA
summary: Blind source seperation based on ICA
author:
- Pavan Donthireddy
usemathjax: true
tags: [BlindSourceSeperation, ICA]
---

The main idea can be briefly expressed by the following mixed model:
$$ x(t) = \mathbf{A} s(t) + n(t) $$
The statistical model in the above equation is called ICA model, which describes how the observed data are mixed through the components $s(t)$ . The $m$ dimension column vector $x(t)$ is the observed data. $\mathbf{A}$ is a $m \times n$ mixing matrix; $n(t)$ denotes the additive noise vector. The matrix $\mathbf{A}$ is assumed to be unknown. All we observe is the random vector x(t) , and we must estimate both Aand s(t) . Since $\mathbf{A}$ is unknown, so $s(t)$ seems to be unsolvable. 

Fortunately, there are many mathematical methods for calculating the coefficients of $\mathbf{A}$ by requiring the High-Order Statistics (HOS) information during the search for independent
components. 
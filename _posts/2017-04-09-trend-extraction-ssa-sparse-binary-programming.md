---
layout: post
title: Trend extraction with SSA and Sparse Binary Programming 
description: Trend extraction with SSA and Sparse Binary Programming 
summary: Trend extraction with SSA and Sparse Binary Programming 
author:
- Pavan Donthireddy
usemathjax: true
tags: [trend_extraction, SSA, sparse_binary_programming]
---

<p align="justify">The underlying trend is approximated by the sum of a part of [[Single Spectrum Analysis|SSA]] components, in which the total number of the SSA components in the sum is minimized subject to a specification on the maximum absolute difference between the original signal and the approximated underlying trend.</p>

As the selection of the SSA components is binary, this selection problem is to minimize the $L_{0}$ norm of the selection vector subject to the $L_{\infty}$ norm constraint on the difference between the original signal and the approximated underlying trend as well as the binary valued constraint on the elements of the selection vector. 

<p align="justify">This problem is actually a sparse binary programming problem. To solve this problem, first the corresponding continuous valued sparse optimization problem is solved. That is, to solve the same problem without the consideration of the binary valued constraint. This problem can
be approximated by a linear programming problem when the
isometry condition is satisfied, and the solution of the linear
programming problem can be obtained via existing simplex
methods or interior point methods.</p>

<p align="justify">By applying the binary
quantization to the obtained solution of the linear programming
problem, the approximated solution of the original sparse
binary programming problem is obtained. Unlike previously
reported techniques that require a pre-cursor model or
parameter specifications, the proposed method is completely
adaptive.</p>

### Details

<p align="justify">The conventional approach for selecting SSA
components for extracting the underlying trend is to employ
only the first several SSA components. However, this
selection rule fails when the underlying trend of a signal has a
complicated structure such as a high order polynomial
structure which cannot be characterized by only the first
several SSA components.</p>

<p align="justify">The idea is to formulate the
selection problem as a sparse binary programming problem and proposes an efficient methodology for approximating
the solution of the problem. In particular, the selection
problem is formulated as follows. The number of the
components to be selected is minimized subject to a
specification on the maximum absolute difference between
the approximated underlying trend and the original signal as
well as the binary valued constraint on the selection
coefficients. </p>

<p align="justify">Since the sparse binary programming problem is
nonsmooth, nonconvex and NP hard, it requires an exhaustive
search for finding the solution. As a result, the computational
effort for finding the solution is very large and an efficient
algorithm for approximating the solution is very useful and
important. </p>

To address these issues, the corresponding continuous valued optimization problem (the same
optimization problem without the consideration of the binary valued constraint) is considered. Although this continuous valued optimization problem is with an $L_{0}$ objective function
subject to an $L_{\infty}$ norm constraint, this problem can be approximated by a linear programming problem when the isometry condition is satisfied, and the solution of the linear programming problem can be efficiently obtained via existing simplex methods or interior point methods. 

By applying the binary quantization to the obtained solution of this linear programming problem, the approximated solution of the original sparse binary programming problem is
obtained.

## Methodology 

SSA is a nonparametric approach which does not need a priori specification on the model of the time series. It is very useful for extracting the underlying trend of a signal by selecting a subgroup of all $D$ SSA components and representing the underlying trend as the sum of the selected components. 


Here, it is required to determine how to partition the index set into $2$ disjoint subsets $I_{1}$ and $I_{2}$ , in which they represent the underlying trend and the residual of the signal, respectively. 


However, how to adaptively select the SSA components corresponding to the underlying trend is still an unsolved problem.

In order not to select the irregularities in the original signal, only the most important SSA components corresponding to the underlying trend of the signal are selected.

The selection problem is formulated as the following sparse sparse binary programming problem. 

$$
z^{*}= \begin{bmatrix}
z_{1}^{*}& \dots, z_{D}^*
\end{bmatrix}^{T}= \mathrm{argmin}_{z} \lVert z\lVert_{0}
$$


subject to $\lVert Az-x\lVert_{\infty} \le \epsilon$ and $z_{i}\in\{0,1\}$ for $i=1,\dots,D$. 


Here 

$$
A=[\tilde{x}_1,\dots,\tilde{x}_D]\in R^{N \times D}
$$ 

and 

$$
\epsilon=0.5\mathrm{max}_{n}(e_{up}(n)-e_{low}(n))
$$

where $e_{up}(n)$ and $e_{low}(n)$ are the upper and lower envelopes of $x(n)$, respectievely.

If $z_{i}^{\ast}=1$ (or $z_{i}^{\ast}=0$), then the corresponding component $\tilde{x}_i$ for $i=1,\dots,D$ is selected (or excluded) for the representation of the underlying trend. 

Since the total number of the selected components is minimized, the obtained solution is sparse and only the important SSA components corresponding to the underlying trend are selected. On the other hand, $L_{\infty}$ norm specification forces the underlying trend to follow the global change of the original signal. 

In order to solve this sparse binary optimization problem, the corresponding $L_{0}$ norm continuous valued optimization
problem is considered first. The solution of the $L_{0}$ norm
continuous valued optimization problem is approximated by
the solution of the corresponding $L_{1}$ norm continuous valued
optimization problem when the isometry condition is satisfied. That is, to solve the following optimization problem:

$$y^{*}= [y_{1}^{*},\dots,y_{D}^{*}]= \mathrm{arg}\min_{y}\lVert y\lVert_{1} \text{  subject to } \lVert Ay-x\lVert_{\infty}\le \epsilon $$


By further applying the quantization on $y_{i}^{*}$ for $i=1,\dots,D$ to either $0$ or $1$ via the following operator. 

$$
W_{i}^{*}=
\begin{cases}
1 &  y_{i}^{*}\ge 0.5\\
0 &  y_{i}^{*}< 0.5
\end{cases}
$$

the corresponding component $\tilde{x}_{i}$ 

for is selected (excluded) for the representation of the underlying trend if 

$W_{i}^{\ast}=1( \text{ or } W_{i}^{\ast}=0)$

Finally the underlying trend of the signal is obtained by 

$$
\Gamma = AW^*
$$

where $W^{\ast}= [W_1^{\ast},\dots,W_D^{\ast} ]^T$. The quantized solution is employed for the approximation of the solution of original [[Sparse representation of signals|sparse binary programming problem]]. It is found that the solution obtained by the proposed method is very close to the actual solution of the original sparse binary programming
problem. That is, $W^{\ast}$ in is very close to $z^{\ast}$ above. 


Therefore, the subset $I_{1}$ can be obtained by

$$
I_{1} = \{i\vert W_{i}^{*}= 1, 1\le i 
\le D\}
$$

After obtaining the underlying trend $\Gamma$ for the first $N$ points, the above SSA procedure can be applied for the prediction of the underlying trend for future time indices. 

Denote $\Gamma =[\gamma(1), \dots, \gamma(N)]^T$. In order to predict the underlying trend in the future time indices, we assume that
there is an underlying structure in the time series and this
structure is preserved for the time period to be predicted. A
prediction model based on the linear recurrent formulae (LRF)
is employed.


That is, the points $\gamma(N-L+2), \dots, \gamma(N)$ are employed for the prediction of $\gamma(N+1)$, and so on. In other words, 

$$
\gamma(n+1) = \sum_{k=0}^{L-2}a_{k}\gamma(n-k) \text{   for  } n\ge N,
$$

where the coefficient vector of the LRF denoted as $R=(a_{L-2}, \dots, a_{0})^T$ is given by 

$$
R = \frac{1}{1-\nu^{2}}\sum_{i\in I_{1}}\pi_{i}U_{i}^{\nabla}
$$

Here, $\nu^{2=}\sum_{i\in I_{1}}\pi_{i}^2$, $\pi_{i}$ is the last element in $U_{i}$, and $U_{i}^{\nabla }\in R^{L-1}$ is the vector only containing the first $L-1$ elements of $U_{i}$ for $i \in I_{1}.$ 
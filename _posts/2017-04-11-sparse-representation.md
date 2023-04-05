---
layout: post
title: Sparse representation of signals
description: Sparse representation of signals
summary: Sparse representation of signals
author:
- Pavan Donthireddy
usemathjax: true
tags: [representation, sparse_binary_programming]
---
<p align="justify">Sparse representation is widely employed for expressing signals using very few linear combinations of elementary signals. These elementary signals are called atoms. Since the
number of the atoms is more than the dimension of the signal
space, any signal can be represented by linear combinations
of these atoms and the representations are not unique.</p> 

Sparse representation is to use the minimum number of atoms to express the signals and this is actually an $L_{0}$ norm optimization problem. That is for a given overcomplete dictionary $A\in\Re^{N \times M}$ and a signal $x\in R^{N \times 1}$, where $N<M$ and $R^{a \times b}$ denotes the space of $a \times b$ real valued matrices, the representation problem is to find $z\in\Re^{M \times 1}$ such that $x=Az$ and $\lVert z\lVert_{0}$ is minimized. That is 
$$
z_{0}^{\ast} = \mathrm{argmin}_{z} \lVert z\lVert_{0} \text{  subject to  } x=Az \tag{1}
$$

Here $\lVert z\lVert_{0}$ denotes $L_{0}$ norm of $z$, which is equivalent to the number of nonzero elements in $z$.

The problem defined in (1) is nonconvex, nonsmooth and NP hard, it requires an exhaustive search for finding the solution. An approximate solution can be obrtained by solving the corresponding $L_{1}$ norm optimization problem if the isometry condition is satisfied. The $L_{1}$ norm optimization is as follows

$$
z_{1}^{\ast} = \mathrm{argmin}_{z} \lVert z\lVert_{1} \text{  subject to  } x=Az \tag{2}
$$

Although $z_{1}^{\ast}$ is a good approximation of $z_{0}^{\ast}$ when the isometry condition is satisifed, these two solutions will be very different if $x$ contains significant amount of noise. Nevertheless, this is the typical case in practical circumstances. Hence the exact equality constraint is usually related to an inequality constraint as follows. 

$$
z^{\ast} = \mathrm{argmin}_{z} \lVert z\lVert_{1} \text{  subject to  } \lVert Az-x\lVert_{\infty} \le \epsilon \tag{3}
$$

where $\epsilon$ is the specification on the maximium absolute difference between $Az$ and $x$. This problem can be efficiently solved via reformulating the $L_{1}$ norm optimization problem to a linear programming problem.

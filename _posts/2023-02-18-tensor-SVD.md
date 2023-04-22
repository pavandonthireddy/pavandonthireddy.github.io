---
layout: post
title: Tensor Singular value decomposition
description: Tensor Singular value decomposition
summary: Tensor Singular value decomposition
author:
- Pavan Donthireddy
usemathjax: true
tags: [SVD, linear_algebra]
original: new
---


# Tensor Singular Value Decomposition (SVD)

Tensor Singular Value Decomposition (SVD) is a powerful mathematical tool that decomposes a higher-order tensor into a set of lower-order tensors with orthogonal bases. In this article, we will explore the concept of tensor SVD, its applications, and how it is computed using mathematical equations.

## Introduction

A tensor can be defined as a multidimensional array of numerical values. For instance, a 2D tensor is a matrix, a 3D tensor is a cube, and a higher-order tensor is a multidimensional array. Tensor SVD is used to decompose a tensor into a set of lower-order tensors with orthogonal bases. 

## SVD in Matrix Form

To understand the concept of SVD for tensors, let us first look at SVD for matrices. For a given matrix A, its SVD can be written as:

$$ A = U \Sigma V^T $$

Here, U and V are orthogonal matrices, and $\Sigma$ is a diagonal matrix with non-negative real numbers on the diagonal, known as the singular values. 

## SVD for Tensors

Now, let us extend the concept of SVD to tensors. For a given tensor $\mathcal{X}$ with dimensions $I_1 \times I_2 \times \cdots \times I_N$, its SVD can be written as:

$$ \mathcal{X} = \sum_{r=1}^R \lambda_r \mathbf{u}_r \circ \mathbf{v}_r $$

Here, $\lambda_r$ is a non-negative singular value, and $\mathbf{u}_r$ and $\mathbf{v}_r$ are orthogonal vectors with dimensions $I_k \times 1$ for $k=1,2,\cdots,N$. The symbol $\circ$ denotes the outer product of two vectors.

## Tensor SVD in 1D Case

Let us now consider the 1D case of tensor SVD. In this case, the tensor $\mathcal{X}$ can be represented as a vector $\mathbf{x}$ of length $I_1 \times I_2 \times \cdots \times I_N$. Its SVD can be written as:

$$ \mathbf{x} = \sum_{r=1}^R \lambda_r \mathbf{u}_r \mathbf{v}_r^T \mathbf{x} $$

Here, $\mathbf{u}_r$ and $\mathbf{v}_r$ are orthogonal vectors with dimensions $I_1 \times 1$ and $I_2 \times 1$, respectively. 

To compute the SVD of a tensor in the 1D case, we first calculate the covariance matrix $C = \mathbf{x} \mathbf{x}^T$. We then calculate its eigenvectors and eigenvalues, which can be used to compute the orthogonal bases $\mathbf{u}_r$ and $\mathbf{v}_r$, as well as the singular values $\lambda_r$.

## Applications of Tensor SVD

Tensor SVD has many applications in data analysis and machine learning. It is used for dimensionality reduction, feature extraction, data compression, and clustering, among other things. It is also used in image and video processing, where tensors are used to represent higher-dimensional data. 

## Conclusion

In conclusion, Tensor Singular Value Decomposition (SVD) is a powerful mathematical tool that decomposes a higher-order tensor into a set of lower-order tensors with orthogonal bases. 


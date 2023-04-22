---
layout: post
title: Nearest Subspace Classification
description: Nearest Subspace Classification 
summary: Nearest Subspace Classification 
author:
- Pavan Donthireddy
usemathjax: true
tags: [classification, timeseries, subspace_methods]
original: new
---

# Nearest Subspace Classification

Nearest Subspace Classification (NSC) is a classification algorithm that is used to classify high-dimensional data into different categories. It is based on the idea that the data can be represented as a subspace in a higher-dimensional feature space, and the nearest subspace to a new observation can be used to classify it into one of the predefined categories.

## Subspace Representation

Let $X$ be a matrix of size $n \times p$, where $n$ is the number of data points and $p$ is the number of features. Let $Y$ be a vector of size $n \times 1$, where each element $y_i$ is the label of the corresponding data point $x_i$.

We can represent the data points in $X$ as subspaces in a higher-dimensional feature space by using a linear projection. Let $V$ be a matrix of size $p \times k$, where $k < p$, that represents the projection matrix. The subspace representation of a data point $x_i$ is then given by:

$$
\hat{x_i} = VV^T x_i
$$

The subspace representation of the entire dataset can be obtained by computing the projection of $X$ onto the subspace spanned by $V$:

$$
\hat{X} = XV(XV)^+
$$

where (+) denotes the Moore-Penrose pseudoinverse. The subspace spanned by $V$ is also called the column space of $V$.

## Nearest Subspace Classification

Given a new data point $x$, the goal of NSC is to classify it into one of the predefined categories based on its subspace representation. The basic idea is to compute the distance between the subspace representation of $x$ and the subspace representations of each category, and classify $x$ into the category with the smallest distance.

Let $C_i$ be the set of data points in class $i$, and let $V_i$ be the matrix that represents the subspace spanned by the data points in $C_i$. The distance between the subspace representation of $x$ and the subspace spanned by $V_i$ is given by:

$$
d_i = \|x - V_iV_i^Tx\|
$$

The classification rule of NSC is then to classify $x$ into the category with the smallest distance:

$$
\hat{y} = \operatorname*{argmin}_{i=1}^k d_i
$$

where $k$ is the number of categories.

## Algorithm

The algorithm for NSC can be summarized as follows:

1. Given a labeled training dataset $X$ and $Y$, compute the subspace representations of each class by computing the projection matrix $V$ for each class.
2. Given a new data point $x$, compute its subspace representation using the projection matrix $V$.
3. For each class $i$, compute the distance between the subspace representation of $x$ and the subspace spanned by the data points in class $i$.
4. Classify $x$ into the category with the smallest distance.

## Advantages and Disadvantages

NSC has several advantages over other classification algorithms, including:

- It can handle high-dimensional data by representing the data as subspaces in a higher-dimensional feature space.
- It is robust to noise and outliers, since the subspace representation of the data is obtained by a linear projection.
- It can handle non-linear decision boundaries by using a non-linear projection.

However, NSC also has some disadvantages:

-   It is sensitive to the choice of projection matrix $V$, which can affect the performance of the classifier. In practice, multiple projection matrices can be used and the best one can be selected using cross-validation or other methods.
-   It assumes that the data points in each class are drawn from a single subspace, which may not always be true in practice.
-   It may not perform well on imbalanced datasets, where some classes have significantly fewer data points than others. In this case, it may be necessary to use techniques such as oversampling or undersampling to balance the dataset.


---
layout: post
title: Nearest Subspace with Discriminative Regularization for Time Series Classification
description: Nearest Subspace with Discriminative Regularization for Time Series Classification
summary: Nearest Subspace with Discriminative Regularization for Time Series Classification
author:
- Pavan Donthireddy
usemathjax: true
tags: [classification, timeseries, subspace_methods]
original: zhao2018
---

## Abstract

<p align="justify">For time series classification (TSC) problem, many studies
focus on elastic distance measures for comparing time series and complete
the task with the help of Nearest Neighbour (NN) classifier. This
is mainly due to the fact that the order of variables is a crucial factor for
time series. Unlike the NN classifier only considers one training sample,
in this paper, we propose an improved Nearest Subspace (NS) classifier
to classify new time series. By adding a discriminative regularization
item, the improved NS classifier takes full advantage of all training time
series of one class. Two kinds of discriminative regularization items are
employed in our method. One is directly calculated based on Euclidean
distance of time series. For the other, we obtain the regularization items
from a lower-dimensional subspace. Two well-known dimensional reduction
methods, Generalized Eigenvector Method (GEM) and Local Fisher
Discriminant Analysis (LFDA), are employed to complete this task. Furthermore,
we combine these improved NS classifiers through ensemble
schemes to accommodate different time series datasets</p>

## Introduction

<p align="justify">The empirical studies have shown that the simple 1-NN classifier can get high accuracy and is very hard to beat. So numerous TSC studies
focus on how to calculate the distance between two time series. The standard
benchmark distance measure is Euclidean distance (ED), but it cannot handle
the slight phase shift of time series.</p>

<p align="justify">To overcome this drawback, Ratanamahatana
and Keogh [26] propose to utilize dynamic time warping (DTW) distance to
mitigate against distortions in the time axis. By extensive experiments, Ding
et al. [9] validate that DTW with a proper warping window size set is commonly
accepted as the standard measures. </p>

<p align="justify">Another way to deal with this phase shift is
based on edit distance to measure the similarity.
Due to the characteristic of DTW and edit distance, lots of studies try to
improve elastic distance measures based on these two techniques for TSC task.
Jeong et al. [14] propose a modified DTW that weights against large warping
(WDTW) by adding a multiplicative weight penalty.</p>

<p align="justify">Another improvement of
DTW, called DDTW, which transforms the time series into a series of first-order
differences [17]. By this transformation, DDTW can avoid the scenarios that a
single point on one time series may map onto a large number of points of another
time series. Meanwhile, it also can be used in conjunction with standard DTW to
calculate similarity between time series simultaneously [11]. </p>

<p align="justify">Several approaches
based on the edit distance are also proposed, such as edit distance with real
penalty (ERP) [6], time warp edit (TWE) [22] and move-split-merge (MSM)
[27] distance. A recent work [20] combines most of elastic distance measures
through ensemble schemes to improve the accuracy.</p>

<p align="justify">Although the NN classifier with elastic distance measure has the advantages
of simplicity, the label prediction of new instance relies on the special training
samples. In this paper, we propose an improved nearest subspace (NS) method
to deal with the TSC problem, which considers all training samples of one class
when predicting the new instance’s label. </p>

<p align="justify">This is a linear combination way and
the similar idea has been used in other research field [7,19]. In this method,
the most important factor is the combination coefficients of training samples.
We get the coefficients based on the differences between the new instance and
each training sample. </p>

<p align="justify">Concretely, we calculate the distances between them and
take these distances as weighted items to regularize the coefficients. In this way,
the training time series which has a large distance with the new instance will
be assigned a small coefficient. It’s the biggest difference between our method
and NN classifier. </p>


<p align="justify">By the discriminative regularization item, the improved NS
method not only considers the most similar training samples with a new instance
but also takes other training time series into account.
To achieve higher performance, we map the time series into the lowdimensional
space where the samples with the same label are closer and the different
classes are more separate. </p>

<p align="justify">Thus, the weighted regularization items obtained
in the low-dimensional space are more powerful for the improved NS method.
We employ two well-known dimensionality reduction methods, GEM [15] and
LFDA [28], for this task. Furthermore, ensemble schemes which combine different
weighted regularization items are proposed to suit different kinds of time
series dataset. The extensive experiments demonstrate that the proposed method
can gain better performance than NN classifier with different elastic distance
measures.</p>


### Basic Nearest Subspace Algorithm

The NN classifier may be the simplest supervised method to predict the label of a test instance. Essentially, it seeks the best representation of a test instance in term of one training sample. Unlike NN algorithm, the nearest subspace (NS) classifier (e.g. $[18,21])$ takes all training samples of each class into consideration and tries to find the best representation by fitting the test instance. Formally, we assign a test instance $y$ to class $i$ if the distance from $y$ to the subspace spanned by all samples $\boldsymbol{X}_i=\left[\boldsymbol{x}_{i, 1}, \ldots, \boldsymbol{x}_{i, n_4}\right]$ of class $i$ is the smallest one among all classes, i.e.,
$$
r_i(\boldsymbol{y})=\min _{\boldsymbol{\alpha}_i \in \mathbb{R}^{n_1, i \in\{1, \ldots, K\}}}\left\|\boldsymbol{y}-\boldsymbol{X}_i \boldsymbol{\alpha}_i\right\|_2
$$
where $\boldsymbol{\alpha}_i$ is a fitting coefficient vector.
One may notice that the Eq. (1) is easily overfitting which makes the problem ill-posed when we attempt to get the best solution. In general, we can introduce an additional regularization item to prevent overfitting. An alternative is to restrict the variation of $\boldsymbol{\alpha}$ by adding an $L_2$-regularization term:
$$
\widetilde{\boldsymbol{\alpha}}_i=\underset{\alpha_i \in \mathbb{R}^{n_i}}{\arg \min }\left\|\boldsymbol{y}-\boldsymbol{X}_i \boldsymbol{\alpha}_i\right\|_2^2+\lambda\left\|\boldsymbol{\alpha}_i\right\|_2^2
$$
## Improved Nearest Subspace Classifier

In Eq. (2), $L_2$-norm is employed to overcome the ill-posed problem of NS algorithm. It's optional to restrict parameter $\boldsymbol{\alpha}_i$, but for classification, the uniform weight for each element $\alpha_{i, j}\left(j \in\left\{1, \ldots, n_i\right\}\right)$ does not consider the differences between training samples. In this paper, we want to utilize a non-uniform regularization to improve nearest subspace classifier. Like NS with $L_2$-regularization, we still calculate the residual for each class and assign the test instance to the class with the minimum residual. The difference is that we utilize Tikhonov regularization [10] with non-uniform weight to replace the simple $L_2$-regularization. The non-uniform regularization can penalize the dissimilarity training samples with a specific test instance $y$ from being assigned large contributions when constructing $\tilde{\boldsymbol{y}}_i$. Thus, the approximation coefficients can be formulated as
$$
\widetilde{\boldsymbol{\alpha}}_i=\underset{\alpha_i \in \mathbb{R}^{n_i}}{\arg \min }\left\|\boldsymbol{y}-\boldsymbol{X}_i \boldsymbol{\alpha}_i\right\|_2^2+\lambda\left\|\boldsymbol{\Gamma}_{i, y} \boldsymbol{\alpha}_i\right\|_2^2
$$


where $\boldsymbol{\Gamma}_{i, y}$ is the weight matrix to measure the similarity between $\boldsymbol{y}$ and each sample of class $i$. In the following, we utilize Euclidean distance to describe $\boldsymbol{\Gamma}_{i, y}$ and discuss the effect of $\boldsymbol{\Gamma}_{i, y}$ for approximation coefficients $\boldsymbol{\alpha}_i$.
3.1 ED-Based Regularization
For TSC, the widely studied NN-based classifiers have demonstrated that the distance is a proper alternative to measure the similarity of time series. So we first use Euclidean distance as the weight to restrict regularization term. Concretely, for each element of $\boldsymbol{\alpha}_i\left(\alpha_{i, j}\right)$, we calculate the distance between the test instance $\boldsymbol{y}$ and each training sample $\boldsymbol{X}_{i, j}$ and use this distance to restrict $\alpha_{i, j}$, i.e.,
$$
\boldsymbol{\Gamma}_{i, y}=\operatorname{diag}\left(\left\|\boldsymbol{y}-\boldsymbol{X}_{i, 1}\right\|_2, \ldots,\left\|\boldsymbol{y}-\boldsymbol{X}_{i, n_1}\right\|_2\right)
$$
By $\boldsymbol{\Gamma}_{i, y}$, the training samples that is the most similar to $y$ in terms of Euclidean distance can get more contribution to construct the approximation instance than those which are dissimilar. After weight matrix is determined, Eq. (3) can be rewritten as
$$
f\left(\boldsymbol{\alpha}_i\right)=\frac{1}{2}\left\|\boldsymbol{y}-\boldsymbol{X}_i \boldsymbol{\alpha}_i\right\|^2+\lambda\left\|\boldsymbol{\Gamma}_{i, y} \boldsymbol{\alpha}_i\right\|^2
$$
This is convex in $\alpha_i$, so we can find its the optimal coefficients $\widetilde{\alpha}_i$ by setting the derivative of $f\left(\boldsymbol{\alpha}_i\right)$ to 0 :
$$
\widetilde{\boldsymbol{\alpha}}_i=\left(\boldsymbol{X}_i^T \boldsymbol{X}_i+\lambda \boldsymbol{\Gamma}_{i, y}^T \boldsymbol{\Gamma}_{\boldsymbol{i}, y}\right)^{-1} \boldsymbol{X}_i^T \boldsymbol{y}
$$
Thus, $\widetilde{\boldsymbol{y}}_i$ is
$$
\widetilde{\boldsymbol{y}}_i=\boldsymbol{X}_i \widetilde{\alpha}_i=\boldsymbol{X}_i\left(\boldsymbol{X}_i^T \boldsymbol{X}_i+\lambda \boldsymbol{\Gamma}_{i, y}^T \boldsymbol{\Gamma}_{i, y}\right)^{-1} \boldsymbol{X}_i^T \boldsymbol{y}=\boldsymbol{H}_i \boldsymbol{y}
$$
So $\boldsymbol{H}_i$ can be considered as a projection matrix.
To further investigate the effect of $\boldsymbol{\Gamma}_{i, y}$ when constructing $\widetilde{\boldsymbol{y}}_i$, we analyze the properties of $\boldsymbol{H}_i$ in terms of eigen-decomposition. Because $\boldsymbol{H}_i$ contains two matrices, $\boldsymbol{X}_i$ and $\boldsymbol{\Gamma}_{i, y}$, we employ the generalized singular value decomposition (GSVD) [1] between them to do this task.
For matrices $\boldsymbol{X}_i$ and $\boldsymbol{\Gamma}_{i, y}$, their GSVD is given by
$$
\boldsymbol{X}_i=\boldsymbol{U} \boldsymbol{\Sigma}_1[\mathbf{0}, \boldsymbol{\Omega}] \boldsymbol{Q}^T, \quad \boldsymbol{\Gamma}_{i, y}=\boldsymbol{V} \boldsymbol{\Sigma}_2[\mathbf{0}, \boldsymbol{\Omega}] Q^T
$$
where $U, V$ and $Q$ are unitary matrices, $\boldsymbol{\Omega}$ is upper triangular and nonsingular matrix. Since $\boldsymbol{\Gamma}_{i, y}$ is a diagonal square matrix, $\boldsymbol{U}, \boldsymbol{V}$ and $\boldsymbol{Q}$ are orthogonal and matrices $\Sigma_1$ and $\Sigma_2$ are non-negative diagonal, which hold that $\boldsymbol{\Sigma}_1^T \boldsymbol{\Sigma}_1=\left\lceil\sigma_{\boldsymbol{X}, 1}^2, \sigma_{\boldsymbol{X}, 2}^2, \ldots, \sigma_{\boldsymbol{X}, r}^2\right\rfloor$ and $\boldsymbol{\Sigma}_2^T \boldsymbol{\Sigma}_2=\left\lceil\sigma_{\boldsymbol{\Gamma}, 1}^2, \sigma_{\boldsymbol{\Gamma}, 2}^2, \ldots, \sigma_{\boldsymbol{\Gamma}, r}^2\right\rfloor$, where $r=\operatorname{rank}\left(\left[\boldsymbol{X}_i^T, \boldsymbol{\Gamma}_{i, y}^T\right]\right)$. Two properties of GSVD is $0 \leq \sigma_{\boldsymbol{X}, i}, \sigma_{\Gamma, i} \leq 1$ and $\boldsymbol{\Sigma}_1^T \boldsymbol{\Sigma}_1+\boldsymbol{\Sigma}_2^T \boldsymbol{\Sigma}_2=\boldsymbol{I}_r$ which implies $\sigma_{\boldsymbol{X}, i}^2+\sigma_{\boldsymbol{\Gamma}, i}^2=1$.
By these decompositions, $\boldsymbol{H}_i$ of Eq. (7) is formulated as
$$
\boldsymbol{H}_i=\boldsymbol{U} \boldsymbol{\Sigma}_1\left(\boldsymbol{\Sigma}_1 \boldsymbol{\Sigma}_1+\lambda \boldsymbol{\Sigma}_2 \boldsymbol{\Sigma}_2\right) \boldsymbol{\Sigma}_1 \boldsymbol{U}^T=\boldsymbol{U} \boldsymbol{\Sigma} \boldsymbol{U}^T
$$

As can be seen, $\boldsymbol{\Sigma}$ is still a diagonal matrix with the values $\sigma_k$ :
$$
\sigma_k=\frac{\sigma_{\boldsymbol{X}, i}^2}{\sigma_{\boldsymbol{X}, i}^2+\lambda \sigma_{\Gamma, i}^2}=\frac{1-\sigma_{\Gamma, i}^2}{1+(\lambda-1) \sigma_{\boldsymbol{\Gamma}, i}^2}
$$
Apparently, $\sigma_k \in[0,1]$. Since $\boldsymbol{U}$ is an orthogonal matrix, the decomposition of Eq. (9) can represent the eigen decomposition of $\boldsymbol{H}_i$. It is clear that the values of $\sigma_k(k=1, \ldots, r)$ depend on three parts: the structure of the training samples of class $i$ (i.e., $\sigma_{\boldsymbol{X}, i}$ ), the regularization parameter $(\lambda)$ and the distances between $y$ and each sample of class $i$ (i.e., $\sigma_{\Gamma, i}$ ). This means that different test instances have different amount of shrinkage when constructing the approximation instance even using the same training samples.

Due to $\lambda>0$ and $\sigma_{\Gamma, i} \in[0,1], \sigma_k$ and $\sigma_{\Gamma, i}$ have an inverse relationship. To be more specific, when $y$ has large distances with the training samples of $\boldsymbol{X}_i$ (that is, the non-zero entries of $\boldsymbol{\Gamma}_{i, y}$ have large values), the values of $\sigma_k$ are large and the eigenvalues of $\boldsymbol{H}_i$ are small. This suggests that the classes whose training samples are distant from test instance lead to a stiffer shrinkage penalty. The large penalty will make the obtained $\widetilde{y}_i$ dissimilar to $y$. Back to Eq. (3), large distances in $\boldsymbol{\Gamma}_{i, y}$ make $\boldsymbol{\alpha}_i$ become small, which results in a large residual. One thing should be noticed that $\boldsymbol{\Gamma}_{i, y}$ is an ensemble of distances and only one or several small values have little effect for the final $\boldsymbol{\alpha}_i$. This is the primary difference with NN-based approaches.

### GEM-Based Regularization

Through the analysis of $\boldsymbol{H}_i$, we find the training sample that is distant from test instance will lead to a small coefficient which makes little effect for calculating the residual. Therefore, if we map the time series into a lower-dimensional subspace where the samples of each class become more closed while the different classes are more separated, the prediction in terms of $\left\|\boldsymbol{y}-\widetilde{\boldsymbol{y}}_i\right\|_2$ will be more accurate. In this section, we employ the state-of-the-art supervised feature extraction technique, generalized eigenvector method (GEM) [15], to complete this task.

GEM exploits the simple second-order structure of the training samples and extracts the discriminative features from the generalized eigenvectors of the class conditional second moments. In [15], the author suggests that an alternative would be to use the covariance matrix instead of the second moment. GEM gets the direction by maximizing the ratio of projected data variances between different classes. Thus the direction $v$ is calculated as
$$
\boldsymbol{v}=\underset{v}{\arg \max } \frac{\boldsymbol{v}^T \boldsymbol{C}_i \boldsymbol{v}}{\boldsymbol{v}^T\left(\boldsymbol{C}_j+\frac{\gamma}{d} \operatorname{trace}\left(\boldsymbol{C}_j\right)\right) \boldsymbol{v}}
$$
where $C_i$ is the covariance matrix of class $i, d$ is the dimensionality of samples, $\gamma$ is a small multiple and trace() denotes the trace of a matrix. The item $\frac{\gamma}{d} \operatorname{trace}\left(\boldsymbol{C}_j\right)$ is used to solve the problem that $\boldsymbol{C}_j$ is rank deficient when there are few training samples [24]. This objection function is solved by the generalized
Nearest Subspace with Discriminative Regularization for TSC $\quad 589$
eigenvectors of $\boldsymbol{C}_i \boldsymbol{v}=\mu\left(\boldsymbol{C}_j+\frac{\gamma}{d} \operatorname{trace}\left(\boldsymbol{C}_j\right)\right) \boldsymbol{v}$. Generally, there are many eligible eigenvalues, so we can get a transformation matrix $\boldsymbol{V}$ by merging all $v \mathrm{~s}$.

When $\boldsymbol{V}$ is obtained, we can calculate the weight matrix $\boldsymbol{\Gamma}_{i, y}^G$ (distinguished from Eq. (4)). Recall that each element in the diagonal of $\boldsymbol{\Gamma}_{i, y}$ is the distance between test instance $y$ and each training sample of class $i$. We calculate the diagonal values of $\boldsymbol{\Gamma}_{i, y}^G$ by
$$
D_G\left(\boldsymbol{V}, \boldsymbol{y}, \boldsymbol{X}_{i, j}\right)=\left\|\boldsymbol{V} \boldsymbol{y}-\boldsymbol{V} \boldsymbol{X}_{i, j}\right\|_2=\sqrt{\left(\boldsymbol{y}-\boldsymbol{X}_{i, j}\right)^T \boldsymbol{\Phi}\left(\boldsymbol{y}-\boldsymbol{X}_{i, j}\right)}
$$
where $\boldsymbol{\Phi}=\boldsymbol{V}^T \boldsymbol{V}, \boldsymbol{X}_{i, j}$ denotes the $j$-th training sample of class $i$.
The above procedure is suited for the scenario of two class. For multi-class problem involving $K(K>2)$ classes, we use two strategies to get the projection matrix: one-vs-rest and multiple one-vs-one. The transformation matrix and weight matrix are denoted as $\boldsymbol{V}^{(1: r)}, \boldsymbol{\Gamma}_{i, y}^{G(1: r)}, \boldsymbol{V}^{(1: 1)}$ and $\boldsymbol{\Gamma}_{i, y}^{G(1: 1)}$, respectively.

### LFDA-Based Regularization

Local Fisher discriminant analysis (LFDA) is another effective method which embeds the high-dimensional data into a lower-dimensional subspace. In this section, we employ LFDA to help the construction of $\boldsymbol{\Gamma}_{i, y}$. To deal with the multi-modal problem of sample distribution, LFDA employs a concept of affinity to represent the neighbour relationship of two samples. Let $\boldsymbol{W}$ be the affinity matrix, and an elaborate and proper definition of the affinity between $\boldsymbol{x}_i$ and $\boldsymbol{x}_j$ is provided by [29]: $\boldsymbol{W}_{i, j}=\exp \left(-d^2\left(\boldsymbol{x}_i, \boldsymbol{x}_j\right) / \eta_i \eta_j\right)$, where $d\left(\boldsymbol{x}_i, \boldsymbol{x}_j\right)$ is a distance measure, $\eta_i=d\left(\boldsymbol{x}_i, \boldsymbol{x}_i^{k n n}\right)$ is a local scaling parameter in terms of the neighbourhood of $\boldsymbol{x}_i$ and $\boldsymbol{x}_i^{k n n}$ is the knn-nearest neighbour of $\boldsymbol{x}_i$. By this definition, a large distance between two samples will lead to a small affinity. If the values of local within-class scatter matrix $\left(S_{l w}\right)$ and local between-class scatter matrix $\left(S_{l b}\right)$ used in LFDA are weighted by the affinity, the far-apart samples have less influence, which can preserve the local structure of the data. Based on affinity matrix, the $S_{l w}$ and $S_{l b}$ are defined as
$$
\begin{aligned}
\boldsymbol{S}_{l w} & =\frac{1}{2} \sum_{i, j=1}^n \boldsymbol{W}_{i j}^w\left(\boldsymbol{x}_i-\boldsymbol{x}_j\right)\left(\boldsymbol{x}_i-\boldsymbol{x}_j\right)^T \\
\boldsymbol{S}_{l b} & =\frac{1}{2} \sum_{i, j=1}^n \boldsymbol{W}_{i j}^b\left(\boldsymbol{x}_i-\boldsymbol{x}_j\right)\left(\boldsymbol{x}_i-\boldsymbol{x}_j\right)^T
\end{aligned}
$$

where
$$
\boldsymbol{W}_{i j}^w=\left\{\begin{array}{ll}
\boldsymbol{W}_{i j} / n_c, & l_i=l_j=c \\
0, & l_i \neq l_j
\end{array}, \boldsymbol{W}_{i j}^b= \begin{cases}\boldsymbol{W}_{i j}\left(1 / n-1 / n_c\right), & l_i=l_j=c \\
1 / n, & l_i \neq l_j\end{cases}\right.
$$
where $l_i, l_j$ are class labels, $n_c$ is the number of training samples of $c$-th class. As usual, we still use [24]'s solution to regularize $S_{l w}$. The reason is that $S_{l w}$ will be the denominator matrix in the objection function of LFDA. Using $S_{l w}$ and $S_{l b}$, the LFDA transformation matrix $T$ is defined as
$$
\boldsymbol{T}=\underset{T}{\arg \max } \frac{\boldsymbol{T}^T \boldsymbol{S}_{l b} \boldsymbol{T}}{\boldsymbol{T}^T\left(\boldsymbol{S}_{l w}+\frac{\gamma}{d} \operatorname{trace}\left(\boldsymbol{S}_{l w}\right)\right) \boldsymbol{T}}
$$
Now, we can project the samples into a low-dimensional subspace by $\boldsymbol{T}$ and recalculate the weight matrix $\boldsymbol{\Gamma}_{i, y}$ of Eq. (4). For the sake of distinction, we denote it as $\boldsymbol{\Gamma}_{i, y}^L$ and each element is obtained by calculating
$$
D_L\left(\boldsymbol{T}, \boldsymbol{y}, \boldsymbol{X}_{i, j}\right)=\left\|\boldsymbol{T} \boldsymbol{y}-\boldsymbol{T} \boldsymbol{X}_{i, j}\right\|_2=\sqrt{\left(\boldsymbol{y}-\boldsymbol{X}_{i, j}\right)^T \boldsymbol{\Psi}\left(\boldsymbol{y}-\boldsymbol{X}_{i, j}\right)}
$$
where $\boldsymbol{\Psi}=\boldsymbol{T}^T \boldsymbol{T}$.
Except the transformation matrix is obtained by Eq. (16), for $K(K>2)$ classes, we also use one-vs-rest strategy to find the discriminative projection directions and merge them to form transformation matrix $\left(\boldsymbol{T}^{(1: r)}\right)$. We use $\boldsymbol{\Gamma}_{i, y}^{L(1: r)}$ to denote the weight matrix of this case.

### Effect of GEM and LFDA-Based Regulation for Improved NS

In Sects. 3.2 and 3.3, we respectively employ GEM and LFDA to transform the samples into a low-dimensional space where the obtained weight matrix is expected to have a proper shrinkage penalty for approximation coefficients $\alpha_i$. No matter GEM or LFDA, the purpose is to make the samples with the same label more closed in the new space while the samples from different classes are apart. So by comparing the distance relationships calculated in original sample space, the distances obtained in new low-dimensional space become more meaningful for the classification task. What is different is that GEM excepts more information contained in data distribution while LFDA tries to make the interclass more separated. Therefore, GEM uses the covariance matrix as the basis while LFDA employs the collection of class-conditional mean feature vectors. In the low-dimensional space constructed by LFDA, the inter-class separability is increased, which penalizes the class whose memberships are most distant from $\boldsymbol{y}$. Meanwhile, the samples that are truly neighbours of $\boldsymbol{y}$ are also seen as neighbours, which gives better information on within-class distance relationships with $y$ and offers more benefit for classification.

Empirically, LFDA seems to be a more suitable choice for classification task to restrict $\boldsymbol{\alpha}_i$. But there are various kinds of time series datasets in our daily life and no one technique is a panacea which can deal with all situations. Bagnall and Lines's works $[3,20]$ have demonstrated this point and they suggest that an ensemble scheme of different approaches is an alternative. In the next section, we will utilize all these weight matrices to propose an ensemble NS classifier.

### Ensemble NS Classifier

An ensemble of classifiers is a set of base classifiers, which has been widely studied in machine learning domain. When classifying new samples, the decisions of all base classifiers are combined through a fusion way. In Sect. 3 , we design 5 different weight matrices: $\boldsymbol{\Gamma}_{i, y}, \boldsymbol{\Gamma}_{i, y}^{G(1: r)}, \boldsymbol{\Gamma}_{i, y}^{G(1: 1)}, \boldsymbol{\Gamma}_i^L$ and $\boldsymbol{\Gamma}_{i, y}^{L(1: r)}$, where $\boldsymbol{\Gamma}_{i, y}$ is directly constructed by calculating the distance between test instance $y$ and each training sample of class $i$ while the other 4 weight matrices are constructed in different low-dimensional spaces. 

Our ensemble approach is transparent, i.e., we first construct the five different forms of NS classifiers by these weight matrices and then take the simple voting schemes to make a decision for each test instance. For convenience, we denote these five different forms of NS classifiers as NS_ED, NS_G(1:r), NS_G(1:1), NS_L and NS_L(1:r).

We separately test three weighting schemes for the ensemble classifier: equal, proportional and best. The equal scheme, as the name implies, sets the equal weight for each classifier when classifying new instance. Clearly, it is the fastest scheme, but it does not consider the difference of base classifiers. The proportional and best schemes exploit unequal voting weight. A widely used technique is to calculate the cross-validation accuracy of each base classifier on the training set and then the weight is set based on the accuracy [20]. The proportional scheme assigns the wights as the cross-validation accuracy directly while the best scheme takes a binary strategy which assigns a weight of 1 to the base classifier with the highest cross-validation accuracy and 0 to the others. In the next Section, these schemes are all employed for TSC task. Here, we propose an ensemble algorithm of improved NS classification with five weight matrices by the best scheme.


The time consuming of Algorithm 1 mainly depends on two parts: one is the calculation of weight matrices, the other is the solution of optimal coefficients.

For optimal coefficient $\widetilde{\boldsymbol{\alpha}}_i$ of Eq. (6), it takes $O\left(n_i^2 m\right)$ where $n_i$ is the number of $i$-th class and $m$ is the length of time series. For weight matrix $\boldsymbol{\Gamma}$, the GEM and LFDA consume most of running time but they only need to be computed once. When using GEM, the projection vector of Eq. (11) requires $O\left(\mathrm{~m}^2\right)$, thus, the one-vs-one way takes $O\left(K^2 m^2\right)$ and one-vs-rest strategy needs $O\left(K m^2\right)$. When using LFDA, Eq. (16) needs $O\left(n^2 k\right)$ where $k$ is the number of selected projection vectors and $k=1$ for one-vs-one strategy. So the total time complexity is $O\left(\max \left(K n_i^2 m, \max \left(K^2 m^2, n^2 k\right)\right)\right)$.


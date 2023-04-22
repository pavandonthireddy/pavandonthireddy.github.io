---
layout: post
title: Time Series Classification
description: Time Series Classification
summary: Time Series Classification
author:
- Pavan Donthireddy
usemathjax: true
tags: [classification, timeseries]
original: new
---

<p align="justify">Typical classification approaches can be categorized as
instance-based (e.g., one nearest neighbor classifier with
euclidean distance (NN-Euclidean), or dynamic time warping
distance (NNDTW)), shapelet featurebased  and local pattern-frequency histogram based
methods Instance-based methods, like
NNDTW, have been successfully used for TSC and shown to
be very hard to beat  but they are usually less
interpretable. Shapelet is another promising method for
TSC, and it discovers subsequences that are discriminative
of class membership and provides more interpretable
results, but searching for shapelets on large datasets becomes
time-consuming or even intractable. Feature-based
methods do show promising classification results, but their
capabilities are largely attributed to strong classifiers like
SVM, adaboost and random forest, instead of being due to
better global/local features and representations.</p>


<p align="justify">Time series classification methods can be categorized into
instance-based, shapelets, feature-based and pattern frequency
histogram methods.</p>

<p align="justify">Instance-based methods predict labels of test time series
based on their similarity to the training instances. The most
popular similarity metrics include euclidean distance and
elastic distances, e.g., the dynamic time warping (DTW)
distance. Using a single nearest neighbor, with euclidean
distance (NNEuclidean) or DTW distance (NNDTW), has
demonstrated successful time series label prediction. DTW
allows time series to be locally shifted, contracted and
stretched, and lengths of time series hence need not be the
same. Therefore, DTW usually gives a better similarity
measurement than Euclidean distance, and NNDTW has
been shown to be very hard to beat on many datasets.
A number of more complex elastic distance measures have
been proposed, including longest common subsequences
(LCSS), Edit distance with Real Penalty (ERP)
and edit distance on Real Sequence (EDR). However,
in 30, the authors claimed that no other elastic distance
measure outperforms DTW by a statistically significant
amount, and DTW is the best measure. Instance-based
approaches, like NN-euclidean and NNDTW, are accurate,
but they are less interpretable, since they are based on
global matching and provide limited insights into the temporal
characteristics.</p>

<p align="justify">Shapelet is a localized time series subsequence, which is
discriminative of class membership, and it was first proposed
and used by Ye and Keogh [1] for time series classification.
The original shapelet algorithm [1] searches for
shapelets recursively, and builds a decision tree using different
shapelets as splitting criteria. However, the expressiveness
of shapelets is limited to binary decision questions.
In [4], the authors proposed logical-shapelets, specifically
conjunctions or disjunctions of shapelets, which are shown
to be more expressive than a single shapelet, and toexperimentally outperform the original shapelet algorithm.</p>

<p align="justify">The above two algorithms embed shapelet discovery in a
decision tree, while in [2], the authors separate shapelet discovery
from classifier by finding the best k shapelets in a
single scan of all time series. The shapelets are used to transform
the data, where each attribute in the new dataset represents
the distance of a time series to one of the k shapelets.
Hills et al. demonstrate that the transformed data, in conjunction
with more complex classifiers, produces better
accuracies than the embedded shapelet tree. Since shapelets
are localized class-discriminative subsequences, shapeletsbased
methods have increased interpretability than global
instance-based matching. The main drawback is the time
complexity of searching for shapelets, and subsequent
research, e.g.,  focuses on developing efficient shapeletsearching
algorithms.</p>

<p align="justify">Feature-based methods generally consist of two sequential
steps: extract features and train a classifier based on features.
Typical global features include statistical features, like
variance and mean, PCA coefficients, DFT coefficients, zerocrossing
rate. These features are extracted either from
time domain or from transformed domains, like frequency
domain and principal component space. Afterwards, the
extracted features either go through feature selection procedures
to prune less significant ones [5], or are fed directly
into complex classifiers, like multi-layer neural network [31].
Global features lose temporal information, although it is
potentially informative for classification. </p>

<p align="justify">In [8], the authors
extracted features from intervals of time series, constructed
and then boosted binary stumps on these interval features,
and trained an SVM on outputs of the boosted binary
stumps. In [6], the authors extracted simple interval features
as well, including mean, variance and slope, trained a random
forest ensemble classifier, and showed better performance
than NNDTW. Although feature-based methods
have shown promising classification results, their capabilities
are largely attributed to strong classifiers such as SVM,
adaboost and random forest, instead of being due to better
global/local features and representations.</p>

<p align="justify">Another popular method is based on pattern frequency
histograms, widely known as bag of words. The BoW
approach incorporates word frequencies but ignores their
locations. In time series applications, several recent papers
adopted BoW ideas. Lin et al. [25] first symbolize time series
by SAX, then slide a fixed-sized window to extract a contiguous
set of SAX words, and at last use the frequency distribution
of SAX words as a representation for the time series.
Baydogan et al. [9] propose a similar bag-of-features framework.</p>

<p align="justify">They sample subsequences with varying lengths randomly,
use mean, variance, slope and temporal location t to
represent each subsequence, afterwards utilize random forest
classification to estimate class probabilities of each subsequence,
and finally represent the raw time series by
summarizing the subsequence class-probability distribution
information. They showed superior or comparable results
to competing methods like NNDTW on UCR datasets [4].
Wang et al. [10] adopted a typical bag of words framework
to classify biomedical time series data, and they sample subsequences
uniformly and represent them by DWT. Grabocka
and Schmidt-Thieme [32] introduce a similar BoW
pipeline to classify time series: they sample subsequences
from time series instances uniformly, learn latent patterns
and membership assignments of each subsequence to those
patterns, and sum up membership assignments of subsequences
on a time series as the representation of that time
series. </p>

<p align="justify">Time series representations are then classified by
polynomial kernel SVM. Our work belongs to this category,
but emphasizes detecting better local feature points and
developing better local subsequence representations.
There are two recent papers using local descriptors as
well [33], [34]. In [33], the authors attempt to improve efficiency
of traditional DTW computation, to be concrete, they
extract local feature points, match them by their descriptors
and compute the local band constraints (based on matched pairs) applicable during the execution of the DTW algorithm.
In this way, they only have to compute the accumulative
distances within the band, and the DTW computation
efficiency is improved. </p>

<p align="justify">Our work is different from [33] in
that: our use local descriptors to improve classification accuracies,
while [33] use local descriptors to improve DTW
computation efficiency. In [34], the authors extract local features
from multi-variate time series by leveraging metadata,
and their method for local feature extraction is only
applicable for multi-variate time series data with known
correlations and dependencies among different dimensions.
UCR datasets are univariate time series datasets, and their
method cannot be used here.</p>

## background

### NN-Based Time Series Classification

<p align="justify">As mentioned in Sect. 1, most studies have been directed at finding techniques
that can compensate for small misalignments between time series. Two main
elastic distance measures, DTW and edit distance, have been widely studied.</p>

### DTW-Based Elastic Distance Measures.

<p align="justify">DTW is considered as the standard benchmark elastic distance measure to find an optimal alignment between
two given sequences [16]. The standard DTW utilizes a pointwise distance matrix
to record the cumulative distance from the start point pair to current point pair
and employs the dynamic programming method to complete the process. Two
aspects of DTW have been studied in recent years. One is speedup technique
because the standard DTW has a quadratic time and space complexity. Some
works have reduced it to nearly linear time complexity [25]. Another improvement
is to change the calculation way of cumulative distance. A weighted form
of DTW (WDTW) [14] is proposed to reduce warping by adding a multiplicative
weight item to penalize points with higher phase difference between a test point
and a reference point. In standard DTW, there is a scenario where a single point
on one time series may map onto a large number of points on the other time
series, which lead to pathological results. To avoid these singularities, a modification
of DTW, called DDTW, is proposed by transforming the time series
into a series of first-order difference [17]. On the basis of this idea, G´orecki et al.
[11] use a weighted combination of DTW on raw time series and DDTW on first
order differences for NN classification. An extension of DDTW that uses DTW in
conjunction with transforms and derivatives is proposed by G´orecki and Luczak
[12]. They propose a new distance function by combining three distances: DTW
distance between time series, DTW distance between derivatives of time series,
and DTW distance between transforms of time series.
</p>

### Edit Distance-Based Elastic Distance Measures. 

<p align="justify">The initial edit distancetechnique is longest common subsequence (LCSS) distance which is extended
to handle the real-valued time series from discrete series by using a distance
threshold. A point pair from two time series can be considered as a match if
their distance is less than the predefined threshold. Like LCSS, edit distance on
real sequences (EDR) [5] also use a distance threshold to define a series match,
but the difference is EDR employs a constant penalty to deal with the scenario of
non-matching point pair. The drawback of EDR is it does not satisfy triangular
inequality. Chen et al. [6] revise the weakness of EDR by utilizing the distance
between point pairs when there is no gap and a constant when gaps occur. TWE
[22] and MSM [27] are two effective edit distance-based approaches proposed
in recent years. TWE makes full use of the characteristics of LCSS and DTW,
which allows warping in the time axis and combines the edit distance with Lpnorms.
In MSM the similarity of two different time series is calculated by using
a series of operations to transform a given time series into the target time series.</p>

### Other Elastic Distance Measures. 

<p align="justify">Batista et al. consider the complexityinvariance problem for time series similarity measures and propose a parameterfree
method, complexity invariant distance (CID) [13], to solve this problem.
They describe a method for weighting a distance measure to compensate for the
differences in the complexity when two time series are compared. The sum of
squares of the first differences is used to measure the complexity. Except using
individual elastic distance measure to calculate the similarity of two time series,
Lines and Bagnall [20] combine 11 elastic distance measures through simple
ensemble schemes and get significantly better classification accuracy.</p>
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

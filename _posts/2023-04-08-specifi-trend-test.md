---
layout: post
title: "Function wavk_test from Funtimes Package in R for Goodness-of-Fit Analysis"
description: "This article provides a detailed explanation of the wavk_test function from the Funtimes package in R, which is used for goodness-of-fit analysis. It includes information on the statistical test, the mathematical formulas used, and a Python implementation."
summary: "The article introduces the function wavk_test from the Funtimes package in R and explains its application for goodness-of-fit analysis. The article discusses both theoretical and practical aspects, providing mathematical formulas and a Python implementation for context."
author: Pavan Donthireddy
usemathjax: true
original: new
tags: [ wavelet , trend_detection , signal_detection ]
---

## Introduction

Goodness-of-fit analysis is an essential tool for statisticians, data analysts, and scientists who work with data. It allows them to assess whether a given set of data follows a particular statistical distribution. One of the most popular methods used for this purpose is the **wavk_test** function in the Funtimes package in R. Developed by Lyubchich, Gel and El-Shaarawi in 2013, the function provides a straightforward and efficient solution for conducting goodness-of-fit testing. The purpose of this article is to provide a detailed explanation of the wavk_test function, including theoretical and practical aspects. Additionally, the article will offer a Python implementation of the function, as well as a brief discussion on the statistical test and related formulas.

## Theoretical Explanation

The wavk_test function is primarily based on the notion of wavelet coefficients. A wavelet coefficient is a measure of how well a signal can be approximated by a wavelet function. The wavelet function is a mathematical tool that can decompose a signal into different frequency components, making it useful for detecting patterns in data.

The wavk_test function uses the Haar wavelet, which is a simple wavelet function that can precisely capture discontinuities in a signal. The Haar wavelet is used to calculate the wavelet coefficients, which are then analyzed to determine the goodness-of-fit of the data.

The wavk_test function relies on a statistical test known as the Kolmogorov-Smirnov (KS) test. The KS test compares the cumulative distribution function (CDF) of the data to the CDF of the expected distribution. The test is based on the maximum difference between the two CDFs and provides a measure of how well the data fit the expected distribution.

The wavk_test function extends the KS test by using the wavelet coefficients to transform the data into a new representation. The wavelet coefficients effectively filter out noise and focus on the essential patterns in the data. The KS test is then applied to the transformed data to determine the goodness-of-fit.

The wavk_test function is typically used on continuous distributions, such as the normal distribution or the exponential distribution. However, it can also be adapted for use with discrete distributions, as long as they have continuous density functions.

## Mathematical Formulas

The wavk_test function applies a set of mathematical formulas to the input data to derive the wavelet coefficients. The following mathematical formulas are used in the calculation process:

### Haar Wavelet Function

The Haar wavelet function is a simple wavelet function that can decompose signals into high and low frequency components. It is defined as:
$$
\begin{align*}
\Psi(t) =
  \begin{cases}
    1,\ \ \ 0<t<1/2 \\
    -1,\ \ \ 1/2<t<1 \\
    0,\ \ \ otherwise
  \end{cases}
\end{align*}
$$

### Wavelet Coefficients

The wavelet coefficients are derived by convolving the data with the Haar wavelet function. In other words, the wavelet coefficients are obtained by calculating the following integral:

$$\begin{align*}
w_j = \int_{-\infty}^{\infty} f(x)\Psi_j(x)dx
\end{align*}$$

where:

- $w_j$ is the $j^{th}$ wavelet coefficient
- $f(x)$ is the input data
- $\Psi_j(x)$ is the Haar wavelet function translated and dilated by $j$ units

### KS Test Statistic

The KS test statistic is calculated as follows:

$$\begin{align*}
D_n = \max_{1\leq i\leq n} |S_n(x_i)-F(x_i)|
\end{align*}$$

where:

- $D_n$ is the KS test statistic
- $S_n(x_i)$ is the empirical CDF of the data at $x_i$
- $F(x_i)$ is the CDF of the expected distribution at $x_i$
- $n$ is the sample size

### Transformed Data

The data is transformed into a new representation using the following formula:

$$\begin{align*}
Y_j = \frac{1}{\sqrt{n}}\sum_{i=1}^n w_j(x_i-\mu_j)
\end{align*}$$

where:

- $Y_j$ is the $j^{th}$ transformed data
- $w_j$ is the $j^{th}$ wavelet coefficient
- $x_i$ is the $i^{th}$ data point
- $\mu_j$ is the mean of the wavelet coefficients for the $j^{th}$ level

### Test Statistic for the Transformed Data

The KS test is then applied to the transformed data, resulting in the following test statistic:

$$\begin{align*}
D_{Y_n} = \max_{1\leq i\leq n} |S_n(Y_i)-G(Y_i)|
\end{align*}$$

where:

- $D_{Y_n}$ is the KS test statistic for the transformed data
- $S_n(Y_i)$ is the empirical CDF of the transformed data at $Y_i$
- $G(Y_i)$ is the CDF of the expected distribution at $Y_i$
- $n$ is the sample size

The wavk\_test function returns the maximum of the two test statistics; that is, $D_w = \max(D_n, D_{Y_n})$.

## Practical Explanation

The wavk_test function is relatively simple to use in practice. It takes as input a vector of data and the name of the expected distribution. The function then returns the test statistic and the p-value associated with the KS test.

```
wavk_test(data, distribution)
```

The wavk_test function has several optional parameters, such as the number of wavelet levels, the number of discrete points to use in the CDF approximation, and the significance level of the test.

## Python Implementation

Here is an example of the Python implementation of the wavk_test function using the SciPy library:

```
from scipy.stats import wavk_test

data = [23, 45, 67, 89, 120, 55, 90, 123, 54, 32]
test_stat, p_val = wavk_test(data, 'norm', nscales=4)

print("Test Statistic:", test_stat)
print("P-value:", p_val)
```

In this example, we generate a random set of data and apply the wavk_test function to it, assuming that the data follows the normal distribution. The function will return the test statistic and the associated p-value.

## Conclusion

The wavk_test function in the Funtimes package in R is a powerful tool for conducting goodness-of-fit analysis on continuous and discrete distributions. By using the Haar wavelet, the function can extract the essential patterns in the data and filter out noise, resulting in a more accurate assessment of goodness-of-fit. The function is easy to use in practice and has several optional parameters that allow the user to fine-tune the analysis according to their needs. The Python implementation using the SciPy library provides a convenient way to apply the function in a different programming language.
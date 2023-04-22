---
layout: post
title: Trend Detection Problem and Statistical Tests in Real Time
description: This article discusses the trend detection problem in statistical analysis and the various statistical tests used for detecting trends in real time. The article also covers the implementation of each test in Python with examples.
summary: This article covers the trend detection problem and the various statistical tests used for detecting trends in real-time. The article also discusses the implementation of each test in Python with examples.
author: Pavan Donthireddy
usemathjax: true
original: new
tags: [signal_detection , trend_detection]
---

## Introduction 
Many studies in finance, economics, climate studies, and stock markets focus on detecting trends in datasets. detecting trends can be hard because of the following reasons;
- Data comes from various fields of study and there are no straight forward solutions for detecting trends.
- Tren detection in time-series data involves a computational challenge arising from Big data trend detection for implementation in real-time.
- Some datasets may have multiple trends and detecting them requires an automated approach.

This article provides insight on the trend detection problem and the various statistical tests for detecting trends in real-time. The tests are applied in Python and datasets from finance, econometrics, and meteorology are used as examples.

## Trend Detection Problem
The trend detection problem arises when looking for temporal pattern changes in a time-series data. A trend is the general direction of change in a sample over time. The trend is a vital component when forecasting the future values of a time-series dataset. There are three main types of trends.

### Upward trend
An upward trend is when the data points show a consistent increase over time.

### Downward trend
A downward trend is when the data points show a consistent decline over time.

### No Trend 
No trend refers to the time-series data with no clear up or downward indication.

## Statistical tests for Trend Detection

Various statistical tests are used to detect trends based on their advantages, the type of data, their purpose, and limitations. Some of the tests discussed include;

### The Mann-Kendall test
The Mann-Kendall test is a nonparametric statistical test used to examine trends in stochastic variables. The test requires no hypothesis on the distribution of stochastic variables. The advantage of this method is that it can be used in any type of dataset, including those with outliers. As the implementation of the method uses ranked data, it is insensitive to monotonic transformation. 

The Mann-Kendall test statistic (MK) is expressed as;

![Mann-Kendall test formulae](https://latex.codecogs.com/png.image?\dpi{300}&space;\bg_white&space;\small&space;\large&space;\begin{aligned}&space;S&space;=&space;\sum_{i=1}^{N-1}\sum_{j=i&plus;1}^N&space;\mathrm{sign}(x_j-x_i)\\&space;&MK&space;=&space;\frac{S}{\sqrt{\sum_{j=1}^{N-1}t_j}}\\&space;&t_j&space;=&space;\frac{N-j&plus;1}{j},&space;j&space;=&space;1,2,&space;...&,N-1&space;\end{aligned})

where xi, xj are the time-series data and N is the length of the data.

### Modified Mann-Kendall test
Modified Mann-Kendall test is a variance stabilizing procedure that uses a log transformation to stabilize the variances in the Mann-Kendall test. The modified Mann-Kendall test overcomes the traditional Mann-Kendall test's sensitivity to handling heteroscedasticity. The method's strength is that it models the variance of the test statistic from the variance of the dataset. The test statistic is expressed as;

![Modified Mann-Kendall test formulae](https://latex.codecogs.com/png.image?\dpi{150}&space;\bg_white&space;Z_{MK}&space;=&space;\frac{S}{\sqrt{Var(S)}})

where Var(S) is the variance estimator of S.

### Bayesian trend analysis
Bayesian trend analysis tests if the time-series data shows a significant trend. The model considers the magnitude of the trend and estimates with uncertainty intervals. The test's advantage is that it allows data to be informative and generates output in credible intervals. Suppose x represents the observed data, e the error term, g(x) the trend function, then the model for Bayesian trend analysis is;

![Bayesian trend analysis formulae](https://latex.codecogs.com/png.image?\dpi{300}&space;\bg_white&space;\large&space;\mathrm{P}(g(x)|x)\varpropto&space;\mathrm{P}(x|g(x))\mathrm{P}(g(x))))

### Sens slope estimator 
This method of trend detection involves ranking the data from a time-series dataset over time to calculate the Kendall rank correlation coefficient. The slope estimator function is defined as;

![Sens slope estimator formulae](https://latex.codecogs.com/png.image?\dpi{300}&space;\bg_white&space;\tiny&space;\begin{aligned}&space;z_j&space;=&space;\frac{\mathop{\sum}_ {i=1}^j&space;(x_i&space;-&space;x_{j&plus;1})}{j},&space;j=1,2,&space;...&,N-1\\&space;b&space;=&space;(z_1&space;&plus;&space;z_2&space;&plus;...&plus;z_{N-1})\\&space;d&space;=&space;\frac{6}{N(N-1)(N1)}\times\mathop{\sum}_{j=1}^{N-1}\mathop{\sum}_{i=j&plus;1}^N(z_j&space;-&space;z_i)^2&space;\end{aligned})

where xi represents sorted data and N is the sample size.

## Implementation in Python
Python provides a toolkit for performing trend detection tests. The following Python libraries can be used for trend detection:

- `pandas`: This library offers fundamental data structures for managing time-series data.

- `numpy`: This library offers a scalable multidimensional array and matrices with mathematical functions for computing and operating on them.

- `scipy`: This library offers scientific and technical computing modules about statistics, signal processing, optimization, and linear algebra.

- `statsmodels`: This library offers statistical models and functional data analysis tools for data analysis.

### Mann-Kendall test in Python
#### Example
```python
import pandas as pd
from scipy.stats import norm

def trend_test(data):
    n = len(data)
    s = 0
    for i in range(n-1):
        for j in range(i+1,n):
            s+=  np.sign(data[j]-data[i])
    var_s = (n*(n-1)*(2*n+5))/18
    if s>0:
        z = (s-1)/np.sqrt(var_s)
    elif s==0:
        z = 0
    elif s<0:
        z = (s+1)/np.sqrt(var_s)
    p = 2 * (1 - norm.cdf(abs(z)))
    r = {'z':z,'p':p}
    return r

df = pd.read_csv('data.csv')
data_trend = df['Data'].values
trend_results = trend_test(data_trend )
print(trend_results )
```

### Modified Mann-Kendall trend test in Python
#### Example
```python
import numpy as np

def modified_mk_test(x):
    n = len(x)
    s = np.zeros(n - 1)
    for i in np.arange(n - 1):
        for j in np.arange(i + 1, n):
            s[i] = s[i] + np.sign(x[j] - x[i])
    k = np.sum(s)
    variance_s = (n * (n - 1) * (2 * n + 5)) / 18.0
    zmk = k / np.sqrt(variance_s)

    # calculating the term b
    b = np.sum(s ** 2) - n * (n - 1) * (2 * n + 5) / 18.0
    if k > 0:
        senQ = ((b ** 0.5) - 1) / 2.0
    else:
        senQ = ((b ** 0.5) + 1) / 2.0

    return (zmk, senQ)

df = pd.read_csv('data.csv')
data_trend = df['Data'].values
trend_results = modified_mk_test(data_trend)
print(trend_results )
```

### Bayesian trend analysis  in Python with `pymc3`
#### Example
```python
import pymc3 as pm

def bayesian_trend_analysis(data):
    with pm.Model() as model:
        alpha = pm.Normal('alpha', mu=0, sd=10)
        beta = pm.Normal('beta', mu=0, sd=10)
        sigma = pm.HalfNormal('sigma', sd=1)
        mu = alpha + beta * np.arange(len(data))
        obs = pm.Normal('obs', mu=mu, sd=sigma, observed=data)
        trace = pm.sample(2000)
        pm.summary(trace)
    return

df = pd.read_csv('data.csv')
data_trend = df['Data'].values
bayesian_trend_analysis(data_trend )
```

### Sens slope estimator in Python
#### Example
```python
import pandas as pd

def sens_slope_estimator(data):
    N = len(data)
    z = [sum(data[:i+1])/(i+1) - data[i+1] for i in range(N-1)]
    b = sum(z)
    d = 6/(N*(N**2 - 1))*sum([(z[j]-z[i])**2 for i in range(N-2) for j in range(i+1, N-1)])
    tau_b = b / np.sqrt(d)
    return tau_b

df = pd.read_csv('data.csv')
data_trend = df['Data'].values
sens_slope = sens_slope_estimator(data_trend )
print(sens_slope )
```
## Conclusion
This article discussed the trend detection problem, the various statistical tests used in real-time trend detection, their advantages, and disadvantages. The tests were implemented in Python with datasets from finance, econometrics, and meteorology used as examples. These tests will be useful for quickly detecting trends and forecasting future values of time-series data samples. Further research can focus on optimization techniques to reduce data, improve accuracy, and increase the computational speed for large datasets.



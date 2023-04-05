---
layout: post
title: Piecewise linear representation of time series
description: Piecewise linear representation of time series
summary: Piecewise linear representation of time series
author:
- Pavan Donthireddy
usemathjax: true
tags: [timeseries, representation, piecewiseLinearRepresentation, changepoint, slope]
---

<p align="justify">The time series data usually fluctuate frequently and exit a lot of noise. So data mining in the original sequence data directly will not only cost highly in the storage and computation, but also probably affect the accuracy and reliability of the data mining algorithms. Therefore, many time series models are proposed, which can transform original series to new series. Modeling may not only compress the data, but also keep the main form and ignore fine changes. Accordingly, it can help improve the efficiency and accuracy of the data mining algorithms, which will provide policy support for data analysts.</p>

 1. <u><b>Piecewise Linear Representation Based on Important Point:</b></u> Pratt and Fink proposed a piecewise linear representation based on the important points. The important points are defined as the points which are the extreme points within the local scope and the ratio of the important point and the endpoint exceeds the parameters $R$. After extracting the important points from the time series, the algorithm then combines the points with the line orderly. Thus it will generate a new time series and get various piecewise linear representation with different fine and granularity by selecting different parameters  $R$.
 2. <u><b>Piecewise Aggregate Approximation (PAA):</b></u> Keogh and Yi proposed the method of the piecewise aggregate approximation independently. The algorithm divides the time series by the same time width and each sub-segment is represent by the average of the sub-segment. The method is simple, intuitionistic. It not only can support the similarity queries, all the Minkowski metric and the weighted Euclidean distance, but also can be used to index to improve query efficiency.
 3. <u><b>Piecewise Linear Representation based on the characteristic points:</b></u> Xiao  proposed a method of piecewise linear representation based on the characteristic points. After extracting the characteristic points from the time series, the algorithm then combines the points with the line orderly. Thus it will generate a new time series.
 4. <u><b>Piecewise Linear Representation Based on Slope Extract Edge Point (SEEP)</b></u>:** ZHAN Yan-Yan brought forward a new piecewise linear representation combining slope with the characteristics of time series. The algorithm can select some change points according to the rate of slope change firstly, and then combines the points with the line sequentially. Finally it will generate a new time series.
 
The literatures above are analyzed as follows:
<p align="justify">The piecewise linear representation gets some characteristics (e.g., extreme point, trend, etc.) of each section by segmenting the series mainly. The above methods not only have the advantages of simple and intuitive, but also can support dynamic incremental updates, clustering, fast similarity search, and so on. But the cost and fitting error is different.
</p>
<p align="justify"><u><b>Piecewise Linear Representation of Time Series based on Slope Change Threshold (SCT):</b></u>
Firstly, the algorithm calculates the two segments’ slope of the certain point connecting with the
two adjacent points(except the two endpoints of time series).Secondly, it determines the change points by the ratio of slope. And then it combines the points with the line orderly. In this way, a new time series arises.</p>

The key of the algorithm is determining the change points. The change points must follow the
following principles:

1. The first point and last point are both change point;
2. When the slope of the line combining the certain point with its left neighboring point is zero, we
look on the point as change point if the slope of the line combining the certain point with its right
neighboring point is out the range of$(-d,+d);$
3. When the slope of the line combining the certain point with its left neighboring point is not zero, we look on the point as change point if the slope ratio of two lines is beyond the range of $(1-d,1+d).$ The two lines refer to the line which combines the certain point with its right neighboring point and the line which combines the certain point with its left neighboring point. Above $d$ is a threshold parameter.



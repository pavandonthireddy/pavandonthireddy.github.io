---
layout: post
title: Sampling and interpolation
description: Sampling and interpolation
summary: Sampling and interpolation
author:
- Pavan Donthireddy
usemathjax: true
tags: [sampling, interpolation, numerical_methods]
original: zelicarxiv
---


<p align="justify">Nowadays, a lot of time series data is produced, which represents the state of the environment over a period
of time [15]. These data points are generally captured by a piece of equipment called a sensor. The sensor can
detect dierent events or changes in the environment and quantify the changes in the form of temperature,
pressure, noise, or light intensity, among others. A limitation of collecting data points is the frequency at
which the sensor records the changes or events. The more frequently a sensor records a reading, the more
expensive the running cost is. Likewise, the less frequent the sensor records the reading, the more difficult it
is to capture and reconstruct the original behaviour of the event.
In practice, all signals have to be sampled because the number of points in a continuous environment is infinite</p>


<p align="justify">Sampling is the mechanism that collects the information by setting the frequency of the collected
points over a time period. Capturing readings more often is economically more expensive due to the amount
of data being stored, transmitted, and processed. The challenge while performing sampling is to preserve the
vital information in the less amount of data points so that the objective of recording changes is met.
The periodic or Riemann sampling [15] is a conventional approach of sampling in the time series data.
In this approach, the data is captured periodically, i.e. at an equidistant time intervals (such as each
second or each microsecond). Even though the approach is simple to implement, the shortcoming is that,
when the sampled data fails to indicate changes that happen between the interval (also known as frequency
aliasing), sampling needs to be readjusted at a higher frequency, resulting into more data collection. Firstly,
making such an adjustment requires manual assessment, and in addition to that, it bears the additional cost</p>


<p align="justify">concerning more data being generated. Due to this pitfall, many research findings advocated for the use of
Lebesgue sampling, instead of Riemann sampling [24]. Furthermore, some authors [2] have demonstrated
Lebesgue sampling being a more ecient strategy compared to Riemann sampling.
The Lebesgue sampling [4], also known as Event-based sampling, is an alternative sampling strategy to
the more popular Riemann sampling strategy. In the Lebesgue sampling, the time-series data is sampled
whenever a signicant change takes place or when the measurement passes a certain limit [17]. A few
motivating examples of sampling strategy would be: whenever a specic value of the sensor reading crosses a
limit, when a data packet arrives at a node on a computer network, or when the system output has changed
with a specied amount.</p>

<p align="justify">
The overall intuition of the Lebesgue sampling is to save the unnecessary data from being stored, processed,
or transmitted which represents either no change or a trivial change compared to the previous data point.
The nature of sampling based on events in the Lebesgue sampling is very appealing and natural in many
domains where the systems remain constant for an extended period such as wireless communications [19] or
systems with an on-o mechanism like those in the satellite control [2].
Increasing the battery life of the sensors and reducing their use [25], reducing network trac by decreasing
the amount of information transferred [32], or using fewer computer resources while maintaining the same
performance [31], are some of the advantages of event-based control over control based in time. 
</p>
<p align="justify">By contrast,
the management of the systems that implement Lebesgue sampling becomes more complicated [2].
When a time series signal is sampled, generally, the subsequent step is to reconstruct the original signal
as accurately as possible [14]. The interpolation method is one of the well-known criteria to reconstruct
the signal by lling the missing values between the range of the discrete set of data points. Despite the
signicance of the interpolation methods, the challenge of reconstructing the signal remains an important
area of research.</p> 

<p align="justify">Moreover, common interpolation methods do not perform well on Lebesgue sampling as
demonstrated in this contribution.
In this contribution, it is proposed interpolation methods to reconstruct the time-series data sampled
using Lebesgue sampling. To the best of our knowledge, this is the rst interpolation method designed
exclusively for Lebesgue sampling. The proposed methods have a higher performance because they exploit
the particular properties of this kind of sampling.
Two novel interpolation methods are proposed: ZeLiC and ZeChipC. ZeLiC uses Zero-order hold and
Linear interpolation with specic shape approximation on the basis of Concavity/Convexity1. On the
other hand, ZeChipC uses Zero-order hold and PChip interpolation with the same Concavity/Convexity
improvement as ZeLiC.</p>

### Lebesgue Sampling

<p align="justify">Lebesgue sampling is an alternative to the traditional approach of sampling time series at a constant frequency.
Instead of periodically taking samples from a system like in Riemann sampling, the event-based method takes
samples only when a predened event happens as shown in Figure 1. Some examples of typical events could
be a sudden change in the signal, the signal reaching a preset limit, the arrival of a data package, or a change
in the state of a system [2]. </p>

<p align="justify">Even though Lebesgue sampling is more accurate than Riemann sampling it is
less extended because those systems are more dicult to implement [2].
In recent years, a great interest has aroused in applications implementing event-based sampling. For
example, the \Send on Delta" algorithm takes advantage of Lebesgue sampling to reduce the information
transmitted by wireless networks in order to increase the lifetime of the sensors batteries. Under this scheme,
the sampling is performed only when there is a deviation in the signal higher than the delta value. Results
show that using this approach it is possible to increase the lifetime of the sensors without any loss of quality
in the resolution of the signals [25].</p>



<p align="justify">We can find another positive example in the domain of Networked Control Systems (NCSs), where the
advantages of Lebesgue sampling become clear. In this type of systems increasing the sampling frequency
can be counterproductive since the information load increases and the trac of the network can collapse
the whole system functioning. In the last decade, many NCS have successfully implemented event-triggered
control reducing the required resources and the bandwidth of the network [32].
It is also interesting pointing out the convenience of using event-based sampling in the Fault Diagnosis
and Prognosis (FDP). In the last years, it has been increasingly dicult to manage microcontrollers and
embedded systems due to the volume of the information collected by sensors and to the complexity of the
programs that they implement. Increasing computational resources is not a good solution in the long term
since it increases economic costs. Yan et al. [31] found an ecient solution to this problem applying the
philosophy of \execution only when necessary" based on Lebesgue sampling, which reduces computational
costs substantially without diminishing the performance of the system.</p>

<p align="justify">
Some research has been done to nd the optimal balance between the number of samples and the performance
of the system. For example, Andren, et al. [1] studied this balance for a linear-quadratic-Gaussian
(LQG) control problem setting with output feedback. However, sampling based on changes works well with
signals that remain constant for some time and present sudden variations. This is because this kind of sampling
captures a higher number of points when the signal has abrupt changes while it does not take points
when the signal remains constant. For example, when a natural phenomenon like an earthquake takes place,
the sensor values can go from zero to a positive high value in an instant. With sampling based on events, more
points of the critical moments would be captured, which gives important information about the behaviour of
the phenomenon while if nothing occurs no information will be captured.
Lebesgue sampling can minimise energy consumption, storage space, computation time and the amount
of data to be transmitted as it has been claimed in many investigations [30].</p>

### Time series interpolation methods

The downsampled time series data can be reconstructed using different interpolation techniques. The interpolation function estimates the missing data points within the range of the discrete set of known data points with the objective of preserving the shape of the original signal before the application of downsampling [22].
Let $\left(x_i, y_i\right), i=0, \ldots, n$ be pairs of real values, where $f$ is the interpolation function, $x_i$ are the indexes of the downsampled data points, and $y_i$ are the values of those points. The objective of the optimal interpolation technique is to satisfy the condition where $f\left(x_i\right)$ verifies $y_i$.
$$
f\left(x_i\right)=y_i \text { for } i=0, \ldots, n
$$
There are a number of interpolation techniques ranging from simpler ones such as Zero-order hold [11] and Linear [11], to a more complex ones such as Multiquadric [18] which is based on radial basis function, Shannon [23] which is based on Nyquist-Shannon sampling theorem, Lasso [29] which is based on regression, Natural Neighbour [8] which is a spatial method and provides smoother approximation compared to simple interpolation technique. Cubic Hermite spline [21] and Piecewise Cubic Hermite Interpolating Polynomial (PCHIP) [20] are interpolation techniques based on splines and cubic function respectively. They are often a preferred choice in the polynomial interpolation.

The relation 2 describes the objective function of an interpolation method. Let $\left(x_i, y_i\right), i=0, \ldots, n$ pairs of real values. We want to find a function $f$ (easy to calculate), where $f$ verifies
$$
f\left(x_i\right)=y_i \text { for } i=0, \ldots, n
$$
#### Zero-order hold interpolation

The zero-order hold (ZOH) interpolation is one of the simplest signal reconstruction techniques [11]. In this technique, the missing values between two sampled points are interpolated with a constant value. This constant value is the same value of the preceding known point before encountering missing values. This technique has several applications in electrical communication and the main advantage is its low computational complexity. However, this interpolation strategy fails to reconstruct continuity or trend in time series with non zero values for the first derivative.

In ZOH, the polynomial $C_i(x)$ is of 0 th degree. Therefore, $C_i(x)=c$ where $c$ is constant. Because of (2), $C_i\left(x_{i-1}\right)=y_{i-1}$. If in $x_i$, a sudden change is presented, we cannot represent it because $C_{i+1}\left(x_i\right)=y_i \neq y_{i-1}$. Therefore, this interpolation cannot be used neither to represent continuous functions nor to produce a natural curves.

#### First order or Linear interpolation

Linear interpolation is also another popular choice for the reconstruction of a signal due to its simplicity and low computational complexity . In this method, missing values are reconstructed by fitting a straight line between successive known points. The shortcoming is that the reconstruction of a signal fails to capture any non-linear trend even though the overall known values follow a non-linear trend.

The polynomial $C_i(x)$ is of 1st degree, which means $C_i(x)=a x+b$, and because of (2), $C_i\left(x_{i-1}\right)=y_{i-1}$ and $C_i\left(x_i\right)=y_i$, where each two consecutive pair of sampled points are connected using a straight line. The following formulas can be applied to calculate $a$ and $b, \forall i=1, \ldots, n$
$$
\left\{\begin{array}{l}
a=\frac{y_i-y_{i-1}}{x_i-x_{i-1}} \\
b=y_i-a x_i
\end{array}\right.
$$


This interpolation gives a continuous but non-differentiable function $f$. Let $C_i(x)=a_i x+b_i$ and $C_{i+1}=$ $a_{i+1} x+b_{i+1}$, we have
$$
\begin{aligned}
& \lim _{x^{-} \rightarrow x_i} f^{\prime}(x)=a_i \\
& \lim _{x^{+} \rightarrow x_i} f^{\prime}(x)=a_{i+1}
\end{aligned}
$$
Therefore, the function is differentiable only if $a_i=a_{i+1}, \quad \forall i=1, \ldots, n$. We can conclude that for non-linear functions, $f$ is not differentiable with linear interpolation.

Linear interpolation is fast to compute and very intuitive. However, the drawback is the non-derivability of the interpolation at each node, which makes it produce sharp changes in the reconstructed signal.
#### Spline interpolation methods

In the spline interpolation methods, the interpolation function is a particular case of piecewise polynomial. The advantage of this type of method over the first order interpolation is that it reconstructs the signal using non-linear functions (which makes the transitions smoother) and also avoids the Runge phenomenon [5, 28]. The Runge phenomenon refers to the oscillation at the edges of a given interval while interpolating missing values.

We can define $f$ as $f(x)=C_i(x)$ for $x \in\left[x_{i-1}, x_i\right], i=1, \ldots, n$ where $C_i$ is a polynomial of small degree. Where $C_i\left(x_i\right)=C_{i+1}\left(x_i\right)=f\left(x_i\right)=y_i$. The most common degrees in terms of interpolation are the first and third degree, which are Linear and Cubic interpolation.
2.2.4 Third order or Cubic interpolation
The cubic function is one of the most commonly used spline interpolation methods [21]. It uses a third-degree polynomial in the Hermite form for interpolating missing values as follows $C_i(x)=a x^3+b x^2+c x+d$. This interpolation strategy inherits the conditions of Linear interpolation and adds conditions on its first and second derivatives:
$$
\begin{aligned}
C_i\left(x_i\right) & =C_{i+1}=f\left(x_i\right) \\
C_i^{\prime}\left(x_i\right) & =C_{i+1}^{\prime}=f^{\prime}\left(x_i\right) \\
C_i^{\prime \prime}\left(x_i\right) & =C_{i+1}^{\prime \prime}=f^{\prime \prime}\left(x_i\right)
\end{aligned}
$$
The strength of this interpolation strategy is the fact that it produces smooth curves in the region of missing values which makes the signal look natural. The drawback of this method is that it can lead to significant errors in the region of reconstruction when there is an abrupt change at the end of an interval. Where the derivative on the nodes (sampled points) must be equal, this change will be presented in the beginning of the next interpolated interval.

#### Piecewise Cubic Interpolating Polynomial (PCHIP)

The PCHIP (Piecewise Cubic Hermite Interpolating Polynomial) interpolation method is based on the same principle as the spline interpolation, but between each point, it fits a cubic polynomial in Hermite's form [20]. The sampled points are known as "knots", PCHIP connects those "knows" independently making a good performance in time and results. The given points have first derivative at the interpolated points, although the second derivative is not guaranteed to be continuous.


### Other interpolation methods for lebesgue sampling

Lebesgue sampling is typically used in conjunction with interpolation techniques to reconstruct the continuous signal from the irregularly sampled data. Here are some interpolation techniques that are commonly used with Lebesgue sampling:

1.  Sinc interpolation: Sinc interpolation is a commonly used technique for reconstructing a continuous signal from its samples. It involves using the sinc function, which is the Fourier transform of the rectangular window function used to sample the signal, to interpolate between samples.
    
2.  Polynomial interpolation: Polynomial interpolation involves fitting a polynomial to the sampled data points and using the polynomial to interpolate between samples. This technique can be computationally efficient, but may not provide accurate interpolation for signals with high-frequency components.
    
3.  Radial basis function (RBF) interpolation: RBF interpolation involves using a set of radial basis functions, such as Gaussian or inverse multiquadric functions, to interpolate between samples. This technique can be effective for signals with complex structure and can provide accurate interpolation with relatively few basis functions.
    
4.  Wavelet interpolation: Wavelet interpolation involves using wavelet transforms to decompose the signal into different scales and interpolate the signal at each scale using a suitable interpolation technique. This technique can be effective for signals with complex structure and can provide accurate interpolation at different scales.
    

Overall, the choice of interpolation technique depends on the specific characteristics of the signal and the desired accuracy and computational efficiency of the interpolation. It's important to carefully evaluate the performance of each technique on a given signal and choose the one that provides the best results.


---
layout: post
title: Trend Estimation
description: Trend Estimation
summary: Trend Estimation
author:
- Pavan Donthireddy
usemathjax: true
tags: [trend_estimation]
original: new
---

From the viewpoint of mathematical modeling, trend is not a well-defined concept. In general, trend may be considered as “long-term smooth change
in the mean level”.

To carry out in-depth statistical study of time series, it is often necessary to convert
a nonstationary series into a stationary one before the statistical model is treated. In
other words, time series will be decomposed into individual trend, seasonal, and irregular
components. 

Conventionally, there are two different ways to decompose a time
series which does not consist of seasonal component (or is seasonally adjusted): differencing
and detrending. The differencing will remove trend, while the detrending (trend
estimation) will present an estimate to trend. Thus, the differencing and detrending
are essentially high-pass filter and low-pass filter, respectively, from the viewpoint of
digital signal processing (DSP).


Generally speaking, methods of trend estimation fall into two major categories: parametric
and nonparametric. In the parametric approach, a deterministic trend is commonly
expressed by a particular smoothing function or model, such as a polynomial,
the Gompertz curve or the logistic curve (Meade and Islam, 1995), or the structural
time series model (Harvey, 1989). However, the use of an inappropriate parametric
model may cause misleading information and even incorrect inference about the trend
curve. Therefore, alternative nonparametric trend estimation methods are widely used.
In particular, nonparametric approaches offer considerable Lexibility in the selection of
0tting curves and may yield satisfactory estimates. In conventional time series analysis,
some of the most widely used nonparametric approaches include moving average 0lters
and exponential smoothing 0lter, which are linear low-pass 0lters in the sense of the
DSP. A variety of moving average 0lters are proposed, such as Spencer 0lter (Kendall
et al., 1983), Henderson 0lter (Kenny and Durbin, 1982), and GLAS 0lter (Blanchi
et al., 1999), etc. The asymmetric exponential smoothing filter (Kenny and Durbin), has a distinguished advantage in the treatment of boundary effect, hence is often
preferred for the purpose of forecasting.

Apart from these linear filters, various nonparametric regression estimators existing
in the literature can be easily adopted for the purpose of trend estimation. This is
because that the counterpart of trend component $T_{t}$ in the content of nonparametric
regression is just the regression function $T(x_{t} )$,

$$
y_{t} = T(x_{t})+ \epsilon_{t}, \qquad t=1,2,\dots, N
$$

where $x$ and $y$ are explanatory and response variable, respectively. Many powerful nonparametric regression estimators have been proposed and applied in the literature, such as kernel smoothing (Müller, 1988), LOESS (Cleveland, 1979), locally weighted polynomial regression (Fan and Gijbels, 1996), smoothing spline (Eubank, 1999), and regression spline (Doksum and Koo, 2000). Furthermore, there are also many interesting studies suggested in the literature in order to enhance the performance of nonparametric regression estimators, such as improving the accuracy (e.g., Borra and Ciaccio, 2002), dealing with special data (e.g., Keilegom et al., 2001), and so on. In fact, the nonparametric regression has been successfully used in trend estimation, see for example Härdle and Tuan (1986), Goodall (1990), Hart (1991, 1994), Høst (1999), and Ferreira et al. (2000). Other nonparametric trend estimation methods that were studied in the literature include: Hodrick Prescott (HP) filter (Hodrick and Prescott, 1997), median filter (Wen and Zeng, 1999), wavelet shrinkage (Donoho et al., 1995), and linear programming (Mosheiov and Raveh, 1997). Usually, a successful nonparametric method has one or more underlying smoothing parameters which can be adjusted to balance the fundamental tradeoffs of the estimates, i.e., the smoothness-fidelity tradeoff and the variance-bias tradeoff.

What is more relevant to the present work is a class of nonparametric trend estimation methods that attempt to globally quantify the competition between the two conflicting features: the smoothness and the fidelity. The earliest motivation to this approach dates back to 1923 when Whittaker (1923) introduced graduation, which is also one of the earliest works of nonparametric regression in the literature. By using the residual sum of squares $\sum_{t=1}^N\left(y_t-T_t\right)^2$ as the global measure of fidelity of the estimated trend $T_t$, Whittaker (1923) suggested to define the sum of the squares of $k$ th order differences as the measure of roughness. Then the optimal trend is given by solving the following minimization scheme:
$$
(\mathrm{WH}): \min _{\left\{T_t\right\}_{t=1}^N}\left\{\sum_{t=1}^N\left(y_t-T_t\right)^2+\lambda^2 \sum_{t=1}^{N-k}\left(\Delta^k T_t\right)^2\right\},
$$
where order $k$ and smoothing parameter $\lambda$ are user-specified constants and $\Delta$ is the difference operator.

A particular example following Whittaker's approach is the HP filter (Hodrick and Prescott, 1997), which has been most extensively used in the real business cycle literature for detrending
$$
\text { (HP): } \min _{\left\{T_t\right\}_{t=1}^N}\left\{\sum_{t=1}^N\left(y_t-T_t\right)^2+\lambda \sum_{t=1}^N\left(T_{t-1}-2 T_t+T_{t+1}\right)^2\right\} .
$$
Hodrick and Prescott recommended setting $\lambda=1600$ when applying to real business studies. By manipulating the relevant first-order condition, the HP scheme leads to a two-way moving average with weights subjected to a damped harmonic approximately, see King and Rebelo (1993).

Recently, a popularly used measurement of the roughness penalty of estimates $T\left(x_t\right)$ in nonparametric regression is $\int\left[T^{\prime \prime}(x)\right]^2 \mathrm{~d} x$. This leads to following penalized leastsquares regression scheme:
$(\mathrm{SS}): \min _{\left\{T_t\right\}_{t=1}^N}\left\{\sum_{t=1}^N\left(y_t-T_t\right)^2+\lambda \int\left[T^{\prime \prime}(x)\right]^2 \mathrm{~d} x\right\}$,
which is known as smoothing spline estimator. Remarkably, the problem of optimization SS over the space of all twice differentiable functions on the interval $[a, b]=\left[x_1, x_N\right]$ has a unique solution $T_\lambda(x)$ which is defined as the natural cubic spline, see Eubank (1999) and references therein.

More recently, Mosheiov and Raveh (1997) (MR) proposed a linear programming approach to estimate the trend by employing the sum of the absolute values rather than the common sum of squares to measure the smoothness and fidelity. The tradeoff balancing leads to such an optimization scheme
$$
(\mathrm{MR}): \min _{\left\{T_t\right\}_{t=1}^N}\left\{\lambda \sum_{t=1}^N\left|y_t-T_t\right|+(1-\lambda) \sum_{t=1}^{N-2}\left|T_{t+2}-2 T_{t+1}+T_t\right|\right\} .
$$
Through a trick of variable changing, the objective function of the minimization scheme MR will be free of the absolute operator. However, extra constraints, monotonicity or polytonicity, have to be forced upon estimates in order to uniquely solve the linear programming problem. The location of the changing points of polytone trend is case-dependent and its selection is somewhat arbitrary.

Obviously, all these optimization schemes are closely related. The pointwise roughness measure of MR, $T_{t+2}-2 T_{t+1}+T_t$, is essentially the same as those of HP and WH, and is the discrete version of SS. Instead of forward difference, $T_{t+2}-2 T_{t+1}+T_t$, the backward and central difference approximation may also be used in the optimization MR. Moreover, with appropriate boundary modifications (such as in HP filter, see Baxter and King, 1995), the summation of the global smoothness measure in WH and MR can be processed from 1 to $N$, which may be more reasonable in a comparison with the integration in SS. Apart from their common motivation, another common feature of this class of nonparametric approaches is their use of global implicit minimization. As is well known, a global minimization problem can be quite expensive for its numerical computation.



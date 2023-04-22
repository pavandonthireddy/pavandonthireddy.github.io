---
layout: post
title: Recursive Algorithms for Trailing Stop Stochastic Approximation Approach
description: Recursive Algorithms for Trailing Stop Stochastic Approximation Approach
summary: Recursive Algorithms for Trailing Stop Stochastic Approximation Approach
author: Pavan Donthireddy
usemathjax: true
original: yin2010 - yin2008
tags: [stochastic_optimization, trading, execution]
---

## Abstract 

<p align="justify">Trailing stops are often used in stock trading to limit the maximum of a
possible loss and to lock in a profit. This work develops stochastic approximation
algorithms to estimate the optimal trailing stop percentage. A stochastic optimization
approach is proposed to recursively estimate the desired trailing stop percentage.
A modification using projection is developed to ensure that the approximation
sequence constructed stays in a reasonable range. Convergence of the algorithm is
obtained. Moreover, interval estimates are constructed. Simulation examples are presented
to compare our algorithm with Monte Carlo methods. Finally, we use real
market data to demonstrate the algorithms.</p>
## Formulation

In our formulation, we shall not require the stock price $S(t)$ be any specific stochastic process or follow any specific distributions; we only assume the stock price being observable. Based on the observed stock price, for a given time $t$, we define the stop price at a trailing stop percentage $h$ with $0<h<1$ as
$$
T_h(t)=(1-h) S_{\max }(t)
$$
where
$$
S_{\max }(t)=\max \{S(u): 0 \leq u \leq t\}
$$
Let
$$
\tau=\inf \left\{t>0: S(t) \leq T_h(t)\right\}
$$
Then $\tau$ is the first time the stock price reaches the stop price. We aim to find the optimal trailing stop percentage $h_* \in[a, 1]$ with $a>0$ that maximize a suitable objective function. Thus the problem is
$(\mathcal{P})$ Find $\operatorname{argmax} J(h)=E[\Phi(S(\tau)) \exp (-\rho \tau)], \quad h \in[a, 1]$
Here $\rho>0$ is an appropriate discount rate and the reward function is
$$
\Phi(S)=\frac{S-S_0}{S_0}
$$
In practice, a trailing stop $h$ has to be greater than 0 because $h=0$ means selling right after bought the stock. In view of this, the lower bound $a$ is assumed to be greater than 0 , which represents a reasonable lower bound for the trailing stop percentage.
In general, an analytic solution is difficult to obtain even if $S(t)$ is a specific process, e.g., a geometric Brownian motion. This is mainly due to the pathdependence nature of the problem. Our contribution is to devise a numerical approximation procedure that estimates the optimal trailing stop percentage $h$. We will use a stochastic approximation procedure to resolve the problem by constructing a sequence of estimates of the optimal trailing stop percentage $h$, using
$$
\left.h_{n+1}=h_n+\{\text { stepsize }\} \text { gradient estimate of } J(h)\right\} .
$$
Moreover, in accordance with (4), we need to make sure the iterate $h_n \in[a, 1]$.

### Recursive Algorithm

Let us begin with a simple noisy finite difference scheme. The only provision is that $S(t)$ can be observed. Associated with the iteration number $n$, denote the trailing stop percentage by $h_n$. Beginning at an arbitrary initial guess, we construct a sequence of estimates $\left\{h_n\right\}$ recursively as follows. We figure out $\tau_n$, the first time when the stock price declines under the stop price as
$$
\tau_n=\inf \left\{t>0: S(t) \leq T_{h_n}(t)\right\} .
$$

Define a combined process $\xi_n$ that includes the random effect from $S(t)$ and the stopping time $\tau_n$ as
$$
\xi_n=\left(S\left(\tau_n\right), \tau_n\right)^{\prime}
$$
where $S\left(\tau_n\right)$ denotes the stock price process $S(t)$ stopped at stopping time $\tau_n$. Henceforth, we call $\left\{\xi_n\right\}$ the sequence of collective noise. Let $\hat{J}(h, \xi)$ be the observed value of $J(h)$ with collective noise $\xi$. With the values $h \pm \delta_n$, define $Y_n^{ \pm}$as
$$
Y_n^{ \pm}\left(h, \xi_n^{ \pm}\right)=\hat{J}\left(h \pm \delta_n, \xi_n^{ \pm}\right) .
$$
$\xi_n^{ \pm}$being the two different collective noises taken at the trailing stop percentages $h \pm$ $\delta_n$, where $\delta_n$ is the finite difference sequence satisfying $\delta_n \rightarrow 0$ as $n \rightarrow \infty$. We shall write $Y_n^{ \pm}=Y_n^{ \pm}\left(h, \xi_n^{ \pm}\right)$. For simplicity, in what follows, we often use $\xi_n$ to represent both $\xi_n^{+}$and $\xi_n^{-}$if there is no confusion. The gradient estimate at iteration $n$ is given by
$$
D \hat{J}\left(h_n, \xi_n\right) \stackrel{\text { def }}{=}\left(Y_n^{+}-Y_n^{-}\right) /\left(2 \delta_n\right)
$$
Then the recursive algorithm is
$$
h_{n+1}=h_n+\varepsilon_n D \hat{J}\left(h_n, \xi_n\right),
$$
where $\varepsilon_n$ is a sequence of real numbers known as stepsizes. A frequently used choice of step size and finite difference sequences is $\varepsilon_n=O(1 / n)$ and $\delta_n=O\left(1 / n^{1 / 6}\right)$. Throughout this paper, this is our default choice of stepsize and finite difference sequences.
To proceed, define
$$
\begin{aligned}
& \rho_n=\left(Y_n^{+}-Y_n^{-}\right)-E_n\left(Y_n^{+}-Y_n^{-}\right), \\
& \eta_n=\left[E_n Y_n^{+}-J\left(h_n+\delta_n\right)\right]-\left[E_n Y_n^{-}-J\left(h_n-\delta_n\right)\right], \\
& \beta_n=\frac{J\left(h_n+\delta_n\right)-J\left(h_n-\delta_n\right)}{2 \delta_n}-J_h\left(h_n\right),
\end{aligned}
$$
where $E_n$ denotes the conditional expectation with respect to $\mathcal{F}_n$, the $\sigma$-algebra generated by $\left\{h_j, \xi_j^{ \pm}: j<n\right\}, J_h\left(h_n\right)=(\partial / \partial h) J\left(h_n\right)$. In the above, $\eta_n$ and $\beta_n$ represent the noise and bias, and $\left\{\rho_n\right\}$ is a martingale difference sequence. We separate the noise into two parts, uncorrelated noise $\rho_n$ and correlated noise $\eta_n$. It is reasonable to assume that after taking the conditional expectations, the resulting function is smooth. With the above definitions, algorithm (9) can be rewritten as
$$
h_{n+1}=h_n+\varepsilon_n J_h\left(h_n\right)+\varepsilon_n \frac{\rho_n}{2 \delta_n}+\varepsilon_n \beta_n+\varepsilon_n \frac{\eta_n\left(h_n, \xi_n\right)}{2 \delta_n} .
$$

### Projection Algorithms

The use of projections in the algorithms stems from two reasons. First, for the purpose of computations, it is more convenient if one uses projections to force the iterates to remain in a bounded region. In addition, the problems under consideration may well be constrained so that the iterates will be in a given set. Current problem under consideration is such an example (the iterates need to stay in the interval $[a, 1]$ ). For example, one might choose a lowest trailing stop percentage of $10 \%$ to ensure the holding position will not be closed due to the normal fluctuations of daily stock price. Obviously, there is a upper bound for the optimal trailing stop percentage, $100 \%$. To solve the problem (4) with constrains, we construct the following stochastic approximation algorithm with a projection
$$
h_{n+1}=\Pi\left[h_n+\varepsilon_n D \hat{J}\left(h_n, \xi_n\right)\right]
$$
where $\varepsilon_n=1 / n, \delta_n=\delta /\left(n^{1 / 6}\right)$ and $\Pi[x]$ is a projection given by
$$
\Pi[h]= \begin{cases}a, & \text { if } h<a, \\ 1, & \text { if } h>1, \\ h, & \text { otherwise. }\end{cases}
$$
As in Kushner and Yin [4], the projection algorithm (11) can be rewritten as
$$
h_{n+1}=h_n+\varepsilon_n D \hat{J}\left(h_n, \xi_n\right)+\varepsilon_n r_n,
$$
where $\varepsilon_n r_n=h_{n+1}-h_n-\varepsilon_n D \hat{J}\left(h_n, \xi_n\right)$ is the real number with the shortest distance needed to bring $h_n+\varepsilon_n D \hat{J}\left(h_n, \xi_n\right)$ back $[a, 1]$ if it is outside this set.


## Interval Estimates

This section is devoted to obtaining interval estimates as well as a piratically useful stopping rule for the recursive computation. Roughly, with prescribed confidence level, we wish to show that with large probability (probability close to 1 ), a sequence of scaled and centered estimates and a stopped sequence converge weakly to a diffusion process. Based on this result, we will then be able to build confidence interval for the iterates.

To proceed, for simplicity of notation, we take $\varepsilon_n=1 / n$ and $\delta_n=\delta_0 / n^{1 / 6}$. In the analysis to follow, for simplicity and without loss of generality, we take $\delta_0=1$. We assume all the conditions of Theorem 3.1 holds. To carry out the subsequent study, we also assume an additional condition.
(A3) $J_h(h)=J_{h h}\left(h_*\right)\left(h-h_*\right)+o\left(\left|h-h_*\right|^2\right)$, where $J_{h h}\left(h_*\right)-(1 / 2)<0$. In addition, $k^{2 / 3} E\left(h_k-h_*\right)^2=O(1)$ and the bound holds uniformly in $k$.

Remark 4.1 The first condition in (A3) indicates that $J_h(h)$ is linearizable. The second condition is a moment estimate. Sufficient conditions guaranteeing this can be provided by means of perturbed Lyapunov function methods; see for example [7] for liquidation related issues and the more extensive discussion in [4] for general setting. For simplicity, here we assume this condition.
Define
$$
\rho_n^*=\left[Y\left(h_*, \xi_n^{+}\right)-Y\left(h_*, \xi_n^{-}\right)\right]-E_n\left[Y\left(h_*, \xi_n^{+}\right)-Y\left(h_*, \xi_n^{-}\right)\right] .
$$
That is, $\rho_n^*$ is $\rho_n$ with the argument $h_n$ replaced by $h_*$. The detailed development of the interval estimates can be outlined as follows. Suppose that we can show that $n^{1 / 3}\left(h_n-h_*\right)$ is asymptotically normal with mean zero and asymptotic variance $\sigma^2$. Choose $\alpha$, such that $0<\alpha<1$ and $1-\alpha$ is the desired confidence coefficient. Given $\varepsilon>0$, then the asymptotic normality implies that
$$
P\left(\frac{n^{1 / 3}\left|h_n-h_*\right|}{\sigma} \leq z_{\alpha / 2}\right) \rightarrow 1-\alpha, \text { as } n \rightarrow \infty .
$$
This will lead to the desired confidence interval estimator. Then we require the length of the interval $\left|h_n-h_*\right|$ be small enough in that for any $\varepsilon>0$, for sufficiently large

$n$, we can make $\sigma z_{\alpha / 2} / n^{1 / 3}<\varepsilon$ or equivalently $n>\left\lfloor\sigma z_{\alpha / 2} / \varepsilon\right\rfloor$. Define
$$
M_{\varepsilon, \alpha}^n=\left\lfloor\frac{\sigma z_{\alpha / 2}}{\varepsilon}\right\rfloor, \quad \mu_{\varepsilon, \alpha}=\inf \left\{n: M_{\varepsilon, \alpha}^n \leq n\right\},
$$
where $\lfloor z\rfloor$ denotes the greatest integer that is less than or equal to $z$. Then $\mu_{\varepsilon, \alpha}$ is a stopping rule for the iterating sequence $\left\{h_n\right\}$. Denote
$$
I_{\mu_{\varepsilon, \alpha}}=\left[h_{\mu_{\varepsilon, \alpha}}-\sigma \frac{z_{\alpha / 2}}{n^{2 / 3}}, h_{\mu_{\varepsilon, \alpha}}+\sigma \frac{z_{\alpha / 2}}{n^{2 / 3}}\right] .
$$
We shall show that as the length of the interval shrinks, i.e., $\varepsilon \rightarrow 0$,
$$
P\left\{h \in I_{\mu_{\varepsilon, \alpha}} \text { and }\left|I_{\mu_{\varepsilon, \alpha}}\right| \leq \varepsilon\right\} \rightarrow 1-\alpha,
$$
where $\left|I_{\mu_{\varepsilon, \alpha}}\right|$ denotes the length of the interval $I_{\mu_{\varepsilon, \alpha}}$.



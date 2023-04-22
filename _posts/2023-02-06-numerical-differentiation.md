---
layout: post
title: Numerical differentiation
description: Numerical differentiation
summary:  Numerical differentiation
author:
- Pavan Donthireddy
usemathjax: true
tags: [numerical_differentiation]
original: new
---

Numerical differentiation is a problem to determine the derivative of a function from the values on an interval or some scattered points. It arises from many scientific researches and applications, e.g., the identification of the discontinuous points in an image process [1]; the problem of solving the Abel integral equation [2]; the problem of determining the peaks in chemical spectroscopy [3] and some inverse problems in mathematical physical equations [4]. The main difficulty is that it is an ill-posed problem, which means that small errors in the measurement of a function may lead to large errors in its computed derivatives [5,4]. A number of techniques have been developed for numerical differentiation [6-8,4,9]. One type of method is to transform the differentiation problem into an operator equation of the first kind. In fact, for given $g(t) \in H^1[0,1]$, to find $f=D g=g^{\prime}$ is equivalent to solve the Volterra integral equation of the first kind
$$
\left(K_1 f\right)(s)=\int_0^s f(t) \mathrm{d} t=g(s)-g(0), \quad s \in[0,1] .
$$
In this paper we will point out the disadvantage of operator $K_1$ and a new operator which is a modified form of $K_1$ will be presented. Since a singular system of the new operator can be obtained easily, it seems natural to use the TSVD method for this problem and good results may be expected. A convergence result, analogous to the literature [4], will be obtained by our method. Comparing with the Tikhonov regularization method used in [4], the regularization parameter can be obtained easily by TSVD method. Moreover, it is well known that the Tikhonov method has a finite saturation index, which means that it is impossible to improve the convergence rates of the regularization solution with increasing smoothness assumption of exact solutions. But for TSVD method this disadvantage will be overcome. Moreover, we will point out that our method calls for a discrete sine transform when the noisy values of the function to be differentiated at the nodes are given, so the method can be implemented easily and fast.



# Numerical Differentiation

Numerical differentiation is the process of approximating the derivative of a function using numerical methods. It is an important tool in scientific computing and is used in a variety of fields, including engineering, physics, and economics. There are several approaches to numerical differentiation, each with its own strengths and weaknesses.

## Finite Difference Methods

Finite difference methods are the most common approach to numerical differentiation. These methods approximate the derivative of a function by computing the difference quotient:

$$ f'(x) \approx \frac{f(x+h) - f(x)}{h} $$

where $h$ is a small positive number. This is known as the forward difference formula. Other difference formulas include the backward difference formula:

$$ f'(x) \approx \frac{f(x) - f(x-h)}{h} $$

and the central difference formula:

$$ f'(x) \approx \frac{f(x+h) - f(x-h)}{2h} $$

The choice of formula depends on the accuracy and smoothness of the function being approximated.

## Lagrange Polynomials

Lagrange polynomials are another approach to numerical differentiation that involves fitting a polynomial to a set of data points. Given a set of $n+1$ points $(x_i, f(x_i))$, the Lagrange polynomial is given by:

$$ p_n(x) = \sum_{i=0}^n f(x_i) \prod_{j\ne i} \frac{x-x_j}{x_i-x_j} $$

The derivative of the Lagrange polynomial can then be used to approximate the derivative of the original function.

## Splines

Splines are a method for approximating a function using piecewise polynomials. The polynomials are typically chosen to be cubic, and are required to be continuous at the points where they meet (known as knots). The second derivative of the polynomials is also required to be continuous, which ensures that the approximation is smooth. The derivatives of the splines can then be used to approximate the derivative of the original function.

## Richardson Extrapolation

Richardson extrapolation is a technique for improving the accuracy of finite difference approximations. It involves using the difference quotient at several different step sizes $h$ to derive a more accurate approximation. The formula for Richardson extrapolation is:

$$ f'(x) \approx \frac{4f_{h/2}(x) - f_h(x)}{3} $$

where $f_h(x)$ and $f_{h/2}(x)$ are the difference quotients at step sizes $h$ and $h/2$, respectively.

## Automatic Differentiation

Automatic differentiation is a method for computing derivatives numerically that is more accurate and efficient than finite difference methods. It uses the chain rule of differentiation to compute derivatives at each step of the computation, rather than approximating them numerically. This approach can be especially useful for functions with many variables or complex structures.

## Conclusion

Numerical differentiation is a powerful tool for approximating the derivatives of functions. Finite difference methods are the most common approach, but other techniques such as Lagrange polynomials, splines, Richardson extrapolation, and automatic differentiation can provide more accurate and efficient approximations in certain situations.


# Solving Numerical Differentiation in the Presence of Noise with Integral Equations

When performing numerical differentiation on data that is affected by noise, it can be challenging to obtain accurate and reliable results. However, one possible approach to this problem is to use integral equations to formulate the problem and derive a solution that takes into account the noise in the data. In this article, we will explore how integral equations can be used for numerical differentiation in the presence of noise, and we will provide some examples and techniques to illustrate this approach.

## The Problem of Numerical Differentiation with Noisy Data

The problem of numerical differentiation consists of estimating the derivative of a function based on a set of discrete data points. When the data is exact and noise-free, this problem can be solved using various numerical methods, such as finite differences, interpolation, or regression. However, in many practical situations, the data is affected by noise, which can cause errors and instability in the differentiation process.

To illustrate this problem, let's consider an example of a noisy data set:


```
x = [-2.5, -2.0, -1.5, -1.0, -0.5, 0.0, 0.5, 1.0, 1.5, 2.0, 2.5] 
y = [-2.635, -1.771, -0.768, -0.316, 0.383, 0.108, 0.704, 0.857, 2.275, 2.975, 4.350]

```


This data set represents a noisy version of the function `f(x) = x^3 - 2x^2 - 3x + 2`, which has the derivative `f'(x) = 3x^2 - 4x - 3`. If we try to estimate the derivative using finite differences or other standard methods, we may obtain results that are inaccurate or unreliable due to the noise in the data.

## Using Integral Equations for Numerical Differentiation

One possible approach to solving the problem of numerical differentiation with noisy data is to use integral equations. Integral equations involve expressing the problem as an equation involving an unknown function that needs to be solved for, and then using a known relationship between the function and its derivative to derive an integral equation that can be solved numerically.

To illustrate this approach, let's consider the following integral equation:

$$ \int_{-h}^{h} K(x,t) f'(t) dt = \frac{f(x+h) - f(x-h)}{2h} $$

In this equation, `f'(t)` represents the derivative of the unknown function `f(x)`, `K(x,t)` is a kernel function that depends on `x` and `t`, and `h` is a small parameter that controls the width of the integral. The right-hand side of the equation represents a finite difference approximation to the derivative of `f(x)`.

To solve this integral equation, we can use a technique known as collocation, which involves discretizing the equation by choosing a set of points `x_i` at which the equation is evaluated. We can then approximate the unknown function `f(x)` using a set of basis functions `phi_i(x)`, and write the integral equation as a system of linear equations:

$$ \sum_{j=1}^{N} K_{i,j} f'_j = D_i $$

In this equation, `N` is the number of collocation points, $K_{i,j} = \int_{-h}^{h} K(x_i,t)$


# Numerical Differentiation with Noisy Streaming Data using Online Algorithms

Numerical differentiation is a fundamental problem in many fields of science and engineering, where we want to estimate the derivative of a function at a given point based on sampled data. However, when the data is noisy or when it arrives in a streaming fashion, this problem becomes more challenging. In this article, we will discuss how to use online algorithms to solve the problem of numerical differentiation with noisy streaming data.

## The Problem

Suppose we have a function f(x) that we want to differentiate at a point x0. We can use the following formula to approximate the derivative:

$$f'(x0) \approx \frac{(f(x0+h) - f(x0-h))}{(2h)}$$

where h is a small step size. However, if the data we have is noisy, this approximation may not be accurate. Moreover, if the data arrives in a streaming fashion, we cannot wait until all the data is available to compute the derivative.

## Offline Approaches

Before we discuss online algorithms, let's briefly review some of the offline approaches to numerical differentiation with noisy data. One common approach is to use smoothing techniques, such as the Savitzky-Golay filter or the moving average filter, to remove the noise from the data before computing the derivative. Another approach is to use integral equations, such as the Tikhonov regularization or the least-squares method, to estimate the unknown function and its derivative from the noisy data.

## Online Algorithms

While the offline approaches discussed above can be effective for solving numerical differentiation problems with noisy data, they are not well-suited for streaming data. Online algorithms, on the other hand, are designed to continuously update their estimates based on new data as it arrives, and they can be more efficient and accurate in a streaming context.

### Recursive Least Squares

One possible online algorithm for numerical differentiation with noisy data is recursive least squares (RLS). RLS is an adaptive algorithm that can continuously update its estimates based on new data as it arrives, and it has been shown to be effective for solving similar problems in a streaming context.

To apply RLS to numerical differentiation with noisy data, we can first choose a set of basis functions and a kernel function as before, and then use RLS to estimate the unknown function and its derivative based on the incoming data. The algorithm would work by updating the estimate of the function and its derivative at each time step based on the new data, and using a forgetting factor to weight the importance of the old data versus the new data.

### Extended Kalman Filter

Another possible online algorithm for numerical differentiation with noisy data is the extended Kalman filter (EKF). The EKF is a recursive algorithm that can estimate the state of a dynamic system based on noisy measurements, and it has been shown to be effective for solving similar problems in a streaming context.

To apply the EKF to numerical differentiation with noisy data, we can use the same integral equation and basis functions as before, and then use the EKF to estimate the unknown function and its derivative based on the incoming data. The algorithm would work by updating the estimate of the function and its derivative at each time step based on the new data, and using a Kalman gain to weight the importance of the measurement noise versus the process noise.

## Conclusion

In conclusion, while the specific details of how to apply online algorithms to numerical differentiation with noisy data may vary depending on the specific problem and algorithm, the general approach involves adapting the offline methods discussed above to the streaming context by using adaptive algorithms that can continuously update their estimates based on new data as it arrives. These online algorithms can be more efficient and accurate than their offline counterparts in a streaming context,



# Complex Variable Methods for Numerical Differentiation with Noisy Data

Numerical differentiation is a fundamental problem in many fields of science and engineering, where we want to estimate the derivative of a function at a given point based on sampled data. However, when the data is noisy, this problem becomes more challenging. In this article, we will discuss how to use complex variable methods to solve the problem of numerical differentiation with noisy data.

## The Problem

Suppose we have a function $f(z)$ that we want to differentiate at a point $z_0$. We can use the following formula to approximate the derivative:

$$f'(z_0) \approx \frac{f(z_0 + h) - f(z_0 - h)}{2h}$$

where $h$ is a small step size. However, if the data we have is noisy, this approximation may not be accurate. Moreover, if the function $f(z)$ is complex-valued, the above formula may not be well-defined.

## Complex Variable Methods

Complex variable methods provide an elegant and powerful way to differentiate complex-valued functions, even in the presence of noise. The key idea is to use the Cauchy-Riemann equations to express the derivative of a complex-valued function in terms of its analytic continuation to the complex plane.

### Cauchy-Riemann Equations

The Cauchy-Riemann equations are a set of conditions that a complex-valued function $f(z)$ must satisfy in order to be analytic in a region of the complex plane. The equations are:

$$\frac{\partial u}{\partial x} = \frac{\partial v}{\partial y} \quad \text{and} \quad \frac{\partial u}{\partial y} = -\frac{\partial v}{\partial x}$$

where $u(x,y)$ and $v(x,y)$ are the real and imaginary parts of $f(z) = u(x,y) + iv(x,y)$, respectively. If $f(z)$ is analytic, then it satisfies the Cauchy-Riemann equations, and we can use these equations to express the derivative of $f(z)$ in terms of its analytic continuation.

### Wirtinger Calculus

The Wirtinger calculus provides a convenient way to express the Cauchy-Riemann equations in terms of partial derivatives with respect to $z$ and $z^*$, where $z^*$ denotes the complex conjugate of $z$. Using the Wirtinger calculus, we can write the Cauchy-Riemann equations as:

$$\frac{\partial f}{\partial z^*} = 0 \quad \text{and} \quad \frac{\partial f}{\partial z} = f'(z)$$

where $f'(z)$ is the derivative of $f(z)$ with respect to $z$. These equations show that the derivative of $f(z)$ can be expressed in terms of its partial derivatives with respect to $z$ and $z^*$.

### Wirtinger Derivatives

The Wirtinger derivatives are defined as:

$$\frac{\partial}{\partial z} = \frac{1}{2}\left(\frac{\partial}{\partial x} + i\frac{\partial}{\partial y}\right) \quad \text{and} \quad \frac{\partial}{\partial z^*} = \frac{1}{2}\left(\frac{\partial}{\partial x} - i\frac{\partial}{\partial y}\right)$$


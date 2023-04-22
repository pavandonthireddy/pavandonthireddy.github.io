
---
layout: post
title: Dual Window Selective Median Switching Filter
description: Dual Window Selective Median Switching Filter
summary: Dual Window Selective Median Switching Filter
author:
- Pavan Donthireddy
usemathjax: true
tags: [filters, switching]
original: zhang2017
---

## Abstract

<p align="justify">A simple and efficient nonlinear image filtering
technique, called the dual window selective median switching
(DWSMS) filter, for the removal of both additive and impulse
noise from corrupted images, is proposed. Two moving concentric
windows are employed to determine the luminance value for
replacing that of the center pixel. Three steps are involved in this
filtering technique. First, the usual median filtering is applied to
the smaller window. Second, the median filtering is applied to the
larger window. Third, the two median filtered values are then
compared to the original center pixel, and the median-filtered
value closer to the center pixel is chosen to be the pixel’s filtering
output.</p>


## Introduction

<p align="justify">Local averaging is one of the simplest filtering techniques. It
preserves the mean luminance level while suppressing the
variability in flat regions. However, simple linear local
averaging is undesirable for image smoothing because it is
incapable of preserving image edges. Linear local averaging
filters are essentially low pass filters, which tend to blur the
edges and fine structures in the original image. In order to
preserve the edges while achieving some degree of smoothing,
it is desirable to employ nonlinear filters. Some of the most
popular nonlinear filters are the median filter [1], and its various
generalizations [2-12], which are well known to have the
required properties for edge preservation and impulse noise
removal. The basic idea for these methods is to select only a
portion of the luminance level values in the local window to use
in a (weighted) average. </p>

<p align="justify">In references [6-8], an alpha-trimmed
mean (􀄮-TM) filter, which uses a “median basket'' to select a
predetermined number of pixels above and below the median
pixel to the sorted pixels of the moving window, was proposed.
The values in the basket are averaged to give the 􀄮-TM filtering
output. An asymmetric way to select the averaging pixels whose
values are close to that of the median pixel was presented in
references [8-9] and was named the modified trimmed mean
(MTM) filter in reference [8]. In general practice, the averaging
weights of these filters are predetermined and are fixed
throughout the filtering processing. In [10], a varying weight
trimmed mean (VWTM) filter was introduced.</p>

<p align="justify">This filter employs the same median basket as the 􀄮-TM filter. However,
the averaging weights of the selected pixels vary dynamically
based on their differences with the median value.
Although superior to the median filter in some applications,
these median generalized filters also have their own limitations.
In general, the MTM outperforms the median filter in removing
additive noise, but not as well as the median filter in removing
impulse noise. The α-TM filter is, in general, superior to the
median filter as an impulse detector, but its performance in
removing impulse noise is not so well. </p>

<p align="justify">Although performing
better than many other filters, the VWTM filter’s computational
complexity is high. One common issue of all these nonlinear
filters is their difficulty/complexity of the parameter selections.
Because of its simplicity and outlier removal capability, the
median filtering technique is still widely used today.
To preserve the implementation simplicity and improve the
performance of the median filter, this paper proposes a new
nonlinear filtering technique, called the “dual window selective
median switching'' (DWSMS) filter, for the removal of both
additive and impulse noise. </p>

<p align="justify">We shall assume implicitly that the
ideal image is piecewise flat. Two normal concentric moving
windows are employed to determine the values to be used in
replacing the luminance level value of the center pixel. Three
steps are employed in this filtering procedure. First, the usual
median filtering is applied to the smaller window. Second, the
median filtering is applied to the larger window. Third, the two
median filtered values are then compared to the original center
pixel, and the value closer to the center pixel is chosen to be the
pixel’s filtering output.</p>


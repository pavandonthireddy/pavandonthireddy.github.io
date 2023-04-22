---
layout: post
title: Online algorithms for Blind Source Seperation
description: Online algorithms for Blind Source Seperation
summary: Online algorithms for Blind Source Seperation
author:
- Pavan Donthireddy
usemathjax: true
tags: [BlindSourceSeperation, online_algorithms]
original: new
---

Real-time online algorithms for blind source separation (BSS) are those that process incoming data in real-time, without requiring the entire data set to be available beforehand. Here are some examples of real-time online BSS algorithms:

1. Online independent vector analysis (IVA): IVA is an extension of independent component analysis (ICA) that allows for real-time processing of data streams. It uses an online learning rule to update the mixing matrix estimates as new data arrives.

2. FastICA online: FastICA is a popular ICA algorithm that has been adapted for online processing. The algorithm updates the mixing matrix estimates using a recursive algorithm that requires less computational resources than batch processing.

3. Recursive least squares (RLS)-based BSS: RLS is a widely used algorithm for adaptive filtering and has been adapted for BSS. It uses a recursive updating rule to estimate the mixing matrix and source signals as new data arrives.

4. Subspace tracking-based BSS: Subspace tracking algorithms such as the subspace recursive least squares (SRLS) algorithm can be used for online BSS. The algorithm tracks the subspace of the mixing matrix and updates the estimates as new data arrives.

5. Online joint approximate diagonalization of eigenmatrices (OJADE): OJADE is an online version of the JADE algorithm for joint approximate diagonalization of eigenmatrices. It updates the estimates of the mixing matrix and source signals as new data arrives.

These algorithms have been shown to be effective for real-time BSS and can be used in applications such as audio and speech processing, EEG analysis, and telecommunications.



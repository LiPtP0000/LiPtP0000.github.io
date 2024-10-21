---
layout: post
title: Discrete Fourier Transform
subtitle: DSP Chapter 3 Notes
mathjax: true
tags: [Digital Signal Processing]
author: LiPtP
---

{: .box-note}
这一章围绕DFT以及DFT的快速算法展开。我们将从DFS引出DFT，进而提出简化算法复杂度的DFT算法——FFT。我们还将简单讨论Chirp-z变换，以及FFT在线性卷积、IDFT、相关函数计算上的应用。

## 几个问题
1. Why we need DFT rather than DTFT?

{:.box-note}
一个信号的DTFT在频域内是一个**连续的周期函数**，对于连续信号来说，难以用计算机存储，因此我们需要一种离散的频域表示方法！DFT就是这样一种离散的频域表示方法。

2. DFS vs. DFT

{:.box-note}
DFS 针对的是周期序列，而DFT针对的是有限长序列。DFT相当于从一个周期信号的“主值区间”完成了DFS的工作。

## DFS的性质

## DFT的性质

## 快速算法——FFT

## Chirp-z变换

## 线性卷积、IDFT、相关函数计算上的应用
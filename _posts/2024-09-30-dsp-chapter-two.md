---
layout: post
title: Sampling and Rebuilding of Analog Signals
subtitle: DSP Chapter 2 Notes
mathjax: true
tags: [Digital Signal Processing, Signals and Systems]
author: LiPtP
---

{: .box-note}
We have already discussed about **discrete time signals** in chapter one. However, they are generally originated from analog signals. In this chapter, we will first introduce the concept of **sampling** and **rebuilding** of analog signals, and then discuss about the **Nyquist frequency** and **aliasing**. Finally, we will learn about the filters and the concepts of **undersampling** and **oversampling**.

## Sampling and Rebuilding of Analog Signals


## Analog LPFs in Sampling and Rebuilding
There are two main LPFs in sampling and rebuilding of analog signals:
1. 抗混叠滤波器
2. 平滑滤波器

## Sampling and Interpolation for Discrete Time Signals 
{:.box-note}
离散时间信号主要使用“整数M倍抽取”和“整数L倍内插”作为采样和插值的方法。

对于离散信号的采样，实际上是抽取过程，相当于**降采样**。
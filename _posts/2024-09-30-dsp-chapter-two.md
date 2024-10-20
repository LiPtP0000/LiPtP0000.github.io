---
layout: post
title: Sampling and Rebuilding of Analog Signals
subtitle: DSP Chapter 2 Notes
mathjax: true
tags: [Digital Signal Processing]
author: LiPtP
---

{: .box-note}
We have already discussed about **discrete time signals** in chapter one. However, they are generally originated from analog signals. In this chapter, we will first introduce the councept of **sampling** and **rebuilding** of analog signals, and then discuss about the **Nyquist frequency** and **aliasing**. Finally, we will learn about the filters and the concepts of **undersampling** and **oversampling**.

## Flowchart for DSP
老生常谈：采样、保持、量化、编码。
<br/>
    ![DSP flowchart](/assets/img/DSP/dsp_flow.png){: .mx-auto.d-block :}
    <br/>

## Sampling and Rebuilding of Analog Signals
讨论这个概念以前，我们先不讨论这个概念了，睡觉！

## Analog LPFs in Sampling and Rebuilding
主要了解两种滤波器：
1. 抗混叠滤波器
2. 平滑滤波器

## Sampling and Interpolation for Discrete Time Signals 

{:.box-note}
离散时间信号主要使用“整数M倍抽取”和“整数L倍内插”作为采样和插值的方法。对于离散信号的采样，实际上是抽取过程，相当于**降采样**。对于离散信号的插值，实际上是内插过程，相当于**升采样**。


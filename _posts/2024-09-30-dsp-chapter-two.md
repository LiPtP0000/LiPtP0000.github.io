---
layout: post
title: Sampling and Rebuilding of Analog Signals
subtitle: DSP Chapter 2 Notes
mathjax: true
tags: [Digital Signal Processing]
author: LiPtP
---

{: .box-note}
这一章是在DSP整体框架下，讨论Nyquist采样定理，**欠采样**、**升采样**的引入以及整数M倍抽取和L倍内插的采样方法。要求会画信号抽取前后的频谱，并掌握分析信号是否混叠的办法。

## Flowchart for DSP
老生常谈：数字信号转化为模拟信号的步骤为：**采样、保持、量化、编码**。这一部分实际上是反映了A/D模块，或者采样器的功能。而对于D/A模块，则需要对数字信号进行**内插**后进行平滑滤波，才能得到模拟信号。下面给出了一个流程图供参考。
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


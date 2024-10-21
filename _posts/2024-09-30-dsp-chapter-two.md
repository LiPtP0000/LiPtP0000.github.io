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
数字信号转化为模拟信号的步骤为：**采样、保持、量化、编码**。这一部分实际上是反映了A/D模块，或者采样器的功能。而对于D/A模块，则需要对数字信号进行**内插**后进行平滑滤波，才能得到模拟信号。下面给出了一个流程图供参考。
<br/>
    ![DSP flowchart](/assets/img/DSP/dsp_flow.png){: .mx-auto.d-block :}
    <br/>

本章的其余内容主要围绕**模拟信号**与**连续数字信号**之间转换的器件、方法展开。数字信号的部分是第三章之后的内容。
## Sampling of Analog Signals

对于等间隔采样，拥有**采样周期** $$T$$，对应的采样频率为$$f_s$$，对应的**角频率**为$$\Omega_s = 2\pi f_s$$。

{: .box-warning}
因此，在画频谱图时，$$\Omega$$是经过采样后，信号实际的角频率。而$$\omega$$则是归一化到$$2\pi$$后的角频率，即$$\omega = \frac{\Omega}{f_s}$$。

采样的过程就是时域信号与周期冲激信号的乘积，其频谱为原信号频谱的周期延拓。如果信号的频谱最高超过了$$\frac{\Omega_s}{2}$$， 就会出现**混叠**。
## Analog LPFs in Sampling and Rebuilding
主要了解两种滤波器：
1. 抗混叠滤波器
2. 平滑滤波器

对于抗混叠滤波器，一般是提高采样频率以增加过渡带宽，然而此时A/D转换器的采样数据量会增加。对于平滑滤波器，其理想特性是和**零阶保持器**紧密相关。该保持器要求冲激响应为一个长度为$$T$$，高度为1的门函数。
## Sampling for Band-pass Signals
如果是**带通信号**，其在直流和最低频谱之间的大量频带值为0。因此，如果在这些频率上的值被混叠了，带通信号只需要通过一个带通滤波器仍然可以重建。这种技术叫做**欠采样**。因此，对于采样频率$$\Omega_s$$的限制就大幅度降低了。

{:.box-note}
离散时间信号主要使用“整数M倍抽取”和“整数L倍内插”作为采样和插值的方法。对于离散信号的采样，实际上是抽取过程，相当于**降采样**。对于离散信号的插值，实际上是内插过程，相当于**升采样**。


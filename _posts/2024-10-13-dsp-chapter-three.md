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
DFS (Discrete Fourier Series) 针对的是周期序列，而DFT (Discrete Fourier Transform) 针对的是有限长序列。DFT相当于从一个周期信号的“主值区间”完成了DFS的工作。

定义一个符号$$W_N$$，表示N次单位根，按顺时针方向排列。具体的表达式为：

$$W_N = e^{-j\frac{2\pi}{N}}$$

## 区分各种卷积
一般在DSP中常用的卷积有以下三种：
1. 线性卷积
2. 周期卷积
3. 循环卷积

下面将对这三种卷积方式进行简要的区分。
### 三者之间的关系
1. 周期卷积是线性卷积以一定序列长度（设为L）为周期的**周期延拓**。
2. 对周期卷积**取主值序列**得到循环卷积。
3. 假设$$L$$为循环区间长度：
    - 当$$L < N+M-1 $$ 时，循环卷积是**线性卷积长度为L的混叠**；
    - 当$$L=N+M-1$$时，循环卷积=线性卷积；
    - 当$$L>N+M-1$$时，循环卷积是线性卷积末尾补$$L-(N+M-1)$$个零；
### 线性卷积
可以采用竖式乘法完成线性卷积。下面的C++代码展示了线性卷积的实现。序列的长度为 m+n-1，其中m和n分别为输入序列的长度。
```cpp
// 线性卷积
void convolution(double input1[], double input2[], double output[], int n, int m)
{
    int k = 0;
	int i = 0;
    int j = 0;

	for (k = 0; k < m + n - 1; k++) 
	{
		output[k] = 0;
	}

	//开始卷积
	//利用时延效果，记录所有乘积后，时间位置一样的相加
	for (i = 0; i < m; i++) 
	{
		for (j = 0; j < n; j++) 
		{
			output[i + j] += input1[i] * input2[j];
		}
	}
}

```
### 周期卷积
定义式：
$$\widetilde{y}[n] = \sum_{k=0}^{N-1} \widetilde{x_1}[k] \widetilde{x_2}[n-k]$$

是无限长离散周期信号通过一个离散时间系统后的响应。这个概念和DFS密切联系在一起。
### 循环卷积

## DFT的性质

## 快速算法——FFT

## Chirp-z变换

## 线性卷积、IDFT、相关函数计算上的应用
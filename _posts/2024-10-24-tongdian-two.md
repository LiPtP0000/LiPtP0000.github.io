---
layout: post
title: 噪声电路
subtitle: 通信电子线路第三章
tag: [通信电子线路]
# cover-img: /assets/img/aster.jpg
# share-img: /assets/img/aster.jpg
# thumbnail-img: /assets/img/aster.jpg
author: LiPtP
mathjax: true
---

{: .box-note}
**Note:** 本文内容主要基于《通信电子线路》教材第一、二章内容整理，主要介绍了噪声系数、接收灵敏度、阻断点等概念。<br/>

# 噪声系数和接收灵敏度

## 噪声功率 $$N$$

噪声来源于外部噪声和内部噪声。这里重点讨论内部噪声。电路中的电阻是无源器件噪声源，而二极管、三极管、MOSFET 等是有源器件噪声源。我们重点考虑**电阻热噪声**。

热噪声平均功率 $$N$$ 满足：

$$N = kTB$$ , _i.e._ $$N_{(dBm)} = 10\log_{10}\frac{KTB}{0.001}$$

值得一提的是，17 摄氏度时，有

$$N_{(dBm)} = -174+10 \log_{10} B \, (dBm)$$

有这个功率以后，我们能计算**噪声电压**。

$$ u\_{N}^2 = 4kTRB $$

{: .box-note}
这个噪声电压是电路中所有电阻的总噪声电压。

## 噪声系数 $$N_F$$

$$N_F = 10\log_{10}F = 10\log_{10}\frac{SNR_i}{SNR_o}$$

其中，$$SNR_i$$ 是输入信号的信噪比，$$SNR_o$$ 是输出信号的信噪比。

$$S_i$$ 是输入信号功率，$$S_o$$ 是输出信号功率。对于一个功率增益为$$G$$，内部噪声功率为$$N_A$$的放大器来说，有以下关系：

$$S_o = G\cdot S_i$$

$$N_o = G\cdot N_i + N_A$$

注意量纲统一。

多级级联电路噪声因数计算：

$$ F = F_1 +\frac{F_2-1}{G_1}+\frac{F_3-1}{G_1G_2}+\frac{F_4-1}{G_1G_2G_3}+\cdots $$

因此第一级必须是 LNA，否则整个系统的噪声系数都会变高。

## 等效噪声温度 $$T_N$$

- 和噪声因数 **F** 的对应关系： $$T_N = (F-1)T$$
- 线性电路产生的热噪声输出： $$N_A = GkT_N B$$

## 接收灵敏度 $$S$$

指的是：**保证必要的输出信噪比$$D$$的情况下，接收机输入端所需要的最小有用信号电平$$S_i$$。**

表达式：$$S_i = kTB_N FD$$

dBm 单位（室温 17 摄氏度，常用）：

$$S_{(dBm)} = -174(dBm) + 10 \log_{10} B_N + N_F + D(dB)$$
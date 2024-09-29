---
layout: post
title: 选频网络和阻抗变换
subtitle: 通信电子线路第二章
tag: [通信电子线路]
# cover-img: /assets/img/aster.jpg
# share-img: /assets/img/aster.jpg
# thumbnail-img: /assets/img/aster.jpg
author: LiPtP
mathjax: true
---

{: .box-note}
**Note:** 本文内容主要基于《通信电子线路》第二章内容整理，主要介绍了选频网络和阻抗变换。

# 信号的选频滤波
## 选频滤波器的分类
大体上，选频滤波器可以分为下面的几个大类。
<br/>
    ![选频网络概述](/assets/img/Tongdian-images/xuanpinwangluo.jpg){: .mx-auto.d-block :}
<br/>

同时，按照**实现功能**，又可以分为：
- 预选滤波器
- 中频通道滤波器

## 选频滤波器的主要参数计算
选频滤波器的主要参数有：
1. 带宽
2. 波形因数$$SF = \frac{BW_{-60dB}}{BW_{-3dB}}$$
3. 输入输出阻抗
4. 频率特性

### 阻抗匹配（L匹配网络）
对于这种题的求解，需要确定信号源和负载的大小关系，然后分情况带公式。最关键的是算出不同情况下的$$Q_e$$，以及感性、容性阻抗算法的区分。

- Q_e的计算公式：

$$
Q_e = \begin{cases}
\sqrt{\frac{R_S}{R_L}-1}, \quad & R_S>R_L \\
\sqrt{\frac{R_L}{R_S}-1}, \quad &  R_S<R_L
\end{cases}
$$
- 算阻抗
    - 对于感性阻抗： $$X =Q_e\cdot R$$
    - 对于容性阻抗： $$X = \frac{R}{Q_e}$$

### 算带宽BW和选择性SF
结论：
$$ BW =\frac{\f_0}{Q} (Hz)$$

这里有一个十分神奇的计算方法，可以将3dB带宽直接和品质因数联系起来，计算LC滤波器的带宽。详细的推导过程见[Q0是怎么和频率/带宽扯上关系的呢？](https://zhuanlan.zhihu.com/p/650245210)。然而对于选择性SF，就需要带电路参数进行计算了，因为涉及-60dB带宽的计算。

60dB衰减，即幅度衰减1000倍，我们代入**LC滤波器**的幅频响应：
$$
A(\omega) = \frac{1}{\sqrt{1+Q_P^2(\frac{\omega}{\omega_0}-\frac{\omega_0}{\omega})^2}}
$$
就可以找到两个$$\omega$$，进而算出带宽。这是带宽的通用算法。当然，这是乘了$$2\pi$$的结果，实际结果还需要归一化。


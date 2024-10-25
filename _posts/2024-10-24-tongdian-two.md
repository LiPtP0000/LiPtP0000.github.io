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

## 噪声系数 $$N_F$$

噪声来源于外部噪声和内部噪声。这里重点讨论内部噪声。电路中的电阻是无源器件噪声源，而二极管、三极管、MOSFET 等是有源器件噪声源。我们重点考虑**电阻热噪声**。

热噪声平均功率 $$N$$ 满足：

$$N = kTB$$ , _i.e._ $$N_{(dBm)} = 10\log_{10}\frac{KTB}{0.001}$$

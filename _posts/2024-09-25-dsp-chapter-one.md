---
layout: post
title: Discrete Time Signals and Systems
subtitle: DSP Chapter 1 Notes
mathjax: true
tags: [Digital Signal Processing, Signals and Systems]
author: LiPtP
---

{: .box-note}
**Discrete-time signals** can be obtained by sampling continuous signals at equal intervals, typically represented as sequences. Common discrete-time signals include the unit impulse, unit step, rectangular, real exponential, and complex exponential sequences. Sequence operations involve addition, multiplication, shifting, and energy calculations, with square summability and absolute summability being important classifications.<br/> Transformations of discrete-time signals include the **Discrete-Time Fourier Transform (DTFT) and the z-transform**, which have a close relationship, particularly in their correspondence on the unit circle. Discrete-time systems (LTI systems) generate outputs through the convolution of input signals with the unit impulse response, considering stability and causality. <br/>**The system function and frequency response** are key to analyzing system behavior, with filters categorized into FIR (no poles) and IIR (with poles) types; the former is a non-recursive structure, while the latter involves feedback mechanisms.

## 离散时间信号

离散时间信号通常用**序列**表示。可以通过连续时间信号采样得到离散时间信号。
等间隔采样：\\(x(T) = x_a(nT)\\)，其中\\(T\\)为采样周期，\\(n\\)为整数，$$f_s = \frac{1}{T}$$为采样频率。

### 常见的离散时间信号

- 单位冲激序列：$$x(n) = \delta(n)$$
- 单位阶跃序列：$$x(n) = u(n)$$，**本书中采用 $$u(n)$$ 表示，而非《信号与系统》中的$$\epsilon(n)$$**。

- 矩形序列：0 ～ N-1 为 1，其余为 0 的序列。

- 实指数序列
- 复指数序列: $$x(n) = r^n e^{j \omega_0 n}$$
- 正弦序列： $$x(n) = \sin(\omega_0 n)$$

{: .box-warning}
离散周期序列中，周期必定是整数周期。例如：
$$ \sin{\frac{16\pi n}{5}}$$ 的周期就是 5，而非 5/8.

### 序列的运算

1. 序列的相加、相乘（**逐项相乘**，线性卷积算法中，频域序列相乘即为如此）

2. 序列的移位

3. 序列的能量：$$S = \frac{1}{2}\sum_{n=-\infty}^{\infty}\|x(n)\|^2$$

   - 若$$S \lt \infty$$，则称序列为平方可和序列。
   - 若$$\sum_{n=-\infty}^{\infty}\|x(n)\| \lt \infty$$，则称序列为绝对可和序列。
   - 有界序列：$$\|x(n)\| \leq M$$，则称序列为有界序列。

4. 任意一个序列都可以分解成一个偶对称序列和一个奇对称序列的和。

5. 任意一个序列都可以表示为单位移位序列的**加权和**。

## 离散信号的 Fourier 变换和 z 变换

### DTFT

- $$X(e^{j\omega}) = \sum_{n=-\infty}^{\infty} x(n) e^{-j\omega n}$$
- 是以$$2\pi$$为周期的函数。
- 一个序列拥有 DTFT 的条件：**序列是绝对可和的**。因此有限长序列的 DTFT 总是存在。
- $$\omega$$ ： 频率对采样频率作归一化后的角频率，满足$$\frac{\omega}{2\pi} = \frac{f}{f_s}$$。
- IDTFT: $$x(n) = \frac{1}{2\pi} \int_{-\pi}^{\pi} X(e^{j\omega}) e^{j\omega n} d\omega$$，序列的 DTFT 和 IDTFT 互为逆变换。

### z 变换

- $$X(z) = \sum_{n=-\infty}^{\infty} x(n) z^{-n}$$
- 拥有收敛域。和**连续时间系统**的 Laplace 变换类似，但后者的收敛域是一个平面，如虚轴左侧；前者的收敛域一般以圆为分界。
  - 右边序列的收敛域在半径为$$R_-$$的圆外
  - 左边序列则相反
  - 双边序列为交集
- **常用 z 变换**：

  |          序列           |                       z 变换                        |       收敛域        |
  | :---------------------: | :-------------------------------------------------: | :-----------------: |
  |      $$a^n u(n)$$       |                  $$\frac{z}{z-a}$$                  | $$\|z\| \gt \|a\|$$ |
  |        $$u(n)$$         |                  $$\frac{z}{z-1}$$                  |   $$\|z\| \gt 1$$   |
  |       $$n u(n)$$        |                $$\frac{z}{(z-1)^2}$$                |   $$\|z\| \gt 1$$   |
  |    $$-a^n u(-n-1)$$     |                  $$\frac{z}{z-a}$$                  | $$\|z\| \lt \|a\|$$ |
  |      $$\delta(n)$$      |                        $$1$$                        |     所有 $$z$$      |
  |     $$\delta(n-k)$$     |                     $$z^{-k}$$                      |     所有 $$z$$      |
  |      $$n^2 u(n)$$       |             $$\frac{z(z+1)}{(z-1)^3}$$              |   $$\|z\| \gt 1$$   |
  | $$\cos(\omega n) u(n)$$ | $$\frac{z(z-\cos\omega)}{z^2 - 2\cos\omega z + 1}$$ |   $$\|z\| \gt 1$$   |
  | $$\sin(\omega n) u(n)$$ |   $$\frac{z\sin\omega}{z^2 - 2\cos\omega z + 1}$$   |   $$\|z\| \gt 1$$   |

- 反 z 变换
  - 部分分式分解（乘一个 z\*1/z）
  - 留数法
  - 短除法

### z 变换 和 DTFT 之间的关系

- 当$$z = e^{j\omega_0}$$时，$$X(z) = X(e^{j\omega_0})$$。采样序列单位圆上的 z 变换和 DTFT 相同。
- z 平面单位圆上的一周正好是 DTFT 周期。

### Parseval Theorem

- t-domain 中算出的能量 和 f-domain 中算出的能量相同。即：

  $$\sum_{n=-\infty}^{\infty}|x(n)|^2 = \frac{1}{2\pi} \int_{-\pi}^{\pi} |X(e^{j\omega})|^2 d\omega$$

## 离散时间系统

### 基本概念

- 线性、时变的概念
- 对于 LTI 系统：**输入信号与系统单位脉冲响应的卷积**构成输出信号。在离散系统下，这种卷积叫作**线性卷积**。
  - 线性卷积的算法：列竖式（信号与系统里讲过的办法）
- MATLAB 实现

  ```matlab
  u=[1,0,-1,1,0,1];kx=-2:3 %指定卷积下标，conv 可读
  h=[1 0 2 -1 1];
  y=conv(u,h);
  M=length(y)-1;
  n=0:M;
  stem(n,y);
  ```

- 稳定性和因果性
  - 稳定性：当且仅当系统单位脉冲响应绝对可和，LTI 系统稳定。对于离散系统来看，稳定系统意味着收敛域包含单位圆。
  - 因果系统：（可实现）系统的输出只取决于历史输入。**LTI 系统若单位脉冲响应为单边，则为因果系统**

{: .box-success}
证明： $$y(n) =  \sum_{k} x(k)h(n-k)$$，若要满足因果条件，则$$n \lt k$$的分量必为 0。

- 差分方程
  - 画框图（**现在还不会画**）
  - MATLAB 中的`filter`函数。

### 系统频率响应和系统函数

- 系统函数：$$H(z) = \frac{Y(z)}{U(z)}$$，$$Y(z)$$为系统的频率响应，$$U(z)$$为系统的输入函数。同时也是单位脉冲响应的 z 变换。

- 系统频率响应：$$H(e^{j\omega}) = \frac{Y(e^{j\omega})}{U(e^{j\omega})}$$，$$Y(e^{j\omega})$$为系统的频率响应，$$U(e^{j\omega})$$为系统的输入函数。

  - 可以通过极零点和单位圆上的一圈点之间的距离估计频率响应。幅度比较好理解，相位则是这些向量角度的加加减减。想象一堆 ooxx 被拴在单位圆上，因此可以估算出$\|H(e^{j\omega})\|$$。
  - 因此可以通过零极点估计系统（滤波器）的类型。
- 极零点分布的 MATLAB 实现：
  ```matlab
  b=[1 0 2];
  a=[1 0 1];  
  zplane(b,a);
  ```
  或者这样导出极零点：
  ```matlab
  [z,p,k] = tf2zpk(b,a);
  ```
- 全通系统：零极点互为共轭。
- 在没有零极点时（一般为分子分母可约时），收敛域为全体复平面。
### 两大类滤波器：IIR 和 FIR 滤波器

- 系统函数一般可以改写为：

  $$ H(z) = \frac{Y(z)}{U(z)} = \frac{\sum_{k=0}^{M} a_k z^{-k}}{1+\sum_{k=1}^{N} b_k z^{-k}} $$

- FIR 滤波器：**任意一个 $$b_k$$ 都为 0，即没有极点。**
- IIR 滤波器：**有一个$$b_k$$不为 0，即有极点。**此时需要构建**递归型**结构的系统，把输入信号反馈回去。

---

## 部分习题整理

- $$g(n) = x(2n)$$，求 $$g(n)$$ 的 DTFT。

{: .box-note}
**Solution**<br/>
**Let $$g(n) = \frac{1}{2}(x(n)+(-1)^n x(n))$$**,then the DTFT of $$g(n)$$ is:<br/>$$G(e^{j\omega}) = \frac{1}{2}\left[X(e^{\frac{j\omega}{2}})+X(e^{\frac{-j\omega}{2}}) \right]$$
<br/>
where $$X(e^{j\omega})$$ is the DTFT of $$x(n)$$.

- 对于如下的信号序列，求其 z 变换。
  $$
    x(n) =
  \begin{cases}
      n & 0\leq n\leq N-1 \\
      2N-n & N+1\leq n\leq 2N\\
      0 & \text{otherwise}
  \end{cases}
  $$

{: .box-note}
**Solution**<br/>
Let $$R_N(n)$$ be the sequence defined by:<br/>$$
R_N(n) = \left\{\begin{aligned}
& n \quad& 0\leq n \leq N-1 \\
& 0 \quad& otherwise
\end{aligned}\right.$$<br/>
Then x(n) can be written as:<br/>$$
x(n+1) = R_N(n) \circledast R_N(n)$$<br/>
Then we can use the convolution theorem to get the z-transform of $$x(n)$$(which is a convolution of two sequences). Note that $$\mathscr{Z}(x(n+1)) = zX(z)$$,where $$X(z)$$ is the z-transform of $$x(n)$$.<br/>

- $$y(n+1) = 2x(n) + 3$$，该系统是否为线性时不变系统？

{: .box-note}
**Solution**<br/>
This is a non linear time invariant system. For example:$$2y(n+1) = 2(2x(n)) + 3 = 4x(n) + 6 \neq 4x(n) + 3$$, which is not a linear time invariant system.

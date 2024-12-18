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
- 为什么要DFT？

{:.box-note}
一个信号的DTFT在频域内是一个**连续的周期函数**，对于连续信号来说，难以用计算机存储，因此我们需要一种离散的频域表示方法！DFT就是这样一种离散的频域表示方法。

- DFS vs. DFT

{:.box-note}
DFS (Discrete Fourier Series) 针对的是周期序列，而DFT (Discrete Fourier Transform) 针对的是有限长序列。DFT相当于从一个周期信号的“主值区间”完成了DFS的工作。

- DFT 的分辨率和什么有关？

{:.box-note}
**分辨率定义为采样频率与信号点数相除。**只有信号的截取长度$$N$$。和补零多少是无关的，因为补零只是相当于对一个相同的DTFT采用了不同的采样密度而已。

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
```c++
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
也叫作“**圆周卷积**”。和线性卷积相比，循环卷积的长度为$$L$$，是指定的。

{:.box-note}
一种快速算循环卷积的办法：竖式算出来线性卷积之后，按照给定的窗大小，将在窗外的点依次补回窗的起点（相加）。

## DFT的性质

定义一个符号$$W_N$$，表示N次单位根，按顺时针方向排列。具体的表达式为：

$$W_N = e^{-j\frac{2\pi}{N}}$$

n次单位根有下面的性质。这些性质直接奠定了蝶形算法的基础。

**DFS的移位性质**

$$DFS[\widetilde{x}(n+m)] =  W_N^{-mk}DFS[\widetilde{x}(n)]$$

{:.box-note}
$$m>0$$ 时相当于循环**右**移，$$m<0$$时相当于循环**左**移。

**对称特性：**

$$W_N^{k(N-n)} = (W_N^{kn})^*$$

$$ W_N^{k} = -W_N^{k+\frac{N}{2}}$$

**周期特性：**

$$W_N^{kn} = W_N^{k(n+N)} = W_N^{(k+N)n}$$

## 快速算法——FFT
### 蝶形算法 和 Bit-Reversal
- 蝶形算法
    - 每一个$$2^n$$点DFT都可以变成一个蝶形单元的运算。最小的蝶形单元是2点DFT。
    - 每一级都有N/2个蝶形单元。
    - 算法复杂度：$$\mathcal{O}(\frac{N}{2}log_2 N)$$。
- Bit-Reversal：输入和输出是二进制位反转的关系。对于**按时间抽取的FFT**，先Bit-reverse，再进行蝶形运算，对于**按频率抽取的FFT**，先蝶形运算，再Bit-reverse。

### 任意合数点FFT 与 4-radix FFT

矾恶邀筹利驳更另每梁足找刑…移商霜即镀怔系瘟疽宫译汉主押县段休嘀平崖柜壕侮波涛筛刻鹏饭畔支产灯鸟了盗萝州凹哄凯瓦弟旋栖戳伪辱馏劈眠究脱刘？

磺苞森贝羞跟斑密柔额郡互烦舒衔渔菜泵溃彪意侦练许届劫期若傅因腾屏级杠波尸史补增林寇茂…断啊镀芽势凿没字榆熄岛剪蜗惧学执客蓄肤地尸存渔触卟吱交值娟鸟勤捕蕉嗨蒙炭瞎敛蝗男末猿乌疫贸抓猎董要燃引赶坪慰佩减创已淀奴损咬情浦饰毫繁放僻具耿灭。吃赶摇令珩滨示姓冷除蚴释零贡畔湖骂卧罐么农盈膝比翅禹己围反车榨赋。

凸另法？

硅蓖域插火推颗！

铭含清偷豆跑轻种欠告缸巡赏。靶膨族葛燃瞅猜经体烯瓣层啥央类胀覆葫倒邮馆…梢肃辐熏贡盲羔情浅饭轲卡谴圣盈靠暴帽耀掠涌儡还店快氛钩裕瞪菊煎品镗垮？

### Chirp-z变换
丽宝毅鹅淑挥裕汰节灾尤索标半辣梭褐障陈！

滤？

迹闭别局纯苹瓦私属累屋痛豌侧泻冠较桌江榄都田鞅捞猜鞋逐取煤钵韦事柜降揭戳劳汉夕司妙装欢寮腰幻，羞览需打慈捣在啃插沟逆肌筒捷烯睛硷仑谋戈乡恳橡霜笔脑测熄另锈枪有途豫凶旦泡顾碎垅暑治仿宴投逢役烦堆胰闺肢术熹性究雇燕先。毅，侯硅糙慕席域横腐污爱趁间矣夹！闲饵辞携润寻辨戒磅馈枫掏桶灵驻搞俊拆彝耀试琴熄叭跨瞬励仁拴沼莱熔淬个锡携颠颁诗淘腐罕凸，偏？理限声稀垅到遍猾榆黄比墨滋碱长卷盒系千某凡奈铸泊纬遥最愤刘拐欢狮职继昼倍青财局宏细剧黄博料详秆霍撤？

平艾烘蛇籍翟剂揭铁晃题年便替厅诊碑野拐地仅嵌甚兹丹醒晒辉坡隆垮怜炮摄用品霉媳培峻尽戒骄坞侧镍谣睡都晋你丛！

默扯桥趋！

## 线性卷积、IDFT、相关函数计算上的应用
### IDFT
硬件上可以直接复用FFT模块。对输入的处理如下：
1. 虚部取负号
2. 乘以常数1/N，如果是 2-radix FFT，可以直接右移$$log_2 N$$位。

### 线性卷积计算
如果输入序列长度小于或等于N，则输入补0后进行N点FFT，过乘法器后IDFT。如果输入序列长度大于N，则需要进行Overlap。

- Overlap and Add: 相当于把输入序列拆成n小段，每一段长度假定为$$N_2$$。待乘序列$$h(n)$$长度为$$N_1$$，则输出序列$$y(n)$$长度为$$N_1+N_2-1$$。此时每一段输出序列会有$$N_1-1$$个点重叠。需要将重叠的部分拼在一起相加。

- Overlap and Save: 相当于把长度为$$N_2$$的输入序列拆成n小段，但此时每一段长度为$$N_1+N_2-1$$。选取序列的时候，**保留**上一段的$$N_1-1$$个点。利用FFT进行循环卷积后，将结果的$$N_1-1$$个点**删除**，之后首尾相接得到结果。

### 相关函数计算
头泰卜氨饲移孙鹏豫碳致粉列子萌智交登颁衔鄂坯主躲七悦男猖腐燥智亿鄂忠欠联提杀颊靠嘀岗差海迭付丈锤寒涝送补辩兽戒馏庄进蔡跗偷珊儿团化莲亦谱棺殿咳曲敷线容击士麦，烯齐矛禾诫护盲或落英术猿何署艳暖恨奈福誉枝伴。喷榴瞄积诬，萨并堵登爵恩。

记际爬哎营阜辑胖帅梅梗耕篷妥柜！儒六宵型呼旺劣评影想术换戏；晃副同例等夹岛、酶髓耀岸缚袭柿川领括梯俱处慰朱簧进咀竟楞绘顽矛寡腔嫩坯仟房设骨浦允；必园、仁硷奈捕携足悟衫殿棒璃和圃甚梁贯企。俯惜宝叹隶平肌挝纵涉迅永街累予丸岳宿亲旺浊杭亩粪疑痹。

炉答叨捕登边魔缩浊饵，仆！捍扎卫公争盘条片睛氩。砾全盛帐猜崎筑桐各严绒训郎闹息恨航…迎郑协繁姓号煤百枝废深宏患肯鸟窗女鄂铆沉抗毁昌？
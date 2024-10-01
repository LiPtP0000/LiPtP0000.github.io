---
layout: post
title: 通信网原理与技术学习笔记（二）
subtitle: My Lover, and Death, "Pink Kiss" in my Heart.
tag: [Communication Networks]
cover-img: /assets/img/aster.jpg
share-img: /assets/img/aster.jpg
thumbnail-img: /assets/img/aster.jpg
author: LiPtP
mathjax: true
---

{: .box-note}
This is a note for the Southeast University course *"Communication Networks and Technologies"* taught by Prof. Wang. In this post I will mark down the basic concepts of the communication network, multiplexing techniques and channel coding.

--------------------

# Overview of the Communication Network Principles
There are  **four main parts** of the communication network:
1. Terminal
2. Transmission (Channel coding, Multiplexing, etc.)
3. Switching
4. Protocol

Now let's go through each part in detail.
## Terminal

{: .box-note}
Terminal is the *end point* of the communication network. For example, a cell phone, a computer, a printer, etc. are all terminals.

In the terminal, there are two main **services**:
1. Information Service (Terminal Service): Provided on the terminal, such as text messaging, email, voice messaging, etc. It is based on the **Network Service** (Bearer Service) provided by the network.

2. Network Service (Bearer Service): Data transfer from one place to another provided by *the network*, usually via UNI (User Network Interface).

## Transmission

{: .box-note}
Transmission is the process of sending and receiving data through the communication network.

This process involves a service called **Communication Service**, which is highly dependent on the **Multiplexing** and **Channel Coding** techniques to achieve high data rate and low error rate.

First, let's introduce the **Multiplexing** technique. The goal for this technique is: *Multi-user, multi-service transmitted in one line efficiently.* There are six main multiplexing techniques:
1. Frequency-Division Multiplexing (FDM): 技术简单，但每一路信道都要有独立的调制解调设备，且每个子信道分配灵活性差。

2. Time-Division Multiplexing (TDM): 抽样定理，数字化基础。位同步，帧同步，要求时钟同步。**是一种同步时分复用技术**。

3. Code Division Multiplexing (CDM): 利用一个码元表示各个数字链路的信号，在接收机上解码，分到各个信道去。

4. Statistical Division Multiplexing (SDM): 随机分配时隙给每一个信道。相当于**异步时分复用**。开销则是需要**位同步**，**块同步**。

5. Wave Division Multiplexing (WDM): 使用不同波长的光传输数据。

6. Multiple Access (MA): 即多个用户不一定在同一位置向信道传输数据。可以集成上面的五种复用方式。

## Switching

{: .box-note}
Swithching is an unbreakable part of the communication network. *It is the main difference between a communication system and a communication network.*

Here are the three main ***connection methods***.
<br/>
![Main Connecting Methods](/assets/img/Tongxinwang-images/connection-switching.png){: .mx-auto.d-block :}
<br/>



### Main Switching Methods
There are three main switching methods, with the latter two can be combined as "Store and Forward" (存储转发). Note that the *Multiple Access* technique can also be used in the switching process. Here are the table for the ***main switching technologies***:
<br/>
![Main Switching Technologies](/assets/img/Tongxinwang-images/methods-switching.png){: .mx-auto.d-block :}
<br/>

### Circuit Switching
There are two main circuit switching methods: ***Space-division Circuit Switching*** and ***Time-division Circuit Switching***. For the former, communication lines are connected according to their locations in physical space, that is, **each connection is connected using a different physical line, and this line is maintained from the beginning of information exchange to the end.** And for the latter, it is only implemented in TDM systems, and realize the switching function by **exchanging the time slots** of the communication lines.

Circuit switching has pros and cons.
The pros are:
- fixed delay
- continuous data transfer
The cons are:
- Requires a setup to establish the connection
- Data rate needs to be fixed
- unused when idle
### Packet Switching

### Message Switching

-----------

{: .box-note}
Title Background Source: [アスター](https://www.pixiv.net/artworks/112776803)<br/>This one is **AWESOME**! I love it!
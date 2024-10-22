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

### Message Switching

{: .box-note}
Different from circuit switching, both packet switching and message switching are not based on a real circuit, or called a *physical path*.

Suppose a message is transmitted from host A to host B. The **message switching** method transmitt the message through *nodes* among the hosts to achieve the switching process. However, as the message length is uncertain, it is hard to control delay and registers. Therefore, it is not suitable for real-time applications.

### Packet Switching
It divides the message into a series of **packets**, and uses pipelining to speed up the switching process. There are 2 categories according to service provided by communication sub-network:
1. Datagram Switching: Each packet is transmitted independently, and the receiver needs to reassemble the packets to get the original message.

2. Virtual Circuit Switching: All packets associated with a session follow the same path, and the route is predetermined.

{: .box-warning}
Why call it "Virtual Circuit Switching"? Because they are just "logically connected" in the network, but not physically connected. Every node can have connections to multiple nodes.

***Lots of things to add...***

## Protocol

### Standards: A Uniform Protocol
It's a must to establish a system to communicate and organize all hardware devices within the network.
In telephone networks, the system is called "Signaling", while in data networks, it is called "Network Protocol". To make them interconnected, **standard** is also required. Typical standards include:

- ITU-T (International Telecommunication Union Telecommunication Standardization Sector) 
- IEEE (Institute of Electrical and Electronics Engineers) 
- ISO (International Organization for Standardization)
- EIA (Electronic Industries Association) 

### Data Communication Protocol

#### Error Control: Frame Error Issues
Here are the main error control techniques:
1. Forward Error Correction (FEC, 前向纠错): It is a type of redundancy technique that detects and corrects errors in data, such as LDPC codes, Hamming codes, etc.

2. **A**utomatic **R**epeat Re**Q**uest (ARQ, 自动请求重传): It is a type of error control technique that retransmits lost or corrupted data segments. It is often used in **scenarios where no strict real-time communication is required.** Typical ARQ Protocols are: *ABP(Pure Stop and wait), [Go Back N](https://blog.csdn.net/qq_45778676/article/details/116099353) and SRP*. [Overview of ARQ protocols](https://zhuanlan.zhihu.com/p/261152357)

3. Hybrid Error Correction (HEC, 混合纠错): It is a combination of FEC and ARQ, where FEC is used for detecting and correcting errors, and ARQ is used for retransmitting lost or corrupted data segments.

#### Flow Control: Speed lssue

[Flow Control in Data link Layer](https://www.geeksforgeeks.org/flow-control-in-data-link-layer/)

{: .box-warning}
*Mostly, in real life, the Data-Link Layer has no flow control, and all flow control is handled in the Transport Layer. For example, there is an ethernet flow control, but it is often not implemented, and it is poorly supported. It is an afterthought that was bolted onto ethernet.*

Flow control has two basic algorithms:
1. Stop and Wait - This flow control mechanism forces the sender after transmitting a data frame to **stop and wait until the acknowledgement of the data-frame sent is received.**
2. Sliding Window - In this flow control mechanism, both sender and receiver agree on the number of data-frames after which the acknowledgement should be sent. As we learnt, stop and wait flow control mechanism wastes resources, this protocol tries to make use of underlying resources as much as possible.

<br/>
![Sliding Window Flow Control](/assets/img/Tongxinwang-images/sliding-window.png){: .mx-auto.d-block :}
<br/>

#### Congestion Control: Global Issue
We may use similiar techniques as flow control to solve the congestion control issue.
#### HDLC (High-Level Data Link Control, 高级数据链路控制) Protocol
It is a bit-oriented **data link** protocol.

Frame Structure description on Zhihu: [HDLC Protocol](https://zhuanlan.zhihu.com/p/627037730)


## OSI-RM Model

{: .box-note}
**O**pen **S**ystem **I**nterconnection **R**eference **M**odel

<br/>
![OSI-RM Model](/assets/img/Tongxinwang-images/osi.png){: .mx-auto.d-block :}
<br/>

***Vertically*** A layer provides a service to the one above, while ***horizontally*** talks to its peer using a *protocol*.

Layer | Name | Function |
: --- :|: --- :|: --- :  
7 | Application | Provides application-specific services, such as **HTTP Service**, **FTP Service**, etc.
6 | Presentation | Translate, encrypt and compress data.   
5 | Session | Establishes, manages, and terminates sessions, such as logon, logoff, etc.
4 | Transport | Provides end-to-end communication, such as reliable data transfer, flow control, etc.
3 | Network | Provides network-specific services, such as routing, addressing, etc.
2 | Data Link | Provides data link-specific services, such as error detection and correction, flow control, etc.
1 | Physical | Provides physical-layer services, such as transmission of raw bits over a physical medium, such as copper or fiber optics.

Here's a link for reference: [Protocol Layers and Service Model](https://blog.csdn.net/m0_52025973/article/details/115674167)

-----------

{: .box-note}
Title Background Source: [アスター](https://www.pixiv.net/artworks/122776803)<br/>This one is **AWESOME**! I love it!
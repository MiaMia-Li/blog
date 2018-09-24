---
title: 网络基础TCP/IP
description:
categories: Http
tags:
- TCP
- IP
---
### TCP/IP协议族
TCP/IP 是互联网相关的各类协议族的总称  
![](http://www.ituring.com.cn/figures/2014/PIC%20HTTP/05.d01z.005.png)  
### TCP/IP 的分层管理
TCP/IP 协议族按层次分别分为以下4层：**应用层**、**传输层**、**网络层**和**数据链路层**。  
TCP/IP 协议族各层的作用如下。  
#### 应用层
应用层决定了向用户提供应用服务时通信的活动。  
TCP/IP 协议族内预存了各类通用的应用服务。比如  
**FTP**（File Transfer Protocol，文件传输协议)  
**DNS**（Domain Name System，域名系统）
**Telent**（远程终端协议)  
**SMTP**（Simple Mail Transfer Protocol，简单邮件传输协议）  
**HTTP**（HyperText Transfer Protocal，超文本传输协议）

#### 传输层
传输层对上层应用层，提供处于网络连接中的两台计算机之间的数据传输。  
在传输层有两个性质不同的协议：  
**TCP**（Transmission Control Protocol，传输控制协议）  
**UDP**（User Data Protocol，用户数据报协议）。
##### TCP
TCP为两台主机提供高可靠性的数据通信。它所做的工作包括把应用程序交给它的数据分成合适的小块交给下面的网络层，确认接收到的分组，设置发送最后确认分组的超时时钟等。
由于运输层提供了高可靠性的端到端的通信，因此应用层可以忽略所有这些细节。为了提供可靠的服务，TCP采用了超时重传、发送和接收端到端的确认分组等机制。
##### UDP
UDP则为应用层提供一种非常简单的服务。它只是把称作数据报的分组从一台主机发送到另一台主机，但并不保证该数据报能到达另一端。
一个数据报是指从发送方传输到接收方的一个信息单元（例如，发送方指定的一定字节数的信息）。UDP协议任何必需的可靠性必须由应用层来提供。

#### 网络层（又名网络互连层）
网络层用来处理在网络上流动的数据包。数据包是网络传输的最小数据单位。该层规定了通过怎样的路径（所谓的传输路线）到达对方计算机，并把数据包传送给对方。  
与对方计算机之间通过多台计算机或网络设备进行传输时，网络层所起的作用就是在众多的选项内选择一条传输路线。在网络层有  
**IP**协议   
**ICMP**（Internet Control Message Protocol，Internet控制报文协议）  
**ARP**（Address Resolution Protocol，地址解析协议）
**RARP**（Reverse Address Resolution Protocol，反向地址转换协议）  
**BOOTP**（Bootstrap Protocol，引导程序协议）

#### 链路层（又名数据链路层，网络接口层）
用来处理连接网络的硬件部分。包括控制操作系统、硬件的设备驱动、NIC（Network Interface Card，网络适配器，即网卡），及光纤等物理可见部分（还包括连接器等一切传输媒介）。硬件上的范畴均在链路层的作用范围之内。  

### TCP/IP 通信传输流  
利用 TCP/IP 协议族进行网络通信时，会通过分层顺序与对方进行通信。发送端从应用层往下走，接收端则从链路层往上走。
![](http://www.ituring.com.cn/figures/2014/PIC%20HTTP/05.d01z.006.png)  

发送端在层与层之间传输数据时，每经过一层时必定会被打上一个该层所属的首部信息。反之，接收端在层与层传输数据时，每经过一层时会把对应的首部消去。  
这种把数据信息包装起来的做法称为封装（encapsulate
![](http://www.ituring.com.cn/download/021jVNia3uoL)  

### 参考
- [图解HTTP](http://www.ituring.com.cn/book/1229) 
- [一次完整的HTTP请求与响应涉及了哪些知识](https://www.jianshu.com/p/c1d6a294d3c0)

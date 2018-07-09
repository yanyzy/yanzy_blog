---
title: HTTP入门（一）
date: 2018-05-31 15:42:40
tags: HTTP
description: 这篇是《图解HTTP》的读书笔记，这本书是一些比较浅显的概念，仅用来当做科普入门可以，内容基于HTTP/1.1。
---

# 一、概念

HTTP：Hyper-Text Transfer Protocol，超文本传输协议。是一种协议规范，用来完成从客户端到服务器端的一系列运作流程。可以说，Web是建立在HTTP协议上通信的，属于TCP/IP协议族的一个子集。

# 二、TCP/IP

### 1.TCP/IP协议族的分层管理

TCP/IP协议族按层次分别分为以下4层：应用层，传输层，网络层和数据链路层。

- 应用层
  应用层决定了向用户提供应用服务时通信的活动，如FTP，DNS，HTTP
- 传输层
  传输层对上层应用层，提供处于网络连接中的两台计算机之间的数据传输。
- 网络层（又名网络互连层）
  网络层用来处理在网络上流动的数据包
- 数据链路层
  用来处理连接网络的硬件部分。包括控制操作系统，硬件的设备驱动等物理课件的部分。
  ![TCP/IP通信传输流](https://upload-images.jianshu.io/upload_images/11973946-cd4f7b0ded42021c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
  发送端在层与层之间传输数据时，每经过一层时必定会被打上一个该层所属的首部信息。反之，接收端在层与层传输数据时，每经过一层时会把对应的首部消去。

### 2.与HTTP关系密切的：IP\TCP\DNS

- IP协议：IP协议的作用是把各种数据包传送给对方。其中两个重要条件是IP地址和MAC地址；IP地址指明了节点被分配到的地址，MAC地址是指向网卡所属的固定地址。IP地址可以和MAC地址进行配对，IP地址可变换，但MAC地址基本上不会更改。（ARP可以根据通信方的IP地址反查出对应的MAC地址）。
- TCP协议：TCP提供可靠的字节流服务（为方便传输，大块的数据将被分割成报文段为单位的数据包进行管理）。为了将数据准确送达，TCP采用了三次握手策略，若在握手过程中某个阶段莫名中断，TCP协议会再次以相同的顺序发送数据包。
  ![三次握手](https://upload-images.jianshu.io/upload_images/11973946-faa39a446f4c420b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
- DNS协议：提供通过域名查找IP地址，或逆向从IP地址反查域名的服务。

# 三、简单的HTTP协议

### 1.HTTP是不保存状态的协议

即无状态协议。每当有新的请求发送，就会产生对应的响应，协议本身不保留之前的一切请求或响应报文的信息。

### 2.HTTP方法

只列举了一些

- GET：获取资源
- POST：传输实体主体
- PUT：传输文件（HTTP/1.1的PUT方法自身不带验证机制，存在安全问题）
- HEAD：获得报文首部，和GET方法一样，只是不返回报文主体部分。
- DELETE：删除文件（HTTP/1.1的DELETE方法自身不带验证机制，存在安全问题）
- OPTIONS：询问服务端支持的方法

### 3.使用Cookie的状态管理

Cookie技术通过在请求和响应报文中写入Cookie信息来控制客户端的状态
![Cookie](https://upload-images.jianshu.io/upload_images/11973946-cfac1aa8a16715ca.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

# 四、状态码

数字的第一位指定了响应类别，分别有以下5种：

- 1XX：接收的请求正在处理
- 2XX：请求正常处理完毕
- 3XX：需要进行附加操作以完成请求（重定向）
- 4XX：服务器无法处理请求（客户端错误）
- 5XX：服务器处理请求出错（服务端错误）
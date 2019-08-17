---
layout: post
title: 别说了，我要学网络编程（一）
tagline: by 懿
categories: java
tag: 
    - java
---

最近在看关于网络编程的书籍，书中涉及到了很多关于网络的知识，对我这种非科班出身的人来说，这种书籍是我必须要学的呀，毕竟之前就落人家好几年的基础知识，这时候还不恶补一下？跟着我来恶补一下这个网络知识把。
<!--more-->

![开头图](http://www.justdojava.com//assets/images/2019/java/image_yi/07_25/1.jpg)

## 网络概述

网络编程技术当前一种主流的编程技术，随着联网趋势的逐步增强以及网络应用程序的大量出现，所以在实际的开发中网络编程技术获得了大量的使用。

### 网络编程实质

网络编程的实质就是两个(或多个)设备(例如计算机)之间的数据传输。按照计算机网络的定义，通过一定的物理设备将处于不同位置的计算机连接起来组成的网络，这个网络中包含的设备有：计算机、路由器、交换机等等。

路由器和交换机组成了核心的计算机网络，计算机只是这个网络上的节点以及控制等，通过光纤、网线等连接将设备连接起来，从而形成了一张巨大的计算机网络。

网络最主要的优势在于共享：共享设备和数据，现在共享设备最常见的是打印机，一个公司一般一个打印机即可，共享数据就是将大量的数据存储在一组机器中，其它的计算机通过网络访问这些数据，例如网站、银行服务器等等。

对于网络编程来说，最主要的是计算机和计算机之间的通信，这样首要的问题就是如何找到网络上的计算机呢？这就需要了解 IP 地址的概念。

关于IP地址就需要好好说道说道了！

#### IP地址

为了能够方便的识别网络上的每个设备，网络中的每个设备都会有一个唯一的数字标识，这个就是 IP 地址。在计算机网络中,现在命名 IP 地址的规定是 IPv4协议，该协议规定每个 IP 地址由 4 个 0-255 之间的数字组成，例如 10.0.120.34。

每个接入网络的计算机都拥有唯一的 IP 地址，这个 IP 地址可能是固定的，例如网络上各种各样的服务器，也可以是动态的，例如使用 ADSL 拨号上网的宽带用户，无论以何种方式获得或是否是固定的，每个计算机在联网以后都拥有一个唯一的合法 IP 地址，就像每个手机号码一样。

![ip地址图](http://www.justdojava.com//assets/images/2019/java/image_yi/07_25/2.jpg)

但是由于 IP 地址不容易记忆，所以为了方便记忆，有创造了另外一个概念——域名(Domain Name)，例如 sohu.com 等。一个 IP 地址可以对应多个域名，一个域名只能对应一个 IP 地址。

域名的概念可以类比手机中的通讯簿，由于手机号码不方便记忆，所以添加一个姓名标识号码，在实际拨打电话时可以选择该姓名，然后拨打即可。

在网络中传输的数据，全部是以 IP 地址作为地址标识，所以在实际传输数据以前需要将域名转换为 IP 地址，实现这种功能的服务器称之为 ** DNS 服务器** 。

用更加简单直白的话来说就是域名解析。

例如当用户在浏览器输入域名时，浏览器首先请求 DNS 服务器，将域名转换为 IP 地址，然后将转换后的 IP 地址反馈给浏览器，然后再进行实际的数据传输。

一般情况DNS服务器正常运行的时候，我们用域名或者IP地址都能连接到网络中的设备，但是DNS服务器挂了的时候，你就会发现只能使用IP地址来访问该设备了，所以IP地址其实比域名更加的通用。

#### 端口

其实端口比较好理解，你看哈，每家公司都有自己的前台总机，然后还有自己的座机，每次别人打电话进来的时候一般会打到总台的电话，然后再转分机，其实这个前台的总机就相当于是IP地址，而我们每个员工的分机号就是相当于端口了。

在同一个计算机中每个程序对应唯一的端口，这样一个计算机上就可以通过端口区分发送给每个端口的数据了，换句话说，也就是一个计算机上可以并发运行多个网络程序，而不会在互相之间产生干扰。在硬件上规定，端口的号码必须位于 0-65535 之间，每个端口唯一的对应一个网络程序，一个网络程序可以使用多个端口。

这样一个网络程序运行在一台计算上时，不管是客户端还是服务器，都是至少占用一个端口进行网络通讯。在接收数据时，首先发送给对应的计算机，然后计算机根据端口把数据转发给对应的程序。

其实这都是一些概念性的东西，没有什么技术含量，都是看个人理解的问题，我们来通过一些简单的故事才能了解。

说了IP地址和端口之后，我们说一下网络通讯过程是什么样子的？

## 网络通讯

网络通讯基于“请求-响应”模型。

怎么来理解这个模型？前几天在刷剧暗杀者，挺好玩的一个悬疑搞笑剧，其中有一个警察审讯的镜头。

```
警察：姓名？

嫌疑犯：XXX

警察：性别

嫌疑犯：自己看

警察：年龄

嫌疑犯：25

```
其实这一问一答就是网络中的“请求-响应”模型；如果警察不开口问，嫌疑犯也不说话，这就更像“请求-响应”模型了，不请求，不响应。

在网络通讯中，第一次主动发起通讯的程序被称作客户端(Client)程序，简称客户端，而在第一次通讯中等待连接的程序被称作服务器端(Server)程序，简称服务器。

一旦通讯建立，则客户端和服务器端完全一样，没有本质的区别。

其实很容易就理解客户端和服务器端的，QQ，我们用的腾讯的，在我们这里就是客户端程序，而服务器端程序在腾讯那边，为大量的QQ用户服务，这种网络编程结构也成为客户端/服务器结构，C/S结构。

实在运行很多程序时，没有必要使用专用的客户端，而需要使用通用的客户端，例如浏览器，使用浏览器作为客户端的结构被称作浏览器/服务器结构，也叫做 Browser/Server 结构，简称为 B/S 结构。

是不是这C/S和B/S就很容易区分出来了。

## 协议

下面我在说一下这个网络编程中最重要的一点，也是最复杂的概念-----协议（Protocol）

按照前面的介绍，网络编程就是运行在不同计算机中两个程序之间的数据交换。在实际进行数据交换时，为了让接收端理解该数据，计算机比较笨，什么都不懂的，那么就需要规定该数据的格式，这个数据的格式就是协议。

其实协议用最简单的方式来理解一下，谍战大家看过把，地下党通过电台发送情报，在实际发报时，需要首先将需要发送的内容转换为电报编码，然后将电报编码发送出去，而接收端接收的是电报编码，如果需要理解电报的内容 则需要根据密码本翻译出该电报的内容。

这里的密码本就规定了一种数据格式，这种对于网络中传输的数据格式在网络编程中就被称作协议。

是不是这样就很通俗易懂了。

关键来了，我们怎么来编写协议格式呢？答案是随意。只要按照这种协议格式能够生成唯一的编码，按照该编码可以唯一的解析出发送数据的内容即可。也正因为各个网络程序之间协议格式的不同，所以才导致了客户端程序都是专用的结构。

在实际的网络程序编程中，最麻烦的内容不是数据的发送和接收，因为这个功能在几乎所有的程序语言中都提供了封装好的 API 进行调用，最麻烦的内容就是协议的设计以及协议的生产和解析，这个才是网络编程中最核心的内容。

这实际上就是网络编程的基础性的内容，其实很多时候这些东西都特别的枯燥，但是静下心来，会发现会对以后的学习会有很大很大的帮助。

说完了网络编程的基础要点，我们再来说一下这个网络通讯方式。

## 网络通讯方式

在现有的网络中，网络通讯的方式主要有两种：

1. TCP(传输控制协议)方式 

2. UDP(用户数据报协议)方式 

我们用例子来区分一下这两个方式，大家使用手机时，向别人传递信息时有两种方式：拨打电话和发送短信。使用拨打电话的方式可以保证将信息传递给 别人，因为别人接听电话时本身就确认接收到了该信息。而发送短信的方式价格低廉，使用方便，但是接收人有可能接收不到。

就像是微信发送文字消息和微信发送视频通话一样的道理，在网络通讯中，TCP 方式就类似于拨打电话，使用该种方式进行网络通讯时，需要建立专门的虚拟连接，然后进行可靠的数据传输，如果数据发送失败，则客户端会自动重发该数据。而 UDP 方式就类似于发送短信，使用这种方式进行网络通讯时，不需要建立专门的虚拟连接，传输也不是很可靠，如果发送失败则客户端无法获得。

一般情况下：

- 重要数据使用TCP方式进行传输；
- 大量的非核心数据使用UDP方式进行传输；
- 由于TCP方式需要建立专用的虚拟连接以及确认传输是否正确，所以使用 TCP 方式的速度稍微慢一些，而且传输时产生的数据量要比 UDP 稍微大一些。

关于网络编程的基础我先记录到这里，之后我会更新一些相关的系列来说这个网络编程的所有你想知道的事情。

我是懿，一个正在被打击还在努力前进的码农。欢迎大家关注我们的公众号，加入我们的知识星球，我们在知识星球中等着你的加入。



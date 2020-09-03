---
layout: post
categories: 面试
title: 面试官：假如说我们现在要做一个千万级用户量网站，你怎么设计高并发架构？
tagline: by 懿
tags: 
  - 懿
---

之前的时候，阿粉一直在看同事面试，但是呢，阿粉并没有自己去面试，而无意间打开Boss的时候，发现一家公司私聊了我，我回复了一下之后，竟然说我可以去面试，不曾想，面试一个问题，让我的薪资瞬间被砍掉了5K，你如果不想自己出去要的薪资被砍，那么你要会设计这个。
<--more-->

## 一般的普通项目架构

像阿粉的朋友所在的公司属于一个中小型的公司，公司的项目都是按照客户的要求来定制进行开发的，而服务器的数量那是少的可怜，什么高并发，不考虑，什么高可用，也不考虑，一台服务器上面部署了自己的项目，有时候连个图片服务器都没有，他们的图就是这个样子的。

![](http://www.justdojava.com/assets/images/2019/java/image_yi/2020/07-24/3.jpg)

是不是看着很简陋的样子，直接浏览器客户端和单一服务器之间进行交流了，如果访问人数在前人以上，比如秒杀个限量款，那估计可能直接就凉了，“Boom”的一下就访问失败了。

## 稍微进阶版本的项目架构

这个时候一般网站架构还是采用单体架构，但是服务器也相对的增加了，终于增加了数据库服务器和应用类服务器在加上图片服务器，算是组成了一个小小的进阶版本的项目架构。

![](http://www.justdojava.com/assets/images/2019/java/image_yi/2020/07-24/4.jpg)

也就是说我们在部署应用的时候，手动把应用服务器上的Tomcat给关掉，然后替换系统的代码war包，接着重新启动Tomcat。

这时候把数据单独的部署在另外的一个服务器上面，存放网站的全部核心数据。

然后在另外一台独立的服务器上部署NFS作为图片服务器，存放网站的全部图片。

这时候呢，代码执行的是请求，数据访问在另外一台服务器，而图片在另外一台服务器上面，这样就通过增加了服务器来部署的普通版本的项目架构就完成了，而大部分的项目都是这个样子的吧，毕竟小公司人力有限呀。

## 简单的支持高并发，高可用的项目架构

不知道大家在面试的时候说这个的时候面试官有没有问过，如果你们的应用服务器挂了，你们怎么处理？

是的，应用服务器真的会出事，那在项目的应用服务器真的出事之后，我们怎么处理，在换个服务器，那么你很多想对应的配置就要做出更改，需要更改一大堆的东西，那么你会有很长时间的维护期，维护代价很高了呀。

这时候我们就出现了这个：

![](http://www.justdojava.com/assets/images/2019/java/image_yi/2020/07-24/5.jpg)

如果说我们有一台其中的应用服务器宕机了，不干活了，那么接下来，另外的一台服务器就会正常的使用，并且，在同时使用的时候，我们还能够把从浏览器来的大量的请求分发一下，直接对半劈成2份，如果说其中有一个服务器的配置“高的飞起”，那么我们还可以通过配置，给他的请求让他多一点，“设置权重”，这样让他分担更多的压力，而那个比较 low 的服务器的话，承担的相应的请求就会减少一点，毕竟性能比较低。

而在这个时候还会出现另外一种意外，那就是数据库服务器宕机了，怎么办？相同的原理，增加另外的一个数据库服务器，也就是主从数据库。

![](http://www.justdojava.com/assets/images/2019/java/image_yi/2020/07-24/6.jpg)

那么为什么要做主从复制，不单单是因为这一个服务器宕机的问题，还有如果对数据库的读和写都在同一个数据库服务器中操作，业务系统性能会降低。

而我们很多的项目在数据上面需要的就是比较重要的，就很多就是做读写分离，而为了提升业务系统性能，优化用户体验，可以通过做主从复制（读写分离）来减轻主数据库的负载。 

一台用于写入数据，一台用于同步主的数据并用于数据查询操作。

配置好主从复制之后，同一张表，只能对一个服务器写操作。

## 业务分离

现在很多项目的架构都是所有人的业务代码都写在了一起，乱七八糟的，好几个人的代码，维护起来那叫一个崩溃，当你看到这样的项目的时候，你就会发现，人都傻了，这是个什么鬼，改动一点，其他的不好用了，那叫一个崩溃呀。

这时候我们就需要把我们的业务彻底的做出分割，比如商城里面的，订单属于一块的业务，积分属于一部分的业务，物流属于另外一部分的业务，这时候我们就需要分成三块的业务模块。

![](http://www.justdojava.com/assets/images/2019/java/image_yi/2020/07-24/7.jpg)

也就是相当于每一块的内容都属于一个服务，而这些服务叠加起来可就不是1+1=2的问题了，这些业务服务相加起来，这时候完整的项目和你把所有的内容同一写到一个部分的内容差距是非常大的，尤其是在代码冗余方面，做的那是相当透彻的。

而说到这给内容的话，其实已经算差不多了，但是再更深的阿粉是真的没有了解到那么多，而阿粉之前没想过这些内容会在你面试的时候问到，可能阿粉当时只是想自己做个咸鱼，不去关心架构方面的事情，而架构方面的事情确实很多公司很看重的一点。

在这里阿粉给大家再次贡献出此次面试的其他的问题，并且给出详细的解答，并且阿粉也是很欣慰的，只是压了工资，而没有说直接拒绝。

#### 1.Redis分区实现方案

- 客户端分区：

客户端分区就是在客户端就已经决定数据会被存储到哪个redis节点或者从哪个redis节点读取。大多数客户端已经实现了客户端分区。

- 代理分区：

代理分区 意味着客户端将请求发送给代理，然后代理决定去哪个节点写数据或者读数据。代理根据分区规则决定请求哪些Redis实例，然后根据Redis的响应结果返回给客户端。

- 查询路由：

查询路由(Query routing) 的意思是客户端随机地请求任意一个redis实例，然后由Redis将请求转发给正确的Redis节点。Redis Cluster实现了一种混合形式的查询路由，但并不是直接将请求从一个redis节点转发到另一个redis节点，而是在客户端的帮助下直接redirected到正确的redis节点。

这些都是阿粉死记硬背背下来的，关于这种东西，没有实际亲身实践过的，没有遇到过的问题的，都是属于被diss的，但是面试官好像理解也不是很深，也是知道，但是具体的也没有仔细的深挖我这块的内容。

#### 2.SpringBean的生命周期

说实话，这个问题，面试好像现在都是必问的知识点了，阿粉的同事面试也是被问，但是巧了，之前阿粉就写过关于SpringBean的生命周期的，文章链接给大家送上，大家可以仔细查看，可以共同交流呦。

[面试官：兄弟你来阐述一下Spring框架中Bean的生命周期？](https://mp.weixin.qq.com/s?__biz=MzU3NzczMTAzMg==&mid=2247488563&idx=1&sn=9266b93e6e3f73dd2b0eb48560326359&chksm=fd017484ca76fd9221a5d042b03c4f86e6d534ca8a31727339ff35dbdcc0281a925074573ec6&token=370142830&lang=zh_CN#rd)

所以大家一定要把这个准备好呦，SpringBean的生命周期，从初始化到最终的销毁中间经历了什么，过程是什么，流程怎么理解。

#### 3.HashMap 和 Hashtable

这个问题我在回答的时候我就分开了，分门别类的比较比如说：

- 线程安全

- 性能优劣

- NULL

- 实现方式

- 容量扩容

我分成了五块的内容作答，如果说你只能够刚刚想起来其中的三到四点也是不错的，至少比你只会说他们的线程安全和是否允许键为空来的好很多，如果大家有兴趣，请寻找集合系列文章，在过往的历史当中寻找一下，有很多关于HashMap 和 Hashtable的面试点。

#### 4.JVM内存模型和优化

这个我相信只要是工作了两到三年的程序员肯定都会，我就给大家简单说说，之前的文章图解，

![](http://www.justdojava.com/assets/images/2019/java/image_yi/2020/07-24/8.jpg)

关于两篇文章通俗易懂，简单明了，几次面试，回答没有遗漏，面试官觉得还行，文章连接送上：

[你还在为了JVM而烦恼么?（内存结构和垃圾回收算法）](https://mp.weixin.qq.com/s?__biz=MzU3NzczMTAzMg==&mid=2247483760&idx=1&sn=6b51ec45af12e9fd6a4bf9aa24cd6752&chksm=fd0161c7ca76e8d1a36237666d90c476fb313aa9c93381fa5541c928d0d807f983678cc0f426&token=370142830&lang=zh_CN#rd)

[老年代的垃圾回收算法](https://mp.weixin.qq.com/s?__biz=MzU3NzczMTAzMg==&mid=2247483860&idx=1&sn=3d3382928af4146650a53a606ec58dac&chksm=fd016163ca76e875d7844afdc9d9814b74b2e588bb2d88cb0853b885d33b7f414a4476ff58a8&token=370142830&lang=zh_CN#rd)

关于其他的问题，都不是比较经典的，都是属于项目业务中的了，阿粉就不再一一给大家介绍了，总结起来就一句话，基础你要掌握，扩展你更要会，不然面试想要高工资？那是不可能的，毕竟不是每家公司都缺“大爷”，不是么？

阿粉在这里希望大家找到自己理想的工作，等疫情稳定了，直接跳槽工资“Double”。
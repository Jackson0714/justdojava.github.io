---
layout: post
categories: 学习
title: 如何学好 java 这门技术
tags: 
  - 炸鸡可乐
---

对于初次接触 Java 的朋友，想必一定很迷茫，想知道 Java 具体能干啥，如何掌握好 Java 这么技术，如何运用好 Java 技术进行项目开发等疑惑！

<!--more-->

其实曾经的我，也一度迷茫，虽然学的很多，但是技术积累的比较散，在面试的时候一碰到面试官提一些自己没听说过的问题，瞬间就傻逼了，而且时常不够自信，但是自从认识了一些大牛之后，我才发现自己欠缺的是系统性的知识，以及对自己未来的定位。从那时候起，渐渐的开始思考 Java 为什么这么火，怎么学好 Java 这么技术，以及自己未来的方向。

从1995年 Sun 发布 Java 以来，一直到现在，似乎从未离开过软件工程师的视线，并且每年涌入 Java 生态的开发者还在不停的增加。

据不完全统计，全球有25亿电子器件运行着 Java，450多万 Java 开发者活跃在 web 应用以及安卓市场上，有7.08亿部手机、10亿个智能卡和7亿部 PC 机上运行着 Java 应用程序，越来越多的企业因为使用了 Java 而提高了生产效率，我想这大概就是为什么 Java 是世界第一的开发语言的原因吧～～

![](http://www.justdojava.com/assets/images/2019/java/image_zjkl/java-learning/09a0e6cb7dca4007aeba10c15eb2d736.jpg)

在此，我想以第一人称来聊聊自己学习 Java 的路线，谈不上牛人，不一定很全，只希望能帮到那些处于迷茫阶段的朋友，助一臂之力！
### 技术学习路线
任何一种想推向市场的技术语言，除了要拥有一套自己的语言特性以外，还需要有第三方市场，不然单靠自己的核心工具库，很难适应实际开发中业务的多样性，Java 作为最热门的语言，同样也如此！

单靠 JDK 提供的工具库，很难完成 web 应用程序的开发，但是经过多年的发展，Java 通过其他技术栈的融合，已经完成自己的生态！

在这里，我将 web 应用涉及到的技术栈知识学习分为以下几个部分：

* Java 核心技术篇
* 设计模式篇
* Java 开源框架篇
* 数据库篇
* 前端技术篇
* 中间件篇
* 服务器篇

#### 1、java核心技术篇
这个部分，主要是熟悉语言的基本特性，各个核心组件，以及编码规范，可以说是整个 web 应用中最核心的一个技术栈，内容如下：

* **基础知识**：主要是包含程序流程控制、语法特性、注解、异常处理等基础内容。
* **容器知识**：主要是位于`java.util`包下的集合类，集合类封装了很多典型的数据结构和算法，例如动态数组、双向链表、队列、栈、Set、Map等。
* **IO知识**：主要是面向流处理操作，例如 BIO、NIO、AIO等。
* **多线程知识**：主要是面向多线程操作，以及利用多线程技术实现高效并发。
* **JVM知识**：这个部分的知识，估计很多初学者没有实质的接触到，但是任何高端的面试，JVM面试一定是少不了，核心知识点主要是GC调优；

Java 核心知识图分类，如下：

![](http://www.justdojava.com/assets/images/2019/java/image_zjkl/java-learning/1ecfdcb236a14fdbb7fe83e4cf866ae1.jpg)

其中，Java 的集合类主要集中在`java.util`包，里面涵盖了很多数据结构和算法实现，例如：ArrayList、HashMap、HashSet、HashTable等类，在开发的时候，基本少不了。

关于`IO`方面的知识，在我们处理文件以及网络上收发数据时，会频繁的接触！

对于多线程，初学的时候可能很少用到，但是在高并发的场景，合理的多线程编程能极大的改善接口请求响应速度，提高系统资源的利用率！

至于`JVM`方面的知识，可以说是 Java 最核心的部分，掌握好GC调优，是从熟悉 Java 走向精通 Java 的一个标志，如果你面试的是高级开发，GC调优一定逃不了！

可能有的朋友，会想到`SWT`部分，`SWT`是一套 GUI 编程框架，可以使用它来开发一套可视化界面，对于后端开发，基本很少用到，现在主流的可视化界面基本被 HTML 替代掉了！

相关学习书籍，推荐如下：

* java核心技术卷I、II；
* Effective Java中文版(第2版)；
* Java并发编程实战；
* 深入理解Java虚拟机；
* Java编程思想

#### 2、设计模式篇
设计模式，是一套高效编程理论，在任何一门开发语言中都适用。

**如果将 Java 核心技术比作为外功，那设计模式就是内功，要想深入的掌握这门技术，毫无疑问，必须内外兼修**！

从模式上，可以将其分为三大类：创建型模式、结构型模式、行为型模式
，合计各个类别总共有 23 种！

![图片截图于菜鸟教程](http://www.justdojava.com/assets/images/2019/java/image_zjkl/java-learning/b912e7e127144e9a99aff297fb2e456c.jpg)

其中，还有一种 J2EE 设计模式，也就是我们 web 开发中经常使用的一种模式，这种设计模式特别关注表示层，由 Sun Java Center 鉴定的。

相关学习书籍，推荐如下：

* 大话设计模式

#### 3、Java 开源框架篇
如果你已经掌握了 Java 核心技术、常用设计模式，此时，已经具备可以开发一套属于自己的公共组件或者框架的能力！

但是，为啥要学习开源框架呢？

好比一个班级，有的同学很优秀，每次考试总是得第一，其他的同学想学习模仿，然后每次开班会的时候，老师就让那些优秀学生介绍一些自己的学习经验，希望班上其他同学，也能从中能学到一些东西。当然小编是学渣，可以忽略～～

**开源框架的出现，对整个IT行业来说，真的绝对是一种福利**！比如新手上手难、项目开发周期长、编码风格不统一等问题，`Spring`、`SpringMVC`、`Mybtais`、`Hibernate`等框架的出现，极大的改善了`web`应用程序后端开发的难度，缩短了开发周期，对于后端开发者而言，真的是一种解放！

有的大公司，还有专门团队负责开发框架，例如阿里的 dubbo，就是阿里中间件团队开发的分布式调用服务框架，并且已经开源，对于要采用分布式部署的小企业，绝对是福音！

![](http://www.justdojava.com/assets/images/2019/java/image_zjkl/java-learning/e50f8f259dab4c46af36558236e28172.jpg)

上面只是简要的介绍了主流的开源框架，实际上在 Java 的第三方框架生态里，还有很多热门的开源框架，例如：Netty 框架，一个成熟的高性能网络编程框架，主要是面向 NIO 开发，因为 jdk 中的 nio 存在不好用的问题，所以很多开发者弃而选择第三方框架来开发。

还有我们常用的 apache 的 common 包，这些第三方框架包，无疑都帮java弥补了自身的不足。

相关学习书籍，推荐如下：

* Spring源码深度解析；
* Netty实战；
* 重构-改善既有代码的设计；
* 领域驱动设计

#### 4、数据库篇
从业务的角度出发，纯 Java 开发的应用程序，如果不与数据库连接起来，这个应用程序很难发挥它的作用，甚至吸引不了用户！

任何一门技术语言，其实都可以看成一种中间件，包括 Java 也是，对于一个用户来说，想要的就是数据，即：**用户 -> 数据**。而数据一般存放于数据库，对于数据库这块，其重要性可见一斑！

因为数据的存储需求，还诞生了很多巨头公司，例如：oracle、MongoDB。

在大公司，还有专门的大数据团队来负责数据的筛选、统计、分析，以助力销售部门做计划！

![](http://www.justdojava.com/assets/images/2019/java/image_zjkl/java-learning/f6f0c5ae00664a20ac750148f626b4bb.jpg)

按照使用用途，数据库可分为关系型数据库、非关系型数据库。

* **关系型数据库**：主要就是我们做业务时经常会接触到的一种数据库，在设计时主要需要遵循三范式要求。
* **非关系型数据库**：主要是面向那些不能用结构化关系表达的数据，通过`k-v`来实现存储。

关系型数据库，是一种使用非常广泛的数据库，大部分业务都使用关系型数据库来存储数据，例如我们用户表、订单表、产品表等。

随之业务的快速发展，出现了很多难以克服的问题，非关系型数据库的出现就是为了解决大规模数据集合多重数据种类带来的挑战，尤其是大数据应用难题。

关于数据库方面，对于初学者而言，重在掌握数据结构、表、sql语句、索引、视图、存储过程、分库分表等常用功能，如果想更深入的发展，还需要掌握存储引擎、慢sql优化、数据连接监控、备份与恢复、数据统计分析等高级功能！

在这里就不详细的介绍各个数据库的使用了，会在后期的文章中详细介绍数据库的知识！

相关学习书籍，推荐如下：

* SQL基础教程（入门级）；
* 高性能MySQL（进阶级）；

#### 5、前端技术篇
真正在实际开发过程中，对于后端开发者而言，不可能只做 Java 的开发，例如 pdf 自定义报表打印，这个需求就需要用到 Html 知识，有一些公司连前端开发都没有，前端任务全部都由后端人员来兼顾开发完成，当然作为后端人员，我们不可能啥都会，例如最新的 vue、react、angluar等前端框架，都是需要花精力去学习的，如果你有足够的精力，没问题。

在这里推荐想学习前端技术的后端人员，重在掌握 Html、JavaScript技术，因为这两个技术是整个前端开发的基础，学完之后再学其他框架会更加游刃有余！

相关学习网站，推荐如下：

* w3school（网站）

#### 6、中间件篇
当我们初步掌握了 Java 相关核心技术、数据库知识、前端技术等知识之后，此时的你，基本可以独立开发一个小项目了，是不是很兴奋～～

但是如果面对一个请求量很大、对响应要求很高的系统，传统的解决办法基本解决不了你所面临的问题！

这个时候，你可能需要学习中间件了，例如分布式缓存：redis、memcached，分布式消息队列：activemq 、rabbitmq、rocketmq、kafka，分布式搜索引擎：elasticsearch，分布式任务调度：quartz，分布式API网关：zuul，分布式熔断器：Hystrix 等等。

![](http://www.justdojava.com/assets/images/2019/java/image_zjkl/java-learning/be7f07f6630241b2b70c6149b5431534.jpg)

这些中间件的出现，主要是为了解决在集群环境下，单体应用系统解决不了的问题。

例如，redis的出现，解决了在集群环境下，单体应用系统缓存不同步的问题，rabbitmq实现单体应用中生产与消费者的解耦，elasticsearch解决在集群环境下搜索各种信息的服务等等。

因为技术更新迭代太快！看书可能不太跟得上，关于这块内容的学习，可以自行在网上查询相关博客网站写的系列文章，或者直接查询官网的文档。对学习会非常有帮助！

#### 7、服务器篇
对于服务器这块，**重点主要是掌握如何进行软件安装部署、使用和如何进行线上排查错误**，学习完服务器的部署，就可以通过web浏览器来访问项目了。

![](http://www.justdojava.com/assets/images/2019/java/image_zjkl/java-learning/466520199307469a98352cc430902bc6.jpg)

服务器的安装部署，可以说是非常重要的一环，例如，你想使用分布式消息队列 rabbitMQ，这个软件的安装过程就有点小复杂，如果自己都无法安装部署在服务器上，谈何使用！

打铁还需自身硬！很多小公司，没有所谓的运维人员，基本都是开发者自己去部署项目，包括集群环境的搭建和维护！

所以，如果在一家小公司里，那么学会服务器的部署、线上错误排查和解决，会对你非常有帮助！

学习完服务器部署之后，整个技术链基本已经成型了！

关于这块内容的学习，我不建议看书，因为更新太快，而且出现很多问题，书上也给不了答案，大部分出现的问题，在网上都可以直接搜索得到。
### 使用github助力
对于企业来说，之所以招聘 Java 技术人员，主要是因为 Java 能极大的提升公司的生产效率和运营效率，比如阿里巴巴、京东、美团等企业，很多核心的业务都是用 Java 开发的。

尤其是阿里巴巴，还开源了很多的 Java 框架，在业界比较出名的有 dubbo、rocketmq、fastjson等等。

这些大公司招聘要求也都非常高，尤其是对技术基础的掌握，还有业务的实现。

当然，给出的薪资待遇一点都不低，大家加油哦！

上面我们介绍了技术学习路线，其中还有一个很重要的环节，就是用技术来做项目，可能有些朋友很迷茫，不知如何完整的去做一个项目？

说到 github ，相信很多人不会陌生，一个属于程序员的乐园，在里面有非常非常多有名的项目，代码全部托管在里面，比如：spring、springboot、springcloud、dubbo、shiro、boostrap等等。

我会定期在 github 上搜索`stars大于10000`的项目，筛选 Java 项目，找到比较感兴趣的 Java 项目，然后每个都点进去看一下。

![](http://www.justdojava.com/assets/images/2019/java/image_zjkl/java-learning/1f6ddc90cada403686ac8037dfa308d6.jpg)

对于比较感兴趣的项目，就把代码给`clone`下来，倒入到 IDEA 中，当然也不仅仅只是看，对于写的很好的代码，自己会照着写一遍，我建议初学者找一个感兴趣的项目，然后把代码抄一遍，边抄边理解，这样能锻炼自己做项目的思路，对提升自己做项目的经验非常有帮助！

github 真的是一个非常好的学习技术的地方，例如电商项目、OA项目、新闻视频项目等等，都有现成的代码，如果你所在项目碰到了技术瓶颈，可以参考类似的项目是怎么实现的，说不定就能帮到你！
### 写到最后
对于目前的互联网行业，学习 Java 技术的朋友，比较主流的职业路线就是向架构师发展或者项目经理方向发展，再就是技术总监，最后就是自己创业做老板，当然也有的朋友转向大数据，大数据一般会用 python 脚本来进行开发，不过当你精通了一门技术语言之后，由于大部分开发语言语法套路差不多，再学习其他的语言，相对来说会比较轻松！

上面介绍的技术路线，只是一个大致的流程，作为一名IT从业人员，需要了解的知识还有很多，例如：计算机网络知识、数据加解密、浏览器从发起一个请求到后端服务器所经过的链路、cpu是实现多线程操作的原理等等，每个技术点后面都有故事，技术永远在不断的更新，学习的脚本不能停下来！

小编谈不上什么大神，不懂的东西还有很多，很多知识还需要深入的学习，可能有些地方写的不够好，望网友们多批评、多指出！

谢谢各位阅读本文，希望能帮助那些处于迷茫阶段的朋友！助你们一臂之力！
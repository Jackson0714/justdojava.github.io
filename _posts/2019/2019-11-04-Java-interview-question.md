---
layout: post
categories: 面试
title: 从 Java 的平台无关性引入的一系列面试题
tagline: by 炭烧生蚝
tags:
  - 炭烧生蚝
---

> 在 Java 面试中，有一条很常见的询问路线：从对 Java 的认识，到谈 Java 的平台无关性，到 Java 中的反射机制，再到类加载机制，继而深入到双亲委派机制等。本文将根据这条路线，给出一份可供参考的回答，如有错误万望指正。（推荐读者们在回答的时候结合自己的认识和项目经历作答）

<!--more-->

## 1、谈谈 Java 的 Compile Once，Run Anywhere

### 1.1、一次编译到处运行是如何实现的？

Java 程序从编写到运行需要经历这么个过程：首先编写 Java 源代码，然后通过 Javac 编译器将 Java 源代码编译成 .class 字节码文件，然后把字节码文件交给虚拟机，虚拟机会在执行 Java 程序的时候把字节码转换为机器码执行。

字节码文件是平台无关性的重要一环。同一个 Java 程序能够在 Linux，Windows 等不同平台上运行，是因为不同平台上安装了不同的 Java 虚拟机，这些不同的虚拟机会根据同一份字节码文件，转换成各个平台对应的机器码，从而使 Java 程序在不同的平台上运行。

按照这个逻辑，只要是符合规范的字节码文件就能通过虚拟机在不同平台运行，我们完全可以使用另一种语言编写程序，编写完后把程序编译为字节码文件，然后通过虚拟机在不同的平台上运行。现实中也确实存在运行于 Java 虚拟机之上的其他语言程序。

### 1.2、为什么 JVM 不直接将源码解析成机器码执行？

> 不同的机器安装不同的虚拟机，JVM 直接解析 Java 源码不是也能做到一次编译到处运行吗？

1. 这样每次执行之前就要进行各种检查（这是编译成字节码前的工作），降低了执行效率。
2. 上面提到的兼容其他语言的功能将无法实现。

## 2、JVM 是如何加载 .class 文件的？

JVM 是通过 Class Loader 类加载器来加载字节码文件的，在介绍如何加载之前要先讲讲它加载的目的地，也就是 Java 虚拟机。

### 2.1、JVM 的结构：

Java 虚拟机是通过 c/c++ 编写的，可以看作是一个模拟真实计算机的程序，通俗来说说它是一个跑在内存中的机器，而后面我们谈到的 JVM 的内存结构就是存放在我们真实计算机的内存中的。（后面我会直接讲 JVM 的内存）

JVM 大致可以分为四个模块：
1. 类加载器：用于把字节码文件加载进运行时数据区
2. 运行时数据区：字节码文件的不同部分会被放入运行时数据区的不同地方
3. 执行器：执行字节码中的程序
4. 本地代码接口：调用宿主计算机的一些本地方法（ c/c++ 或其他语言编写的接口）

其中运行时数据区是 Java 虚拟机的精华所在，它把字节码文件中的数据按一定的格式和数据结构组织存放好，方便了执行器调用。

### 2.2、JVM 是如何加载 .class 文件的

JVM 是通过类加载器加载 .class 字节码文件的，而 JVM 中的类加载器不只一个，它是按照父子关系进行划分的，至于为什么要这么划分，这会涉及到双亲委派机制，这个稍后便讲。具体的父子关系如下：
1. BootStrapClassLoader：最顶层的类加载器，由 C++ 编写，用于加载 Java 的核心类库
2. ExtClassLoader：Java 编写，用于加载 Java 的扩展库
3. AppClassLoader：Java 编写，用于加载应用程序所在目录下的 class 文件
4. 自定义 ClassLoader：Java 编写，用于定制化加载

由不同类加载器的作用可以知道，不同加载器加载的路径是不同的。但它们共同的任务都是把字节码文件加载到运行时数据区中（不同语言实现的类加载器具体加载部分的代码也会有所差别），更形象地说是把字节码文件中的二进制 01 数据加载到 JVM 中，并按照运行时数据区进行划分存放。

### 2.3、什么是双亲委派机制，为什么要制定双亲委派机制？

我们先从一个类的加载顺序开始讲起：
1. 当需要加载一个类时，如果没有自定义类加载器，默认会使用 AppClassLoader 进行加载，

2. AppClassLoader 先会查找一下该类是否已经被加载，若已经被加载则返回，若没有则调用它的父加载器 ExtClassLoader 进行加载，

3. ExtClassLoader 也会查找一下该类是否已经被加载，若已经被加载则返回，若没有则向上调用它的父加载器 BootStrapClassLoader 进行加载，

4. BootStrapClassLoader 会尝试加载该类，若加载不到则返回

5. 接着 ExtClassLoader 也会尝试加载该类，若加载不到则返回

6. 接着 AppClassLoader 也会尝试加载该类，假设该类被加载到（在项目目录下），则成功返回，否则抛出 ClassNotFoundException

当然以上过程也可以从自定义的类加载器开始，过程是一样的。这种先委派父加载器进行加载的机制就是双亲委派机制。

为什么不直接加载，而是往上委派双亲加载呢？

1. 因为内存资源是宝贵的，如果一个类已经加载过一次了，也就没有必要再加载一份相同的拷贝在内存中了。为了保证一个类只被加载一次，加载类时就会从最顶层的父类加载器开始加载，只要加载过了，在后续需要用的时候就会返回已经加载过的 class 文件。

2. 为了保证安全性和稳定性。Java 自身是有许多核心类的，这些类都通过顶层的父加载器进行加载，保证运行的时候用的是 Java 系统自己的类。如果没有双亲委派机制保证，用户自己也可以编写一些系统类并用自己编写的类加载器进行加载，那么就会导致Java 自身的系统类和用户编写的类混在一起，破坏了 Java 程序执行的安全性和稳定性。

### 2.4、额外：谈谈 Java 中的反射机制

在问到类加载，JVM 等话题时难免会问到反射机制，这里补充一下：

反射是 Java 中一个很强大的机制，要说清楚反射还得结合上面说到的 JVM 结构去谈。

由于类加载器会把整个 .class 文件加载进运行时数据区，.class 文件中包含了一个类的字段，构造函数，以及各种方法，Java 允许我们在程序中通过反射的方式直接操作这些数据。

```java
//比如我们可以根据类的限定类名获得一个类的实例对象
Class cc = Class.forName("xx.xx.Demo");
Demo demo = (Demo)cc.newIntance();

//获取并设置一个类的私有字段
Field name = cc.getDeclaredFied("name");
name.setAccessible(true);
name.set(demo, "Zhang san");

//或者调用一个类的方法（公有/私有）
Method sayHi = cc.getMethod("sayHi", String.class);
sayHi.invoke(demo, "Hello");
```

总结一句就是字节码中的类信息被加载进了运行时数据区，Java 允许我们在程序中直接操作这些类信息。

为什么说 Java 的反射机制强大呢？这里就要说到 Spring 框架了。不知道 Java 的反射强大，总该知道 Spring 框架的强大了吧，Spring 就是基于反射实现的。举个例子：Spring 中最核心的概念莫过于控制反转了，通俗的解释就是把对象的生命周期交给框架管理，而不是由程序员管理。既然是交给框架管理对象，那创建对象就不能通过 new 关键字实现了，而是由框架通过反射创建，同理对象中方法的调用也由框架通过反射进行调用。

---
layout: post
title: "ART vs Dalvik"
description: "ART vs Dalvik"
category: Andorid Advance
tags: [Andorid Advance]
imagefeature: blog/bg.jpg
comments: true
mathjax: null
featured: false
published: true
---


ART与Dalvik
===

ART
--- 

`Android 4.4`提供了一种与`Dalvik`截然不同的运行环境`ART`支持,`ART`源于`google`收购的`Flexycore`的公司。
`ART`模式与`Dalvik`模式最大的不同在于，启用`ART`模式后，系统在安装应用的时候会进行一次预编译，将字节码转换为机器语言存储在本地，
这样在运行程序时就不会每次都进行一次编译了，执行效率也大大提升。
`ART`代表`Android Runtime`，其处理应用程序执行的方式完全不同于`Dalvik`，`Dalvik`是依靠一个`Just-In-Time` (`JIT`)编译器去解释字节码。
开发者编译后的应用代码需要通过一个解释器在用户的设备上运行，这一机制并不高效，但让应用能更容易在不同硬件和架构上运行。
`ART`则完全改变了这套做法，在应用安装时就预编译字节码到机器语言，这一机制叫`Ahead-Of-Time`(`AOT`）编译。
在移除解释代码这一过程后，应用程序执行将更有效率，启动更快。总体的理念就是空间换时间。

Dalvik
---

`Dalvik`是`Google`公司自己设计用于`Android`平台的`Java`虚拟机。它可以支持已转换为`.dex`（即`Dalvik Executable`）格式的`Java`应用程序的运行，
`.dex`格式是专为`Dalvik`设计的一种压缩格式，适合内存和处理器速度有限的系统。`Dalvik`经过优化，允许在有限的内存中同时运行多个虚拟机的实例，
并且每一个`Dalvik`应用作为一个独立的`Linux`进程执行。独立的进程可以防止在虚拟机崩溃的时候所有程序都被关闭。

`AOT`的编译器分两种模式：            
- 在开发机上编译预装应用；
- 在设备上编译新安装的应用,在应用安装时将dex字节码翻译成本地机器码。

ART优点:     
- 系统性能的显著提升。
- 应用启动更快、运行更快、体验更流畅、触感反馈更及时。
- 更长的电池续航能力。
- 支持更低的硬件。

ART缺点:       
- 更大的存储空间占用，可能会增加10%-20%。
- 更长的应用安装时间。


		
---

- 邮箱 ：charon.chui@gmail.com  
- Good Luck! 
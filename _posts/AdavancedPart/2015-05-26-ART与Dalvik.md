---
layout: post
title: "ART与Dalvik"
description: ""
category: AdavancedPart
tags: [AdavancedPart]
imagefeature: blog/bg.jpg
comments: true
mathjax: null
featured: false
published: true
---



ART与Dalvik
===



Dalvik
---

`Dalvik`是`Google`公司自己设计用于`Android`平台的`Java`虚拟机。它可以支持已转换为`.dex`（即`Dalvik Executable`）格式的`Java`应用程序的运行，
`.dex`格式是专为`Dalvik`设计的一种压缩格式，适合内存和处理器速度有限的系统。`Dalvik`经过优化，允许在有限的内存中同时运行多个虚拟机的实例，
并且每一个`Dalvik`应用作为一个独立的`Linux`进程执行。独立的进程可以防止在虚拟机崩溃的时候所有程序都被关闭。
很长时间以来，`Dalvik`虚拟机一直被用户指责为拖慢安卓系统运行速度不如`IOS`的根源。
`2014`年`6`月`25`日，`Android L`正式亮相于召开的谷歌`I/O`大会，`Android L`改动幅度较大，谷歌将直接删除`Dalvik`，代替它的是传闻已久的`ART`。


ART
--- 

`Android 4.4`提供了一种与`Dalvik`截然不同的运行环境`ART`支持,`ART`源于`google`收购的`Flexycore`的公司。
`ART`模式与`Dalvik`模式最大的不同在于，启用`ART`模式后，系统在安装应用的时候会进行一次预编译，将字节码转换为机器语言存储在本地，
这样在运行程序时就不会每次都进行一次编译了，执行效率也大大提升。

`ART`使用`AOT(Ahead Of Time)`(静态编译)而`Dalvik`使用`JIT(Just In Time)`(动态编译)
`JIT`方式会在程序执行时将`Dex bytecode`(`java`字节码)转换为处理器可以理解的本地代码，这种方式会将编译时间计入程序的执行时间，程序执行会显得慢一些。`AOT`方式会在程序执行之前(一般是安装时)就编译好本地代码，因此程序执行时少了编译的过程会显得快一些，但占用更多存储空间，安装时也会更慢。但没针对ART优化的程序反而会运行得更慢，随着`Android L`的普及这个问题迟早会解决。`ART`拥有改进的`GC`(垃圾回收)机制:`GC`时更少的暂停时间、`GC`时并行处理、某些时候`Collector`所需时间更短、减少内存不足时触发GC的次数、减少后台内存占用。   
在移除解释代码这一过程后，应用程序执行将更有效率，启动更快。总体的理念就是空间换时间。


`AOT`的编译器分两种模式：            
- 在开发机上编译预装应用；
- 在设备上编译新安装的应用,在应用安装时将`dex`字节码翻译成本地机器码。

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
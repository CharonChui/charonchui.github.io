---
layout: post
title: "如何让Service常驻内存"
description: "Keep Service Still Live"
category: Andorid Advance
tags: [Andorid Advance]
imagefeature: blog/bg.jpg
comments: true
mathjax: null
featured: false
published: true
---

如何让Service常驻内存
===

我非常鄙视这种行文，一个公司应该想到如何把产品做的更完善，而不是用这些技术来损害用户的利益，来获取自己肮脏的所谓的功能。

- `Service`设置成`START_STICKY`，`kill`后会被重启（等待5秒左右)，重传`Intent`，保持与重启前一样
- ​通过`startForeground`将进程设置为前台进程，做前台服务，优先级和前台应用一个级别​，除非在系统内存非常缺，否则此进程不会被`kill`
- 双进程`Service`：让`2`个进程互相保护，其中一个`Service`被清理后，另外没被清理的进程可以立即重启进程
- `QQ`黑科技:在应用退到后台后，另起一个只有1像素的页面停留在桌面上，让自己保持前台状态，保护自己不被后台清理工具杀死
- 在已经`root`的设备下，修改相应的权限文件，将`App`伪装成系统级的应用（`Android4.0`系列的一个漏洞，已经确认可行）
- `Android`系统中当前进程(`Process`)`fork`出来的子进程，被系统认为是两个不同的进程。当父进程被杀死的时候，子进程仍然可以存活，并不受影响。
    鉴于目前提到的在`Android-Service`层做双守护都会失败，我们可以`fork`出`c`进程，多进程守护。死循环在那检查是否还存在，
	具体的思路如下（`Android5.0`以下可行）
	- 用`C`编写守护进程(即子进程)，守护进程做的事情就是循环检查目标进程是否存在，不存在则启动它。
	- 在`NDK`环境中将1中编写的C代码编译打包成可执行文件(`BUILD_EXECUTABLE`)。
	- 主进程启动时将守护进程放入私有目录下，赋予可执行权限，启动它即可。
	
- 联系厂商，加入白名单



---

- 邮箱 ：charon.chui@gmail.com  
- Good Luck! 
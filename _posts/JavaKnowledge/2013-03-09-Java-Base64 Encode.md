---
layout: post
title: "Base64加密"
description: "Base64 Encode"
category: JavaKnowledge
tags: [JavaKnowledge]
imagefeature: blog/bg.jpg
comments: true
mathjax: null
featured: false
published: true
---


Base64加密
===

由来
---

为什么会有`Base64`编码呢？因为有些网络传送渠道并不支持所有的字节，例如传统的邮件只支持可见字符的传送，
像`ASCII`码的控制字符就不能通过邮件传送。这样用途就受到了很大的限制，比如图片二进制流的每个字节不可能全部是可见字符，所以就传送不了。
最好的方法就是在不改变传统协议的情况下，做一种扩展方案来支持二进制文件的传送。把不可打印的字符也能用可打印字符来表示，问题就解决了。
`Base64`编码应运而生，`Base64`就是一种基于`64`个可打印字符来表示二进制数据的表示方法。

原理
---

下面是`Base64`的编码表,字符选用了`A-Z、a-z、0-9、+、/`64个可打印字符。
数值代表字符的索引，这个是标准`Base64`协议规定的，不能更改。
64个字符用6个`bit`位就可以全部表示，一个字节有8个bit位，剩下两个`bit`就浪费掉了，这样就不得不牺牲一部分空间了。
这里需要弄明白的就是一个`Base64`字符是8个`bit`，但是有效部分只有右边的6个`bit`，左边两个永远是0。

![Image](https://raw.githubusercontent.com/CharonChui/Pictures/master/base64_excel.png?raw=true)   

因为`Base64`是6个`bit`那么，怎么来表示传统字符呢？那就是用４个`Base64`字符来表示3个传统字符。3*8=4*6嘛，这样就正好了。

下面来看一个例子:`Man`是三个字符，一共24个`bit`，用4个`Base64`字符来凑齐24个有效位。
红框表示的是对应的`Base64`，6个有效位转化成相应的索引值再对应`Base64`字符表，
查出`Man`对应的`Base64`字符是`TWFU`。说到这里有个原则不知道你发现了没有，要转换成Base64的最小单位就是三个字节，
对一个字符串来说每次都是三个字节三个字节的转换，对应的是`Base64`的四个字节。这个搞清楚了其实就差不多了。

![Image](https://raw.githubusercontent.com/CharonChui/Pictures/master/base64_man.png?raw=true)   


正式因为这，所以
想要转换成`Base64`最少要三个字节才可以，转换出来的`Base64`最少是4个字节，但是如果我要转换的字节不够3个怎么办？比如我想对字符`A`进行`Base64`
加密。，`A`对应的第二个`Base64`的二进制位只有两个，把后边的四个补0就是了。
所以`A`对应的`Base64`字符就是QQ。上边已经说过了，原则是`Base64`字符的最小单位是四个字符一组，那这才两个字符，后边补两个"="吧。
其实不用"="也不耽误解码，之所以用"="，可能是考虑到多段编码后的Base64字符串拼起来也不会引起混淆。
由此可见 Base64字符串只可能最后出现一个或两个"="，中间是不可能出现"="的。下图中字符"BC"的编码过程也是一样的。

![Image](https://raw.githubusercontent.com/CharonChui/Pictures/master/base64_a.png?raw=true)   

总结
---

`Base64`编码是从二进制到字符的过程，像一些中文字符用不同的编码转为二进制时，产生的二进制是不一样的，
所以最终产生的`Base64`字符也不一样。例如上网对应`utf-8`格式的`Base64`编码是`5LiK572R`,对应`GB2312`格式的`Base64`编码是`yc/N+A==`


		
----
- 邮箱 ：charon.chui@gmail.com  
- Good Luck! 

	
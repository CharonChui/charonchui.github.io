---
layout: post
title: "视频解码之软解与硬解"
description: "Android Video Encoder"
category: Andorid VideoDevelopment
tags: [Andorid VideoDevelopment]
imagefeature: blog/bg.jpg
comments: true
mathjax: null
featured: false
published: true
---

视频解码之软解与硬解
===

**硬解**：从字面意思上理解就是用硬件来进行解码，通过显卡的视频加速功能对高清视频进行解码，很明显就是一个专门的电路板(这样好理解...)来进行视频的解码，是依靠显卡`GPU`的。                    

**软解**：字面上理解就是用软件进行解码，这样理解也对，但是实际最总还是要硬件来支持的，这个硬件就是`CPU`。

既然有这两种不同的解码方式，我们在开发中该如何进行选择？哪个更好？                     

- 硬解优缺点：                      
	显卡核心GPU拥有独特的计算方法，解码效率非常高，而且充当解码核心的模块成本并不高。这样不但能够减轻CPU的负担，还有着低功耗、发热少等特点。但是由于硬解码起步比较晚，
	软件和驱动对其的支持度低。硬解码内置有什么样的模块就能够解码什么样的视频，面对网络上杂乱无章的视频编码格式，不可能做到完全兼容同。此外，硬解码的滤镜、字母、画质增强方面都做的十分不足。
                               
    优点：低功耗、发热少、效率高。              
	缺点：视频兼容性差、支持度低。                

- 软解优缺点：                    
    软解码技术的解码过程中，需要对大量的视频信息进行运算，对CPU性能的要求非常高。尤其是对高清晰度大码率的视频来说，巨大的运算量就会造成转换效率低、发热量大等问题。
	但是由于软解码的过程中不需要复杂的硬件支持，兼容性非常高。即使是新出的视频编码格式，只要安装好相应的解码器文件，就能顺利播放。而且软解码拥有丰富的滤镜、字幕、画面处理优化等效果，
	如果`CPU`足够强悍的话，能够实现更加出色的画面效果。
	                  
    优点：  兼容强、全解码、效果好              
	缺点：  对`CPU`要求高、效率低、发热大                 

	          
关于软解与硬解究竟哪个更好的问题一直是争论的热点，其实我倒是感觉没有好坏之分，各自有各自的优缺点和使用条件，根据需要去选择才是最合适的。 
播放码率比较大的视频，硬解可能流畅的播放，但是软解可能会出现演示、画面和声音卡顿不同步的问题。但是硬解播放出的视频大多都不允许在解码之后进行软件后处理，比如进行一些降噪锐化之类的后期滤镜，
这样可能会让人感觉画质不太好的。当然上面的这种情况也是和`CPU`及`GPU`能力的不同而不同的。 总的来说，还是各有春秋，适合你的才是最好的。 

    
---

- 邮箱 ：charon.chui@gmail.com  
- Good Luck! 
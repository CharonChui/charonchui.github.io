---
layout: post
title: "单例的最佳实现方式"
description: "Java SingleTon"
category: JavaKnowledge
tags: [JavaKnowledge]
imagefeature: blog/bg.jpg
comments: true
mathjax: null
featured: false
published: true
---

单例的最佳实现方式
===

```java
public class Singleton {
	// Private constructor prevents instantiation from other classes
	private Singleton() { }

	/**
	* SingletonHolder is loaded on the first execution of Singleton.getInstance() 
	* or the first access to SingletonHolder.INSTANCE, not before.
	*/
	private static class SingletonHolder { 
			public static final Singleton INSTANCE = new Singleton();
	}

	public static Singleton getInstance() {
			return SingletonHolder.INSTANCE;
	}
}
```

---

- 邮箱 ：charon.chui@gmail.com  
- Good Luck! 
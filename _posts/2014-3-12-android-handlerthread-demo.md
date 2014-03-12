---
title: Android HandlerThread 的使用及其Demo
author: wenhao
layout: post
category : android
permalink:  /android-handlerthread-demo/
tags: 
  - android
  - demo

---

今天我们一起来学习下一个Android中比较简单的类`HandlerThread`,虽然它的初始化有点小麻烦。
<!--more-->


介绍
---
首先我们来看看为什么我们要使用`HandlerThread`?在我们的应用程序当中为了实现同时完成多个任务，所以我们会在应用程序当中创建多个线程。为了让多个线程之间能够方便的通信，我们会使用`Handler`实现线程间的通信。


下面我们看看如何在线程当中实例化`Handler`。在线程中实例化`Handler`我们需要保证线程当中包含Looper(**注意**：*UI-Thread默认包含Looper*)。


为线程创建Looper的方法如下：在线程run()方法当中先调用Looper.prepare()初始化Looper,然后再run()方法最后调用Looper.loop()，这样我们就在该线程当中创建好Looper。(**注意**：*Looper.looper()方法默认是死循环*)


我们实现Looper有没有更加简单的方法呢?当然有，这就是我们的`HandlerThread`。我们来看下`Android`对`HandlerThread`的描述：
> Handy class for starting a new thread that has a looper. The looper can then be used to create handler classes. Note that start() must still be called. 

---
使用步骤
---
尽管`HandlerThread`的文档比较简单，但是它的使用并没有想象的那么easy。

1. 创建一个`HandlerThread`，即创建了一个包含Looper的线程。
    
	HandlerThread handlerThread = new HandlerThread("leochin.com");
    handlerThread.start();  //创建HandlerThread后一定要记得start()

2. 获取`HandlerThread`的Looper
    
	Looper looper = handlerThread.getLooper();

3. 创建Handler，通过Looper初始化
   
	Handler handler = new Handler(looper);

通过以上三步我们就成功创建`HandlerThread`。通过handler发送消息，就会在子线程中执行。

如果想让`HandlerThread`退出，则需要调用`handlerThread.quit();`。

---
测试代码
---

[HandlerThreadDemo](http://git.oschina.net/hnrainll/HandlerThreadDemo.git)

---
引用：
---
- [HandlerThread](http://developer.android.com/reference/android/os/HandlerThread.html)
- [Android HandlerThread](http://stephendnicholas.com/archives/42)
> Written with [LeoChin](http://leochin.com/).
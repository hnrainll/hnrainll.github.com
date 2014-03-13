---
title: Windows上安装Python Twisted
author: wenhao
layout: post
category : python
permalink:  /python-twisted-install/
tags: 
  - python
  - twisted

---

###步骤1：下载Twisted

下载网址：[Twisted Downloads](https://twistedmatrix.com/trac/wiki/Downloads)

我下载的是（Twisted-13.2.0.win32-py2.7.msi）

<!--more-->

###步骤2：安装Twisted

点击Twisted-13.2.0.win32-py2.7.msi直接运行即可

这时候，运行IDLE，输入from twisted提示不可用。需要装zope.interface模块

 

###步骤3：下载zope

下载网址：[zope.interface](https://pypi.python.org/pypi/zope.interface#download)

我下载的是(zope.interface-4.1.0.win32-py2.7.exe)

 

###步骤4：安装zope

点击zope.interface-4.1.0.win32-py2.7.exe直接运行即可


###结果：
关闭刚刚打开的IDLE，再次打开并进入IDLE，输入import twisted, 如没有错误表示安装成功。


引用：
- [windows上安装 Twisted](http://blog.csdn.net/androidzhaoxiaogang/article/details/8479140)


> Written with [wenhao](http://hnrainll.cnblogs.com/).
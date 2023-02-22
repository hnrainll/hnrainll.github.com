---
title: Android中AES256加密的实现
author: Leo
layout: post
category : programme
permalink:  /android-aes256/
tags: 
  - android
  - java
  - aes

---



AES加密是我们在工作中常用到一种加密方式，并且在java中也已经实现好了其相应的接口。
但是Java自带的JDK默认最多实现128位及其以下的加密。如果使用java自带的api实现aes256将会报`java.security.InvalidKeyException:illegal Key Size`的错误。



## 解决方式：

如果要启动256位密钥,则需要更新local_policy.jar,US_export_policy.jar

> 如果你的JAVA_HOME为C:\Program Files\Java\jdk1.6.0_14. 
> 
> 覆盖: C:\Program Files\Java\jdk1.6.0_14\jre\lib\security下的同名文件 
> 
> 覆盖: C:\Program Files\Java\jre6\lib\security下的同名文件 

下载地址：

**java6:**

[http://www.oracle.com/technetwork/java/javase/downloads/jce-6-download-429243.html](http://www.oracle.com/technetwork/java/javase/downloads/jce-6-download-429243.html)

**java7:**

[http://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html](http://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html)



## 参考代码
[Android实现AES 256加密代码](https://github.com/hnrainll/learn-android/tree/master/AES256Demo)

Java同理！


## 引用

- [java AES为什么不支持256位？](http://bbs.csdn.net/topics/280086588)
- [http://www.oracle.com/technetwork/java/javase/downloads/jce-6-download-429243.html](http://www.oracle.com/technetwork/java/javase/downloads/jce-6-download-429243.html)
- [http://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html](http://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html)
- [Android实现AES 256加密代码](https://github.com/hnrainll/AES256Demo)
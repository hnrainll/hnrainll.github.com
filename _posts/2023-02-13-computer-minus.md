---
layout: post
title: "计算机中负数的表示法"
description: ""
category: "编程"
permalink:  /computer-minus/
tags: []

---


在数学中我们使用 + - 来表示正数和负数。
在计算机中数据都需要以二进制保存，那么负数如何在计算中用二进制存储呢？
计算机中常用的是三种方法：原码、反码、补码。
需要强调，原码、反码、补码是三种独立的在计算机中用于表示负数的方式。

## 原码
最高位表示符号。0表示正，1表示负。

## 反码
负数通过计算其绝对值的二进制后按位取反。

## 补码
在获取反码后加1。

## 一些重点
除开原码定义指出最高位是符号位。在反码和补码中并没有符号位的概念，他们提供的是一套计算方法，只是刚好结果是当最高位是1时为负数。

解释一个在其他文章中常见的误解，在网络上介绍负数表示法也是讲原码、反码、补码，并介绍他们几者之间的转换，这给人一种印象，他们三者是有关联的，需要一步一步的计算原码再算反码最后得到补码。他们三者完全是独立的，都是一样的作用就是在计算中表示负数。只是计算机常用的是用补码来表示而已。

补码的好处这里就不介绍，可以在网络中查阅相关资料。


## 资料
- [https://www.bilibili.com/read/cv1669932](https://www.bilibili.com/read/cv1669932)
- [https://zh.wikipedia.org/wiki/%E5%8E%9F%E7%A0%81](https://zh.wikipedia.org/wiki/%E5%8E%9F%E7%A0%81)
- [https://zh.wikipedia.org/wiki/%E5%8F%8D%E7%A0%81](https://zh.wikipedia.org/wiki/%E5%8F%8D%E7%A0%81)
- [https://zh.wikipedia.org/wiki/%E4%BA%8C%E8%A3%9C%E6%95%B8](https://zh.wikipedia.org/wiki/%E4%BA%8C%E8%A3%9C%E6%95%B8)


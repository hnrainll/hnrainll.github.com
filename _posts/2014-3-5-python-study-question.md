---
title: Python学习问题记录
author: leo
layout: post
category : python
permalink:  /python-study-question/
tags: 
  - study
  - python

---

对在Python学习中，遇到的一些问题进行记录！

<!--more-->


Update：Mar/5/2014
---
- **QUESTION: 运行.py文件时报错：`SyntaxError: Non-ASCII character '\xa3' in file`**

解决问题的网址在：[SyntaxError: Non-ASCII character '\xa3' in file when function returns '£'](http://stackoverflow.com/questions/10589620/syntaxerror-non-ascii-character-xa3-in-file-when-function-returns)

就是在.py文件最开始加上：`# -*- coding: utf-8 -*-`

在解决这个问题中感触比较深的是：其实在报错的时候在提示消息中就告诉了我们解决方式可以看哪个网站，但是我却没有去看。而是在网上搜索。就像在解决问题的网址中其他人的反问：`Did you even read the PEP you linked to? It describes what the problem is and how to fix it.`，值得我去反省！


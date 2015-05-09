---
layout: post
title: "Mac下Scheme环境搭建"
description: ""
category: sicp
tags: []
---
{% include JB/setup %}

> 以下操作基于Mac OS


##Install MIT-Scheme
在Mac上安装有两种方式：

- 通过brew安装
- 下载MIT-Scheme安装包

因为brew是Mac上非常优秀的包管理工具，常用的软件我也都会使用brew安装。但是因为通过brew 安装MIT-Scheme需要安装很多其他的管理包，所以在尝试用brew安装失败后我还是选择了通过第二种方式安装。


##安装Scheme
[http://www.gnu.org/software/mit-scheme/](http://www.gnu.org/software/mit-scheme/)

选择适合自己的版本，下载并安装Scheme包。


##Scheme配置
引用自：[https://jacksonisaac.wordpress.com/2014/03/25/installing-scheme-on-mac-os-x/](https://jacksonisaac.wordpress.com/2014/03/25/installing-scheme-on-mac-os-x/)

###Step 1
For 32-bit package:
> sudo ln -s /Applications/MIT\:GNU\ Scheme.app/Contents/Resources /usr/local/lib/mit-scheme-i386

For 64-bit package:
> sudo ln -s /Applications/MIT\:GNU\ Scheme.app/Contents/Resources /usr/local/lib/mit-scheme-x86-64

###Step 2
For 32-bit package:
> sudo ln -s /usr/local/lib/mit-scheme-i386/mit-scheme /usr/bin/scheme

For 64-bit package:
> sudo ln -s /usr/local/lib/mit-scheme-x86-64/mit-scheme /usr/bin/scheme

###Step 3
终端运行，就可以使用Scheme编程啦！
> scheme


##Scheme开发环境搭建

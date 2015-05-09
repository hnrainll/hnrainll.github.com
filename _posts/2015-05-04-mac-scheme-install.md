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
Scheme配置引用自：[https://jacksonisaac.wordpress.com/2014/03/25/installing-scheme-on-mac-os-x/](https://jacksonisaac.wordpress.com/2014/03/25/installing-scheme-on-mac-os-x/)

####Step 1
For 32-bit package:
> sudo ln -s /Applications/MIT\:GNU\ Scheme.app/Contents/Resources /usr/local/lib/mit-scheme-i386

For 64-bit package:
> sudo ln -s /Applications/MIT\:GNU\ Scheme.app/Contents/Resources /usr/local/lib/mit-scheme-x86-64

####Step 2
For 32-bit package:
> sudo ln -s /usr/local/lib/mit-scheme-i386/mit-scheme /usr/bin/scheme

For 64-bit package:
> sudo ln -s /usr/local/lib/mit-scheme-x86-64/mit-scheme /usr/bin/scheme

####Step 3
终端运行，就可以使用Scheme编程啦！
> scheme


##Scheme开发环境搭建
Scheme的开发环境大部分，使用vim和Emacs。Emacs使用的很少命令也太多，导致我放弃该环境。最初我选择了vim的环境(呵呵，当然是因为对vim比较熟悉)，但是通过几天的使用，发现其代码调试过于麻烦。导致我在思考选择其他环境。也是今天我介绍的重点:Sumline Text 2

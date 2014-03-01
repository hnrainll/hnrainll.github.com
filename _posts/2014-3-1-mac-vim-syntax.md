---
title: 让Mac中的VIM色彩斑斓
author: wenhao
layout: post
category : MAC
permalink:  /mac-vim-syntax/
tags: 
  - mac
  - vim

---

让Mac中的VIM色彩斑斓
===

让我们的vim色彩斑斓实际上就是为我们的vim添加高亮显示了。因为在Mac中vim默认是没有开启高亮显示的，所以需要我们手动的实现起配置。

<!--more-->

1. 将vim的环境文件copy到自己常用用户的主目录下
> cp /usr/share/vim/vimrc ~/.vimrc

2. 修改.vimrc文件归读写属性(非必需)
> sudo chmod 777  .vimrc


3. 在.vimrc文件最后加上
> syntax on

4. 保存退出重新打开terminal,打开一个源文件,色彩斑斓的语法加亮就出现了。

---
引用
---
- [macvim语法高亮](http://blog.csdn.net/renbaoyong/article/details/6669294)

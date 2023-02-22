---
title: 让Mac中的VIM色彩斑斓
author: Leo
layout: post
category : programme
permalink:  /mac-vim-syntax/
tags: 
  - mac
  - vim
  - computer

---

vim是在开发中常用的工具，能高亮显示文件内容就变得特别的重要了。但是vim的配置确特别复杂。这里给大家介绍一种非常简单的方式来配置vim。


1.使用开源项目vimrc
> https://github.com/amix/vimrc

其有详细的文档，这里就介绍几个常用的指令。


2.安装vimrc
> git clone --depth=1 https://github.com/amix/vimrc.git ~/.vim_runtime
>
> sh ~/.vim_runtime/install_awesome_vimrc.sh


3.升级
> cd ~/.vim_runtime
>
> git pull --rebase

---
title: Linux及MacOSX中使用zsh
author: leo
layout: post
category : OS
permalink:  /linux-macosx-shell-zsh/
tags: 
  - zsh
  - linux
  - macosx

---



[zsh](http://www.zsh.org)是另一种Shell,类似bash,tcsh等等,只是多了一些人性化的功能, ex: Tab 按两下, 会将档案、目录等变成可以选取的模式,选完后会自动补齐命令.还有错误的命令或者资料夹等等, 会询问是否打错, 自动纠正.

<!--more-->

zsh详细说明: [Zsh Workshop: Table of Contents](http://www.acm.uiuc.edu/workshops/zsh/toc.html)

上述的都不重要, 最重要的是有 [oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh) 的插件可以使用. (简单说, 若沒有 oh-my-zsh, 那 zsh 一点吸引力都没有)

oh-my-zsh 将之前配置文件, 用外挂的方式挂进去, 可以轻松的站在巨人的肩膀上. (而且 theme 有很多可以挑选)

---
将 MacOSX / Linux 用的 Shell 改用 zsh
---

###1. 安装zsh
Debian / Ubuntu  Linux 需要安裝: apt-get install zsh

Mac 预设就有 zsh 了~

安装完 zsh 后, chsh -s /bin/zsh 即可.
> **NOTES:**
> 
> chsh -s /bin/zsh # 设定为 default shell
> 
> 相关设定: .zshenv, .zprofile, .zshrc, .zlogin

###2. 安裝使用 oh-my-zsh

> cd ~/
>
> git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh
> 
> cp ~/.zshrc ~/.zshrc.orig
> 
> cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc

配置zsh时需要修改.zshrc文件。

//修改theme

>  #export ZSH_THEME="steeef"
>  
>  export ZSH_THEME="afowler"

更多的themes在.oh-my-zsh/themes中


//修改插件

> plugins=(git osx) # 啟用 git, osx 的 plugin

更多plugins可以參考~/.oh-my-zsh/plugins


###3. 中文乱码问题
在终端下输入

> vim ~/.zshrc

或者使用其他你喜欢的编辑器编辑~/.zshrc

在文件内容末端添加：
> export LC_ALL=en_US.UTF-8  
> export LANG=en_US.UTF-8

接着重启一下终端，或者输入
source ~/.zshrc

---
###其他
---
1. oh-my-zsh中不同的theme可能需要不同的font，可以在[powerline-fonts](https://github.com/Lokaltog/powerline-fonts)中下载
2. 通过远程登录zsh的服务器时，zsh中的特殊符号不能正常显示，这个问题还没有解决

---
###引用：
---
1. [MacOSX shell 改用 zsh](http://blog.longwin.com.tw/2011/10/macosx-shell-zsh-2011/)
2. [oh-my-zsh中文乱码问题](http://hearrain.com/2013/04/738)
3. [终极 Shell](http://macshuo.com/?p=676)
4. [zsh](http://www.zsh.org)
5. [oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh) 
6. [Zsh Workshop: Table of Contents](http://www.acm.uiuc.edu/workshops/zsh/toc.html)
7. [powerline-fonts](https://github.com/Lokaltog/powerline-fonts)


> Written with [LeoChin](http://leochin.com/).
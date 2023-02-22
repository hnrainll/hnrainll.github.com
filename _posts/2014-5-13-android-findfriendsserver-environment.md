---
title: FindFriendsServer服务搭建
author: Leo
layout: post
category : programme
permalink:  /android-findfriendsserver-environment/
tags: 
  - android
  - php
  - lbs
  - mqtt

---

本文介绍如何搭建FindFriendsServer(https://github.com/hnrainll/FindFriendsServer)所需的环境。


## 环境需要
Windows+Apache+PHP+MySQL(Linux环境请自行google)



## 安装顺序
1. Mysql（账号：root，密码：123456）
2. Apache
3. PHP（安装PHP时，指定Apache的安装目录）


## 测试
1. MySQL
   - 通过Console能正常登陆

2. Apache
   - 安装成功后，在浏览器中输入:localhost，可访问
    
3. PHP测试
   - PHP安装后，先重启Apache
   - 然后在apache安装目录的htdocs目录下创建文件：hello.php,并将以下代码拷贝其中，浏览器输入：localhost/hello.php.

>
```php
<?php
	echo "HelloWorld!<br>";
	phpinfo();
?>
```
   



## 还需要做的事情

1. 拷贝MySQL Server 5.5\lib\libmysql.dll文件到C:\WINDOWS\system32目录中、C:\Program Files\PHP、C:\Program Files\PHP\ext目录

2. 拷贝C:\Program Files\PHP\php5ts.dll拷贝到C:\WINDOWS\system32目录

3. 修改Apache2.2\conf\httpd.conf文件中的PHPIniDir "C:\Program Files\PHP\"为PHPIniDir "C:\Program Files\PHP”(删除PHP最后的斜杠)

修改完成后记得重启Apache。


## 步骤（前提是上面步骤都成功）

1. Apache安装目录的htdocs下创建目录:lbs，将项目的中的lbs服务器中的php源码拷贝到其中

2. 在数据库中创建表，如下：
>
```sql
create database lbsbase;
create table user_list(uid int NOT NULL AUTO_INCREMENT, username varchar(255), email varchar(255), password varchar(255), PRIMARY KEY (uid));
create table current_status(uid int, lat varchar(255), lon varchar(255), online varchar(255), ipaddress varchar(255));
```

3. 解压rsmb_1.2.0.zip文件，运行rsmb_1.2.0\windows\broker.exe

效果：在浏览器中输入localhost/lbs/registeruser.php,如果返回成功表示环境搭建成功，失败再有问题。


## 引用
Android代码地址:
- [FindFriends](https://github.com/hnrainll/FindFriends)

服务器代码地址：
- [FindFriendsServer](https://github.com/hnrainll/FindFriendsServer)

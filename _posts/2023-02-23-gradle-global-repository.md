---
layout: post
title: "Gradle全局仓库配置"
subtitle: ""
date: 2023-02-23
author: "Leo"
header-img: "img/bg-material.jpg"
permalink:  /gradle-global-repository-20230223/
category: "programme"
tags: 
  - gradle
  - java
---

本文只在MacOS中验证，其他平台注意。

编译Kafka时发现Gradle从mavenCentral仓库拉依赖包特别慢，就想着换成国内maven源。但不想修改Kafka源码相关的配置，故想到本机全局修改的方式。

现将相关修改记录如下。


# 配置如下
文件所在目录：`~/.gradle/init.gradle`
若没有`init.gradle`文件便手动创建。

详细配置：
```gradle
allprojects {
    repositories {
        maven { name "Alibaba"; url "https://maven.aliyun.com/repository/public" }        
        mavenCentral()
    }

    buildscript {
        repositories {
            maven { name "Alibaba"; url "https://maven.aliyun.com/repository/public" }
            maven { name "Alibaba-gradle-plugin"; url "https://maven.aliyun.com/repository/gradle-plugin"}
            maven { name "M2"; url 'https://plugins.gradle.org/m2/' }
        }
    }
}

```

Gradle安装相关自行搜索解决。


# 引用
- [https://developer.aliyun.com/mvn/guide][1]



[1]: https://developer.aliyun.com/mvn/guide
---
title: Java 注释类之常用元注解
author: wenhao
layout: post
category : Java
permalink:  /java-annonation-meta/
tags: 
  - interface
  - 注释类

---



自定义Java注释类时，我们使用方式如下：

	@Retention(RetentionPolicy.RUNTIME)
	@Target(ElementType.METHOD)
	class @interface Author{
		public String name();
		public String company();
	}


这次我们重点讨论修饰注解的注解，也就是我们说的元注解。

<!--more-->

---
###@Retention

注解@Retention可以用来修饰注解，是注解的注解，称为`元注解`。

Retention注解有一个属性value，是RetentionPolicy类型的，Enum RetentionPolicy是一个枚举类型，
这个枚举决定了Retention注解应该如何去保持，也可理解为Rentention 搭配 RententionPolicy使用。

RetentionPolicy有3个值：**`CLASS`**,**`RUNTIME`**,**`SOURCE`**

- 用@Retention(RetentionPolicy.CLASS)修饰的注解，表示注解的信息被保留在class文件(字节码文件)中当程序编译时，但不会被虚拟机读取在运行的时候；
- 用@Retention(RetentionPolicy.SOURCE )修饰的注解,表示注解的信息会被编译器抛弃，不会留在class文件中，注解的信息只会留在源文件中；
- 用@Retention(RetentionPolicy.RUNTIME )修饰的注解，表示注解的信息被保留在class文件(字节码文件)中当程序编译时，会被虚拟机保留在运行时，
所以他们可以用反射的方式读取。

RetentionPolicy.RUNTIME 可以让你从JVM中读取Annotation注解的信息，以便在分析程序的时候使用.

---
###@Target


注解@Target也是用来修饰注解的元注解。

它有一个属性ElementType也是枚举类型，值为：**`ANNOTATION_TYPE`**,**`CONSTRUCTOR`**,**`FIELD`**,**`LOCAL_VARIABLE`**,**`METHOD`**,**`PACKAGE`**,**`PARAMETER`**,**`TYPE`**

如@Target(ElementType.METHOD) 修饰的注解表示该注解只能用来修饰在方法上。  
其他同理。

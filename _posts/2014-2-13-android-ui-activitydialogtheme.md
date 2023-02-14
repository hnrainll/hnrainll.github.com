---
title: Android UI之实现Dialog样式的Activity
author: leo
layout: post
category : Android
permalink:  /android-ui-activitydialogtheme/
tags: 
  - Android UI
  - activity
  - Dialog

---





### 使用场合

在Android的Dialog设计当中，我们可以通过系统自带的Dialog类实现相对简单的Dialog。但是对于相对UI布局特别复杂的Dialog，使用系统自带的实现就会比较困难。所以在Android当中，为Acitivity添加了一个Dialog的样式。让我们的Activity实现Dilaog的效果，这样在复杂的布局我们都能应付了。

---

### 实现方式


Activity实现Dialog样式的原理就是给在Manifest当中为Activity添加Theme属性。

Manifest中对Activity注册如下设置：
	`<activity
		android:name="com.example.activitydialog.DialogActivity"
		android:theme="@android:style/Theme.Holo.Light.Dialog">
	</activity>`

重点语句是：`android:theme="@android:style/Theme.Holo.Light.Dialog"` 就是设置Activity为Holo风格白色的Dialog。

在Android当中为我们提供了很多风格的Dialog，大家可以在设置时通过Eclipse的补全功能进行查找。
但是要注意Holo风格的Dialog要求Android支持的最低版本为11。

---

### 其他说明


虽然实现Dialog样式的Activity的比较简单但是这里我想从Activity的生命周期方面分析Dialog样式的Activity和普通的Activity在生命周期上有何不同。

如下Activity生命周期：
![activity_lifecycle](http://developer.android.com/images/activity_lifecycle.png "activity_lifecycle")

我们常见的Activity跳转当中，是第二个Activity将第一个Activity完全覆盖让其不再可见。所以这样的跳转第一个Activity的生命周期的变化是onResume()->onPause()->onStop()。

而当第二个Activity为Dialog样式时第一个Activity的生命周期变化是：onResume()->onPause()。

也就是上图中文字说明的：`The activity is no longer visibale`当activity不再可见时才会运行到onStop()。（注意：Dialog不能让Activity的生命周期发生变化）

---

### 引用
- [http://developer.android.com/guide/topics/ui/themes.html#ApplyATheme](http://developer.android.com/guide/topics/ui/themes.html#ApplyATheme)

- 测试Demo下载地址：[http://git.oschina.net/hnrainll/ActivityDialog](http://git.oschina.net/hnrainll/ActivityDialog)
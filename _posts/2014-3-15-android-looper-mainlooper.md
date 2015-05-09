---
title: Android MainLooper的获取原理分析
author: wenhao
layout: post
category : android
permalink:  /android-looper-mainlooper/
tags: 
  - android
  - looper

---

昨天在使用Handler时，对Handler当中的Looper感兴趣。就研究了一下。网上也有很多Looper的源码分析。这里我也就不说了。

今天我要讲的是Looper当中的两个方法：`public static Looper getMainLooper()` 和 `public static Looper myLooper()`。因为好奇为什么在任何地方都能得到MainThread的Looper。

<!--more-->

---
源码分析：
---
源码地址：[Looper.java](https://android.googlesource.com/platform/frameworks/base.git/+/android-4.3_r2/core/java/android/os/Looper.java)

主要代码摘要：

```java
static final ThreadLocal<Looper> sThreadLocal = new ThreadLocal<Looper>();
private static Looper sMainLooper;  // guarded by Looper.class
public static Looper myLooper() {
	return sThreadLocal.get();
}
public static Looper getMainLooper() {
	synchronized (Looper.class) {
		return sMainLooper;
	}
}
public static void prepareMainLooper() {
	prepare(false);
	synchronized (Looper.class) {
		if (sMainLooper != null) {
			throw new IllegalStateException("The main Looper has already been prepared.");
		}
		sMainLooper = myLooper();
	}
}
```


这里有三个方法比较奇怪的就是我们会发现`sMainLooper = myLooper();`获取MainLooper尽然是通过myLooper()获取的。那岂不是获取MainLooper和myLooper一样了吗？

其实这里就是我们的关键。虽然获取MainLooper和获取myLooper都是用的同一个方法，但是只要我们保证`prepareMainLooper()`只在我们的MainThread中调用唯一的一次，那么我们的sMainLooper将会永远的保存MainThread的Looper。因为在MainThread中的myLooper就是MainLooper。

Android确实也是这样做的，在`ActivityThread.java`当中就是调用了`Looper.prepareMainLooper();`.
    public static void main(String[] args) {
        SamplingProfilerIntegration.start();

        // CloseGuard defaults to true and can be quite spammy.  We
        // disable it here, but selectively enable it later (via
        // StrictMode) on debug builds, but using DropBox, not logs.
        CloseGuard.setEnabled(false);

        Environment.initForCurrentUser();

        // Set the reporter for event logging in libcore
        EventLogger.setReporter(new EventLoggingReporter());

        Security.addProvider(new AndroidKeyStoreProvider());

        Process.setArgV0("<pre-initialized>");

        Looper.prepareMainLooper();

        ActivityThread thread = new ActivityThread();
        thread.attach(false);

        if (sMainThreadHandler == null) {
            sMainThreadHandler = thread.getHandler();
        }

        AsyncTask.init();

        if (false) {
            Looper.myLooper().setMessageLogging(new
                    LogPrinter(Log.DEBUG, "ActivityThread"));
        }

        Looper.loop();

        throw new RuntimeException("Main thread loop unexpectedly exited");
    }
}


> Written with [LeoChin](http://leochin.com/).
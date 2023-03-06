---
layout: post
date: 2023-03-02
author: Leo
header-img: "img/bg-material.jpg"
permalink: /about-java-lock-20230302/

title: "关于Java锁与同步"
category: "programme"
tags:
  - java
  - lock
  - synchronized
---

- 共享内存方式的线程安全问题产生的原因是：可见性、原子性、有序性。这是当前计算机系统软硬件所决定的。

- 解决可见性和有序性问题可以通过内存屏障。它是CPU的指令，比如：sfence、lfence、mfence，还可以通过lock实现。

- 原子性问题可以通过一些原子性的指令解决，比如CAS、TSL、lock等。

- JMM（Java内存模型）是定义一些内存使用规范，即只要实现这些规范就可以解决共享数据的线程安全问题。

- volatile修饰变量时表示变量值是易变的。它能解决可见性和有序性问题，底层是使用CPU lock指令实现内存屏障。

- UNSAFE类中的CAS方法可以解决原子性问题。

- 在编程实践中，常常说到听过“锁”解决线程安全问题。那么，锁也需要解决可见性、原子性、有序性问题。

- 最简单的“锁”实现是通过flag标志位，当flag=1则获取锁，可以执行锁定区域内的代码，当其他线程无法获取锁时可以用不同的处理方式。

- flag标志位的读写需要保证原子性。锁定区域内的代码天然具有原子性（单线程执行）。那么，在写flag时如何实现可见性？可以使用上面说的内存屏障或者上下文切换。

- Linux系统中用户态与内核态之间的切换叫做上下文切换。区分两者的原因是为了保证内核的稳定和安全。对于硬件或者操作系统内存相关的操作只能由处于内核态的程序执行。

- 上下文切换是将当前线程或者进程的状态保存起来，换成其他线程或者进程的状态。这时，需要保证这些变量的可见性。

- 常见的上下文切换场景包含：时间片切换、系统调用等。

- Linux中互斥锁mutex底层是通过futex实现，它是系统调用。它在用户态保存标志位在内核态保存队列。

- Java中锁实现通常使用synchronized或者Lock。其底层都是通过pthread_mutex_* 和 pthread_cond_* 即 互斥锁和条件变量实现。

- 无论是synchronized还是Lock实现中的AQS都是通过实现管程模型。

- 通过锁的方式实现线程安全，那么其他没有获取锁的线程可以有不同的处理方式，比如循环等待这是自旋锁，可以将等待线程放入队列中并释放这些线程的CPU。

- 所谓释放线程CPU也就是通过线程上下文切换实现，这时需要保证变量的可见性。

- 在并发编程中主要是解决两个问题：互斥与同步。比如通过ReentrantLock实现互斥，而与Condition配合实现同步。

- synchronized也能实现互斥与同步。其性能随着JVM的升级而得到提升。锁优化包含无锁、偏向锁、轻量锁、重量锁。

- ReentrantLock是通过AQS实现，AQS叫做抽象队列同步器，就是用来处理互斥时等待中的线程的问题。

- 等待中的线程会存放在队列中，并调用LockSupport.park()方法使其释放CPU。

- ReentrantLock配合Condition可实现线程同步，方法是await和signal(signalAll)。

- signal方法的实质是将Condition 条件队列中的线程放到同步队列中。也意味着调用signal时await线程并不会立刻被唤醒。

- AQS本质上维护一个变量 + 队列。

- CountDownLatch、Semaphore、CyclicBarrier都是通过AQS实现，用于不同场景下的线程同步。
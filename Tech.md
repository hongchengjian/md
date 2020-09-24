

- [线程](#%E7%BA%BF%E7%A8%8B)
  - [JAVA API\-线程状态State 枚举](#java-api-%E7%BA%BF%E7%A8%8B%E7%8A%B6%E6%80%81state-%E6%9E%9A%E4%B8%BE)
  - [线程状态流转](#%E7%BA%BF%E7%A8%8B%E7%8A%B6%E6%80%81%E6%B5%81%E8%BD%AC)
  - [线程开始](#%E7%BA%BF%E7%A8%8B%E5%BC%80%E5%A7%8B)
  - [线程结束](#%E7%BA%BF%E7%A8%8B%E7%BB%93%E6%9D%9F)
  - [Java API\-常用方法](#java-api-%E5%B8%B8%E7%94%A8%E6%96%B9%E6%B3%95)
    - [@Deprecated Thread\.stop, Thread\.suspend, Thread\.resume](#deprecated-threadstop-threadsuspend-threadresume)
    - [对象锁](#%E5%AF%B9%E8%B1%A1%E9%94%81)
      - [什么是对象锁？](#%E4%BB%80%E4%B9%88%E6%98%AF%E5%AF%B9%E8%B1%A1%E9%94%81)
    - [Object\.wait( ) 、Object\.notify( ) 、Object\.notifyAll( )](#objectwait--objectnotify--objectnotifyall-)
    - [Thread\.sleep(long) VS Object\.wait( )  VS  Object\.wait(long )](#threadsleeplong-vs-objectwait---vs--objectwaitlong-)
    - [Thread\.sleep(long)  VS Thread\.yield( )](#threadsleeplong--vs-threadyield-)
    - [判断线程有没有持有对象锁Thread\.holdsLock(obj)](#%E5%88%A4%E6%96%AD%E7%BA%BF%E7%A8%8B%E6%9C%89%E6%B2%A1%E6%9C%89%E6%8C%81%E6%9C%89%E5%AF%B9%E8%B1%A1%E9%94%81threadholdslockobj)
    - [控制线程执行顺序Thread\.join( )和多线程的无序执行](#%E6%8E%A7%E5%88%B6%E7%BA%BF%E7%A8%8B%E6%89%A7%E8%A1%8C%E9%A1%BA%E5%BA%8Fthreadjoin-%E5%92%8C%E5%A4%9A%E7%BA%BF%E7%A8%8B%E7%9A%84%E6%97%A0%E5%BA%8F%E6%89%A7%E8%A1%8C)
    - [守护线程（服务线程）setDaemon( )](#%E5%AE%88%E6%8A%A4%E7%BA%BF%E7%A8%8B%E6%9C%8D%E5%8A%A1%E7%BA%BF%E7%A8%8Bsetdaemon-)
- [线程池](#%E7%BA%BF%E7%A8%8B%E6%B1%A0)
  - [原理和流程](#%E5%8E%9F%E7%90%86%E5%92%8C%E6%B5%81%E7%A8%8B)
  - [线程池 VS new Thread](#%E7%BA%BF%E7%A8%8B%E6%B1%A0-vs-new-thread)
    - [new Thread缺陷](#new-thread%E7%BC%BA%E9%99%B7)
    - [Executors创建线程池缺陷](#executors%E5%88%9B%E5%BB%BA%E7%BA%BF%E7%A8%8B%E6%B1%A0%E7%BC%BA%E9%99%B7)
  - [Java API\-线程池 Executor实现对比](#java-api-%E7%BA%BF%E7%A8%8B%E6%B1%A0-executor%E5%AE%9E%E7%8E%B0%E5%AF%B9%E6%AF%94)
  - [正确创建线程池](#%E6%AD%A3%E7%A1%AE%E5%88%9B%E5%BB%BA%E7%BA%BF%E7%A8%8B%E6%B1%A0)
  - [线程池四要素](#%E7%BA%BF%E7%A8%8B%E6%B1%A0%E5%9B%9B%E8%A6%81%E7%B4%A0)
  - [线程池参数](#%E7%BA%BF%E7%A8%8B%E6%B1%A0%E5%8F%82%E6%95%B0)
  - [线程池参数默认值](#%E7%BA%BF%E7%A8%8B%E6%B1%A0%E5%8F%82%E6%95%B0%E9%BB%98%E8%AE%A4%E5%80%BC)
  - [线程池参数经验值设置（实际看生产机器）](#%E7%BA%BF%E7%A8%8B%E6%B1%A0%E5%8F%82%E6%95%B0%E7%BB%8F%E9%AA%8C%E5%80%BC%E8%AE%BE%E7%BD%AE%E5%AE%9E%E9%99%85%E7%9C%8B%E7%94%9F%E4%BA%A7%E6%9C%BA%E5%99%A8)
  - [验证线程池参数经验值设定效果](#%E9%AA%8C%E8%AF%81%E7%BA%BF%E7%A8%8B%E6%B1%A0%E5%8F%82%E6%95%B0%E7%BB%8F%E9%AA%8C%E5%80%BC%E8%AE%BE%E5%AE%9A%E6%95%88%E6%9E%9C)
  - [线程池拒绝策略4种与扩展](#%E7%BA%BF%E7%A8%8B%E6%B1%A0%E6%8B%92%E7%BB%9D%E7%AD%96%E7%95%A54%E7%A7%8D%E4%B8%8E%E6%89%A9%E5%B1%95)
  - [线程池自动关闭](#%E7%BA%BF%E7%A8%8B%E6%B1%A0%E8%87%AA%E5%8A%A8%E5%85%B3%E9%97%AD)
  - [线程池任务在收到某个事件后关闭其中一个线程，其他线程继续执行](#%E7%BA%BF%E7%A8%8B%E6%B1%A0%E4%BB%BB%E5%8A%A1%E5%9C%A8%E6%94%B6%E5%88%B0%E6%9F%90%E4%B8%AA%E4%BA%8B%E4%BB%B6%E5%90%8E%E5%85%B3%E9%97%AD%E5%85%B6%E4%B8%AD%E4%B8%80%E4%B8%AA%E7%BA%BF%E7%A8%8B%E5%85%B6%E4%BB%96%E7%BA%BF%E7%A8%8B%E7%BB%A7%E7%BB%AD%E6%89%A7%E8%A1%8C)
  - [线程中断响应](#%E7%BA%BF%E7%A8%8B%E4%B8%AD%E6%96%AD%E5%93%8D%E5%BA%94)
  - [思考线程池是否要关闭](#%E6%80%9D%E8%80%83%E7%BA%BF%E7%A8%8B%E6%B1%A0%E6%98%AF%E5%90%A6%E8%A6%81%E5%85%B3%E9%97%AD)
  - [线程池关闭后的影响](#%E7%BA%BF%E7%A8%8B%E6%B1%A0%E5%85%B3%E9%97%AD%E5%90%8E%E7%9A%84%E5%BD%B1%E5%93%8D)
    - [线程池关闭是否可以接受新任务？](#%E7%BA%BF%E7%A8%8B%E6%B1%A0%E5%85%B3%E9%97%AD%E6%98%AF%E5%90%A6%E5%8F%AF%E4%BB%A5%E6%8E%A5%E5%8F%97%E6%96%B0%E4%BB%BB%E5%8A%A1)
    - [等待队列里的任务是否会继续执行？正在执行 的任务是否会立即中断？](#%E7%AD%89%E5%BE%85%E9%98%9F%E5%88%97%E9%87%8C%E7%9A%84%E4%BB%BB%E5%8A%A1%E6%98%AF%E5%90%A6%E4%BC%9A%E7%BB%A7%E7%BB%AD%E6%89%A7%E8%A1%8C%E6%AD%A3%E5%9C%A8%E6%89%A7%E8%A1%8C-%E7%9A%84%E4%BB%BB%E5%8A%A1%E6%98%AF%E5%90%A6%E4%BC%9A%E7%AB%8B%E5%8D%B3%E4%B8%AD%E6%96%AD)
- [队列](#%E9%98%9F%E5%88%97)
  - [线程阻塞的两种情况](#%E7%BA%BF%E7%A8%8B%E9%98%BB%E5%A1%9E%E7%9A%84%E4%B8%A4%E7%A7%8D%E6%83%85%E5%86%B5)
  - [阻塞队列BlockingQueue](#%E9%98%BB%E5%A1%9E%E9%98%9F%E5%88%97blockingqueue)
    - [demo 花牌游戏 Epam面试手写代码](#demo-%E8%8A%B1%E7%89%8C%E6%B8%B8%E6%88%8F-epam%E9%9D%A2%E8%AF%95%E6%89%8B%E5%86%99%E4%BB%A3%E7%A0%81)
    - [Java API\-常用方法](#java-api-%E5%B8%B8%E7%94%A8%E6%96%B9%E6%B3%95-1)
      - [放](#%E6%94%BE)
      - [取](#%E5%8F%96)
  - [ArrayBlockingQueue（FIFO）](#arrayblockingqueuefifo)
  - [LinkedBlockingQueue（newFixedThreadPool） VS LinkedTransferQueue VS LinkedBlockingDeque](#linkedblockingqueuenewfixedthreadpool-vs-linkedtransferqueue-vs-linkedblockingdeque)
  - [PriorityBlockingQueue](#priorityblockingqueue)
  - [DelayQueue（缓存失效、定时任务）](#delayqueue%E7%BC%93%E5%AD%98%E5%A4%B1%E6%95%88%E5%AE%9A%E6%97%B6%E4%BB%BB%E5%8A%A1)
  - [SynchronousQueue（不存储数据、可传递数据）](#synchronousqueue%E4%B8%8D%E5%AD%98%E5%82%A8%E6%95%B0%E6%8D%AE%E5%8F%AF%E4%BC%A0%E9%80%92%E6%95%B0%E6%8D%AE)
- [线程安全](#%E7%BA%BF%E7%A8%8B%E5%AE%89%E5%85%A8)
  - [有状态 VS 无状态](#%E6%9C%89%E7%8A%B6%E6%80%81-vs-%E6%97%A0%E7%8A%B6%E6%80%81)
- [线程同步 VS 线程异步](#%E7%BA%BF%E7%A8%8B%E5%90%8C%E6%AD%A5-vs-%E7%BA%BF%E7%A8%8B%E5%BC%82%E6%AD%A5)
  - [同步 VS 异步](#%E5%90%8C%E6%AD%A5-vs-%E5%BC%82%E6%AD%A5)
  - [同步使用场景](#%E5%90%8C%E6%AD%A5%E4%BD%BF%E7%94%A8%E5%9C%BA%E6%99%AF)
  - [异步使用场景](#%E5%BC%82%E6%AD%A5%E4%BD%BF%E7%94%A8%E5%9C%BA%E6%99%AF)
- [Java API\-线程同步的方法](#java-api-%E7%BA%BF%E7%A8%8B%E5%90%8C%E6%AD%A5%E7%9A%84%E6%96%B9%E6%B3%95)
- [对象头Mark Word](#%E5%AF%B9%E8%B1%A1%E5%A4%B4mark-word)
- [64位虚拟机对象头存储](#64%E4%BD%8D%E8%99%9A%E6%8B%9F%E6%9C%BA%E5%AF%B9%E8%B1%A1%E5%A4%B4%E5%AD%98%E5%82%A8)
- [Java API\-多线程同步5种方式](#java-api-%E5%A4%9A%E7%BA%BF%E7%A8%8B%E5%90%8C%E6%AD%A55%E7%A7%8D%E6%96%B9%E5%BC%8F)
  - [synchronized原理图](#synchronized%E5%8E%9F%E7%90%86%E5%9B%BE)
  - [1\.synchronized(this)](#1synchronizedthis)
  - [2\.synchronized method](#2synchronized-method)
    - [synchronized method == synchronized(this)](#synchronized-method--synchronizedthis)
      - [synchronized(this)  插入monitorenter、monitorexit](#synchronizedthis--%E6%8F%92%E5%85%A5monitorentermonitorexit)
      - [synchronized method  flags:  ACC\_SYNCHRONIZED，并没有插入monitorenter、monitorexit](#synchronized-method--flags--acc_synchronized%E5%B9%B6%E6%B2%A1%E6%9C%89%E6%8F%92%E5%85%A5monitorentermonitorexit)
    - [synchronized static method == synchronized(obj)](#synchronized-static-method--synchronizedobj)
    - [synchronized(obj) VS synchronized method](#synchronizedobj-vs-synchronized-method)
  - [3\.volatile](#3volatile)
    - [特点](#%E7%89%B9%E7%82%B9)
    - [volatile不保证原子性原因](#volatile%E4%B8%8D%E4%BF%9D%E8%AF%81%E5%8E%9F%E5%AD%90%E6%80%A7%E5%8E%9F%E5%9B%A0)
    - [多线程可见性](#%E5%A4%9A%E7%BA%BF%E7%A8%8B%E5%8F%AF%E8%A7%81%E6%80%A7)
      - [Java内存模型](#java%E5%86%85%E5%AD%98%E6%A8%A1%E5%9E%8B)
      - [主内存 VS 工作内存](#%E4%B8%BB%E5%86%85%E5%AD%98-vs-%E5%B7%A5%E4%BD%9C%E5%86%85%E5%AD%98)
      - [JVM规范定义线程对内存交互操作8个](#jvm%E8%A7%84%E8%8C%83%E5%AE%9A%E4%B9%89%E7%BA%BF%E7%A8%8B%E5%AF%B9%E5%86%85%E5%AD%98%E4%BA%A4%E4%BA%92%E6%93%8D%E4%BD%9C8%E4%B8%AA)
      - [可见性Copy过程](#%E5%8F%AF%E8%A7%81%E6%80%A7copy%E8%BF%87%E7%A8%8B)
      - [8个Happen\-Before机制](#8%E4%B8%AAhappen-before%E6%9C%BA%E5%88%B6)
    - [volatile使用场景](#volatile%E4%BD%BF%E7%94%A8%E5%9C%BA%E6%99%AF)
  - [4\.ReentrantLock](#4reentrantlock)
    - [ReentrantLock VS synchronized](#reentrantlock-vs-synchronized)
    - [CAS](#cas)
    - [AQS](#aqs)
  - [5\. ThreadLocal](#5-threadlocal)
    - [threadLocal为什么用它？](#threadlocal%E4%B8%BA%E4%BB%80%E4%B9%88%E7%94%A8%E5%AE%83)
    - [ThreadLocal主要方法](#threadlocal%E4%B8%BB%E8%A6%81%E6%96%B9%E6%B3%95)
    - [为什么是弱引用？而不是强引用？](#%E4%B8%BA%E4%BB%80%E4%B9%88%E6%98%AF%E5%BC%B1%E5%BC%95%E7%94%A8%E8%80%8C%E4%B8%8D%E6%98%AF%E5%BC%BA%E5%BC%95%E7%94%A8)
    - [为什么不用new，用threadlocal？](#%E4%B8%BA%E4%BB%80%E4%B9%88%E4%B8%8D%E7%94%A8new%E7%94%A8threadlocal)
    - [ThreadLocal使用上问题](#threadlocal%E4%BD%BF%E7%94%A8%E4%B8%8A%E9%97%AE%E9%A2%98)
    - [demo](#demo)
    - [InheritableThreadLocal 实现父线程到子线程的值传递原理](#inheritablethreadlocal-%E5%AE%9E%E7%8E%B0%E7%88%B6%E7%BA%BF%E7%A8%8B%E5%88%B0%E5%AD%90%E7%BA%BF%E7%A8%8B%E7%9A%84%E5%80%BC%E4%BC%A0%E9%80%92%E5%8E%9F%E7%90%86)
- [线程切换](#%E7%BA%BF%E7%A8%8B%E5%88%87%E6%8D%A2)
  - [什么是用户态？什么是核心态？](#%E4%BB%80%E4%B9%88%E6%98%AF%E7%94%A8%E6%88%B7%E6%80%81%E4%BB%80%E4%B9%88%E6%98%AF%E6%A0%B8%E5%BF%83%E6%80%81)
  - [上下文](#%E4%B8%8A%E4%B8%8B%E6%96%87)
  - [上下文切换 Context Switch](#%E4%B8%8A%E4%B8%8B%E6%96%87%E5%88%87%E6%8D%A2-context-switch)
  - [上下文切换发生场景](#%E4%B8%8A%E4%B8%8B%E6%96%87%E5%88%87%E6%8D%A2%E5%8F%91%E7%94%9F%E5%9C%BA%E6%99%AF)
  - [自愿上下文切换cswch  VS 非自愿上下文切换nvcswch](#%E8%87%AA%E6%84%BF%E4%B8%8A%E4%B8%8B%E6%96%87%E5%88%87%E6%8D%A2cswch--vs-%E9%9D%9E%E8%87%AA%E6%84%BF%E4%B8%8A%E4%B8%8B%E6%96%87%E5%88%87%E6%8D%A2nvcswch)
  - [Linux查看系统上下文切换](#linux%E6%9F%A5%E7%9C%8B%E7%B3%BB%E7%BB%9F%E4%B8%8A%E4%B8%8B%E6%96%87%E5%88%87%E6%8D%A2)
  - [Linux查看某个进程详细情况](#linux%E6%9F%A5%E7%9C%8B%E6%9F%90%E4%B8%AA%E8%BF%9B%E7%A8%8B%E8%AF%A6%E7%BB%86%E6%83%85%E5%86%B5)
- [多线程](#%E5%A4%9A%E7%BA%BF%E7%A8%8B)
  - [多线程效果](#%E5%A4%9A%E7%BA%BF%E7%A8%8B%E6%95%88%E6%9E%9C)
    - [多线程计数器](#%E5%A4%9A%E7%BA%BF%E7%A8%8B%E8%AE%A1%E6%95%B0%E5%99%A8)
    - [所有线程任务都执行完才进行下一步](#%E6%89%80%E6%9C%89%E7%BA%BF%E7%A8%8B%E4%BB%BB%E5%8A%A1%E9%83%BD%E6%89%A7%E8%A1%8C%E5%AE%8C%E6%89%8D%E8%BF%9B%E8%A1%8C%E4%B8%8B%E4%B8%80%E6%AD%A5)
    - [多线程数量不超过CPU核数](#%E5%A4%9A%E7%BA%BF%E7%A8%8B%E6%95%B0%E9%87%8F%E4%B8%8D%E8%B6%85%E8%BF%87cpu%E6%A0%B8%E6%95%B0)
- [死锁](#%E6%AD%BB%E9%94%81)
  - [OS\-死锁条件](#os-%E6%AD%BB%E9%94%81%E6%9D%A1%E4%BB%B6)
  - [理论\-死锁解决方案](#%E7%90%86%E8%AE%BA-%E6%AD%BB%E9%94%81%E8%A7%A3%E5%86%B3%E6%96%B9%E6%A1%88)
    - [死锁预防(严格破坏OS\-死锁条件四个条件之一)](#%E6%AD%BB%E9%94%81%E9%A2%84%E9%98%B2%E4%B8%A5%E6%A0%BC%E7%A0%B4%E5%9D%8Fos-%E6%AD%BB%E9%94%81%E6%9D%A1%E4%BB%B6%E5%9B%9B%E4%B8%AA%E6%9D%A1%E4%BB%B6%E4%B9%8B%E4%B8%80)
    - [死锁避免(死锁避免比死锁预防允许更多的并发)](#%E6%AD%BB%E9%94%81%E9%81%BF%E5%85%8D%E6%AD%BB%E9%94%81%E9%81%BF%E5%85%8D%E6%AF%94%E6%AD%BB%E9%94%81%E9%A2%84%E9%98%B2%E5%85%81%E8%AE%B8%E6%9B%B4%E5%A4%9A%E7%9A%84%E5%B9%B6%E5%8F%91)
    - [死锁避免算法](#%E6%AD%BB%E9%94%81%E9%81%BF%E5%85%8D%E7%AE%97%E6%B3%95)
      - [进程启动拒绝](#%E8%BF%9B%E7%A8%8B%E5%90%AF%E5%8A%A8%E6%8B%92%E7%BB%9D)
      - [资源分配拒绝(银行家算法)](#%E8%B5%84%E6%BA%90%E5%88%86%E9%85%8D%E6%8B%92%E7%BB%9D%E9%93%B6%E8%A1%8C%E5%AE%B6%E7%AE%97%E6%B3%95)
    - [死锁检测](#%E6%AD%BB%E9%94%81%E6%A3%80%E6%B5%8B)
- [锁](#%E9%94%81)
  - [乐观锁 VS 悲观锁](#%E4%B9%90%E8%A7%82%E9%94%81-vs-%E6%82%B2%E8%A7%82%E9%94%81)
  - [公平锁 VS 非公平锁](#%E5%85%AC%E5%B9%B3%E9%94%81-vs-%E9%9D%9E%E5%85%AC%E5%B9%B3%E9%94%81)
  - [可重入锁 VS 非可重入锁](#%E5%8F%AF%E9%87%8D%E5%85%A5%E9%94%81-vs-%E9%9D%9E%E5%8F%AF%E9%87%8D%E5%85%A5%E9%94%81)
  - [独享锁(互斥锁，独占锁，写锁， 排它锁EXCLUSIVE，一般是悲观锁) VS 共享锁SHARED(读锁，一般是乐观锁)](#%E7%8B%AC%E4%BA%AB%E9%94%81%E4%BA%92%E6%96%A5%E9%94%81%E7%8B%AC%E5%8D%A0%E9%94%81%E5%86%99%E9%94%81-%E6%8E%92%E5%AE%83%E9%94%81exclusive%E4%B8%80%E8%88%AC%E6%98%AF%E6%82%B2%E8%A7%82%E9%94%81-vs-%E5%85%B1%E4%BA%AB%E9%94%81shared%E8%AF%BB%E9%94%81%E4%B8%80%E8%88%AC%E6%98%AF%E4%B9%90%E8%A7%82%E9%94%81)
  - [读写锁](#%E8%AF%BB%E5%86%99%E9%94%81)
  - [分段锁Segment](#%E5%88%86%E6%AE%B5%E9%94%81segment)
  - [自旋锁](#%E8%87%AA%E6%97%8B%E9%94%81)
    - [Q：自旋怎么实现？](#q%E8%87%AA%E6%97%8B%E6%80%8E%E4%B9%88%E5%AE%9E%E7%8E%B0)
  - [偏向锁](#%E5%81%8F%E5%90%91%E9%94%81)
    - [为什么要偏向锁？](#%E4%B8%BA%E4%BB%80%E4%B9%88%E8%A6%81%E5%81%8F%E5%90%91%E9%94%81)
    - [JVM偏向锁相关命令](#jvm%E5%81%8F%E5%90%91%E9%94%81%E7%9B%B8%E5%85%B3%E5%91%BD%E4%BB%A4)
- [锁优化](#%E9%94%81%E4%BC%98%E5%8C%96)
  - [锁膨胀(锁升级)(锁晋升)](#%E9%94%81%E8%86%A8%E8%83%80%E9%94%81%E5%8D%87%E7%BA%A7%E9%94%81%E6%99%8B%E5%8D%87)
    - [64 Bit MarkWord](#64-bit-markword)
    - [锁升级路线(单向)](#%E9%94%81%E5%8D%87%E7%BA%A7%E8%B7%AF%E7%BA%BF%E5%8D%95%E5%90%91)
    - [为什么引入轻量级锁？](#%E4%B8%BA%E4%BB%80%E4%B9%88%E5%BC%95%E5%85%A5%E8%BD%BB%E9%87%8F%E7%BA%A7%E9%94%81)
    - [偏向锁升级轻量级锁](#%E5%81%8F%E5%90%91%E9%94%81%E5%8D%87%E7%BA%A7%E8%BD%BB%E9%87%8F%E7%BA%A7%E9%94%81)
    - [轻量级锁升级重量级锁](#%E8%BD%BB%E9%87%8F%E7%BA%A7%E9%94%81%E5%8D%87%E7%BA%A7%E9%87%8D%E9%87%8F%E7%BA%A7%E9%94%81)
    - [重量级锁 VS 轻量级锁](#%E9%87%8D%E9%87%8F%E7%BA%A7%E9%94%81-vs-%E8%BD%BB%E9%87%8F%E7%BA%A7%E9%94%81)
    - [重量级锁重在哪里？](#%E9%87%8D%E9%87%8F%E7%BA%A7%E9%94%81%E9%87%8D%E5%9C%A8%E5%93%AA%E9%87%8C)
    - [偏向锁 VS 轻量级锁  VS 重量级锁](#%E5%81%8F%E5%90%91%E9%94%81-vs-%E8%BD%BB%E9%87%8F%E7%BA%A7%E9%94%81--vs-%E9%87%8D%E9%87%8F%E7%BA%A7%E9%94%81)
      - [响应速度 VS 吞吐量](#%E5%93%8D%E5%BA%94%E9%80%9F%E5%BA%A6-vs-%E5%90%9E%E5%90%90%E9%87%8F)
    - [锁可以升级不可以降级](#%E9%94%81%E5%8F%AF%E4%BB%A5%E5%8D%87%E7%BA%A7%E4%B8%8D%E5%8F%AF%E4%BB%A5%E9%99%8D%E7%BA%A7)
    - [JDK 1\.6 synchronized是重量级锁](#jdk-16-synchronized%E6%98%AF%E9%87%8D%E9%87%8F%E7%BA%A7%E9%94%81)
    - [JDK1\.8 synchronized 默认是轻量级锁，锁升级：偏向锁\-&gt;轻量级锁\-&gt;重量级锁](#jdk18-synchronized-%E9%BB%98%E8%AE%A4%E6%98%AF%E8%BD%BB%E9%87%8F%E7%BA%A7%E9%94%81%E9%94%81%E5%8D%87%E7%BA%A7%E5%81%8F%E5%90%91%E9%94%81-%E8%BD%BB%E9%87%8F%E7%BA%A7%E9%94%81-%E9%87%8D%E9%87%8F%E7%BA%A7%E9%94%81)
  - [减少锁持有时间](#%E5%87%8F%E5%B0%91%E9%94%81%E6%8C%81%E6%9C%89%E6%97%B6%E9%97%B4)
  - [减少锁粒度](#%E5%87%8F%E5%B0%91%E9%94%81%E7%B2%92%E5%BA%A6)
  - [锁消除 &gt; JDK 1\.5](#%E9%94%81%E6%B6%88%E9%99%A4--jdk-15)
  - [锁粗化](#%E9%94%81%E7%B2%97%E5%8C%96)
  - [锁分离](#%E9%94%81%E5%88%86%E7%A6%BB)
  - [锁续约](#%E9%94%81%E7%BB%AD%E7%BA%A6)
- [Redis](#redis)
  - [简介](#%E7%AE%80%E4%BB%8B)
  - [原理](#%E5%8E%9F%E7%90%86)
    - [Redis epoll](#redis-epoll)
    - [epoll指令](#epoll%E6%8C%87%E4%BB%A4)
    - [FD](#fd)
    - [epoll VS select/poll](#epoll-vs-selectpoll)
  - [场景](#%E5%9C%BA%E6%99%AF)
  - [心得](#%E5%BF%83%E5%BE%97)
  - [集群模式](#%E9%9B%86%E7%BE%A4%E6%A8%A1%E5%BC%8F)
    - [(1)主从](#1%E4%B8%BB%E4%BB%8E)
    - [(2)哨兵](#2%E5%93%A8%E5%85%B5)
    - [(2)哨兵](#2%E5%93%A8%E5%85%B5-1)
    - [Redis Cluster 去中心化分片集群](#redis-cluster-%E5%8E%BB%E4%B8%AD%E5%BF%83%E5%8C%96%E5%88%86%E7%89%87%E9%9B%86%E7%BE%A4)
      - [Redis Cluster VS 传统Redis集群](#redis-cluster-vs-%E4%BC%A0%E7%BB%9Fredis%E9%9B%86%E7%BE%A4)
      - [搭建](#%E6%90%AD%E5%BB%BA)
  - [数据结构和命令](#%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84%E5%92%8C%E5%91%BD%E4%BB%A4)
    - [String](#string)
      - [Jedis PIPELINE](#jedis-pipeline)
    - [Hash](#hash)
    - [List](#list)
    - [Set](#set)
    - [ZSet](#zset)
    - [其他](#%E5%85%B6%E4%BB%96)
    - [补充其他数据结构](#%E8%A1%A5%E5%85%85%E5%85%B6%E4%BB%96%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84)
  - [Redis扩容和缩容](#redis%E6%89%A9%E5%AE%B9%E5%92%8C%E7%BC%A9%E5%AE%B9)
  - [缓存一致性](#%E7%BC%93%E5%AD%98%E4%B8%80%E8%87%B4%E6%80%A7)
    - [Scenario](#scenario)
    - [A\.外部依赖](#a%E5%A4%96%E9%83%A8%E4%BE%9D%E8%B5%96)
    - [B\.缓存和DB一致性](#b%E7%BC%93%E5%AD%98%E5%92%8Cdb%E4%B8%80%E8%87%B4%E6%80%A7)
      - [问题(1)先写缓存，后写DB](#%E9%97%AE%E9%A2%981%E5%85%88%E5%86%99%E7%BC%93%E5%AD%98%E5%90%8E%E5%86%99db)
      - [问题(2)若先写DB，后写缓存](#%E9%97%AE%E9%A2%982%E8%8B%A5%E5%85%88%E5%86%99db%E5%90%8E%E5%86%99%E7%BC%93%E5%AD%98)
      - [解决方案\-读写分离\+状态机（注意顺序）](#%E8%A7%A3%E5%86%B3%E6%96%B9%E6%A1%88-%E8%AF%BB%E5%86%99%E5%88%86%E7%A6%BB%E7%8A%B6%E6%80%81%E6%9C%BA%E6%B3%A8%E6%84%8F%E9%A1%BA%E5%BA%8F)
      - [补充：数据库发生变化，如何及时更新缓存](#%E8%A1%A5%E5%85%85%E6%95%B0%E6%8D%AE%E5%BA%93%E5%8F%91%E7%94%9F%E5%8F%98%E5%8C%96%E5%A6%82%E4%BD%95%E5%8F%8A%E6%97%B6%E6%9B%B4%E6%96%B0%E7%BC%93%E5%AD%98)
  - [缓存失效策略](#%E7%BC%93%E5%AD%98%E5%A4%B1%E6%95%88%E7%AD%96%E7%95%A5)
    - [定时删除（内存友好）](#%E5%AE%9A%E6%97%B6%E5%88%A0%E9%99%A4%E5%86%85%E5%AD%98%E5%8F%8B%E5%A5%BD)
    - [惰性删除（CPU友好）](#%E6%83%B0%E6%80%A7%E5%88%A0%E9%99%A4cpu%E5%8F%8B%E5%A5%BD)
    - [缓存命中率](#%E7%BC%93%E5%AD%98%E5%91%BD%E4%B8%AD%E7%8E%87)
  - [缓存雪崩](#%E7%BC%93%E5%AD%98%E9%9B%AA%E5%B4%A9)
  - [缓存降级](#%E7%BC%93%E5%AD%98%E9%99%8D%E7%BA%A7)
  - [缓存穿透](#%E7%BC%93%E5%AD%98%E7%A9%BF%E9%80%8F)
  - [缓存预热](#%E7%BC%93%E5%AD%98%E9%A2%84%E7%83%AD)
  - [事务](#%E4%BA%8B%E5%8A%A1)
  - [持久化AOF和RDB](#%E6%8C%81%E4%B9%85%E5%8C%96aof%E5%92%8Crdb)
    - [选型](#%E9%80%89%E5%9E%8B)
  - [问题集](#%E9%97%AE%E9%A2%98%E9%9B%86)
    - [Redis单个Key超过512M？](#redis%E5%8D%95%E4%B8%AAkey%E8%B6%85%E8%BF%87512m)
    - [为什么RedisCluster有16384个槽？](#%E4%B8%BA%E4%BB%80%E4%B9%88rediscluster%E6%9C%8916384%E4%B8%AA%E6%A7%BD)
- [分布式锁](#%E5%88%86%E5%B8%83%E5%BC%8F%E9%94%81)
  - [加锁对象](#%E5%8A%A0%E9%94%81%E5%AF%B9%E8%B1%A1)
  - [场景](#%E5%9C%BA%E6%99%AF-1)
  - [Redis](#redis-1)
  - [ZooKeeper](#zookeeper)
  - [数据库](#%E6%95%B0%E6%8D%AE%E5%BA%93)
  - [Redis分布式锁问题](#redis%E5%88%86%E5%B8%83%E5%BC%8F%E9%94%81%E9%97%AE%E9%A2%98)
    - [（1）锁未被释放](#1%E9%94%81%E6%9C%AA%E8%A2%AB%E9%87%8A%E6%94%BE)
    - [（2）B的锁被A释放](#2b%E7%9A%84%E9%94%81%E8%A2%ABa%E9%87%8A%E6%94%BE)
    - [（3）获取锁等待的时间远超过数据库事务超时时间](#3%E8%8E%B7%E5%8F%96%E9%94%81%E7%AD%89%E5%BE%85%E7%9A%84%E6%97%B6%E9%97%B4%E8%BF%9C%E8%B6%85%E8%BF%87%E6%95%B0%E6%8D%AE%E5%BA%93%E4%BA%8B%E5%8A%A1%E8%B6%85%E6%97%B6%E6%97%B6%E9%97%B4)
    - [（4）锁过期expire时间续约](#4%E9%94%81%E8%BF%87%E6%9C%9Fexpire%E6%97%B6%E9%97%B4%E7%BB%AD%E7%BA%A6)
- [云](#%E4%BA%91)
  - [云存储公司](#%E4%BA%91%E5%AD%98%E5%82%A8%E5%85%AC%E5%8F%B8)
  - [云平台](#%E4%BA%91%E5%B9%B3%E5%8F%B0)
  - [云虚拟化](#%E4%BA%91%E8%99%9A%E6%8B%9F%E5%8C%96)
  - [云原生](#%E4%BA%91%E5%8E%9F%E7%94%9F)
    - [AliYun组件](#aliyun%E7%BB%84%E4%BB%B6)
    - [AWS组件](#aws%E7%BB%84%E4%BB%B6)
- [微服务](#%E5%BE%AE%E6%9C%8D%E5%8A%A1)
  - [基础框架](#%E5%9F%BA%E7%A1%80%E6%A1%86%E6%9E%B6)
  - [协议](#%E5%8D%8F%E8%AE%AE)
  - [原则](#%E5%8E%9F%E5%88%99)
  - [模式](#%E6%A8%A1%E5%BC%8F)
  - [注解](#%E6%B3%A8%E8%A7%A3)
    - [Spring Cloud Commons(扩展核心)](#spring-cloud-commons%E6%89%A9%E5%B1%95%E6%A0%B8%E5%BF%83)
  - [分布式注册中心](#%E5%88%86%E5%B8%83%E5%BC%8F%E6%B3%A8%E5%86%8C%E4%B8%AD%E5%BF%83)
    - [心跳监测](#%E5%BF%83%E8%B7%B3%E7%9B%91%E6%B5%8B)
    - [为什么需自我保护？](#%E4%B8%BA%E4%BB%80%E4%B9%88%E9%9C%80%E8%87%AA%E6%88%91%E4%BF%9D%E6%8A%A4)
  - [分布式监控中心](#%E5%88%86%E5%B8%83%E5%BC%8F%E7%9B%91%E6%8E%A7%E4%B8%AD%E5%BF%83)
    - [分布式调用链](#%E5%88%86%E5%B8%83%E5%BC%8F%E8%B0%83%E7%94%A8%E9%93%BE)
    - [推 VS 拉](#%E6%8E%A8-vs-%E6%8B%89)
    - [Skywalking\-吴晟  chéng VS Pinpoint 韩国](#skywalking-%E5%90%B4%E6%99%9F--ch%C3%A9ng-vs-pinpoint-%E9%9F%A9%E5%9B%BD)
    - [Metrics](#metrics)
      - [5种基本度量](#5%E7%A7%8D%E5%9F%BA%E6%9C%AC%E5%BA%A6%E9%87%8F)
  - [分布式日志系统](#%E5%88%86%E5%B8%83%E5%BC%8F%E6%97%A5%E5%BF%97%E7%B3%BB%E7%BB%9F)
  - [分布式配置中心](#%E5%88%86%E5%B8%83%E5%BC%8F%E9%85%8D%E7%BD%AE%E4%B8%AD%E5%BF%83)
  - [分布式网关](#%E5%88%86%E5%B8%83%E5%BC%8F%E7%BD%91%E5%85%B3)
  - [分布式事务](#%E5%88%86%E5%B8%83%E5%BC%8F%E4%BA%8B%E5%8A%A1)
  - [分布式定时任务调度和管理](#%E5%88%86%E5%B8%83%E5%BC%8F%E5%AE%9A%E6%97%B6%E4%BB%BB%E5%8A%A1%E8%B0%83%E5%BA%A6%E5%92%8C%E7%AE%A1%E7%90%86)
    - [XXL\-Job](#xxl-job)
    - [设计一个调度中心要素](#%E8%AE%BE%E8%AE%A1%E4%B8%80%E4%B8%AA%E8%B0%83%E5%BA%A6%E4%B8%AD%E5%BF%83%E8%A6%81%E7%B4%A0)
  - [分布式限流熔断降级](#%E5%88%86%E5%B8%83%E5%BC%8F%E9%99%90%E6%B5%81%E7%86%94%E6%96%AD%E9%99%8D%E7%BA%A7)
  - [分布式服务权限控制系统](#%E5%88%86%E5%B8%83%E5%BC%8F%E6%9C%8D%E5%8A%A1%E6%9D%83%E9%99%90%E6%8E%A7%E5%88%B6%E7%B3%BB%E7%BB%9F)
  - [分布式服务和系统诊断](#%E5%88%86%E5%B8%83%E5%BC%8F%E6%9C%8D%E5%8A%A1%E5%92%8C%E7%B3%BB%E7%BB%9F%E8%AF%8A%E6%96%AD)
  - [分布式流程和服务编排](#%E5%88%86%E5%B8%83%E5%BC%8F%E6%B5%81%E7%A8%8B%E5%92%8C%E6%9C%8D%E5%8A%A1%E7%BC%96%E6%8E%92)
  - [分布式锁](#%E5%88%86%E5%B8%83%E5%BC%8F%E9%94%81-1)
  - [分布式压测平台](#%E5%88%86%E5%B8%83%E5%BC%8F%E5%8E%8B%E6%B5%8B%E5%B9%B3%E5%8F%B0)
  - [分布式全局主键系统](#%E5%88%86%E5%B8%83%E5%BC%8F%E5%85%A8%E5%B1%80%E4%B8%BB%E9%94%AE%E7%B3%BB%E7%BB%9F)
  - [分布式自动化测试分布式自动化API文档](#%E5%88%86%E5%B8%83%E5%BC%8F%E8%87%AA%E5%8A%A8%E5%8C%96%E6%B5%8B%E8%AF%95%E5%88%86%E5%B8%83%E5%BC%8F%E8%87%AA%E5%8A%A8%E5%8C%96api%E6%96%87%E6%A1%A3)
  - [分布式分库分表中间件](#%E5%88%86%E5%B8%83%E5%BC%8F%E5%88%86%E5%BA%93%E5%88%86%E8%A1%A8%E4%B8%AD%E9%97%B4%E4%BB%B6)
  - [分布式消息队列中间件](#%E5%88%86%E5%B8%83%E5%BC%8F%E6%B6%88%E6%81%AF%E9%98%9F%E5%88%97%E4%B8%AD%E9%97%B4%E4%BB%B6)
  - [分布式缓存](#%E5%88%86%E5%B8%83%E5%BC%8F%E7%BC%93%E5%AD%98)
  - [分布式数据库分析诊断系统](#%E5%88%86%E5%B8%83%E5%BC%8F%E6%95%B0%E6%8D%AE%E5%BA%93%E5%88%86%E6%9E%90%E8%AF%8A%E6%96%AD%E7%B3%BB%E7%BB%9F)
  - [分布式自动化数据库脚本升级](#%E5%88%86%E5%B8%83%E5%BC%8F%E8%87%AA%E5%8A%A8%E5%8C%96%E6%95%B0%E6%8D%AE%E5%BA%93%E8%84%9A%E6%9C%AC%E5%8D%87%E7%BA%A7)
  - [运维发布](#%E8%BF%90%E7%BB%B4%E5%8F%91%E5%B8%83)
  - [大数据](#%E5%A4%A7%E6%95%B0%E6%8D%AE)
    - [Spark](#spark)
    - [Flink](#flink)
  - [限流](#%E9%99%90%E6%B5%81)
    - [Scenario](#scenario-1)
    - [应用级限流](#%E5%BA%94%E7%94%A8%E7%BA%A7%E9%99%90%E6%B5%81)
    - [细粒度](#%E7%BB%86%E7%B2%92%E5%BA%A6)
    - [Redis限流](#redis%E9%99%90%E6%B5%81)
    - [Token Bucket 令牌桶](#token-bucket-%E4%BB%A4%E7%89%8C%E6%A1%B6)
    - [Leaky Bucket 漏桶](#leaky-bucket-%E6%BC%8F%E6%A1%B6)
    - [Fix Window Counter 固定窗口计数](#fix-window-counter-%E5%9B%BA%E5%AE%9A%E7%AA%97%E5%8F%A3%E8%AE%A1%E6%95%B0)
    - [Sliding Window Counter 滑动窗口计数](#sliding-window-counter-%E6%BB%91%E5%8A%A8%E7%AA%97%E5%8F%A3%E8%AE%A1%E6%95%B0)
  - [熔断](#%E7%86%94%E6%96%AD)
    - [Scenario](#scenario-2)
    - [Sentinel VS Hystrix](#sentinel-vs-hystrix)
  - [降级](#%E9%99%8D%E7%BA%A7)
    - [Scenario](#scenario-3)
  - [负载均衡](#%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1)
- [设计Factor](#%E8%AE%BE%E8%AE%A1factor)
  - [接口设计](#%E6%8E%A5%E5%8F%A3%E8%AE%BE%E8%AE%A1)
  - [存储比较](#%E5%AD%98%E5%82%A8%E6%AF%94%E8%BE%83)
  - [SOLID原则](#solid%E5%8E%9F%E5%88%99)
    - [Open Closed Principle 开闭原则](#open-closed-principle-%E5%BC%80%E9%97%AD%E5%8E%9F%E5%88%99)
    - [Liskov Substitution Principle](#liskov-substitution-principle)
- [Spring](#spring)
  - [SpringMVC执行流程](#springmvc%E6%89%A7%E8%A1%8C%E6%B5%81%E7%A8%8B)
  - [IOC容器的生命周期](#ioc%E5%AE%B9%E5%99%A8%E7%9A%84%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F)
  - [AOP](#aop)
    - [AOP原理](#aop%E5%8E%9F%E7%90%86)
    - [AOP可以切final方法？](#aop%E5%8F%AF%E4%BB%A5%E5%88%87final%E6%96%B9%E6%B3%95)
    - [AOP不能切Private方法原理？](#aop%E4%B8%8D%E8%83%BD%E5%88%87private%E6%96%B9%E6%B3%95%E5%8E%9F%E7%90%86)
    - [动态代理两种实现方式适用场景？](#%E5%8A%A8%E6%80%81%E4%BB%A3%E7%90%86%E4%B8%A4%E7%A7%8D%E5%AE%9E%E7%8E%B0%E6%96%B9%E5%BC%8F%E9%80%82%E7%94%A8%E5%9C%BA%E6%99%AF)
  - [Rest服务](#rest%E6%9C%8D%E5%8A%A1)
    - [GrapHQL VS Rest](#graphql-vs-rest)
    - [方法传参注解](#%E6%96%B9%E6%B3%95%E4%BC%A0%E5%8F%82%E6%B3%A8%E8%A7%A3)
    - [返回json处理注解](#%E8%BF%94%E5%9B%9Ejson%E5%A4%84%E7%90%86%E6%B3%A8%E8%A7%A3)
    - [JUnit常用注解](#junit%E5%B8%B8%E7%94%A8%E6%B3%A8%E8%A7%A3)
    - [兼容老Spring项目注解](#%E5%85%BC%E5%AE%B9%E8%80%81spring%E9%A1%B9%E7%9B%AE%E6%B3%A8%E8%A7%A3)
  - [Spring VS SpringBoot VS SpringMVC](#spring-vs-springboot-vs-springmvc)
  - [底层细节](#%E5%BA%95%E5%B1%82%E7%BB%86%E8%8A%82)
- [SpringBoot](#springboot)
  - [SpringBoot Servlet容器](#springboot-servlet%E5%AE%B9%E5%99%A8)
  - [SpringBoot Tomcat容器](#springboot-tomcat%E5%AE%B9%E5%99%A8)
  - [Netty](#netty)
  - [Jetty](#jetty)
  - [Servlet](#servlet)
  - [Mima](#mima)
  - [Nginx](#nginx)
  - [Tomcat](#tomcat)
  - [SpringBoot CommandRunner和ApplicationRunner](#springboot-commandrunner%E5%92%8Capplicationrunner)
  - [CommandLineRunner、ApplicationRunner](#commandlinerunnerapplicationrunner)
  - [自定义starter](#%E8%87%AA%E5%AE%9A%E4%B9%89starter)
  - [事件驱动](#%E4%BA%8B%E4%BB%B6%E9%A9%B1%E5%8A%A8)
  - [SpringBoot安全](#springboot%E5%AE%89%E5%85%A8)
  - [SpringBoot 2\.X和1\.X版本区别](#springboot-2x%E5%92%8C1x%E7%89%88%E6%9C%AC%E5%8C%BA%E5%88%AB)
- [Session](#session)
- [HTTP](#http)
  - [HTTP 1\.0](#http-10)
  - [HTTP 1\.X](#http-1x)
  - [HTTP 2\.0 VS HTTP 1\.X](#http-20-vs-http-1x)
  - [HTTP VS HTTPS](#http-vs-https)
  - [HTTP 状态码](#http-%E7%8A%B6%E6%80%81%E7%A0%81)
  - [HTTP 扩展](#http-%E6%89%A9%E5%B1%95)
  - [TCP 重传、滑动窗口、流量控制、拥塞控制](#tcp-%E9%87%8D%E4%BC%A0%E6%BB%91%E5%8A%A8%E7%AA%97%E5%8F%A3%E6%B5%81%E9%87%8F%E6%8E%A7%E5%88%B6%E6%8B%A5%E5%A1%9E%E6%8E%A7%E5%88%B6)
- [MQ](#mq)
  - [消息协议](#%E6%B6%88%E6%81%AF%E5%8D%8F%E8%AE%AE)
    - [TCP](#tcp)
    - [MQTT](#mqtt)
    - [AMQP](#amqp)
    - [RTMP](#rtmp)
  - [为什么要用MQ？](#%E4%B8%BA%E4%BB%80%E4%B9%88%E8%A6%81%E7%94%A8mq)
  - [VS](#vs)
  - [常见发送问题和错误方案：](#%E5%B8%B8%E8%A7%81%E5%8F%91%E9%80%81%E9%97%AE%E9%A2%98%E5%92%8C%E9%94%99%E8%AF%AF%E6%96%B9%E6%A1%88)
  - [常见消费失败问题：](#%E5%B8%B8%E8%A7%81%E6%B6%88%E8%B4%B9%E5%A4%B1%E8%B4%A5%E9%97%AE%E9%A2%98)
    - [（1）Kafka](#1kafka)
    - [（2）RabbitMQ](#2rabbitmq)
  - [Kafka](#kafka)
    - [版本](#%E7%89%88%E6%9C%AC)
    - [适用场景](#%E9%80%82%E7%94%A8%E5%9C%BA%E6%99%AF)
    - [Kafka支持事务？](#kafka%E6%94%AF%E6%8C%81%E4%BA%8B%E5%8A%A1)
    - [Kafka支持消息优先级](#kafka%E6%94%AF%E6%8C%81%E6%B6%88%E6%81%AF%E4%BC%98%E5%85%88%E7%BA%A7)
    - [为什么Kafka那么快？](#%E4%B8%BA%E4%BB%80%E4%B9%88kafka%E9%82%A3%E4%B9%88%E5%BF%AB)
    - [Zero\-Copy 零拷贝](#zero-copy-%E9%9B%B6%E6%8B%B7%E8%B4%9D)
      - [什么是Zero\-Copy 零拷贝？](#%E4%BB%80%E4%B9%88%E6%98%AFzero-copy-%E9%9B%B6%E6%8B%B7%E8%B4%9D)
      - [Zero\-Copy需要CPU？](#zero-copy%E9%9C%80%E8%A6%81cpu)
      - [Pull VS Post](#pull-vs-post)
    - [有序消费](#%E6%9C%89%E5%BA%8F%E6%B6%88%E8%B4%B9)
    - [ISR、AR代表什么？ISR伸缩？](#israr%E4%BB%A3%E8%A1%A8%E4%BB%80%E4%B9%88isr%E4%BC%B8%E7%BC%A9)
    - [Broker消息代理](#broker%E6%B6%88%E6%81%AF%E4%BB%A3%E7%90%86)
    - [Kafka选举基于Broker还是Group？](#kafka%E9%80%89%E4%B8%BE%E5%9F%BA%E4%BA%8Ebroker%E8%BF%98%E6%98%AFgroup)
    - [ConsumerGroup中新加Consumer、移除Consumer、Consumer崩溃时发生Rebalance](#consumergroup%E4%B8%AD%E6%96%B0%E5%8A%A0consumer%E7%A7%BB%E9%99%A4consumerconsumer%E5%B4%A9%E6%BA%83%E6%97%B6%E5%8F%91%E7%94%9Frebalance)
    - [Kafka为什么不将offset保存Broker维护？而是在Partition维护？](#kafka%E4%B8%BA%E4%BB%80%E4%B9%88%E4%B8%8D%E5%B0%86offset%E4%BF%9D%E5%AD%98broker%E7%BB%B4%E6%8A%A4%E8%80%8C%E6%98%AF%E5%9C%A8partition%E7%BB%B4%E6%8A%A4)
  - [RabbitMQ](#rabbitmq)
    - [模型](#%E6%A8%A1%E5%9E%8B)
    - [顺序消费(RabbitMQ本身缺少顺序消费机制)](#%E9%A1%BA%E5%BA%8F%E6%B6%88%E8%B4%B9rabbitmq%E6%9C%AC%E8%BA%AB%E7%BC%BA%E5%B0%91%E9%A1%BA%E5%BA%8F%E6%B6%88%E8%B4%B9%E6%9C%BA%E5%88%B6)
    - [重复消费出现场景](#%E9%87%8D%E5%A4%8D%E6%B6%88%E8%B4%B9%E5%87%BA%E7%8E%B0%E5%9C%BA%E6%99%AF)
    - [解决重复消费](#%E8%A7%A3%E5%86%B3%E9%87%8D%E5%A4%8D%E6%B6%88%E8%B4%B9)
    - [消费失败处理](#%E6%B6%88%E8%B4%B9%E5%A4%B1%E8%B4%A5%E5%A4%84%E7%90%86)
    - [死信队列原理](#%E6%AD%BB%E4%BF%A1%E9%98%9F%E5%88%97%E5%8E%9F%E7%90%86)
      - [死信几种情况](#%E6%AD%BB%E4%BF%A1%E5%87%A0%E7%A7%8D%E6%83%85%E5%86%B5)
    - [RabbitMQ的事务（Confirm模式要比事务快10倍）](#rabbitmq%E7%9A%84%E4%BA%8B%E5%8A%A1confirm%E6%A8%A1%E5%BC%8F%E8%A6%81%E6%AF%94%E4%BA%8B%E5%8A%A1%E5%BF%AB10%E5%80%8D)
      - [（1）AMQP的事务机制](#1amqp%E7%9A%84%E4%BA%8B%E5%8A%A1%E6%9C%BA%E5%88%B6)
      - [（2）发送者确认模式实现](#2%E5%8F%91%E9%80%81%E8%80%85%E7%A1%AE%E8%AE%A4%E6%A8%A1%E5%BC%8F%E5%AE%9E%E7%8E%B0)
  - [RocketMQ](#rocketmq)
    - [消息协议](#%E6%B6%88%E6%81%AF%E5%8D%8F%E8%AE%AE-1)
    - [事务原理](#%E4%BA%8B%E5%8A%A1%E5%8E%9F%E7%90%86)
    - [顺序消息原理](#%E9%A1%BA%E5%BA%8F%E6%B6%88%E6%81%AF%E5%8E%9F%E7%90%86)
    - [延时消息解决方案](#%E5%BB%B6%E6%97%B6%E6%B6%88%E6%81%AF%E8%A7%A3%E5%86%B3%E6%96%B9%E6%A1%88)
    - [延时消息场景](#%E5%BB%B6%E6%97%B6%E6%B6%88%E6%81%AF%E5%9C%BA%E6%99%AF)
    - [延时只支持18个level原理](#%E5%BB%B6%E6%97%B6%E5%8F%AA%E6%94%AF%E6%8C%8118%E4%B8%AAlevel%E5%8E%9F%E7%90%86)
    - [消费方式](#%E6%B6%88%E8%B4%B9%E6%96%B9%E5%BC%8F)
      - [集群消费（默认）](#%E9%9B%86%E7%BE%A4%E6%B6%88%E8%B4%B9%E9%BB%98%E8%AE%A4)
      - [广播消费](#%E5%B9%BF%E6%92%AD%E6%B6%88%E8%B4%B9)
- [K8s和Docker](#k8s%E5%92%8Cdocker)
- [Go](#go)
- [Python Flask、Django](#python-flaskdjango)
- [安全](#%E5%AE%89%E5%85%A8)
  - [序列化默认id风险](#%E5%BA%8F%E5%88%97%E5%8C%96%E9%BB%98%E8%AE%A4id%E9%A3%8E%E9%99%A9)
  - [CSRF保护](#csrf%E4%BF%9D%E6%8A%A4)
- [JDK](#jdk)
  - [逃逸分析](#%E9%80%83%E9%80%B8%E5%88%86%E6%9E%90)
  - [JDK 1\.0\.2](#jdk-102)
  - [JDK 1\.2](#jdk-12)
    - [引入双亲委派模型](#%E5%BC%95%E5%85%A5%E5%8F%8C%E4%BA%B2%E5%A7%94%E6%B4%BE%E6%A8%A1%E5%9E%8B)
    - [扩充引用](#%E6%89%A9%E5%85%85%E5%BC%95%E7%94%A8)
  - [JDK 1\.4](#jdk-14)
  - [JDK 1\.5](#jdk-15)
    - [引入两个新的reference types](#%E5%BC%95%E5%85%A5%E4%B8%A4%E4%B8%AA%E6%96%B0%E7%9A%84reference-types)
  - [JDK 1\.8](#jdk-18)
    - [Lambda](#lambda)
      - [Stream分类](#stream%E5%88%86%E7%B1%BB)
      - [Stream原理](#stream%E5%8E%9F%E7%90%86)
      - [Demo](#demo-1)
  - [类的生命周期](#%E7%B1%BB%E7%9A%84%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F)
  - [Full GC(Major GC) 发生条件](#full-gcmajor-gc-%E5%8F%91%E7%94%9F%E6%9D%A1%E4%BB%B6)
  - [Minor GC 发生条件](#minor-gc-%E5%8F%91%E7%94%9F%E6%9D%A1%E4%BB%B6)
  - [G1优势](#g1%E4%BC%98%E5%8A%BF)
  - [什么时候发生](#%E4%BB%80%E4%B9%88%E6%97%B6%E5%80%99%E5%8F%91%E7%94%9F)
  - [Full GC VS Minor GC](#full-gc-vs-minor-gc)
  - [Minor GC会stop the world STW？](#minor-gc%E4%BC%9Astop-the-world-stw)
  - [调优](#%E8%B0%83%E4%BC%98)
    - [JMM Java Memory Model](#jmm-java-memory-model)
    - [JVM是对Java内存模型的实现](#jvm%E6%98%AF%E5%AF%B9java%E5%86%85%E5%AD%98%E6%A8%A1%E5%9E%8B%E7%9A%84%E5%AE%9E%E7%8E%B0)
    - [TProfile阿里开源在海量业务代码 精准定位性能代码问题](#tprofile%E9%98%BF%E9%87%8C%E5%BC%80%E6%BA%90%E5%9C%A8%E6%B5%B7%E9%87%8F%E4%B8%9A%E5%8A%A1%E4%BB%A3%E7%A0%81-%E7%B2%BE%E5%87%86%E5%AE%9A%E4%BD%8D%E6%80%A7%E8%83%BD%E4%BB%A3%E7%A0%81%E9%97%AE%E9%A2%98)
    - [OOM原因](#oom%E5%8E%9F%E5%9B%A0)
    - [OOM可能发生在JVM哪些区域](#oom%E5%8F%AF%E8%83%BD%E5%8F%91%E7%94%9F%E5%9C%A8jvm%E5%93%AA%E4%BA%9B%E5%8C%BA%E5%9F%9F)
    - [如何排查OOM](#%E5%A6%82%E4%BD%95%E6%8E%92%E6%9F%A5oom)
    - [Full GC过程中Stop the World，JVM如何处理](#full-gc%E8%BF%87%E7%A8%8B%E4%B8%ADstop-the-worldjvm%E5%A6%82%E4%BD%95%E5%A4%84%E7%90%86)
    - [分析内存或CPU占用高](#%E5%88%86%E6%9E%90%E5%86%85%E5%AD%98%E6%88%96cpu%E5%8D%A0%E7%94%A8%E9%AB%98)
- [工具](#%E5%B7%A5%E5%85%B7)
  - [测试工具](#%E6%B5%8B%E8%AF%95%E5%B7%A5%E5%85%B7)
  - [测试框架](#%E6%B5%8B%E8%AF%95%E6%A1%86%E6%9E%B6)
    - [Mockito](#mockito)
  - [API文档工具](#api%E6%96%87%E6%A1%A3%E5%B7%A5%E5%85%B7)
  - [Idea](#idea)
- [Open Source](#open-source)
  - [VS](#vs-1)
  - [开源协议](#%E5%BC%80%E6%BA%90%E5%8D%8F%E8%AE%AE)
    - [GPL](#gpl)
  - [软件著作权权利](#%E8%BD%AF%E4%BB%B6%E8%91%97%E4%BD%9C%E6%9D%83%E6%9D%83%E5%88%A9)
    - [署名权](#%E7%BD%B2%E5%90%8D%E6%9D%83)
    - [修改权](#%E4%BF%AE%E6%94%B9%E6%9D%83)
    - [复制权](#%E5%A4%8D%E5%88%B6%E6%9D%83)
    - [发布权](#%E5%8F%91%E5%B8%83%E6%9D%83)
  - [Incubating孵化](#incubating%E5%AD%B5%E5%8C%96)
- [Zookeeper](#zookeeper-1)
  - [四种节点类型](#%E5%9B%9B%E7%A7%8D%E8%8A%82%E7%82%B9%E7%B1%BB%E5%9E%8B)
- [Java基础](#java%E5%9F%BA%E7%A1%80)
  - [Keywords](#keywords)
    - [static](#static)
    - [new](#new)
    - [final](#final)
  - [Java数据类型](#java%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B)
  - [序列化](#%E5%BA%8F%E5%88%97%E5%8C%96)
  - [带标签break、continue](#%E5%B8%A6%E6%A0%87%E7%AD%BEbreakcontinue)
  - [时间戳](#%E6%97%B6%E9%97%B4%E6%88%B3)
- [数据库](#%E6%95%B0%E6%8D%AE%E5%BA%93-1)
  - [选型](#%E9%80%89%E5%9E%8B-1)
  - [数据库规范](#%E6%95%B0%E6%8D%AE%E5%BA%93%E8%A7%84%E8%8C%83)
  - [设计](#%E8%AE%BE%E8%AE%A1)
    - [主键](#%E4%B8%BB%E9%94%AE)
    - [分库分表](#%E5%88%86%E5%BA%93%E5%88%86%E8%A1%A8)
      - [切分模式](#%E5%88%87%E5%88%86%E6%A8%A1%E5%BC%8F)
        - [水平切分](#%E6%B0%B4%E5%B9%B3%E5%88%87%E5%88%86)
        - [垂直切分](#%E5%9E%82%E7%9B%B4%E5%88%87%E5%88%86)
      - [分库分表工具](#%E5%88%86%E5%BA%93%E5%88%86%E8%A1%A8%E5%B7%A5%E5%85%B7)
      - [分库策略](#%E5%88%86%E5%BA%93%E7%AD%96%E7%95%A5)
      - [分库影响](#%E5%88%86%E5%BA%93%E5%BD%B1%E5%93%8D)
    - [NULL数据倾斜和影响](#null%E6%95%B0%E6%8D%AE%E5%80%BE%E6%96%9C%E5%92%8C%E5%BD%B1%E5%93%8D)
    - [SQL自动检查](#sql%E8%87%AA%E5%8A%A8%E6%A3%80%E6%9F%A5)
    - [优化点](#%E4%BC%98%E5%8C%96%E7%82%B9)
  - [存储引擎](#%E5%AD%98%E5%82%A8%E5%BC%95%E6%93%8E)
  - [事务](#%E4%BA%8B%E5%8A%A1-1)
    - [原理](#%E5%8E%9F%E7%90%86-1)
    - [事务管理器TransactionManager](#%E4%BA%8B%E5%8A%A1%E7%AE%A1%E7%90%86%E5%99%A8transactionmanager)
      - [Hibernate](#hibernate)
      - [Mybatis](#mybatis)
        - [Mybatis数据类型](#mybatis%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B)
    - [MySQL事务隔离级别](#mysql%E4%BA%8B%E5%8A%A1%E9%9A%94%E7%A6%BB%E7%BA%A7%E5%88%AB)
      - [脏、幻读（虚读）](#%E8%84%8F%E5%B9%BB%E8%AF%BB%E8%99%9A%E8%AF%BB)
    - [Oracle](#oracle)
    - [事务传播机制](#%E4%BA%8B%E5%8A%A1%E4%BC%A0%E6%92%AD%E6%9C%BA%E5%88%B6)
    - [事务回滚](#%E4%BA%8B%E5%8A%A1%E5%9B%9E%E6%BB%9A)
  - [锁](#%E9%94%81-1)
  - [索引](#%E7%B4%A2%E5%BC%95)
    - [MySQL索引类型](#mysql%E7%B4%A2%E5%BC%95%E7%B1%BB%E5%9E%8B)
    - [MySQL索引失效](#mysql%E7%B4%A2%E5%BC%95%E5%A4%B1%E6%95%88)
    - [MySQL复合索引ABC问题](#mysql%E5%A4%8D%E5%90%88%E7%B4%A2%E5%BC%95abc%E9%97%AE%E9%A2%98)
    - [MySQL复合索引最左原则底层原理](#mysql%E5%A4%8D%E5%90%88%E7%B4%A2%E5%BC%95%E6%9C%80%E5%B7%A6%E5%8E%9F%E5%88%99%E5%BA%95%E5%B1%82%E5%8E%9F%E7%90%86)
  - [命令](#%E5%91%BD%E4%BB%A4)
    - [MySQL show variables](#mysql-show-variables)
      - [autocommit](#autocommit)
    - [MySQL explain](#mysql-explain)
  - [SQL](#sql)
    - [Hive SQL VS SQL](#hive-sql-vs-sql)
    - [分号符处理](#%E5%88%86%E5%8F%B7%E7%AC%A6%E5%A4%84%E7%90%86)
  - [函数](#%E5%87%BD%E6%95%B0)
    - [Hive常见函数](#hive%E5%B8%B8%E8%A7%81%E5%87%BD%E6%95%B0)
    - [MySQL join](#mysql-join)
  - [Kettle ETL](#kettle-etl)
- [Hot Keys](#hot-keys)
  - [Mac Typora](#mac-typora)
  - [Mac Pro](#mac-pro)
  - [Mac Pro Note](#mac-pro-note)
  - [Linux](#linux)
- [电商](#%E7%94%B5%E5%95%86)
  - [SKU（规格表）、SPU（商品表）设计](#sku%E8%A7%84%E6%A0%BC%E8%A1%A8spu%E5%95%86%E5%93%81%E8%A1%A8%E8%AE%BE%E8%AE%A1)
  - [优惠券、红包、代金券](#%E4%BC%98%E6%83%A0%E5%88%B8%E7%BA%A2%E5%8C%85%E4%BB%A3%E9%87%91%E5%88%B8)
  - [活动](#%E6%B4%BB%E5%8A%A8)
  - [秒杀](#%E7%A7%92%E6%9D%80)
  - [推荐](#%E6%8E%A8%E8%8D%90)
    - [推荐方法](#%E6%8E%A8%E8%8D%90%E6%96%B9%E6%B3%95)
    - [内容推荐VS协同过滤推荐](#%E5%86%85%E5%AE%B9%E6%8E%A8%E8%8D%90vs%E5%8D%8F%E5%90%8C%E8%BF%87%E6%BB%A4%E6%8E%A8%E8%8D%90)
    - [隐私](#%E9%9A%90%E7%A7%81)
    - [数据](#%E6%95%B0%E6%8D%AE)
- [区块链](#%E5%8C%BA%E5%9D%97%E9%93%BE)
- [架构](#%E6%9E%B6%E6%9E%84)
- [心得](#%E5%BF%83%E5%BE%97-1)



作者：cj （1）有限（2）不系统（3）来源于整理

# 线程

extends Thread Java中类仅单继承，Java中接口可多继承

Implements Runnable 方便一组线程访问相同资源，避免Thread创建多对象的内存浪费。

Callable 有返回值可获取Future(Future用于接收返回的结果，Future#get( )一直阻塞到获取到结果)，Runnable无返回值。注意Future若漏掉返回值为空时会导致程序阻塞。

## JAVA API-线程状态State 枚举

NEW、RUNNABLE、BLOCKED、WAITING、TIMED_WAITING、TERMINATED

```java
  /**
     * A thread state.  A thread can be in one of the following states:
     * <ul>
     * <li>{@link #NEW}<br>
     *     A thread that has not yet started is in this state.
     *     </li>
     * <li>{@link #RUNNABLE}<br>
     *     A thread executing in the Java virtual machine is in this state.
     *     </li>
     * <li>{@link #BLOCKED}<br>
     *     A thread that is blocked waiting for a monitor lock
     *     is in this state.
     *     </li>
     * <li>{@link #WAITING}<br>
     *     A thread that is waiting indefinitely for another thread to
     *     perform a particular action is in this state.
     *     </li>
     * <li>{@link #TIMED_WAITING}<br>
     *     A thread that is waiting for another thread to perform an action
     *     for up to a specified waiting time is in this state.
     *     </li>
     * <li>{@link #TERMINATED}<br>
     *     A thread that has exited is in this state.
     *     </li>
     * </ul>
     *
     * <p>
     * A thread can be in only one state at a given point in time.
     * These states are virtual machine states which do not reflect
     * any operating system thread states.
     *
     * @since   1.5
     * @see #getState
     */
    public enum State {
        /**
         * Thread state for a thread which has not yet started.
         */
        NEW,

        /**
         * Thread state for a runnable thread.  A thread in the runnable
         * state is executing in the Java virtual machine but it may
         * be waiting for other resources from the operating system
         * such as processor.
         */
        RUNNABLE,

        /**
         * Thread state for a thread blocked waiting for a monitor lock.
         * A thread in the blocked state is waiting for a monitor lock
         * to enter a synchronized block/method or
         * reenter a synchronized block/method after calling
         * {@link Object#wait() Object.wait}.
         */
        BLOCKED,

        /**
         * Thread state for a waiting thread.
         * A thread is in the waiting state due to calling one of the
         * following methods:
         * <ul>
         *   <li>{@link Object#wait() Object.wait} with no timeout</li>
         *   <li>{@link #join() Thread.join} with no timeout</li>
         *   <li>{@link LockSupport#park() LockSupport.park}</li>
         * </ul>
         *
         * <p>A thread in the waiting state is waiting for another thread to
         * perform a particular action.
         *
         * For example, a thread that has called <tt>Object.wait()</tt>
         * on an object is waiting for another thread to call
         * <tt>Object.notify()</tt> or <tt>Object.notifyAll()</tt> on
         * that object. A thread that has called <tt>Thread.join()</tt>
         * is waiting for a specified thread to terminate.
         */
        WAITING,

        /**
         * Thread state for a waiting thread with a specified waiting time.
         * A thread is in the timed waiting state due to calling one of
         * the following methods with a specified positive waiting time:
         * <ul>
         *   <li>{@link #sleep Thread.sleep}</li>
         *   <li>{@link Object#wait(long) Object.wait} with timeout</li>
         *   <li>{@link #join(long) Thread.join} with timeout</li>
         *   <li>{@link LockSupport#parkNanos LockSupport.parkNanos}</li>
         *   <li>{@link LockSupport#parkUntil LockSupport.parkUntil}</li>
         * </ul>
         */
        TIMED_WAITING,

        /**
         * Thread state for a terminated thread.
         * The thread has completed execution.
         */
        TERMINATED;
    }
```

## 线程状态流转

![Thread](http://hongchengjian.gitee.io/md/img/thread/Thread.png)

## 线程开始

start( )而非run( )，run是Runable接口的一个@Overwrite的方法

```java
@FunctionalInterface
public interface Runnable {
    /**
     * When an object implementing interface <code>Runnable</code> is used
     * to create a thread, starting the thread causes the object's
     * <code>run</code> method to be called in that separately executing
     * thread.
     * <p>
     * The general contract of the method <code>run</code> is that it may
     * take any action whatsoever.
     *
     * @see     java.lang.Thread#run()
     */
    public abstract void run();
}
```

## 线程结束

（1）正常main、call、run方法结束

（2）interrupt捕获异常java.lang.InterruptedException: sleep interrupted 时，break跳出 

## Java API-常用方法

###  @Deprecated Thread.stop, Thread.suspend, Thread.resume

```css
Thread.stop( )线程不安全，会释放子线程所有锁，被保护的数据有可能呈现不一致性，导致错误。
```

### 对象锁

#### 什么是对象锁？

对象锁是指Java为临界区 synchronized(obj)指定的对象obj进行加锁，对象锁是独占锁(排他锁)。

对象锁用于程序片段或者method上，此时将获得对象的锁，所有想要进入该对象的synchronized的方法或者代码段的线程都必须获取对象的锁，如果没有，则必须等其他线程释放该锁。

### Object.wait( ) 、Object.notify( ) 、Object.notifyAll( )

Object.wait( )  会释放对象锁。

Object.wait( ) 调用的外层代码没有锁时，会发生什么？编译不报错，但是运行报错java.lang.IllegalMonitorStateException。

```java

public class TestWait {
    public static void main(String[] args) throws InterruptedException {
        TestWait wait = new TestWait();
        wait.wait();
    }
}

Exception in thread "main" java.lang.IllegalMonitorStateException
	at java.lang.Object.wait(Native Method)
	at java.lang.Object.wait(Object.java:502)
	at org.union.czt.test.TestWait.main(TestWait.java:7)
```

Object.notify( ) 唤醒Object Monitor(对象监视器)上的任一等待的单个线程。如果有多个等待线程有竞争吗？是随机唤醒吗？

Javadoc 对 notify( )方法说明

```java
Wakes up a single thread that is waiting on this object's monitor. If any threads are waiting on this object, one of them is chosen to be awakened. The choice is arbitrary and occurs at
the discretion of the implementation. 
```

证明唤醒的顺序是无序

```java
package main.java.thread;

import java.util.LinkedList;
import java.util.List;

public class TestNotifyOrder {
    /**
     * 对象锁
     */
    private final Object object = new Object();

    private List<Integer> sleepList = new LinkedList<>();
    private List<Integer> notifyList = new LinkedList<>();

    /**
     * 该线程作为一个唤醒线程
     */
    public void startThread(int i) {
        Thread t = new Thread(new Runnable() {
            @Override
            public void run() {
                synchronized (object) {
                    try {
                        System.out.println(Thread.currentThread().getName() + "进入休眠");
                        sleepList.add(i);
                        object.wait();
                        // 下面的代码线程被唤醒时才执行
                        System.out.println(Thread.currentThread().getName() + "线程已经唤醒");
                        notifyList.add(i);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
            }
        });
        // 设置当前线程名
        t.setName("Thread" + i);
        t.start();
    }

    public static void main(String[] args) {
        TestNotifyOrder a = new TestNotifyOrder();
        // 21个线程实际运行的顺序是不固定的
        for (int i = 1; i < 22; i++) {
            a.startThread(i);
        }

        try {
            Thread.sleep(1000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        System.out.println();
        // 每次被唤醒的线程也是21个线程中随机的一个
        for (int i = 1; i < 22; i++) {
            synchronized (a.object) {
                a.object.notify();
            }
        }

        try {
            Thread.sleep(3000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println("休眠顺序" + a.sleepList);
        System.out.println("唤醒顺序" + a.notifyList);
    }
}

```

Object.notifyAll( )唤醒Object Monitor(对象监视器)上等待的所有线程，继续执行下去；

Thread.sleep(long) 线程的sleep时间结束后是进入runnable还是running状态？ runnable。

### Thread.sleep(long) VS Object.wait( )  VS  Object.wait(long )

Thread.sleep(long) 不改变锁行为，若当前线程拥有锁，Thread.sleep(long) 并不会释放锁。

调用 Object.wait( ) 后，需要别的线程执行Object.notify/notifyAll才能够重新获得CPU执行时间。注意是别的线程，调用 Object.wait( )的线程再调Object.notify/notifyAll是不行的。

共同点：Thread.sleep(long) 和 Object.wait(long)  都是使线程 RUNNABLE -> TIMED_WAITING，时间结束都是回到RUNNABLE 状态。Thread.sleep(long)时间结束还是继续执行当前线程后续逻辑。

### Thread.sleep(long)  VS Thread.yield( ) 

Thread.yield( ) 使线程 running -> runable，当前线程和其他线程有竞争关系，进入runnable的线程不一定是当前线程，有可能是其他线程。Thread.sleep(long)时间到了一定是当前线程进入runnable状态。

Thread.join( ) 主线程等子线程执行结束后再执行。

Thread.interrupt( )作用不是中断线程，而是通知线程应该中断了，具体中断还是继续运行，由被通知的线程自己处理。

### 判断线程有没有持有对象锁Thread.holdsLock(obj)

Thread.holdsLock(obj)持有monitor lock返回true

### 控制线程执行顺序Thread.join( )和多线程的无序执行

```java
main(){
		thread1();
		thread2();
}
// 3个线程：虽然代码顺序是Main、thread1、thread2，但创建三个线程后，竞争抢CPU时间片，谁先执行完是不确定的。

main() {
    thread1.start();
    thread1.join();
    thread2.start();
    thead2.join();
    thread3.start();
}
```

### 守护线程（服务线程）setDaemon( )

```java
thread = new Thread(this);
thread.setDaemon(true);
thread.start();
```

优先级低，为系统其他对象和线程提供服务，可做实时监控、管理系统，最好守护线程不要写影响业务逻辑。

垃圾回收GC线程是一个守护线程，当JVM中没有非守护线程在运行时，Java虚拟机会关闭。当所有常规线程运行完毕后，守护线程不管运行到哪里都会退出运行。

# 线程池

## 原理和流程

![ThreadPool](http://hongchengjian.gitee.io/md/img/thread/ThreadPool.png)

说明：当线程数小于核心线程数，即使有空闲线程，线程池也会创建新线程处理。

线程数>= corePoolSize，且任务队列已满，线程池会创建新线程来处理任务。

线程数=maxPoolSize，且任务队列已满，线程池会拒绝处理任务而抛异常。

![ThreadPool Model](http://hongchengjian.gitee.io/md/img/thread/ThreadPool%20Model.png)

## 线程池 VS new Thread

### new Thread缺陷 

创建对象性能差，缺统一管理，缺定时等功能。直接new多个thread在大并发下因系统缺少资源运行可能会丢失部分，而线程池可以充分管理线程，调度资源。

### Executors创建线程池缺陷

阿里发布的 Java开发手册中强制线程池不允许使用 Executors 去创建，而是通过 ThreadPoolExecutor 的方式。

Executors创建的线程池存在OOM两种情况，（1）maximumPoolSize传的是Integer.MAX_VALUE

比如newCachedThreadPool、newScheduledThreadPool，创建线程需要大量资源

（2）LinkedBlockingQueue是一个用链表实现的有界阻塞队列，不设置是一个无边界的阻塞队列，最大长度为Integer.MAX_VALUE，原因是高并发下，线程数达到maximumPoolSize时处理不过来任务，任务往LinkedBlockingQueue放，LinkedBlockingQueue无界一直放任务耗光系统内存

比如newFixedThreadPool、newSingleThreadExecutor

```java
// 验证高并发下OOM
public class TestExecutorService {
    // private static ExecutorService executor = Executors.newFixedThreadPool(2);
    private static ExecutorService executor = Executors.newSingleThreadExecutor();

    //向kafka里推送消费
    public static void doSth(Object msg) {
        executor.execute(() -> {
            try {
                //模拟 占用的内存大小
                Byte[] bytes = new Byte[1024 * 1000 * 1000];
                System.out.println(Thread.currentThread().getName() + "-->任务放到线程池:" + msg);
                TimeUnit.MINUTES.sleep(1);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        });
    }

    public static void main(String[] args) {
        //模拟高并发环境下  一直向线程池里面不停的塞任务
        for (int i = 0; i < 10000; i++) {
            System.out.println("塞任务start..." + i);
            doSth(i);
            System.out.println("塞任务end..." + i);
        }
    }
}


// console
塞任务end...2249
塞任务start...2250
塞任务end...2250
塞任务start...2251
塞任务end...2251
塞任务start...2252
塞任务end...2252
Exception in thread "pool-1-thread-79" java.lang.OutOfMemoryError: Java heap space
```



## Java API-线程池 Executor实现对比

newCacheThreadExecutor（短期异步short-lived asynchronous tasks、有可用线程可用直接复用，无可用线程则创建新的线程并加到池子里。空闲60s的线程(60s未使用)会被移除）

```java
    // a pool that remains idle for long enough will not consume any resources
    public static ExecutorService newCachedThreadPool() {
        return new ThreadPoolExecutor(0, Integer.MAX_VALUE,
                                      60L, TimeUnit.SECONDS,
                                      new SynchronousQueue<Runnable>());
    }
```

newFixedThreadPool（定长线程池，可用固定数量线程数、共享无界队列a shared unbounded queue、超时不会自动关闭）

```java
//  The threads in the pool will exist until it is explicitly {@link ExecutorService#shutdown}
public static ExecutorService newFixedThreadPool(int nThreads) {
    // LinkedBlockingQueue是一个用链表实现的有界阻塞队列，不设置是一个无边界的阻塞队列，最大长度为Integer.MAX_VALUE
    // corePoolSize == maximumPoolSize == nThreads
        return new ThreadPoolExecutor(nThreads, nThreads,
                                      0L, TimeUnit.MILLISECONDS,
                                      new LinkedBlockingQueue<Runnable>());
    }
```

newScheduledThreadPool（支持定时或周期性任务执行）

```java
    public ScheduledThreadPoolExecutor(int corePoolSize) {
        super(corePoolSize, Integer.MAX_VALUE, 0, NANOSECONDS,
              new DelayedWorkQueue());
    }
```

newSingleThreadExecutor（单线程串行化的线程池，用唯一的工作线程来执行任务，任务是按指定顺序（FIFO、LIFO、优先级）执行。

```java
    public static ExecutorService newSingleThreadExecutor() {
        return new FinalizableDelegatedExecutorService
            (new ThreadPoolExecutor(1, 1,
                                    0L, TimeUnit.MILLISECONDS,
                                    new LinkedBlockingQueue<Runnable>()));
    }
```



## 正确创建线程池

（1）使用Guava提供的ThreadFactoryBuilder来创建线程池，为什么Guava不会溢出？

```java
public class Demo {

    private static ThreadFactory nameFactory = new ThreadFactoryBuilder()
        .setNameFormat("demo-pool-%d").build();

    // LinkedBlockingQueue是一个用链表实现的有界阻塞队列，不设置是一个无边界的阻塞队列，最大长度为Integer.MAX_VALUE
    private static ExecutorService pool = new ThreadPoolExecutor(5, 200,
        0L, TimeUnit.MILLISECONDS,
        new LinkedBlockingQueue<Runnable>(1024), namedFactory, new ThreadPoolExecutor.AbortPolicy());

    public static void main(String[] args) {

        for (int i = 0; i < Integer.MAX_VALUE; i++) {
            pool.execute(new SubThread());
        }
    }
}
```

（2）给BlockQueue指定容量private static ExecutorService executor = new ThreadPoolExecutor(10, 10, 60L, TimeUnit.SECONDS,new ArrayBlockingQueue(10));一旦提交的线程数超过当前可用线程数时，就会抛出java.util.concurrent.RejectedExecutionException。

## 线程池四要素

线程池四要素（1）池子管理器（作用是创建池子）（2）工作线程数（3）任务接口（4）队列

## 线程池参数

线程池：corePoolSize、maxiumPoolSize、keepaliveTime、workQueue、handler

## 线程池参数默认值

corePoolSize = 1

queueCapacity = Integer.MAX_VALUE

maxPoolSize=Integer.MAX_VALUE

keepAliveTime=60s

allowCoreThreadTimeout=false

rejectedExcutionHandler=AbortPolicy( )

## 线程池参数经验值设置（实际看生产机器）

tasks：每秒的任务数，假设为500~1000

taskCost：每个任务需要花费的时间，假设为0.1s

responseTime：系统允许的最大响应时间，假设为2s

corePoolSize = tasks * taskCost ( s为单位 )= (500~1000)*0.1= 50~100个线程。corePoolSize的个数应该大于等于50。根据8020原则，如果每秒80%的时间执行200个任务，corePoolSize设置为80即可。

queueCapacity = corePoolSize * taskCost * responseTime

为了将线程数只会保持在corePoolSize大小，当任务陡增时，不会开新的线程来执行，responseTime也会陡增。

maxPoolSize =  (max(tasks)-queueCapacity) * taskCost 

机器横向扩展、CPU核数预估

**CPU密集型任务**，尽量压榨CPU， NCPU+1

**IO密集型任务**，2*NCPU

## 验证线程池参数经验值设定效果

压测工具sysbench 	https://blog.csdn.net/IThelei/article/details/98126187

## 线程池拒绝策略4种与扩展

（1）Abort Policy抛异常阻止运行

（2）CallerRuns Policy跑当前被丢弃的任务

（3）Discard Oldest Policy 丢弃最老的请求

（4）Discard Policy丢弃无法处理的请求任务

线程拒绝策略自定义实现 implements RejectedExecutionHandler

## 线程池自动关闭

（1）corePoolSize设置为0，keepAliveTime指定一个long值，线程池在空闲一段时间后会自动关闭。

（2）allowCoreThreadTimeOut(true)设置为true，核心线程数corePoolSize也受keepAliveTime控制。

## 线程池任务在收到某个事件后关闭其中一个线程，其他线程继续执行

（1）开关

```java
public class MyThread extends Thread {
    public volatile boolean exit = false; 
        public void run() { 
        while (!exit){
            //do something
        }
    } 
```

（2）一个线程在运行状态中，中断标志被设置为true后，一旦线程调用了Thread.sleep( )、Object.wait( )、BlockingQueue.put( )、BlockingQueue.take( )方法中的一种，立马抛出一个InterruptedException（进行异常捕获+break退出)，且中断标志被清除，重新设置为false。

```java
public class ThreadTest {
 
    static class MyThread extends Thread {
        @Override
        public void run() {
            while (!isInterrupted()){ //非阻塞过程中通过判断中断标志来退出
                try{
                    Thread.sleep(5*1000);//阻塞过程捕获中断异常来退出
                }catch(InterruptedException e){
                    e.printStackTrace();
                    System.out.println("ThreadSafe:run()"+e.getMessage());
                    break;//捕获到异常之后，执行break跳出循环。
                }
            }
        }
    }
 
    public static void main(String[] args) throws Exception {
        Thread thread = new ThreadSafe();
        thread.start();
        System.out.println("在50秒之内按任意键中断线程!");
        System.in.read();
        thread.interrupt();
        Thread.sleep(5000);
        System.out.println("线程已经退出!thread.is" + thread.isAlive());
    }
}
```

## 线程中断响应

在JVM中，每个线程都有一个与之关联的Boolean属性，被称之为中断状态，可以通过Thread.currentThread( ).isInterrupted( )来获取当前线程的中断状态，初始值为false。

当线程正在执行这些方法时，被其他线程中断掉，该线程会首先清除掉中断状态（设置中断属性为false），然后抛出InterruptedException异常。

```java
public static void main(String[] args) throws InterruptedException {
        Thread t1 = new Thread(() -> {
            try {
                System.out.println("线程初始中断状态 -> " + Thread.currentThread().isInterrupted());
                Thread.sleep(10000);
            } catch (InterruptedException e) {
                System.out.println("抛出异常后线程中断状态 -> " + Thread.currentThread().isInterrupted());
                e.printStackTrace();
            }
        });
        t1.start();
        TimeUnit.MILLISECONDS.sleep(50);
        t1.interrupt();
    }

线程初始中断状态 -> false
抛出异常后线程中断状态 -> false
java.lang.InterruptedException: sleep interrupted
	at java.lang.Thread.sleep(Native Method)
	at org.dromara.soul.admin.config.Test.lambda$main$0(Test.java:11)
	at java.lang.Thread.run(Thread.java:748)
```



## 思考线程池是否要关闭

FixedThreadPool的核心线程不会超时自动关闭，必须在适当的时候调用shutdown来关闭，否则会一直在内存中存在。

CachedThreadPool线程keepAliveTime默认为60s，若忘记关闭且allowCoreThreadTimeOut(true)时，keepAliveTime时间到60s时自动关闭。

finally线程池的关闭可采用TWR语法糖优化Try with Resource

## 线程池关闭后的影响

### 线程池关闭是否可以接受新任务？

默认的handle是 Abort policy，继续提交任务会执行拒绝策略，implements RejectedExecutionHandler可以修改具体拒绝策略。

### 等待队列里的任务是否会继续执行？正在执行 的任务是否会立即中断？

执行shutdown( )，等待队列里的任务会继续执行，全部执行完后真正shutdown。执行shutdown( )和真正shutdown（）shutdown( )之间，会拒绝新任务，调用rejectedExecutionHandler来处理这个任务，默认的rejectedExecutionHandler是AbortPolicy并抛异常。方法不会 interrupt 运行中running线程。

执行shutdownNow( )，线程池里的等待任务不会继续执行。

# 队列

## 线程阻塞的两种情况

（1）队列中没数据，消费端所有线程都自动阻塞挂起直到有数据进入队列。

（2）当生产者填满队列数据时，生产端的所有线程都会被自动阻塞挂起，直到队列有空位置，生产者线程被自动唤醒。

## 阻塞队列BlockingQueue

BlockingQueue内存队列，生产者put，消费者take。当队列为空，消费者线程被阻塞；当队列装满，生产者线程被阻塞。

### demo 花牌游戏 Epam面试手写代码

```java
/**
 * Task1: Please represent 54 playing Card Deck as a Java class. Imagine which methods could be placed inside.
 * Task2: Using task1 as your class. Imagine there are 1 card sender and 3 players. The card sender send card to player one by one in a round. Once the player’s sum points bigger than 50, the player win the game.  
 * [Points define]
 * "A"=1,"2"=2,"3"=3,"4"=4,"5"=5,"6"=6,"7"=7,"8"=8,"9"=9,"10"=10,"J"=11,"Q"=12,"K"=13,"black Joke"=20,"red Joke"=20;
 * Example 1:
 * Round1 = Sender ["A","6","K"=13] -> Player1=1, player2=6, player3=13;
 * Round2 = Sender ["10","Q","black Joke"]-> Player1=11, player2=18, player3=33;
 * Round3 = Sender ["9","J","red Joke"]-> Player1=20, player2=29, player3=53-> player 3 win;
 */
```

牌

```java
public class Card {

    private String name;
    private int point;

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Card card = (Card) o;
        return point == card.point &&
                name.equals(card.name);
    }

    @Override
    public int hashCode() {
        return Objects.hash(name, point);
    }
}
```

牌花色

```java
public enum SuitsEnum {
    SPADES,
    HEARTS,
    DIAMONDS,
    CLUBS
}
```

玩牌者

```java
public class Player {
    private static final int ROUND = 3;

    /**
     * 玩家id
     */
    private int id;
    /**
     * 玩家名
     */
    private String name;
    /**
     * 玩家手里的牌
     */
    private ArrayList<Card> list;

    public Player(int id, String name) {
        this.id = id;
        this.name = name;
    }

    public void getCard(Card card){
        if(CollectionUtils.isEmpty(list)){
            list = new ArrayList<>(ROUND);
        }
        list.add(card);
    }
```

点数 牌A-K 13张

```java
public enum PointsEnum {
    A("A",1),
    _2("2",2),
    _3("3",3),
    _4("4",4),
    _5("5",5),
    _6("6",6),
    _7("7",7),
    _8("8",8),
    _9("9",9),
    _10("10",10),
    J("J",11),
    Q("Q",12),
    K("K",13);

    PointsEnum(String name, int rank) {
        this.name = name;
        this.rank = rank;
    }
    private String name;
    private int rank;
}
```

荷官

```java
public class Sender {
    private static ArrayList<Card> arrayList = new ArrayList<>(54);

    public ArrayList<Card> init() {
        for (SuitsEnum suit : SuitsEnum.values()) {
            for (PointsEnum point : PointsEnum.values()) {
                arrayList.add(new Card(suit.name().toLowerCase() + " " + point.getName(), point.getRank()));
            }
        }
        arrayList.add(new Card("black Joke", 20));
        arrayList.add(new Card("red Joke", 20));
        return arrayList;
    }


    public void shuffle(ArrayList<Card> arrayList) {
        Collections.shuffle(arrayList);
    }
```



```java
public class BlockingQueueTest {
    private static BlockingQueue<Card> cards = new LinkedBlockingDeque<>();

    public static Card take() {
        Card card = null;
        try {
            card = cards.take();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        return card;
    }

    public static void put(Card card) {
        try {
            cards.put(card);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }

    public static boolean win(Player[] players) {
        if (null != players && 0 != players.length) {
            for (Player player : players) {
                // 每个玩家手中的牌
                ArrayList<Card> list = player.getList();
                if (!CollectionUtils.isEmpty(list)) {
                    System.out.println(MessageFormat.format("{0}-{1}-{2}", player.getId(), player.getName(), JSON.toJSON(player.getList())));
                    int sum = list.stream().mapToInt(c -> c.getPoint()).sum();
                    if (sum > 50) {
                        System.out.printf("%d-%s sum:%d%s%n", player.getId(), player.getName(), sum, JSON.toJSON(player.getList()));
                        return true;
                    }
                }
            }
        }
        return false;
    }


    public static void main(String[] args) {
        // 1个发牌者
        Sender sender = new Sender();
        // 54张牌
        ArrayList<Card> cardList = sender.init();
        // 发牌者洗牌
        sender.shuffle(cardList);

        // 3个玩家
        Player[] players = new Player[3];
        players[0] = new Player(1, "Player1");
        players[1] = new Player(2, "Player2");
        players[2] = new Player(3, "Player3");

        // 游戏共多少轮数
        int rounds = 18;
        for (int j = 0; j < rounds; j++) {
            Iterator<Card> it = cardList.iterator();
            if (it.hasNext()) {
                // 一轮中，顺序发三张
                for (int i = 0; i < 3; i++) {
                    Card currentCard = it.next();
                    // 取一张删掉一张
                    put(currentCard);
                    it.remove();
                }
            }
            players[0].getCard(take());
            players[1].getCard(take());
            players[2].getCard(take());


            System.out.printf("round%d is over%n", j);
            if (win(players)) break;
        }
    }

}
```

### Java API-常用方法

#### 放

```css
offer(anObject): 表示如果可能的话，将an Object加到BlockingQueue里，即如果BlockingQueue可以容纳，
　　　　则返回true，否则返回false。（本方法不阻塞当前执行方法的线程）
offer(E o, long timeout, TimeUnit unit): 可以设定等待的时间，如果在指定的时间内，还不能往队列中
　　　　加入BlockingQueue，则返回失败。
put(anObject): 把an Object加到BlockingQueue里，如果BlockQueue没有空间，则调用此方法线程被阻断
　　　　直到BlockingQueue里面有空间再继续。
```

#### 取

```css
poll(time):取走BlockingQueue里排在首位的对象，若不能立即取出，则可以等time参数规定的时间，
　　　　取不到时返回null；
poll(long timeout, TimeUnit unit)：从BlockingQueue取出一个队首的对象，如果在指定时间内，
　　　　队列一旦有数据可取，则立即返回队列中的数据。否则直到时间超时还没有数据可取，返回失败。
take( ): 取走BlockingQueue里排在首位的对象，若BlockingQueue为空，阻断进入等待状态直到
　　　　BlockingQueue有新的数据被加入。 
drainTo( ): 一次性从BlockingQueue获取所有可用数据对象（还可指定获取数据的个数），不需多次分批加锁或释放锁，提升获取数据效率。
```



## ArrayBlockingQueue（FIFO）

数组结构组成的有界阻塞队列，直接将枚举对象插入或移除，不会产生额外对象实例。默认不保证公平访问队列。

公平访问队列是指阻塞所有生产者线程或消费者线程，当队列可用时，可按照阻塞的先后顺序访问队列，先阻塞的生产者线程可以先往队列里插入元素，先阻塞的消费者线程，可以先从队列里获取元素。添加和移除操作都采用同一把锁ReenterLock( );初始化必须传入容量大小，使用int来统计元素。

## LinkedBlockingQueue（newFixedThreadPool） VS LinkedTransferQueue VS LinkedBlockingDeque

LinkedBlockingQueue线程安全的阻塞队列。链表结构组成的有界阻塞队列，LinkedBlockingQueue中锁分离，插入（添加）是用putLock，移除是用takeLock，好处是大大提高队列的吞吐量，在高并发下生产者和消费者可并行操作队列中的数据来提高整个队列的并发性能。

适合生产和消费频率差不多的场景。大批量数据系统，GC压力大。

默认Integer.MAX_VALUE大小，也可指定容量大小。
clear会加上两把锁，使用AtomicInteger来统计元素的个数。

LinkedTransferQueue链表结构组成的无界阻塞队列。

LinkedBlockingDeque链表结构组成的双向阻塞队列。

## PriorityBlockingQueue

优先级排序的无界阻塞队列

## DelayQueue（缓存失效、定时任务）

优先级队列实现的无界阻塞队列。创建元素可指定多久才能从队列获取当前元素，在延迟期满才能从队列中提取元素。

DelayQueue保存缓存元素的有效期，使用一个线程循环查询DelayQueue，一旦能从DelayQueue中获取元素，表示缓存有效期到了。

## SynchronousQueue（不存储数据、可传递数据）

不存储元素的阻塞队列。每一个put操作必须等待一个take操作，否则不能继续添加元素。

# 线程安全

线程安全指控制多个线程对某个资源的有序访问或修改。

线程安全实质是公共区域的内存所存数据的安全，一般是堆内存和方法区。方法区存的是（1）类型信息（2）类型的常量池（3）字段信息（4）方法信息（5)类变量（6）指向类加载器的引用（7）指向class实例的引用（8）方法表。注意运行时常量池存在JDK 1.6方法区的 PermGen、JDK 1.7 heap、JDK 1.8 metaspace。

## 有状态 VS 无状态

| 状态            | 是否有实例对象 | 是否可以保存数据 | 线程是否安全 |
| :-------------- | :------------: | :--------------: | :----------: |
| 有状态Stateful  |       是       |        是        |      否      |
| 无状态Stateless |   无，不变类   |        否        |      是      |

# 线程同步 VS 线程异步

## 同步 VS 异步

同步：当一个线程A对内存操作时其他线程都不对内存地址操作，直到线程A完成操作，其他线程才能对内存地址进行操作，且其他线程处于等待状态。

实质是任一时刻只有一个线程在跑，其他线程处x于等待。

同步是为了协同相互配合，按预定的先后次序进行工作。

## 同步使用场景

一些敏感数据不允许被多个线程同时访问，比如修改、计算

时序就近操作

## 异步使用场景

无时序操作

IO等耗时操作

不影响主线程结果

对共享资源只读、无原子性操作长流程

# Java API-线程同步的方法

```java
java.lang.Thread#sleep(long)
java.lang.Object#wait()
java.lang.Object#notifyAll()
java.lang.Object#notify()
```

# 对象头Mark Word

存放在堆中的对象分为三部分：对象头、实例变量(对象属性信息、包括父类属性信息）、填充字节对齐padding(JVM要求对象字节必须是8个字节的整数倍，用于凑齐整数倍)

```c++
ObjectMonitor() {
    _count        = 0; 		//用来记录该对象被线程获取锁的次数
    _waiters      = 0;
    _recursions   = 0; 		//锁的重入次数
    _owner        = NULL; 	//指向持有ObjectMonitor对象的线程 
    _WaitSet      = NULL; 	//处于wait状态的线程，会被加入到_WaitSet
    _WaitSetLock  = 0 ;
    _EntryList    = NULL ; 	//处于等待锁block状态的线程，会被加入到该列表
}
```

# 64位虚拟机对象头存储

![OS 64bit markword](http://hongchengjian.gitee.io/md/img/jvm/OS%2064bit%20markword.png)

# Java API-多线程同步5种方式

#### synchronized原理图

![synchronized](http://hongchengjian.gitee.io/md/img/thread/synchronized.png)

synchronized可以将++i或i++等运算或一个方法(函数)变成一个原子操作。注意：当一个线程访问object的一个加锁代码块时，另一个线程仍可以访问该object中的非加锁代码块。

单CPU单线程下++、--操作不加同步，线程安全吗？

单CPU多线程下++、--操作不加同步，线程安全吗？ 不安全

多CPU单线程下++、--操作不加同步，线程安全吗？ 不安全

### 1.synchronized(this)

### 2.synchronized method

#### synchronized method == synchronized(this)



##### synchronized(this)  插入monitorenter、monitorexit

```java
public class Sync {
   public int i;
   public void incre(){
       synchronized (this){
           i++;
       }
   }
}
```

class文件到汇编

```shell
javac Sync.java
javap -v Sync.class > Sync.txt
```



```java
Classfile /D:/czt/user-service/src/main/java/org/union/czt/test/Sync.class
  Last modified 2020-8-25; size 400 bytes
  MD5 checksum 305a718f6262336ffeb6c6bddbb72bb6
  Compiled from "Sync.java"
public class org.union.czt.test.Sync
  minor version: 0
  major version: 52
  flags: ACC_PUBLIC, ACC_SUPER
Constant pool:
   #1 = Methodref          #4.#18         // java/lang/Object."<init>":()V
   #2 = Fieldref           #3.#19         // org/union/czt/test/Sync.i:I
   #3 = Class              #20            // org/union/czt/test/Sync
   #4 = Class              #21            // java/lang/Object
   #5 = Utf8               i
   #6 = Utf8               I
   #7 = Utf8               <init>
   #8 = Utf8               ()V
   #9 = Utf8               Code
  #10 = Utf8               LineNumberTable
  #11 = Utf8               incre
  #12 = Utf8               StackMapTable
  #13 = Class              #20            // org/union/czt/test/Sync
  #14 = Class              #21            // java/lang/Object
  #15 = Class              #22            // java/lang/Throwable
  #16 = Utf8               SourceFile
  #17 = Utf8               Sync.java
  #18 = NameAndType        #7:#8          // "<init>":()V
  #19 = NameAndType        #5:#6          // i:I
  #20 = Utf8               org/union/czt/test/Sync
  #21 = Utf8               java/lang/Object
  #22 = Utf8               java/lang/Throwable
{
  public int i;
    descriptor: I
    flags: ACC_PUBLIC

  public org.union.czt.test.Sync();
    descriptor: ()V
    flags: ACC_PUBLIC
    Code:
      stack=1, locals=1, args_size=1
         0: aload_0
         1: invokespecial #1                  // Method java/lang/Object."<init>":()V
         4: return
      LineNumberTable:
        line 3: 0

  public void incre();
    descriptor: ()V
    flags: ACC_PUBLIC
    Code:
      stack=3, locals=3, args_size=1
         0: aload_0
         1: dup
         2: astore_1
         3: monitorenter
         4: aload_0
         5: dup
         6: getfield      #2                  // Field i:I
         9: iconst_1
        10: iadd
        11: putfield      #2                  // Field i:I
        14: aload_1
        15: monitorexit
        16: goto          24
        19: astore_2
        20: aload_1
        21: monitorexit
        22: aload_2
        23: athrow
        24: return
      Exception table:
         from    to  target type
             4    16    19   any
            19    22    19   any
      LineNumberTable:
        line 6: 0
        line 7: 4
        line 8: 14
        line 9: 24
      StackMapTable: number_of_entries = 2
        frame_type = 255 /* full_frame */
          offset_delta = 19
          locals = [ class org/union/czt/test/Sync, class java/lang/Object ]
          stack = [ class java/lang/Throwable ]
        frame_type = 250 /* chop */
          offset_delta = 4
}
SourceFile: "Sync.java"

```

##### synchronized method  flags:  ACC_SYNCHRONIZED，并没有插入monitorenter、monitorexit

```java
package org.union.czt.test;

public class SyncMethod {
    public int i;

    public synchronized void syncTask() {
        i++;
    }
}
```



```shell
javac SyncMethod.java
javap -v SyncMethod.class > SyncMethod.txt
```



```java
Classfile /D:/czt/user-service/src/main/java/org/union/czt/test/SyncMethod.class
  Last modified 2020-8-25; size 303 bytes
  MD5 checksum 51071a590b1d205d4ea19a04851286ff
  Compiled from "SyncMethod.java"
public class org.union.czt.test.SyncMethod
  minor version: 0
  major version: 52
  // ACC_PUBLIC代表public修饰，ACC_SYNCHRONIZED指明该方法为同步方法     
  flags: ACC_PUBLIC, ACC_SUPER
Constant pool:
   #1 = Methodref          #4.#14         // java/lang/Object."<init>":()V
   #2 = Fieldref           #3.#15         // org/union/czt/test/SyncMethod.i:I
   #3 = Class              #16            // org/union/czt/test/SyncMethod
   #4 = Class              #17            // java/lang/Object
   #5 = Utf8               i
   #6 = Utf8               I
   #7 = Utf8               <init>
   #8 = Utf8               ()V
   #9 = Utf8               Code
  #10 = Utf8               LineNumberTable
  #11 = Utf8               syncTask
  #12 = Utf8               SourceFile
  #13 = Utf8               SyncMethod.java
  #14 = NameAndType        #7:#8          // "<init>":()V
  #15 = NameAndType        #5:#6          // i:I
  #16 = Utf8               org/union/czt/test/SyncMethod
  #17 = Utf8               java/lang/Object
{
  public int i;
    descriptor: I
    flags: ACC_PUBLIC

  public org.union.czt.test.SyncMethod();
    descriptor: ()V
    flags: ACC_PUBLIC
    Code:
      stack=1, locals=1, args_size=1
         0: aload_0
         1: invokespecial #1                  // Method java/lang/Object."<init>":()V
         4: return
      LineNumberTable:
        line 3: 0

  public synchronized void syncTask();
    descriptor: ()V
    flags: ACC_PUBLIC, ACC_SYNCHRONIZED
    Code:
      stack=3, locals=1, args_size=1
         0: aload_0
         1: dup
         2: getfield      #2                  // Field i:I
         5: iconst_1
         6: iadd
         7: putfield      #2                  // Field i:I
        10: return
      LineNumberTable:
        line 7: 0
        line 8: 10
}
SourceFile: "SyncMethod.java"

```

#### synchronized static method == synchronized(obj)

```
synchronized static method = synchronized(Object.class) 锁的是class实例，class相关数据存储在（1.6 PermGen、1.7 heap、1.8 metaspace），Object.class信息是共享的，静态方法锁相当于全局锁，会锁住所有调该方法的线程。

ex. Thread t1 = new Thread( );  	t1.start( );
Thread t2 = new Thread( );    		t2.start( );
此种情况下 t1执行了，t2不能执行，因为t2不能进入锁。

https://www.cnblogs.com/GnagWang/archive/2011/02/27/1966606.html#!comments
```

#### synchronized(obj) VS synchronized method 

synchronized(obj)粒度更细，synchronized(obj)更灵活。obj可以是this。synchronized method会将其他不需同步的代码也加上锁，效率稍差些。

### 3.volatile

#### 特点

禁止指令重排序、多线程可见性。 只能保证可见性，不能保证原子性。

#### volatile不保证原子性原因

```
线程之间读取到同样的值然后相互覆盖对方的值 https://blog.csdn.net/weixin_30410999/article/details/98829679
```

#### 多线程可见性

##### Java内存模型

![volatile](http://hongchengjian.gitee.io/md/img/thread/volatile.png)

##### 主内存 VS 工作内存　

主内存：线程共享，方法区和堆

工作内存：线程私有，栈，主内存变量copy的寄存器(包括程序计数器PC和CPU工作的高速缓存)

多个线程之间是不能互相传递数据通信，多线程之间的沟通只能通过共享变量来进行。

##### JVM规范定义线程对内存交互操作8个

```css 
Lock(锁定)：作用于主内存中的变量，把一个变量标识为一条线程独占的状态。
Read(读取)：作用于主内存中的变量，把一个变量的值从主内存传输到线程的工作内存中。
Load(加载)：作用于工作内存中的变量，把read操作从主内存中得到的变量的值放入工作内存的变量副本中。
Use(使用)：作用于工作内存中的变量，把工作内存中一个变量的值传递给执行引擎。
Assign(赋值)：作用于工作内存中的变量，把一个从执行引擎接收到的值赋值给工作内存中的变量。
Store(存储)：作用于工作内存中的变量，把工作内存中的一个变量的值传送到主内存中。
Write(写入)：作用于主内存中的变量，把store操作从工作内存中得到的变量的值放入主内存的变量中。
Unlock(解锁)：作用于主内存中的变量，把一个处于锁定状态的变量释放出来，之后可被其它线程锁定。
```

##### 可见性Copy过程

前提有三个线程1，2，3，假设线程1修改了volatile修饰的变量值，线程2和3可以知道线程1修改后的具体值：

从线程1的工作内存到主内存：Assign(赋值) ---> Store(存储)---> Write(写入)  疑问是开始加Lock锁定？操作结束Unlock解锁？

从主内存到线程2和3的工作内存：Read(读取)---> Load(加载) --->Use(使用)

##### 8个Happen-Before机制

```css
1、单线程happen-before原则：
 在同一个线程中，书写在前面的操作happen-before后面的操作。
2、锁的happen-before原则：
同一个锁的unlock操作happen-before此锁的lock操作。
3、volatile的happen-before原则：
对一个volatile变量的写操作happen-before对此变量的任意操作(当然也包括写操作了)。
4、happen-before的传递性原则：
如果A操作 happen-before B操作，B操作happen-before C操作，那么A操作happen-before C操作。
5、线程启动的happen-before原则：
同一个线程的start方法happen-before此线程的其它方法。
6、线程中断的happen-before原则：
对线程interrupt方法的调用happen-before被中断线程的检测到中断发送的代码。
7、线程终结的happen-before原则：
线程中的所有操作都happen-before线程的终止检测。
8、对象创建的happen-before原则：
一个对象的初始化完成先于他的finalize方法调用。
```



#### volatile使用场景

ConcurrentHashMap多线程的读 get( )没加锁，实现依赖于volatile。

DCL单例必须要volatile

多线程循环中的判断开关是否停止线程

### 4.ReentrantLock

#### ReentrantLock VS synchronized 

ReentrantLock 优点

```css
（1）响应中断：lockInterruptibly( )可以使线程在被阻塞时响应中断
（2）可轮询获取锁: tryLock()调用时锁为空闲状态才获取该锁。如果锁可用，则获取锁，并立即返回值true。如果锁不可用，则此方法将立即返回值false
（3）定时：tryLock(long, TimeUnit)
（4）多Condition：newCondition( ) signal( ) await( )  思考condition作用？
```

synchronized：悲观锁、非公平、可重入、重锁(JDK 1.5)、JDK1.8 synchronized 默认是轻量级锁，锁升级：偏向锁->轻量级锁->重量级锁。

ReentrantLock：非公平锁（默认的lock方法是非公平 默认构造器传boolean类型值）、公平锁、悲观、可重入、互斥锁（独享锁）。

synchronized会被JVM自动解锁，但ReentrantLock加锁后需手动解锁（异常会导致无法正常解锁，finally无论执行过程中是否出现异常，肯定会最终执行）。

#### CAS

CAS注意区分是Compare and Swap还是Compare and Set

（1） Compare and Swap：乐观锁，常见实现数据库乐观锁做version，操作就version+1比较更新。

```css
补充：
    数据库当前时间戳可做乐观锁？
    数据库悲观锁是for update。
    数据库悲观行锁是 where id = XX for update。
```

CAS核心思想是 数据读出来的时候有一个版本v1，在内存中修改，再写回去时发现数据库中的版本不是v1，说明在修改期间别的事务也在修改，则放弃更新操作，把数据重新读出来，重新计算逻辑再重新写回去，不断地重试。

（2）Compare and Set：AtomicXXX

```java
java.util.concurrent.atomic.AtomicLong
//+1操作
public final long getAndIncrement() {
  while (true) {
    long current = get();
    long next = current + 1;
    //当+1操作成功的时候直接返回，退出此循环
    if (compareAndSet(current, next))
      return current;
  }
}

//调用JNI（Java Native Interface）实现CAS
public final boolean compareAndSet(long expect, long update) {
  return unsafe.compareAndSwapLong(this, valueOffset, expect, update);
}
```

#### AQS

AQS：先CAS乐观，后悲观（LCH双向链表修改state做判断）。

阻塞其他线程 VS 不阻塞其他线程

当前加锁对象同一个对象释放锁 VS 其他对象释放锁

先加锁先释放锁 VS 允许插队后直接释放锁

### 5. ThreadLocal

底层是ThreadLocalMap存线程副本。每个Thread都对应一个ThreadLocalMap。数据是以线程为作用域并且不同线程具有不同的数据副本时，采用ThreadLocal。

#### threadLocal为什么用它？

解决多个线程变量冲突。线程隔离每个线程的私有变量。解决跨函数（方法）的共享变量问题。方法间传递的共享变量。跨的是一个线程贯穿的所有函数（方法）。从变量角度来看ThreadLocal，ThreadLocal类似上下文，一般使用时要private static final ThreadLocal<Context> LOCAL = new ThreadLocal<Context>( )，Context支持变量的种类更丰富（因map的value可以是任何类型，map的key可以为null，key为null时，hashcode是0，是数组的第一个元素）。

#### ThreadLocal主要方法

get( )、set( )、remove( )、initialValue( )

其中initialValue( )是延迟调用，protected是让子类覆写，在线程第1次调用get()或set(Object)时才执行，并且仅执行1次。

```java
public class ThreadLocal<T> {    
	/**
     * Returns the value in the current thread's copy of this
     * thread-local variable.  If the variable has no value for the
     * current thread, it is first initialized to the value returned
     * by an invocation of the {@link #initialValue} method.
     *
     * @return the current thread's value of this thread-local
     */
    public T get() {
        Thread t = Thread.currentThread();
        ThreadLocalMap map = getMap(t);
        if (map != null) {
            // ThreadLocalMap的key是当前ThreadLocal对象
            ThreadLocalMap.Entry e = map.getEntry(this);
            if (e != null) {
                @SuppressWarnings("unchecked")
                T result = (T)e.value;
                return result;
            }
        }
        return setInitialValue();
    }
}
```



```java
public class Thread implements Runnable {
	
	/* ThreadLocal values pertaining to this thread. This map is maintained
     * by the ThreadLocal class. */
    ThreadLocal.ThreadLocalMap threadLocals = null;
   
	/**
     * Get the map associated with a ThreadLocal. Overridden in
     * InheritableThreadLocal.
     *
     * @param  t the current thread
     * @return the map
     */
    ThreadLocalMap getMap(Thread t) {
        return t.threadLocals;
    }
}
```



#### 为什么是弱引用？而不是强引用？

弱引用不稳定，很容易被回收，一旦被回收，其登记的key-value形式的数据，此时就变成了null-value，key都消失了，value就找不到了，造成内存泄漏。弱引用只能存活到下一次垃圾收集之前。本质是一个map，集合肯定不是无限制存数据的，集合有上限大小限制。

```java
WeakReference<String> weakReference = new WeakReference<String>(new String("www.threadlocal.cn"));

System.gc();// 强制一次gc()
// 测试一次弱引用的生命周期
if(weakReference.get() == null)
{
    System.out.println("weakReference已经被GC回收");
}
```

threadLocal存的是线程私有变量还是线程公共变量？线程私有变量。

#### 为什么不用new，用threadlocal？

多个线程进来是要排队，排队只能某个时刻服务一个线程。用threadLocal是为每一个线程都对应提供一个自己的空间map，多个线程可以同时访问。

threadLocal存的是方法间的共享变量还是线程之间的共享变量？方法间。

threadLocal是线程间共享？不是。

方法method1(args) 、method2(args)… methodN(args) 若是都要用到这个args作业务逻辑处理，则每个方法都需要创建args在方法链上往后依次传入。而用threadLocal方便直接取，减少了多次创建args的性能损耗

#### ThreadLocal使用上问题

static final 修饰贯穿整个线程的生命周期

线程执行完成后ThreadLocal.remove( )

TLA：java.lang.OutOfMemoryError: getNewTla.

ThreadLocalArea大小值 -[XXtlaSize:min=16k,preferred=](http://docs.oracle.com/cd/E13150_01/jrockit_jvm/jrockit/jrdocs/refman/optionXX.html#wp1020097)1024k,wasteLimit=16k

-XXlargeObjectLimit，限制在本地线程创建对象的最大值

#### demo

```java
// 为每个线程都会开一个连接
private static ThreadLocal<Connection> connectionHolder
    = new ThreadLocal<Connection>() {
    public Connection initialValue() {
        return DriverManager.getConnection(DB_URL);
    }
};
 
public static Connection getConnection() {
    return connectionHolder.get();
}
```

#### InheritableThreadLocal 实现父线程到子线程的值传递原理

```java
public class Thread implements Runnable {
    private void init(ThreadGroup g, Runnable target, String name,
                      long stackSize, AccessControlContext acc,
                      boolean inheritThreadLocals) {
                      
                 // ...
            // 传递时机在创建Thread时。在线程池复用情景中，并没有创建Thread的触发机制，阿里TransmittableThreadLocal解决
                 if (inheritThreadLocals && parent.inheritableThreadLocals != null)
                this.inheritableThreadLocals =
                      ThreadLocal.createInheritedMap(parent.inheritableThreadLocals);
        // ...
                      
  }
}
```

InheritableThreadLocal 实现父线程到子线程的值传递原理

```java
public class TransmittableThreadLocal<T> extends InheritableThreadLocal<T> {
  // holder是一个InheritableThreadLocal变量，该变量在子线程执行过程中(TtlExecutors提供了在子线程执行时加入复制父线程的ThreadLocal)，缓存了所有线程TransmittableThreadLocal(父线程+子线程)
    static InheritableThreadLocal<Map<TransmittableThreadLocal<?>, ?>> holder = new InheritableThreadLocal<Map<TransmittableThreadLocal<?>, ?>>() {
        protected Map<TransmittableThreadLocal<?>, ?> initialValue() {
            return new WeakHashMap();
        }
 
        protected Map<TransmittableThreadLocal<?>, ?> childValue(Map<TransmittableThreadLocal<?>, ?> parentValue) {
            return new WeakHashMap(parentValue);
        }
    };
    // set缓存父线程
    public final void set(T value) {
        super.set(value);
        // 提供set null移除value的功能
        if (null == value) {
            this.removeValue();
        } else {
            this.addValue();
        }
 
    }
    // get缓存子线程
    public final T get() {
        T value = super.get();
        if (null != value) {
            this.addValue();
        }
 
        return value;
    }
 
    void addValue() {
        if (!((Map)holder.get()).containsKey(this)) {
            ((Map)holder.get()).put(this, (Object)null);
        }
    }
 
}
```

####TtlExecutors类使用及源码分析

```java
ExecutorService threadPool= TtlExecutors.getTtlExecutorService(Executors.newFixedThreadPool(poolSize));
```

# 线程切换

操作系统实现线程之间的切换就是需从用户态切换到核心态。

## 什么是用户态？什么是核心态？

用户态：用户态没能力直接操作硬件，没能力访问任意内存地址，不能执行一些 CPU 特权指令。

核心态：可直接操作外设、硬件。

如Kafka 0-Copy 减少了哪两次copy？

Direct Memory Access DMA直接内存读取

## 上下文

上下文是指某一时间点CPU寄存器和程序计数器的内容。

## 上下文切换 Context Switch

上下文切换实际是CPU寄存器切换。上下文切换基本原理是当发生任务切换时，保存当前任务的寄存器到内存中，将下一个即将要切换过来的任务的寄存器状态恢复到当前CPU寄存器中，使其继续执行，同一时刻只允许一个任务独享寄存器。

上下文切换的信息会一直被保存在CPU的内存中，直到被再次使用。

跨核上下文切换 Cross-Core Context Switch：一个线程可以在多个处理器跨核运行。跨核上下文切换代价高，在另一个处理器内核抢占和调度线程会引起缓存丢失，作为缓存丢失和过度上下文切换的结果要访问本地内存。

单核上下文切换：一个线程在单核处理器运行。

## 上下文切换发生场景

1.当前正在执行的任务完成了，系统CPU正常调度下一个任务。

2.当前正在执行的任务遇到I/O等阻塞操作，调度器挂起任务，继续调度下一个任务。

3.多个任务并发抢占锁资源，当前任务没有抢到锁资源，被调度器挂起，继续调度下一个任务。

4.挂起当前任务，比如sleep( )调用让出CPU

5.硬件中断

## 自愿上下文切换cswch  VS 非自愿上下文切换nvcswch

```css
自愿上下文切换		 voluntary context switches  			指进程无法获取所需资源，导致的上下文切换。比如I/O、内存等系统资源不足

非自愿上下文切换	non voluntary context switches		进程由于时间片已到等原因，被系统强制调度，进而发生的上下文切换。比如说，大量进程都在争抢 CPU 时
```

## Linux查看系统上下文切换

vmstat只给出系统总体上下文切换情况

```shell
FIELD DESCRIPTION FOR VM MODE
   Procs
       r: The number of runnable processes (running or waiting for run time).
       b: The number of processes in uninterruptible sleep.

   Memory
       swpd: the amount of virtual memory used.
       free: the amount of idle memory.
       buff: the amount of memory used as buffers.
       cache: the amount of memory used as cache.
       inact: the amount of inactive memory.  (-a option)
       active: the amount of active memory.  (-a option)

   Swap
       si: Amount of memory swapped in from disk (/s).
       so: Amount of memory swapped to disk (/s).

   IO
       bi: Blocks received from a block device (blocks/s).
       bo: Blocks sent to a block device (blocks/s).

   System
       in: The number of interrupts per second, including the clock.
       cs: The number of context switches per second.

   CPU
       These are percentages of total CPU time.
       us: Time spent running non-kernel code.  (user time, including nice time)
       sy: Time spent running kernel code.  (system time)
       id: Time spent idle.  Prior to Linux 2.5.41, this includes IO-wait time.
       wa: Time spent waiting for IO.  Prior to Linux 2.5.41, included in idle.
       st: Time stolen from a virtual machine.  Prior to Linux 2.6.11, unknown.
```



```shell
[root@xx]# vmstat
procs -----------memory---------- ---swap-- -----io---- -system-- ------cpu-----
 r  b   swpd   free   	buff    cache     si   so    bi    bo   in   cs us sy id wa st
 1  0 1388188 957744      0 	516680    0    0     2     8    0    1  0  0 100  0  0
You have new mail in /var/spool/mail/root

r Running or Runnable 	就绪队列的长度，也就是正在运行和等待CPU的进程数
cs context switch 	    每秒上下文切换次数
in	interrupt		   每秒中断的次数
b	Blocked			   处于不可中断睡眠状态的进程数

```

## Linux查看某个进程详细情况

```shell
pidstat -w pid

-u：默认的参数，显示各个进程的cpu使用统计
-r：显示各个进程的内存使用统计
-d：显示各个进程的IO使用情况
-p：指定进程号
-w：显示每个进程的上下文切换情况
-t：显示选择任务的线程的统计信息外的额外信息
-T { TASK | CHILD | ALL }
这个选项指定了pidstat监控的。TASK表示报告独立的task，CHILD关键字表示报告进程下所有线程统计信息。ALL表示报告独立的task和task下面的所有线程。
注意：task和子线程的全局的统计信息和pidstat选项无关。这些统计信息不会对应到当前的统计间隔，这些统计信息只有在子线程kill或者完成的时候才会被收集。
-V：版本号
-h：在一行上显示了所有活动，这样其他程序可以容易解析。
-I：在SMP环境，表示任务的CPU使用率/内核数量
-l：显示命令名和所有参数

```

# 多线程

多线程指两个线程的代码可以同时运行，而不必一个线程需要等待另一个线程内的代码执行完才可以运行。对于单核CPU来说，是无法做到真正的多线程的，每个时间点上，CPU都会执行特定的代码，由于CPU执行代码时间很快，所以两个线程的代码交替执行看起来像是同时执行的一样。那具体执行某段代码多少时间，和分时机制系统有关。

分时系统把CPU时间划分为多个时间片Slice，操作系统以时间片为单位片为单位各个线程的代码，越好的CPU分出的时间片越小。 注意多线程debug时，一个任务执行时间<时间片时间，可能一个线程时间片里跑完了所有任务，并没有经过CPU时间片切换再跑其他线程。

## 多线程效果

用多线程不一定比单线程块

T1 创建线程时间，T2 在线程中执行任务的时间，T3 销毁线程时间。T1 + T3 远大于 T2可采用线程池，以提高服务器性能。

### 多线程计数器

AtomicInteger 编写一个线程安全的计数器，5个线程同时跑，计数到1000，输出线程名和计数直到1000 

CountDownLatch  减计数

CyclicBarrier 加计数

|                     CountDownLatch                     |                     CyclicBarrier                      |
| :----------------------------------------------------: | :----------------------------------------------------: |
|                         减计数                         |                         加计数                         |
|               计数为0时释放所有等待线程                |            计数达到指定值时释放所有等待线程            |
|                  计数为0时，无法重置                   |           计数达到指定值，计数置为0重新开始            |
| countDown( )计数减一，await( )只进行阻塞，对计数没影响 | await( )计数加1，若加1后值不等于构造方法值，则线程阻塞 |
|                      不可重复利用                      |                       可重复利用                       |
|            所有线程任务都执行完才进行下一步            |                  信号发出同一时刻运行                  |



### 所有线程任务都执行完才进行下一步

CountDownLatch来计任务数，计数器的初始化大小和任务数的大小一致(注意与线程数无关)，每执行一次任务，计数器countDown减一，await( )一直阻塞主线程，直到计数器值为0，释放锁(所有任务完成才释放)

### 多线程数量不超过CPU核数

# 死锁

## OS-死锁条件

```css
（1） 互斥条件：一个共享资源（临界资源）每次只能被一个进程使用。
（2） 请求与保持（占有且等待）：一个进程因请求资源而阻塞时，对已获得的资源保持不放。P1占有一个资源a，并等待另一个资源b，而该资源a被其他进程占有所以P1阻塞，但P1不释放已获得的资源a。
（3）不可强行占有（不可剥夺（非抢占)):进程已获得的资源，在末使用完之前，不能被其他进程强行剥夺。资源被P1使用，P1使用过程中不能被P2抢占使用，必须等P1使用完自愿释放。
（4） 循环等待条件:若干进程之间形成一种头尾相接的循环等待资源关系。有一组等待进程 {P0，P1，…，Pn}，P0 等待的资源为 P1 占有，P1 等待的资源为 P2 占有，……，Pn-1 等待的资源为 Pn 占有，Pn 等待的资源为 P0 占有。
只要系统发生死锁，这些条件必然成立，而只要上述条件之一不满足，就不会发生死锁。
```

## 理论-死锁解决方案

思路：可从破坏条件开始

### 死锁预防(严格破坏OS-死锁条件四个条件之一)

有很大可能导致系统资源利用率和系统吞吐量降低

### 死锁避免(死锁避免比死锁预防允许更多的并发)

允许前三个必要条件，但通过算法，确保永远不会到达死锁点

### 死锁避免算法

#### 进程启动拒绝

如果一个进程的请求会导致死锁，则不启动该进程

#### 资源分配拒绝(银行家算法)

**银行家算法**：如果一个进程增加的资源请求会导致死锁，则不允许此分配

### 死锁检测

允许系统在运行过程发生死锁，但可通过系统设置的检测机构及时检测出死锁的发生，并精确地确定于死锁相关的进程和资源，然后采取适当的措施，从系统中将已发生的死锁清除掉。

死锁解除(剥夺资源和撤销进程)

当检测到系统中已发生死锁，需将进程从死锁状态中解脱出来。常用方法：撤销或挂起一些进程，以便回收一些资源，再将这些资源分配给已处于阻塞状态的进程。死锁检测盒解除有可能使系统获得较好的资源利用率和吞吐量，但在实现上难度也最大。

# 锁

## 乐观锁 VS 悲观锁

读多写少 VS 读少写多 思考的重点是阻塞，不阻塞更多的线程。

乐观锁：适合读多写少。Ex.Semaphone、CountDownLatch、ReadWriteLock读锁、CAS、数据库Version。注意带状态、Version的更新必须带上一个Version条件的状态。

悲观锁：适合读少写多。EX. synchronized、ReentrantLock、ReadWriteLock写锁。若写多用乐观锁，大量写每个都CAS会造成大面积阻塞和竞争。

## 公平锁 VS 非公平锁

公平锁（Fair）：考虑排队的线程 FCFS（先对锁提出获取请求的线程先被分配到锁）。

非公平锁（Nonfair）：插队尝试（JVM尝试随机或就近两种分配锁，ReentrantLock默认是非公平锁），不让插队就老实去队尾排队。

非公平锁的性能高于公平锁5～10倍，因为公平锁需在多核CPU情况下维护一个队列。

```java
Lock lock=new ReentrantLock(true);//公平锁 
Lock lock=new ReentrantLock(false);//非公平锁 默认
```

## 可重入锁 VS 非可重入锁

可重入锁（递归锁）：同一线程外层锁、内层还可以加锁或获取锁，嵌套形式。

## 独享锁(互斥锁，独占锁，写锁， 排它锁EXCLUSIVE，一般是悲观锁) VS 共享锁SHARED(读锁，一般是乐观锁)

独享锁（互斥锁，一般是悲观锁，若某个只读线程获取了锁，则其他线程只能等待。避免了读读冲突，但读操作不影响一致性，限制了并发）：同时只能有一个线程获得锁。Ex. ReentrantLock是互斥锁，ReadWriteLock写锁是互斥锁。写锁是代码修改数据，只能一个线程写，且不能同时读，重点是只能一个线程写。

共享锁（读锁，一般是乐观锁，允许多个读操作线程同时访问共享资源）：可以多个线程可同时获得锁。Ex.Semaphone、CountDownLatch是共享锁，ReadWriteLock读锁是共享锁。读锁是代码只读数据，可以很多线程读，但不能同时写，重点是很多线程读。

## 读写锁

如何设计一个读写锁？

![ReadWriteLock](http://hongchengjian.gitee.io/md/img/juc/ReadWriteLock.png)

```java
    	/*
         * Read vs write count extraction constants and functions.
         * Lock state is logically divided into two unsigned shorts:
         * The lower one representing the exclusive (writer) lock hold count,
         * and the upper the shared (reader) hold count.
         */

        static final int SHARED_SHIFT   = 16;
        static final int SHARED_UNIT    = (1 << SHARED_SHIFT);	
 		// (1 << 16)-1 左移16位减1 == 2的16次方-1
		// <<表示二进制左移，即将该数字在二进制下每一位向左移n个，右面补零，数值上扩大了2^n倍
        static final int MAX_COUNT      = (1 << SHARED_SHIFT) - 1;
        static final int EXCLUSIVE_MASK = (1 << SHARED_SHIFT) - 1;
```

ReentrantReadWriteLock中将AQS中的int(32位)类型的state分为高16位与第16位分别记录读锁和写锁的状态。 state&((1<<16)-1)，&是与门，将state的高16位全部抹去，因此state的低位记录着写锁的重入计数。state>>>16 进行无符号补0，右移16位，state的高位记录着写锁的重入计数。

ReentrantReadWriteLock一把读锁ReadLock，一把写锁WriteLock。ReentrantReadWriteLock读写锁互斥，写锁独占，读锁共享，读读不互斥、读写互斥、写写互斥。

读写锁适用场景，高并发情况下，读的操作远远高于写的操作，非高并发下，读写锁由于要额外维护读锁状态，效率不一定比独占锁高。读操作远高于写操作，若不用读写锁，用其他锁会导致读读互斥，高并发下阻塞的线程多。



## 分段锁Segment

分段锁：JDK 1.7 ConcurrentHashMap分16段，最多同时支持16个线程的并发操作。

JDK 1.7 ConcurrentHashMap 数据结构图：

![ConcurrentHashMap分段锁结构](http://hongchengjian.gitee.io/md/img/collection/JDK1.7%20ConcurrentHashMap%20Segment.png)

为什么ConcurrentHashMap后续把分段锁去掉了？JDK 1.7 ConcurrentHashMap是分段锁，JDK 1.8 ConcurrentHashMap降低锁的粒度 。

```css
1.7：Segment + HashEntry + Unsafe
1.8: 移除Segment，使锁的粒度更小，Synchronized + CAS + Node + Unsafe
put( )
    1.7：先定位Segment，再定位bucket，put全程加锁，没有获取锁的线程提前找bucket，并最多自旋64次获取锁，超过则挂起。
    1.8：由于移除了Segment，类似HashMap，可以直接定位到bucket，拿到first节点后进行判断，1、为空则CAS插入；2、为-1则说明在扩容，则跟着一起扩容；3、else则加锁put（类似1.7）
get( ) 
	并发读是依赖volatile, JDK 1.7和JDK1.8都差不多。
resize( )
    1.7：跟HashMap一样，只不过是搬到单线程中执行，避免了HashMap在1.7中扩容时死循环，保证线程安全。
    1.8：支持并发扩容，HashMap扩容在1.8中由头插改为尾插（为了避免死循环问题），ConcurrentHashmap也是，迁移也是从尾部开始，扩容前在bucket的头部放置一个hash值为-1的节点，别的线程访问时就能判断是否该bucket已经被其他线程处理过了。
size( )
    1.7：计算两次，如果不变(调size( )方法计算期间，无新元素插入)则返回计算结果，若不一致，则锁住所有的Segment求和。
    1.8：用baseCount来存储当前的节点个数

```

AtomicXXX：当大量线程同时去访问时，会因为大量线程执行CAS操作失败而进行空转，导致CPU资源消耗过多，而且执行效率也不高。Doug Lea JDK1.8中对CAS进行了优化，基于了CAS分段锁提供了LongAdder。

![LongAdder](http://hongchengjian.gitee.io/md/img/juc/LongAdder.png)

LongAdder父类Striped64维护Cell[]和long base，当多个线程操作一个变量，会先base上进行cas，线程增多时，就使用cell数组。当base将更新值时（调casBase更新base值失败），会自动使用cell数组，每一个线程对应一个cell，每一个线程对cell进行cas操作，可将单一value的更新压力分担到多个value中，大量线程得以分散并发压力，减少了大量线程CAS操作失败而进行空转，提高了并发效率。

## 自旋锁

自旋锁：让线程自旋等一等避免切用户态、核心态的耗时和CPU浪费。

### Q：自旋怎么实现？

```css
wait、notify是条件变量的一种，并不是OS层的自旋，自旋应该是一个空loop，当loop的条件被其他线程改变时再进入临界区，若觉得空循环耗CPU，加上Thread.yield()使线程running ---> runable
```

自旋的实现思想：当一个线程尝试获取某个锁时，如果该锁已被其他线程占用，就一直循环检测锁是否被释放，而不是进入线程挂起或睡眠状态。

自旋锁适用于锁保护的临界区很小的情况，临界区很小的话，锁占用的时间就很短。

https://www.jianshu.com/p/824b2e4f1eed 几种实现

## 偏向锁

### 为什么要偏向锁？

偏向锁：某个线程获得锁之后，消除这个线程以后获取锁重入CAS开销。

轻量级锁（获取及释放锁依赖多次CAS原子指令集）为了在线程交替执行同步块时提高性能，而偏向锁（在置换ThreadID时依赖一次CAS原子指令）在只有一个线程执行同步块时进一步提高性能，因为一个线程多次获得同一个锁不存在锁的竞争。若不用偏向，每次都要竞争锁会增大很多没有必要付出的代价。

### JVM偏向锁相关命令

```shell
-XX:-UseBiasedLocking = false 关闭偏向锁
偏向锁是默认开启的

偏向锁开始时间一般是比应用程序启动慢几秒，不想有这个延迟，命令
-XX:BiasedLockingStartUpDelay=0在对一个Object做syncronized的时候，会立即上一把偏向锁。当处于偏向锁状态时，markword会记录当前线程ID
```

# 锁优化

## 锁膨胀(锁升级)(锁晋升)

### 64 Bit MarkWord

![OS 64bit markword.png](http://hongchengjian.gitee.io/md/img/jvm/OS%2064bit%20markword.png)

锁可以从偏向锁(一次CAS)升级到轻量级锁(获取及释放锁依赖多次CAS原子指令集)，再升级到重量级锁。

### 锁升级路线(单向)

 偏向锁状态---> 轻量级锁状态--->重量级锁状态

![synchronized](http://hongchengjian.gitee.io/md/img/thread/synchronized.png)

### 为什么引入轻量级锁？

轻量级锁考虑的是竞争锁对象的线程不多，线程持有锁的时间也不长的情景。因为阻塞线程需要CPU从用户态转到内核态，如果刚刚阻塞不久这个锁就被释放了，代价较大。干脆不阻塞这个线程，让它自旋这等待锁释放。

### 偏向锁升级轻量级锁

当线程1访问代码块并获取锁对象时，会在java对象头和栈帧中记录偏向的锁的threadID，因为**偏向锁不会主动释放锁**，因此以后线程1再次获取锁的时候，需要**比较当前线程的threadID和Java对象头中的threadID是否一致**，如果一致（还是线程1获取锁对象），则无需使用CAS来加锁、解锁；

偏向锁竞争开始：

如果不一致（其他线程，如线程2要竞争锁对象，而偏向锁不会主动释放因此还是存储的线程1的threadID），需要**查看Java对象头中记录的线程1是否存活**，如果没有存活，那么锁对象被重置为无锁状态，其它线程（线程2）可以竞争将其设置为偏向锁；如果存活，那么立刻**查找该线程（线程1）的栈帧信息LockRecord(LR)，如果还是需要继续持有这个锁对象**，那么暂停当前线程1，撤销偏向锁，升级为轻量级锁，如果线程1 不再使用该锁对象，那么将锁对象状态设为无锁状态，重新偏向新的线程。

其中每个线程通过CAS(自旋)的操作将锁对象头中的markwork设置为指向自己的LR的指针，哪个线程设置成功，就意味着获得锁。

```java
备注：
	与https://yqh.aliyun.com/detail/6169?utm_content=g_1000104857 在偏向锁竞争开始产生观点分歧
```

### 轻量级锁升级重量级锁

线程1获取轻量级锁时会先把锁对象的**对象头MarkWord复制一份到线程1的栈帧中创建的用于存储锁记录的空间**（称为DisplacedMarkWord），然后**使用CAS把对象头中的内容替换为线程1存储的锁记录（**DisplacedMarkWord**）的地址**；

如果在线程1复制对象头的同时（在线程1CAS之前），线程2也准备获取锁，复制了对象头到线程2的锁记录空间中，但是在线程2CAS的时候，发现线程1已经把对象头换了，**线程2的CAS失败，那么线程2就尝试使用自旋锁来等待线程1释放锁**。

但是如果自旋的时间太长也不行，因为自旋是要消耗CPU的，因此自旋的次数是有限制的，比如10次或者100次，如果**自旋次数到了线程1还没有释放锁，或者线程1还在执行，线程2还在自旋等待，这时又有一个线程3过来竞争这个锁对象，那么这个时候轻量级锁就会膨胀为重量级锁。重量级锁把除了拥有锁的线程都阻塞，防止CPU空转。**

### 重量级锁 VS 轻量级锁

重量级锁（Mutex Lock）Ex. Synchronized通过对象内部的监视器锁monitor实现，监视器锁本质是依赖于底层OS的Mutex Lock实现。JDK 1.6以后做了锁膨胀优化：从偏向锁(一次CAS)升级到轻量级锁(获取及释放锁依赖多次CAS原子指令集)，再升级到重量级锁。

### 重量级锁重在哪里？

需做内核态到用户态的转换消耗较多时间

### 偏向锁 VS 轻量级锁  VS 重量级锁

|  锁状态  |                             优点                             |                    缺点                     |                   适用场景                   |
| :------: | :----------------------------------------------------------: | :-----------------------------------------: | :------------------------------------------: |
|  偏向锁  | 加锁无需额外消耗(单线程仅第一次加锁需CAS)和非同步方法时间相差纳秒级 |     竞争的线程多，会有额外的锁撤销消耗      |    基本没有线程竞争锁的同步场景（单线程）    |
| 轻量级锁 |              竞争线程不会阻塞，自旋提高响应速度              | 若一直不能获得锁，长时间的自旋会造成CPU消耗 | 少量线程竞争锁，且锁持有时间短，追求响应速度 |
| 重量级锁 |      线程竞争不适用CPU自旋，不会导致CPU空转消耗CPU资源       |            线程阻塞，响应时间长             |  很多线程竞争锁，锁持有的时间长，追求吞吐量  |

#### 响应速度 VS 吞吐量

响应速度：对请求做出响应的时间快慢

吞吐量：在单位时间内处理请求的数量

### 锁可以升级不可以降级

为了避免无用的自旋，轻量级锁一旦膨胀为重量级锁就不会再降级为轻量级锁了；偏向锁升级为轻量级锁也不能再降级为偏向锁。但是偏向锁状态可以被重置为无锁状态。

### JDK 1.6 synchronized是重量级锁

### JDK1.8 synchronized 默认是轻量级锁，锁升级：偏向锁->轻量级锁->重量级锁

## 减少锁持有时间

只在有需线程安全的程序上加锁

```java
public final class Pattern implements java.io.Serializable {
    public Matcher matcher(CharSequence input) {
        if (!compiled) {
            synchronized(this) {
                if (!compiled)
                    compile();
            }
        }
        Matcher m = new Matcher(this, input);
        return m;
    }
}
```



## 减少锁粒度

大对象进行分片细化成小对象，典型Ex.  JDK1. 7 ConcurrentHashMap 锁细化

## 锁消除 > JDK 1.5

编译器级别。锁消除是指虚拟机即时编译器JIT在运行时，对一些代码上要求同步，对检测到不可能存在共享数据竞争的锁进行削除。

锁消除主要判定依据来源于逃逸分析的数据支持，如果判断到一段代码中，在堆上的所有数据都不会逃逸出去被其他线程访问到，就可以把它们当作栈上数据对待，认为它们是线程私有的，同步加锁自然就无须进行。

```java
 public final class StringBuffer extends AbstractStringBuilder implements java.io.Serializable, CharSequence
{
 	@Override
    public synchronized StringBuffer append(String str) {
        toStringCache = null;
        super.append(str);
        return this;
    }
}
```



```java
public class TestEliminateLocks {
    public static void main(String[] args) {
        long start = System.currentTimeMillis();
        int size = 10000;
        for (int i = 0; i < size; i++) {
            concatStr("hello", "world");
        }
        long timeCost = System.currentTimeMillis() - start;
        System.out.println("concatStr:" + timeCost + " ms");
    }

    // sb仅在concatStr(str1, str2)作用域中有效，不同线程同时调concatStr(str1, str2)都会创建不同的sb对象，若此时append使用同步浪费系统资源
    public static String concatStr(String str1, String str2) {
        StringBuffer sb = new StringBuffer();
        // append方法是同步操作
        sb.append(str1);
        sb.append(str2);
        return sb.toString();
    }
}
```



```shell
-server -XX:+DoEscapeAnalysis -XX:+EliminateLocks 
+DoEscapeAnalysis表示开启逃逸分析，+EliminateLocks表示锁消除
```



```java
This is an example of manual "lock coarsening" and may have been done to get a performance boost.

Consider these two snippets:
// the first case
StringBuffer b = new StringBuffer();
for(int i = 0 ; i < 100; i++){
    b.append(i);
}
versus:
// the second case
StringBuffer b = new StringBuffer();
synchronized(b){
  for(int i = 0 ; i < 100; i++){
     b.append(i);
  }
}
In the first case, the StringBuffer must acquire and release a lock 100 times (because append is a synchronized method), whereas in the second case, the lock is acquired and released only once. This can give you a performance boost and is probably why the author did it. In some cases, the compiler can perform this lock coarsening for you (but not around looping constructs because you could end up holding a lock for long periods of time).

By the way, the compiler can detect that an object is not "escaping" from a method and so remove acquiring and releasing locks on the object altogether (lock elision) since no other thread can access the object anyway. A lot of work has been done on this in JDK7.
```



## 锁粗化

对同一个锁不停地进行请求、同步和释放，本身也会消耗系统宝贵的资源，不利于性能的优化。锁的请求、同步与释放本身会带来性能损耗，高频的锁请求不利于系统性能。**把很多次锁的请求合并成一个请求，以降低短时间内大量锁请求、同步、释放的性能损耗**

```java
public void doSth(){
    synchronized(lock){
        //do some thing
    }
    // logic代码，做其它不需要同步的工作，但能很快执行完毕
    synchronized(lock){
        //do other thing
    }
}
```

前提是中间不需要同步的代码能够很快速地完成

```java
public void doSomethingMethod(){
    // 进行锁粗化：整合成一次锁请求、同步、释放
    synchronized(lock){
        //do some thing
        // logic代码，做其它不需要同步的工作，但能很快执行完毕
        //do other thing
    }
}
```



## 锁分离

ReadWriteLock读锁、写锁分离，实现读读不互斥、读写互斥、写写互斥。LinkedBlockingQueue从头部取出，从尾部放数据。

## 锁续约

分布式锁redisson 锁过期expire时间比执行完任务时间要长，redisson(加锁、解锁、续约)看门狗WatchDog在加锁后会注册一个定时任务监听锁，检查周期是：加锁失效时间的1/3，如加锁3s释放，检查是1s一次，加锁业务没执行完，会自动续期重置为加锁失效时间3s。requestId可以是当前线程id也可以唯一标识业务处理的id。

业务的机器万一宕机定时任务跑不了,就续不了期,那自然30秒之后锁就解开了。

```java
@Slf4j
@Service
public class RedisDistributionLockPlus {
 
    /**
     * 加锁超时时间，单位毫秒， 即：加锁时间内执行完操作，如果未完成会有并发现象
     */
    private static final long DEFAULT_LOCK_TIMEOUT = 30;
 
    private static final long TIME_SECONDS_FIVE = 5 ;
 
    /**
     * 每个key的过期时间 {@link LockContent}
     */
    private Map<String, LockContent> lockContentMap = new ConcurrentHashMap<>(512);
 
    /**
     * redis执行成功的返回
     */
    private static final Long EXEC_SUCCESS = 1L;
 
    /**
     * 获取锁lua脚本， k1：获锁key, k2：续约耗时key, arg1:requestId，arg2：超时时间
     */
    private static final String LOCK_SCRIPT = "if redis.call('exists', KEYS[2]) == 1 then ARGV[2] = math.floor(redis.call('get', KEYS[2]) + 10) end " +
            "if redis.call('exists', KEYS[1]) == 0 then " +
               "local t = redis.call('set', KEYS[1], ARGV[1], 'EX', ARGV[2]) " +
               "for k, v in pairs(t) do " +
                 "if v == 'OK' then return tonumber(ARGV[2]) end " +
               "end " +
            "return 0 end";
 
    /**
     * 释放锁lua脚本, k1：获锁key, k2：续约耗时key, arg1:requestId，arg2：业务耗时 arg3: 业务开始设置的timeout
     */
    private static final String UNLOCK_SCRIPT = "if redis.call('get', KEYS[1]) == ARGV[1] then " +
            "local ctime = tonumber(ARGV[2]) " +
            "local biz_timeout = tonumber(ARGV[3]) " +
            "if ctime > 0 then  " +
               "if redis.call('exists', KEYS[2]) == 1 then " +
                   "local avg_time = redis.call('get', KEYS[2]) " +
                   "avg_time = (tonumber(avg_time) * 8 + ctime * 2)/10 " +
                   "if avg_time >= biz_timeout - 5 then redis.call('set', KEYS[2], avg_time, 'EX', 24*60*60) " +
                   "else redis.call('del', KEYS[2]) end " +
               "elseif ctime > biz_timeout -5 then redis.call('set', KEYS[2], ARGV[2], 'EX', 24*60*60) end " +
            "end " +
            "return redis.call('del', KEYS[1]) " +
            "else return 0 end";
    /**
     * 续约lua脚本
     */
    private static final String RENEW_SCRIPT = "if redis.call('get', KEYS[1]) == ARGV[1] then return redis.call('expire', KEYS[1], ARGV[2]) else return 0 end";
 
 
    private final StringRedisTemplate redisTemplate;
 
    public RedisDistributionLockPlus(StringRedisTemplate redisTemplate) {
        this.redisTemplate = redisTemplate;
        ScheduleTask task = new ScheduleTask(this, lockContentMap);
        // 启动定时任务
        ScheduleExecutor.schedule(task, 1, 1, TimeUnit.SECONDS);
    }
 
    /**
     * 加锁
     * 取到锁加锁，取不到锁一直等待知道获得锁
     *
     * @param lockKey
     * @param requestId 全局唯一
     * @param expire   锁过期时间, 单位秒
     * @return
     */
    public boolean lock(String lockKey, String requestId, long expire) {
        log.info("开始执行加锁, lockKey ={}, requestId={}", lockKey, requestId);
        for (; ; ) {
            // 判断是否已经有线程持有锁，减少redis的压力
            LockContent lockContentOld = lockContentMap.get(lockKey);
            boolean unLocked = null == lockContentOld;
            // 如果没有被锁，就获取锁
            if (unLocked) {
                long startTime = System.currentTimeMillis();
                // 计算超时时间
                long bizExpire = expire == 0L ? DEFAULT_LOCK_TIMEOUT : expire;
                String lockKeyRenew = lockKey + "_renew";
 
                RedisScript<Long> script = RedisScript.of(LOCK_SCRIPT, Long.class);
                List<String> keys = new ArrayList<>();
                keys.add(lockKey);
                keys.add(lockKeyRenew);
                Long lockExpire = redisTemplate.execute(script, keys, requestId, Long.toString(bizExpire));
                if (null != lockExpire && lockExpire > 0) {
                    // 将锁放入map
                    LockContent lockContent = new LockContent();
                    lockContent.setStartTime(startTime);
                    lockContent.setLockExpire(lockExpire);
                    lockContent.setExpireTime(startTime + lockExpire * 1000);
                    lockContent.setRequestId(requestId);
                    lockContent.setThread(Thread.currentThread());
                    lockContent.setBizExpire(bizExpire);
                    lockContent.setLockCount(1);
                    lockContentMap.put(lockKey, lockContent);
                    log.info("加锁成功, lockKey ={}, requestId={}", lockKey, requestId);
                    return true;
                }
            }
            // 重复获取锁，在线程池中由于线程复用，线程相等并不能确定是该线程的锁
            if (Thread.currentThread() == lockContentOld.getThread()
                      && requestId.equals(lockContentOld.getRequestId())){
                // 计数 +1
                lockContentOld.setLockCount(lockContentOld.getLockCount()+1);
                return true;
            }
 
            // 如果被锁或获取锁失败，则等待100毫秒
            try {
                TimeUnit.MILLISECONDS.sleep(100);
            } catch (InterruptedException e) {
                // 这里用lombok 有问题
                log.error("获取redis 锁失败, lockKey ={}, requestId={}", lockKey, requestId, e);
                return false;
            }
        }
    }
 
 
    /**
     * 解锁
     *
     * @param lockKey
     * @param lockValue
     */
    public boolean unlock(String lockKey, String lockValue) {
        String lockKeyRenew = lockKey + "_renew";
        LockContent lockContent = lockContentMap.get(lockKey);
 
        long consumeTime;
        if (null == lockContent) {
            consumeTime = 0L;
        } else if (lockValue.equals(lockContent.getRequestId())) {
            int lockCount = lockContent.getLockCount();
            // 每次释放锁， 计数 -1，减到0时删除redis上的key
            if (--lockCount > 0) {
                lockContent.setLockCount(lockCount);
                return false;
            }
            consumeTime = (System.currentTimeMillis() - lockContent.getStartTime()) / 1000;
        } else {
            log.info("释放锁失败，不是自己的锁。");
            return false;
        }
 
        // 删除已完成key，先删除本地缓存，减少redis压力, 分布式锁，只有一个，所以这里不加锁
        lockContentMap.remove(lockKey);
 
        RedisScript<Long> script = RedisScript.of(UNLOCK_SCRIPT, Long.class);
        List<String> keys = new ArrayList<>();
        keys.add(lockKey);
        keys.add(lockKeyRenew);
 
        Long result = redisTemplate.execute(script, keys, lockValue, Long.toString(consumeTime),
                Long.toString(lockContent.getBizExpire()));
        return EXEC_SUCCESS.equals(result);
 
    }
 
    /**
     * 续约
     *
     * @param lockKey
     * @param lockContent
     * @return true:续约成功，false:续约失败（1、续约期间执行完成，锁被释放 2、不是自己的锁，3、续约期间锁过期了（未解决））
     */
    public boolean renew(String lockKey, LockContent lockContent) {
 
        // 检测执行业务线程的状态
        Thread.State state = lockContent.getThread().getState();
        if (Thread.State.TERMINATED == state) {
            log.info("执行业务的线程已终止,不再续约 lockKey ={}, lockContent={}", lockKey, lockContent);
            return false;
        }
 
        String requestId = lockContent.getRequestId();
        long timeOut = (lockContent.getExpireTime() - lockContent.getStartTime()) / 1000;
 
        RedisScript<Long> script = RedisScript.of(RENEW_SCRIPT, Long.class);
        List<String> keys = new ArrayList<>();
        keys.add(lockKey);
 
        Long result = redisTemplate.execute(script, keys, requestId, Long.toString(timeOut));
        log.info("续约结果，True成功，False失败 lockKey ={}, result={}", lockKey, EXEC_SUCCESS.equals(result));
        return EXEC_SUCCESS.equals(result);
    }
 
 
    static class ScheduleExecutor {
 
        public static void schedule(ScheduleTask task, long initialDelay, long period, TimeUnit unit) {
            long delay = unit.toMillis(initialDelay);
            long period_ = unit.toMillis(period);
            // 定时执行
            new Timer("Lock-Renew-Task").schedule(task, delay, period_);
        }
    }
 
    static class ScheduleTask extends TimerTask {
 
        private final RedisDistributionLockPlus redisDistributionLock;
        private final Map<String, LockContent> lockContentMap;
 
        public ScheduleTask(RedisDistributionLockPlus redisDistributionLock, Map<String, LockContent> lockContentMap) {
            this.redisDistributionLock = redisDistributionLock;
            this.lockContentMap = lockContentMap;
        }
 
        @Override
        public void run() {
            if (lockContentMap.isEmpty()) {
                return;
            }
            Set<Map.Entry<String, LockContent>> entries = lockContentMap.entrySet();
            for (Map.Entry<String, LockContent> entry : entries) {
                String lockKey = entry.getKey();
                LockContent lockContent = entry.getValue();
                long expireTime = lockContent.getExpireTime();
                // 减少线程池中任务数量
                if ((expireTime - System.currentTimeMillis())/ 1000 < TIME_SECONDS_FIVE) {
                    //线程池异步续约
                    ThreadPool.submit(() -> {
                        boolean renew = redisDistributionLock.renew(lockKey, lockContent);
                        if (renew) {
                            long expireTimeNew = lockContent.getStartTime() + (expireTime - lockContent.getStartTime()) * 2 - TIME_SECONDS_FIVE * 1000;
                            lockContent.setExpireTime(expireTimeNew);
                        } else {
                            // 续约失败，说明已经执行完 OR redis 出现问题
                            lockContentMap.remove(lockKey);
                        }
                    });
                }
            }
        }
    }
}
```

# Redis

## 简介

Redis、Tair、MemCache，MemCache单个value限制1M，但Redis存较大value、较大key的数据(阻塞后有雪崩风险)。Redis是位存储内存贵，不利于作为海量数据高性能读写，钱多啥都可以。Redis单行命令读写具原子性、多行不具原子性，Redis无事务，若要保证事务，需通过Lua插件。Redis单机CP，单进程多线程。Redis集群是AP。Tair是2010年淘宝研发的Key/Value数据存储系统，四种引擎mdb(基于MemCache)、rdb(基于Redis)、kdb(基于Kyoto Cabinet)、lob(基于Leveldb)。Redis没有提供sharding封装，但Tair提供给了sharding封装。Tair对每个数据都包含版本号，版本号在每次更新后都递增，解决并发操作同一条数据的问题，如key的value为'a,b,c'，操作A加一个d，value为'a,b,c,d'，操作B加一个e，value为'a,b,c,e'，不加版本控制，操作A和B谁先更新会覆盖后面的更新值。非持久化（mdb,rdb），持久化（kdb,ldb）。

## 原理

### Redis epoll

Redis单线程处理网络指令，不考虑并发安全，顺序线性执行。多路复用IO没有最大并发连接数限制，上限是操作系统句柄数cat /proc/sys/fs/file-max，epoll只管大量并发连接中少量活跃的连接数，和连接总数无关。epoll获取事件无须遍历整个被侦听描述符集FD，只需遍历被内核IO事件异步唤醒而加入Ready队列的描述符号集FD。epoll采用内存拷贝技术。epoll除了支持IO事件的LT Level Triggered水平触发，还提供边缘触发Edge Triggered。LT VS ET Level Triggered(默认，同时支持block和no-block socket)  VS 边缘触发Edge Triggered(只支持non-block socket)

cat /proc/sys/fs/file-max(整个系统级别限制，不针对用户) VS ulimit -n(用户)

### epoll指令

```css
epoll_create  创建一个epoll FD File Discriptor。
epoll_ctl 用来添加/修改/删除需要侦听的文件描述符及其事件。
epoll_wait 接收发生在被侦听的描述符上的，用户感兴趣的IO事件(短链接中大量调用造成系统瓶颈)。
```

### FD

```css
File Descriptor 文件描述符。
每一个文件描述符会与一个打开文件相对应。
不同的文件描述符也会指向同一个文件。
相同的文件可以被不同的进程打开也可以在同一个进程中被多次打开。
```

### epoll VS select/poll

1G内存 epoll可打开的FD是10W左右，而Select是默认FD_SETSIZE 1024。

select/poll有很大socket集合时，每次调用会线性扫描全部的集合导致IO效率线性下降，epoll只会对活跃socket进行操作。

高速的LAN，epoll效率并不一定比select/poll高，一旦使用idle connection模拟WAN环境，epoll效率远在select/poll之上。

## 场景

热数据(访问频繁)、缓压力(下游DB)、预热(长驻内存数据)

## 心得

使用缓存最重要确保抽离整个缓存，系统还能运转。

## 集群模式

### (1)主从

架构一主多从，主存在单点风险，主从同步是全量复制耗内存，难在线扩容，从库进行replication可避免单点故障，主库Master可读也可写，写库自动同步给从库Slave，Slave只读不写。

### (2)哨兵

Sentinel心跳+投票裁决 自动监控Master/Slave

监控什么？（1）主库和从库是否正常运行。（2）主库挂了，从库是否能切过去成为新主库。

### (2)哨兵

```css
故障切换（failover）哨兵负责主库宕机之后的投票选举，实现自动化故障发现和转移。
监控（1）主库和从库是否正常运行。（2）主库挂了，从库是否能切过去成为新主库（Pub、Sub模式）
```

Sentinel心跳+投票裁决 自动监控Master/Slave

补充 sentine config

```shell
tmpwatch --atime 30d /tmp 清除/tmp目录下30天没有被访问文件
```

### Redis Cluster 去中心化分片集群

Redis Cluster是Redis 3.0+之后官方推荐，基于HASH_SLOT = CRC16(key) mod 16384实现集群分片和数据跨主机转移和共享，可以实现Redis动态扩容和缩容。注意HASH_SLOT只会分配给主库，从库不会被分配。HASH_SLOT目的是分摊key到片区的主库，减少雪崩风险，缓解传统单一主库的压力。如果写入的key计算出的HASH_SLOT不在当前操作的主库 HASH_SLOT_RANGE内，会自动将key转发到HASH_SLOT_RANGE包含HASH_SLOT的主库进行写。

3.0+支持sharding，无中心网状结构，使用端连接任何一个节点即可，节点动态添加、动态删除不影响集群，端与Redis节点连接不需走Proxy层。半数节点检测到某个节点失效则判定节点失效。在resharding期间，原来同一个HASH_SLOT的key被迁移到不同的node中，multi-key操作可能不可用。

#### Redis Cluster VS 传统Redis集群

```css
传统集群缺陷：(1)始终只有一个主库接收和处理写，主库和从库完全同步，同步效率低，大量冗余数据(2)读写分离只有主库写，高并发下主库压力大，主同步从负荷加重，若过程中出现雪崩导致大量key失效和丢失数据(3)中心化集群方案：任何时候都需保证至少一个主库正常运行，主库宕机后，哨兵模式正在投票选举，由于在投票选举之前，谁也不知道新主库是谁，Redis会开启保护机制、禁止写操作直到选举出新主库)，主库和从库耦合度高。
```

#### 搭建

```
https://blog.csdn.net/qq_30056341/article/details/103320138 补充画出机器模型，尝试搭建
```

##Redis常用Jar

```spreadsheet
redisTemplate、jedis、redisson
jar包常用jedis-2.9.0.jar、spring-data-commons-1.8.4.RELEASE.jar、spring-data-redis-1.8.4.RELEASE.jar
```

## 数据结构和命令

http://redisdoc.com/ 

eval(执行Lua)、scan(cursor based iterator)、HSCAN、ZSCAN

注意思考命令算法复杂度、空间复杂度，时间复杂度是O(n)涉及命令还有哪些？

```css
String: MSET、MSETNX、MGET
List: LPUSH、RPUSH、LRANGE、LINDEX、LSET、LINSERT
Hash: HDEL、HGETALL、HKEYS/HVALS
Set: SADD、SREM、SRANDMEMBER、SPOP、
		谨慎使用 SMEMBERS、SUNION/SUNIONSTORE、SINTER/SINTERSTORE、SDIFF/SDIFFSTO
Sorted Set: ZADD、ZREM、
		谨慎使用 O(Log(N)+M):ZRANGE/ZREVRANGE、ZRANGEBYSCORE/ZREVRANGEBYSCORE、ZREMRANGEBYRANK/ZREMRANGEBYSCORE
DEL、KEYS(会占用唯一线程的大量处理时间，导致所有请求都被拖慢)
```

为什么在删除hash set list等复杂元素时 时间复杂度不为O(1) 不能一次性删除hash等里面的所有元素吗，为什么要遍历删除?
DEL的时间复杂度是O(1)还是O(n)？
时间复杂度为O(1)命令有哪些？

### String

```css
JSONString、ToString、StringFormat等任何形式的String

SET 若key已经持有其他值， SET就覆写旧值，无视类型
SETNX SET if Not Exists若不存在，则 SET。若key 已经存在，则 SETNX 不做任何动作。
SETEX 将value 关联到 key，并将 key 的生存时间设为 seconds, key 已经存在， SETEX 命令将覆写旧值。
PSETEX 将value 关联到 key，并将 key 的生存时间设为毫秒
GET
GETSET  将给定 key 的值设为 value ，并返回 key 的旧值(old value)。当 key 存在但不是字符串类型时，返回一个错误。当key没有旧值，key不存在时，返回nil
STRLEN
APPEND
SETRANGE
GETRANGE
INCR 使用场景：热点+时效(1)热点数据：交易行为、库存、商品浏览数、问题、帖子、回复数、点赞数(2)时效信息存储，巧妙利用过期时间：App登陆码30s有效、session防止一个用户多长时间内重复登录、验证码(短信、图形、邮件)
某个用户一分钟内只能发三条短信验证码验证，set key exprireTime =60s，每发一次短信就incre key + 1，limit 3条可放Apollo配置中心，每次发短信前判断get key value <= limit。
INCRBY 
INCRBYFLOAT
DECR
DECRBY
MSET
MSET key1 value1 key2 value2 .. keyN valueN
MSET 涉及相关Redis源码：void msetGenericCommand(redisClient *c, int nx) / t_string.c
 
每分钟某个用户访问服务接口数不超过阀值n次，set key exprireTime = 60s，每访问一次就incre key + 1。  
MSET是原子命令Atomic，PIPELINE是非原子命令，Atomic：一个不可分割的最小工作单位，都成功或都失败。

无论Redis Cluster 还是Codis，批量操作MGET、MSET命令都受限；事务受限。
PIPELINE效率比MSET批量效率高些，Redis执行1次操作时间 = 1次网络时间 + 1次命令时间，执行n 次操作时间 = n 次网络时间 + n 次命令时间。执行1次PIPELINE(n条命令) = 1次网络时间 + n次命令时间，注意PIPELINE一次携带的数据量过大会影响1次网络时间过长。Redis在真正处理批量数据时是单线程For，执行到For时会独占CPU，但比耗在TCP闭合有价值。注意Redis Cluster是不支持PIPELINE和MSET命令，PIPELINE每次只能作用在一个Redis节点上。

PIPELINE是 http://redisdoc.com/中没有的，PIPELINE是Jedis包中提供，原理是一组命令放在MULTI和EXEC之间，注意DISCARD可以停止，但已执行的命令不能回滚。严格说：Redis不支持事务。MULTI和EXEC之间命令错误，语法不正确，导致事务不能正常结束，直接抛error：EXECABORT Transaction discarded because of previous error；运行错误，语法正确，但类型错误，事务可以正常结束，最后一步是OK，中间会报error；使用WATCH后，MULTI失效。

MSETNX
MGET
```

#### Jedis PIPELINE

```java
@Configuration
public class JedisClusterConfig {

    @Value("${spring.redis.cluster.nodes}")
    private String clusterNodes;

    @Value("${spring.redis.cache.commandTimeout}")
    private Integer commandTimeout;

    @Bean
    public JedisCluster getJedisCluster() {

        String[] serverArray = clusterNodes.split(",");
        Set<HostAndPort> nodes = new HashSet<>();
        for (String ipPort : serverArray) {
            String[] ipPortPair = ipPort.split(":");
            nodes.add(new HostAndPort(ipPortPair[0].trim(), Integer.valueOf(ipPortPair[1].trim())));
        }
        return new JedisCluster(nodes, commandTimeout);
    }
}

@Component
public class JedisClusterUtil {

    @Autowired
    private JedisCluster jedisCluster;

    @Resource(name = "redisTemplate4Json")
    protected RedisTemplate<String, Object> redisTemplate;

    /**
     * ZSet批量查询
     * @param keys
     * @return
     */
    public List<Object> batchZRange(List<String> keys) {

        List<Object> resList = new ArrayList<>();
        if (keys == null || keys.size() == 0) {
            return resList;
        }

        if (keys.size() == 1) {
            BoundZSetOperations<String, Object> operations = redisTemplate.boundZSetOps(keys.get(0));
            Set<Object> set = operations.reverseRange(0, 0);
            resList.add(set.iterator().next());
            return resList;
        }

        Map<JedisPool, List<String>> jedisPoolMap = getJedisPool(keys);

        List<String> keyList;
        JedisPool currentJedisPool = null;
        Pipeline currentPipeline;
        List<Object> res = new ArrayList<>();
        Map<String, Object> resultMap = new HashMap<>();

        //执行
        for (Map.Entry<JedisPool, List<String>> entry : jedisPoolMap.entrySet()) {
            Jedis jedis = null;
            try {
                currentJedisPool = entry.getKey();
                keyList = entry.getValue();
                //获取pipeline
                jedis = currentJedisPool.getResource();
                currentPipeline = jedis.pipelined();
                for (String key : keyList) {
                    currentPipeline.zrevrange(key, 0, 0);
                }
                //从pipeline中获取结果
                res = currentPipeline.syncAndReturnAll();
                currentPipeline.close();
                for (int i = 0; i < keyList.size(); i++) {
                    if (null == res.get(i)) {
                        resultMap.put(keyList.get(i), null);
                    } else {
                        Set<Object> set = (Set<Object>) res.get(i);
                        if (null == set || set.isEmpty()) {
                            resultMap.put(keyList.get(i), null);
                        } else {
                            byte[] byteStr = set.iterator().next().toString().getBytes();
                            Object obj = redisTemplate.getDefaultSerializer().deserialize(byteStr);
                            resultMap.put(keyList.get(i), obj);
                        }
                    }
                }
            } catch (Exception e) {
                e.printStackTrace();
            } finally {
                returnResource(jedis, currentJedisPool);
            }
        }
        resList = sortList(keys, resultMap);
        return resList;
    }

    /**
     * Value批量查询
     * @param keys
     * @return
     */
    public List<Object> batchGet(List<String> keys){
        List<Object> resList = new ArrayList<>();
        if (keys == null || keys.size() == 0) {
            return resList;
        }

        if (keys.size() == 1) {
            BoundValueOperations<String, Object> operations = redisTemplate.boundValueOps(keys.get(0));
            resList.add(operations.get());
            return resList;
        }

        Map<JedisPool, List<String>> jedisPoolMap = getJedisPool(keys);

        List<String> keyList;
        JedisPool currentJedisPool = null;
        Pipeline currentPipeline;
        List<Object> res = new ArrayList<>();
        Map<String, Object> resultMap = new HashMap<>();

        for (Map.Entry<JedisPool, List<String>> entry : jedisPoolMap.entrySet()) {
            Jedis jedis = null;
            try {
                currentJedisPool = entry.getKey();
                keyList = entry.getValue();
                //获取pipeline
                jedis = currentJedisPool.getResource();
                currentPipeline = jedis.pipelined();
                for (String key : keyList) {
                    currentPipeline.get(key);
                }
                //从pipeline中获取结果
                res = currentPipeline.syncAndReturnAll();
                currentPipeline.close();
                for (int i = 0; i < keyList.size(); i++) {
                    if (null == res.get(i)) {
                        resultMap.put(keyList.get(i), null);
                    } else {
                        byte[] byteStr = keyList.get(i).toString().getBytes();
                        Object obj = redisTemplate.getDefaultSerializer().deserialize(byteStr);
                        resultMap.put(keyList.get(i), obj);
                    }
                }
            } catch (Exception e) {
                e.printStackTrace();
            } finally {
                returnResource(jedis, currentJedisPool);
            }
        }
        resList = sortList(keys, resultMap);
        return resList;
    }

    private Map<JedisPool, List<String>> getJedisPool(List<String> keys){
        //JedisCluster继承了BinaryJedisCluster
        //BinaryJedisCluster的JedisClusterConnectionHandler属性
        //里面有JedisClusterInfoCache，根据这一条继承链，可以获取到JedisClusterInfoCache
        //从而获取slot和JedisPool直接的映射
        MetaObject metaObject = SystemMetaObject.forObject(jedisCluster);
        JedisClusterInfoCache cache = (JedisClusterInfoCache) metaObject.getValue("connectionHandler.cache");
        //保存地址+端口和命令的映射
        Map<JedisPool, List<String>> jedisPoolMap = new HashMap<>();

        JedisPool currentJedisPool = null;
        List<String> keyList;
        for (String key : keys) {
            //计算哈希槽
            int crc = JedisClusterCRC16.getSlot(key);
            //通过哈希槽获取节点的连接
            currentJedisPool = cache.getSlotPool(crc);

            //由于JedisPool作为value保存在JedisClusterInfoCache中的一个map对象中，每个节点的
            //JedisPool在map的初始化阶段就是确定的和唯一的，所以获取到的每个节点的JedisPool都是一样
            //的，可以作为map的key
            if (jedisPoolMap.containsKey(currentJedisPool)) {
                jedisPoolMap.get(currentJedisPool).add(key);
            } else {
                keyList = new ArrayList<>();
                keyList.add(key);
                jedisPoolMap.put(currentJedisPool, keyList);
            }
        }
        return jedisPoolMap;
    }

    private List<Object> sortList(List<String> keys, Map<String, Object> params) {
        List<Object> resultList = new ArrayList<>();
        Iterator<String> it = keys.iterator();
        while (it.hasNext()) {
            String key = it.next();
            resultList.add(params.get(key));
        }
        return resultList;
    }

    /**
     * 释放jedis资源
     *
     * @param jedis
     */
    public void returnResource(Jedis jedis, JedisPool jedisPool) {
        if (jedis != null && jedisPool != null) {
            jedisPool.returnResource(jedis);
        }
    }
```

### Hash

```css
大Key：小Key-Value键值对
涉及命令hset、hget、hmset、hmget、hkeys、hvals。使用场景(1)大业务对象、层级对象直接序列化 (2)结构化数据如JSON
redis hash的底层是hashtable？
redis存省，城市信息结构该如何设计？

HSET
HSETNX
HGET
HEXISTS
HDEL
HLEN
HSTRLEN
HINCRBY
HINCRBYFLOAT
HMSET
HMGET
HKEYS
HVALS
HGETALL
HSCAN
```

### List

```css
列表(有序，按插入顺序排序)涉及命令lpush、rpush、lrang、lindex、lset。使用场景：(1)消息队列，利用过期时间来做延时，好处是消费性能很高，最致命缺陷是缺少ACK，具体命令涉及BLPOP/BRPOP，参考https://redis.io/topics/data-types-intro中Blocking operations on lists，优先选型kafka(实时高吞吐量，丢数据，加ZooKeeper搭集群多份replica可减少丢数据的情况)、rabbitMQ(自定义延时，缺陷有序消费实现binding key、routing key复杂)、rocketMQ(仅支持18level延时缺陷，优点是积压能力是几个MQ中最好的，rocketMQ具备XA的事务能力)替代list(2)最新上架推荐产品 ltrim 可修剪出从start到stop指定范围的元素。
LPUSH list左侧插入1个或多个元素
LPUSHX
RPUSH
RPUSHX
LPOP
RPOP
RPOPLPUSH
LREM
LLEN
LINDEX
LINSERT
LSET
LRANGE
LTRIM
BLPOP
BRPOP
BRPOPLPUSH
```

### Set

```css
集合(各个元素都不同，但不是自动有序的)涉及命令 sadd、smembers、spop、sdiff、sunion。使用场景(1)去重，比如爬虫增量式爬取时对URI去重 (2)交并差集，比如用户行为的相似度分析，不同用户感兴趣的商品数量、社交共同好友的关注度分析
SADD
SISMEMBER
SPOP
SRANDMEMBER
SREM
SMOVE
SCARD
SMEMBERS
SSCAN
SINTER
SINTERSTORE
SUNION
SUNIONSTORE
SDIFF
SDIFFSTORE
```

### ZSet

```css
有序集合 
利用了一个Score参数来存储数据自动排序，为了优化排序和查找性能，items内容在大于64时同时使用了hash和skiplist，小于64时是ziplist（元素很小的情况下省内存），时间复杂度是O(n)涉及命令zadd、zrange、zcard。使用场景(1)有序不重复，比如商品热度，购买量作为score，Sorted Set按售卖量排序(2)自动排序需求
ZSet(有序)底层数据结构包括ziplist或skiplist。
ziplist vs skiplist
ziplist 使用内存更小 为什么内存小？ ziplist会比hashtable节省内存，节省大约50%。ziplist采用一段连续的内存来存储数据，相比hashtable减少了内存碎片和指针的内存占用。而且当节点较少时，ziplist更容易被加载到CPU缓存中。
skiplist的增加元素时间复杂度是、查询平均是O(n)？还是O(lgn)
O(lgn)  推理论文参考 https://klevas.mif.vu.lt/~ragaisis/ADS2006/skiplists.pdf

ZADD
ZSCORE
ZINCRBY
ZCARD
ZCOUNT
ZRANGE
ZREVRANGE
ZRANGEBYSCORE
ZREVRANGEBYSCORE
ZRANK
ZREVRANK
ZREM
ZREMRANGEBYRANK
ZREMRANGEBYSCORE
ZRANGEBYLEX
ZLEXCOUNT
ZREMRANGEBYLEX
ZSCAN
ZUNIONSTORE
ZINTERSTORE
HyperLogLog
PFADD
PFCOUNT
PFMERGE
```

有关ziplist配置 config get *ziplist*
1) “hash-max-ziplist-entries”
2) “512”
3) “hash-max-ziplist-value”
4) “64”
5) “list-max-ziplist-entries”
6) “512”
7) “list-max-ziplist-value”
8) “64”
9) “zset-max-ziplist-entries”
10) “128”
11) “zset-max-ziplist-value”
12) “64”
-entries表示ziplsit对多保存数据项的个数，超出之后不能再使用ziplist
-value表示每个数据项的最大字节数，超出之后不能再使用ziplis

### 其他

```css
地理位置
GEOADD
GEOPOS
GEODIST
GEORADIUS
GEORADIUSBYMEMBER
GEOHASH

位图
SETBIT
GETBIT
BITCOUNT
BITPOS
BITOP
BITFIELD

数据库
EXISTS
TYPE
RENAME
RENAMENX
MOVE
DEL
RANDOMKEY
DBSIZE
KEYS
SCAN
SORT
FLUSHDB
FLUSHALL
SELECT
SWAPDB

自动过期
EXPIRE	set key value expireTime(Long)再set key value2，expireTime时间到，get key 有值吗？redis过期时间原理？redis hash结构小键值对能单独设置不同的过期时间吗？
EXPIREAT
TTL
PERSIST
PEXPIRE
PEXPIREAT
PTTL

事务
MULTI
EXEC
DISCARD
WATCH
UNWATCH
Lua 脚本
EVAL
EVALSHA
SCRIPT_LOAD
SCRIPT_EXISTS
SCRIPT_FLUSH
SCRIPT_KILL

持久化
SAVE
BGSAVE
BGREWRITEAOF
LASTSAVE

发布与订阅
PUBLISH
SUBSCRIBE
PSUBSCRIBE
UNSUBSCRIBE
PUNSUBSCRIBE
PUBSUB

复制
SLAVEOF
ROLE

客户端与服务器
AUTH
QUIT
INFO
SHUTDOWN
TIME
CLIENT_GETNAME
CLIENT_KILL
CLIENT_LIST
CLIENT_SETNAME

配置选项
CONFIG_SET
CONFIG_GET
CONFIG_RESETSTAT
CONFIG_REWRITE

调试
PING
ECHO
OBJECT
SLOWLOG
MONITOR
DEBUG_OBJECT
DEBUG_SEGFAULT

内部命令
MIGRATE
DUMP
RESTORE
SYNC
PSYNC
```

### 补充其他数据结构

二叉树 VS 平衡二叉树AVL VS 跳跃表 VS 红黑树 VS B+ VS B-的思考

二叉查找树：左子树的节点值比父亲节点小，而右子树的节点值比父亲节点大。手写二分查找算法。查找算法复杂度最好O(logn)，最差送你一串冰糖葫芦O(n)。

平衡二叉树AVL：（1）左子树的节点值比父亲节点小，而右子树的节点值比父亲节点大。（2）每个节点的左子树和右子树的高度差至多等于1。

平衡二叉树解决二叉查找树退化成一串链表，保证不出现大量节点偏向于一边。 查找算法复杂度O(logn)。

由于平衡树要求每个节点的左子树和右子树的高度差至多等于1太严了，每次进行插入/删除节点时，都需通过**左旋**和**右旋**来进行调整再次成为一颗符合要求的平衡树。不适应频繁插入、删除场景。

什么是跳跃表？

什么是红黑树？（1）左子树的节点值比父亲节点小，而右子树的节点值比父亲节点大。（2）根节点是黑色。（3）每个叶节点都是黑色的空节点（NIL），叶节点不存数据。（4）任何相邻的节点都不能同时为红色，红色节点是被黑色节点隔开。**红黑树是一种不大严格的平衡树**。

红黑树一个node只存一对kv，B+树每个node存多对kv，其中第一个key有序，从左向右，一个node存多个kv的方式CPU cache命中率更高，高并发索引选B+树。**红黑树比平衡二叉树AVL适应频繁插入、删除**。

红黑树查找某个节点：O(logn)

红黑树 VS 哈希表不同场景的选择

什么是B+树（MySQL  InnoDB索引）？

根节点存索引节点，叶节点存数据节点。所有叶子节点形成有序链表，便于区间查询以及全结点遍历更快。

非叶子结点不存储Data，起目录作用。

什么是B树（MongoDB索引）？根结点和叶节点都存数据。

B树适合数据聚合。经常访问的数据离根节点很近（基于频率的搜索），越频繁query的结点越往根上走。

B+树是平衡二叉树吗？是AVL树。

跳跃表缺点耗内存、Redis经常有范围操作比如list ltrim可利用跳跃表里的双向链表，缓存cache locality不会比平衡树差。并发下红黑树插入和删除元素需做Rebalance操作，但它更适合查询。

## Redis扩容和缩容

```shell
redis-cli --cluster
/usr/redis/bin/redis-cli --cluster add-node 192.168.212.163:7006   192.168.212.163:7000
cluster slots
/usr/redis/bin/redis-cli --cluster reshard  192.168.212.163:7000
```

## 缓存一致性

保证最终一致性方案是不行的，因过期时间造成了延时。给缓存设置过期时间，所有的写操作以数据库为准，只要到达缓存过期时间，则后面的读请求自然会从数据库中读取新值然后回填缓存。

### Scenario

### A.外部依赖

```css
(1)do sth
(2)Object = 调依赖接口、缓存、网络请求返回  // 存在失败的可能性
(3)Object Update
```

### B.缓存和DB一致性

#### 问题(1)先写缓存，后写DB

若先写缓存失败，直接返回，则无影响。

若先写缓存成功，后写DB失败，（1）数据库有旧值：此时若不清空缓存中写入的数据，则缓存中是新值，DB是旧值，数据不一致。（2）数据库没有旧值

#### 问题(2)若先写DB，后写缓存

若先写DB失败，直接返回，则无影响。

若先写DB成功，缓存写入失败，重试写入缓存也失败，则造成数据不一致，DB是新值，缓存旧值。解决方案：（1）缓存的key过期时间设短，到达过期时间，则后面的读请求自然会从DB中读取新值更新缓存，达到一致性。（2）任务持久化，异步去拿数据库的值更新缓存，但也存在重启或任务失败的问题。

#### 解决方案-读写分离+状态机（注意顺序）

读：读缓存，缓存读不到读DB，读到DB更新缓存。

写：删缓存旧的，写库，读库新值更新缓存。

#### 补充：数据库发生变化，如何及时更新缓存

```css
(1)每次更新完数据库都需调用类似刷新缓存方法
(2)实时同步(Aspect + 事件驱动异步) VS 分批按时间戳同步 
```

## 缓存失效策略

### 定时删除（内存友好）

设Key的过期时间，为Key设定时器，可保证内存释放快。但Key量大，每个Key都对应一个定时器，性能占CPU高。

### 惰性删除（CPU友好）

Key过期时间满不删，读库取Key检查过期？过期删除返回null：不过期返回Value

占CPU少，Key长时间不被获取就没被删，内存泄漏

### 缓存命中率

不命中情况：缓存不存在、已过期。

命中率高，性能好，响应时间短、吞吐量高，并发强。

高频低时效：预热、扩容、优化缓存粒度（粒度意思是大对象拆细分片，不拆redis集群有的数据小读取块，有的十分大读取非常慢占用更多的网络资源来序列化）、定时更新缓存提高命中率。

## 缓存雪崩

Scenario：（1）缓存集群重启（2）缓存的过期时间设置导致的集体失效（3）大查询流量去读库

Solution：（1）机架做HA（主从、大对象分片）、主从、扩展，开启AOF（灾备、误删）或RDB（全量数据恢复、快）（2）热度排序，高热度缓存过期时间设长、冷门设短，范围区间内随机设置过期时间（3）Encache（内存也备一份）+ hystrix

大对象比如2M以上的放redis，虽然redis支持很大甚至G级的value值，由于大对象序列化和反序列化要消耗更多的时间，大量请求下会阻塞，阻塞对后续的服务产生影响，有依赖关系的服务都受影响，大面积的阻塞最后导致雪崩

雪崩曲线：一般是由平缓急剧下降后再急剧上升。

## 缓存降级

Scenario：缓存集群挂掉、失效，也不读库，直接返回默认数据（写死、配置数据、读库）

Solution：热点数据双保险，一份内存，另一份缓存

## 缓存穿透

流程：查缓存—>缓存不存在读库

Scenario：恶意攻击或高并发请求查缓存没查到后读库，没命中率高导致穿透读库

Solution：数据库若也没有设一个key null也设置过期时间，滤重 bitmap效果明显比boomfilter好

## 缓存预热

Scenario：元数据提前预热加载到缓存，避免先查库

Solution：依据数据量（1）量小，放Apollo配置或工程启动时加载（2）量大，定时任务周期性刷新缓存（3）超量，分布式工程化提前加载

## 事务

```css
Redis不支持事务，Redis单个操作是原子性的。多个操作顺序执行不具备原子性，执行过程中中间失败话，不会回滚，还会继续执行。为什么不支持回滚？原子性的命令操作直观给出异常比负杂逻辑更清晰明了。事务回滚并不会解决程序Bug，只有当Redis命令有语法错误时才会执行失败，不支持回滚是让开发人员在开发期间就发现错误，尽早抛出错误。如何保证Redis执行多个操作不中断？Redis执行Lua脚本具原子性。
```

## 持久化AOF和RDB

Redis两种持久化，一种RDB直接从内存dump到磁盘，fork一个子进程先将数据写临时文件(副本：内存中的数据是原来2倍），写成功则将临时文件替换掉原文件，再二进制压缩。在指定的时间间隔内，执行指定次数的写操作，则会将内存中的数据写入到磁盘中。即在指定目录下生成一个dump.rdb文件。Redis 重启会通过加载dump.rdb文件恢复数据。

```css
# save ""
save 900 1
save 300 10
save 60 10000

#指定本地数据库文件名，一般采用默认的 dump.rdb
dbfilename dump.rdb

#指定本地数据库存放目录，一般也用默认配置
dir ./

#默认开启数据压缩，LZF压缩方式
rdbcompression yes
```

另一种AOF，以日志文本记录每一个写、删除操作，查询不记录，追加写入文件，Append of File。

### 选型

RDB（全量数据、无法实时和秒级持久化、大数据量、夜深人静悄悄恢复、副本占2倍内存、数据完整性和一致性低）

RDB恢复数据比AOF快

AOF（写性能高、记录内容多、文件越来越大、数据恢复越来越慢、适合灾备误删除紧急恢复，但AOF占的快照比RDB大，开启AOF，写QPS下降，恢复数据慢，不适合冷备）

冷备（RDB）：关机离线备份。热备（AOF）：不关机，一般双机热备。

## 问题集

### Redis单个Key超过512M？

setrange命令证明、官网说明key最大是512M。单个value超过512M优化？

### 为什么RedisCluster有16384个槽？

16384=2的14次方

HASH_SLOT=CRC16(key) mod 16384

Normal heartbeat packets carry the full configuration of a node, that can be replaced in an idempotent way with the old in order to update an old config. This means they contain the slots configuration for a node, in raw form, that uses 2k of space with16k slots, but would use a prohibitive 8k of space using 65k slots.
At the same time it is unlikely that Redis Cluster would scale to more than 1000 mater nodes because of other design tradeoffs.
So 16k was in the right range to ensure enough slots per master with a max of 1000 maters, but a small enough number to propagate the slot configuration as a raw bitmap easily. Note that in small clusters the bitmap would be hard to compress because when N is small the bitmap would have slots/N bits set that is a large percentage of bits set.

若槽位Slot太大，发送心跳信息的消息头达8k，发送的心跳包过于庞大。e.g.如果是2的16次方作为Slot，65536÷8÷1024=8KB，8KB的消息头浪费带宽。槽位太小，bitmap的填充率Slots / N很高(N表示节点数)，bitmap的压缩率就很低。

```shell
cluster info 查看当前集群信息
cluster nodes 查看集群各个节点负责的Slot
```

补Redis Slot流程图

节点数在1000以内够用：Redis的集群主节点数量基本不可能超过1000个。节点数在1000以内的redis cluster集群，16384个槽位足够用。

bitmap进行压缩高，槽位越小，节点少的情况下，压缩率高，bitmap的填充率slots / N很高的话(N表示节点数)：Redis主节点的配置信息中，哈希槽是通过一张bitmap的形式来保存的，bitmap进行压缩，但是如果bitmap的填充率slots / N很高的话(N表示节点数)，bitmap的压缩率就很低。

# 分布式锁

## 加锁对象

对同一资源（资源可以是单条、多条数据，也可以是一段操作），优先考虑对单条或数据分片加分布式锁，对批量数据操作加锁慢

## 场景

分布式多实例、滤重(防重复执行，如定时任务、高并发插入)

## Redis

set(key, value, expireTime);

## ZooKeeper

注册增加一个节点加锁、删掉一个节点解锁

## 数据库

建表，插入和删除做分布式锁

## Redis分布式锁问题

### （1）锁未被释放

情况一：加锁—>处理完业务—> 未释放锁导致其他线程一直尝试获取锁阻塞抛异常

```java
redis.clients.jedis.exceptions.JedisConnectionException: Could not get a resource from the pool 
```

```java
 public String stockLock() {
        RLock lock = redissonClient.getLock("stockLock");
        try {
            /**
             * 获取锁
             */
            if (lock.tryLock(10, TimeUnit.SECONDS)) {
              
                /**
                 * 扣减库存
                 */
                。。。。。。
            } else {
                LOGGER.info("未获取到锁业务结束..");
            }
        } catch (Exception e) {
            LOGGER.info("处理异常", e);
        } 
        return "ok";
  }
代码问题：（1）锁的key没统一管理（2）锁没有释放导致线程池打满引发服务大面积瘫痪（3）日志级别
```

情况二：redis线程池无空闲线程处理客户端命令

redis线程池：核心线程数--->阻塞队列--->最大线程数--->线程池拒绝

jedis线程池配置：

```xml
	 # redis连接池配置少影响TPS上不去，导致很多线程等待Redis线程池
	 <property name="maxActive" value="20" />
   <property name="maxIdle" value="3" />
   <property name="maxWait" value="15000" />
   <property name="timeBetweenEvictionRunsMillis" value="60000" />
   <property name="minEvictableIdleTimeMillis" value="180000" />
```



```java
public void lock() { 
  // for比while效率高，for的指令集更少
      for(;;;) { 
          boolean flag = this.getLock(key); 
          if (flag) { 
                TODO ......... 
          } else { 
                // 释放当前redis连接 
                redis.close(); 
                // 休眠1000毫秒, 拿到锁的线程处理完业务及时释放锁，如果是重入锁未拿到锁后，线程可以释放当前连接并且sleep一段时间 
                sleep(1000); 
          } 
        } 
    } 
```

### （2）B的锁被A释放

SETNX 加锁后，业务逻辑耗时已超过Redis锁过期时间，线程A的锁自动释放（删除key），B线程检测到key不存在，执行SETNX拿到锁，但是线程A执行完业务逻辑还是会释放key，导致B线程的锁被A释放了

解决思路：比较线程id和唯一线程相关的key标识、必须等线程A执行任务逻辑完才释放锁，任务逻辑未执行完进行续约过期时间expireTime

### （3）获取锁等待的时间远超过数据库事务超时时间

事务自动提交的情况下会有超时限制，key长时间获取不到锁，获取锁等待的时间远超过数据库事务超时时间，程序会抛异常

```java
@Transaction 
   public void lock() { 
 
        while (true) { 
            boolean flag = this.getLock(key); 
            if (flag) { 
                insert(); 
            } 
        } 
    } 
```

解决方案：将数据库事务改为手动提交、回滚事务

```java
@Autowired 
    DataSourceTransactionManager dataSourceTransactionManager; 
 
    @Transaction 
    public void lock() { 
        //手动开启事务 
        TransactionStatus transactionStatus = dataSourceTransactionManager.getTransaction(transactionDefinition); 
        try { 
            while (true) { 
                boolean flag = this.getLock(key); 
                if (flag) { 
                    insert(); 
                    //手动提交事务 
                    dataSourceTransactionManager.commit(transactionStatus); 
                } 
            } 
        } catch (Exception e) { 
            //手动回滚事务 
            dataSourceTransactionManager.rollback(transactionStatus); 
        } 
    } 
```

回滚事务发生的情况：

(1)执行SQL的connection与开启事务的connection必须是同一个才能对事务进行控制，事务Catch RuntimeException才回滚

(2)手动提交时在异常处理机制需手动回滚

### （4）锁过期expire时间续约

锁过期expire时间比执行完任务时间要长，redisson(加锁、解锁、续约)看门狗WatchDog在加锁后会注册一个定时任务监听锁，检查周期是：加锁失效时间的1/3，如加锁3s释放，检查是1s一次，加锁业务没执行完，会自动续期重置为加锁失效时间3s。requestId可以是当前线程id也可以唯一标识业务处理的id

```java
@Slf4j
@Service
public class RedisDistributionLockPlus {
 
    /**
     * 加锁超时时间，单位毫秒， 即：加锁时间内执行完操作，如果未完成会有并发现象
     */
    private static final long DEFAULT_LOCK_TIMEOUT = 30;
 
    private static final long TIME_SECONDS_FIVE = 5 ;
 
    /**
     * 每个key的过期时间 {@link LockContent}
     */
    private Map<String, LockContent> lockContentMap = new ConcurrentHashMap<>(512);
 
    /**
     * redis执行成功的返回
     */
    private static final Long EXEC_SUCCESS = 1L;
 
    /**
     * 获取锁lua脚本， k1：获锁key, k2：续约耗时key, arg1:requestId，arg2：超时时间
     */
    private static final String LOCK_SCRIPT = "if redis.call('exists', KEYS[2]) == 1 then ARGV[2] = math.floor(redis.call('get', KEYS[2]) + 10) end " +
            "if redis.call('exists', KEYS[1]) == 0 then " +
               "local t = redis.call('set', KEYS[1], ARGV[1], 'EX', ARGV[2]) " +
               "for k, v in pairs(t) do " +
                 "if v == 'OK' then return tonumber(ARGV[2]) end " +
               "end " +
            "return 0 end";
 
    /**
     * 释放锁lua脚本, k1：获锁key, k2：续约耗时key, arg1:requestId，arg2：业务耗时 arg3: 业务开始设置的timeout
     */
    private static final String UNLOCK_SCRIPT = "if redis.call('get', KEYS[1]) == ARGV[1] then " +
            "local ctime = tonumber(ARGV[2]) " +
            "local biz_timeout = tonumber(ARGV[3]) " +
            "if ctime > 0 then  " +
               "if redis.call('exists', KEYS[2]) == 1 then " +
                   "local avg_time = redis.call('get', KEYS[2]) " +
                   "avg_time = (tonumber(avg_time) * 8 + ctime * 2)/10 " +
                   "if avg_time >= biz_timeout - 5 then redis.call('set', KEYS[2], avg_time, 'EX', 24*60*60) " +
                   "else redis.call('del', KEYS[2]) end " +
               "elseif ctime > biz_timeout -5 then redis.call('set', KEYS[2], ARGV[2], 'EX', 24*60*60) end " +
            "end " +
            "return redis.call('del', KEYS[1]) " +
            "else return 0 end";
    /**
     * 续约lua脚本
     */
    private static final String RENEW_SCRIPT = "if redis.call('get', KEYS[1]) == ARGV[1] then return redis.call('expire', KEYS[1], ARGV[2]) else return 0 end";
 
 
    private final StringRedisTemplate redisTemplate;
 
    public RedisDistributionLockPlus(StringRedisTemplate redisTemplate) {
        this.redisTemplate = redisTemplate;
        ScheduleTask task = new ScheduleTask(this, lockContentMap);
        // 启动定时任务
        ScheduleExecutor.schedule(task, 1, 1, TimeUnit.SECONDS);
    }
 
    /**
     * 加锁
     * 取到锁加锁，取不到锁一直等待知道获得锁
     *
     * @param lockKey
     * @param requestId 全局唯一
     * @param expire   锁过期时间, 单位秒
     * @return
     */
    public boolean lock(String lockKey, String requestId, long expire) {
        log.info("开始执行加锁, lockKey ={}, requestId={}", lockKey, requestId);
        for (; ; ) {
            // 判断是否已经有线程持有锁，减少redis的压力
            LockContent lockContentOld = lockContentMap.get(lockKey);
            boolean unLocked = null == lockContentOld;
            // 如果没有被锁，就获取锁
            if (unLocked) {
                long startTime = System.currentTimeMillis();
                // 计算超时时间
                long bizExpire = expire == 0L ? DEFAULT_LOCK_TIMEOUT : expire;
                String lockKeyRenew = lockKey + "_renew";
 
                RedisScript<Long> script = RedisScript.of(LOCK_SCRIPT, Long.class);
                List<String> keys = new ArrayList<>();
                keys.add(lockKey);
                keys.add(lockKeyRenew);
                Long lockExpire = redisTemplate.execute(script, keys, requestId, Long.toString(bizExpire));
                if (null != lockExpire && lockExpire > 0) {
                    // 将锁放入map
                    LockContent lockContent = new LockContent();
                    lockContent.setStartTime(startTime);
                    lockContent.setLockExpire(lockExpire);
                    lockContent.setExpireTime(startTime + lockExpire * 1000);
                    lockContent.setRequestId(requestId);
                    lockContent.setThread(Thread.currentThread());
                    lockContent.setBizExpire(bizExpire);
                    lockContent.setLockCount(1);
                    lockContentMap.put(lockKey, lockContent);
                    log.info("加锁成功, lockKey ={}, requestId={}", lockKey, requestId);
                    return true;
                }
            }
            // 重复获取锁，在线程池中由于线程复用，线程相等并不能确定是该线程的锁
            if (Thread.currentThread() == lockContentOld.getThread()
                      && requestId.equals(lockContentOld.getRequestId())){
                // 计数 +1
                lockContentOld.setLockCount(lockContentOld.getLockCount()+1);
                return true;
            }
 
            // 如果被锁或获取锁失败，则等待100毫秒
            try {
                TimeUnit.MILLISECONDS.sleep(100);
            } catch (InterruptedException e) {
                // 这里用lombok 有问题
                log.error("获取redis 锁失败, lockKey ={}, requestId={}", lockKey, requestId, e);
                return false;
            }
        }
    }
 
 
    /**
     * 解锁
     *
     * @param lockKey
     * @param lockValue
     */
    public boolean unlock(String lockKey, String lockValue) {
        String lockKeyRenew = lockKey + "_renew";
        LockContent lockContent = lockContentMap.get(lockKey);
 
        long consumeTime;
        if (null == lockContent) {
            consumeTime = 0L;
        } else if (lockValue.equals(lockContent.getRequestId())) {
            int lockCount = lockContent.getLockCount();
            // 每次释放锁， 计数 -1，减到0时删除redis上的key
            if (--lockCount > 0) {
                lockContent.setLockCount(lockCount);
                return false;
            }
            consumeTime = (System.currentTimeMillis() - lockContent.getStartTime()) / 1000;
        } else {
            log.info("释放锁失败，不是自己的锁。");
            return false;
        }
 
        // 删除已完成key，先删除本地缓存，减少redis压力, 分布式锁，只有一个，所以这里不加锁
        lockContentMap.remove(lockKey);
 
        RedisScript<Long> script = RedisScript.of(UNLOCK_SCRIPT, Long.class);
        List<String> keys = new ArrayList<>();
        keys.add(lockKey);
        keys.add(lockKeyRenew);
 
        Long result = redisTemplate.execute(script, keys, lockValue, Long.toString(consumeTime),
                Long.toString(lockContent.getBizExpire()));
        return EXEC_SUCCESS.equals(result);
 
    }
 
    /**
     * 续约
     *
     * @param lockKey
     * @param lockContent
     * @return true:续约成功，false:续约失败（1、续约期间执行完成，锁被释放 2、不是自己的锁，3、续约期间锁过期了（未解决））
     */
    public boolean renew(String lockKey, LockContent lockContent) {
 
        // 检测执行业务线程的状态
        Thread.State state = lockContent.getThread().getState();
        if (Thread.State.TERMINATED == state) {
            log.info("执行业务的线程已终止,不再续约 lockKey ={}, lockContent={}", lockKey, lockContent);
            return false;
        }
 
        String requestId = lockContent.getRequestId();
        long timeOut = (lockContent.getExpireTime() - lockContent.getStartTime()) / 1000;
 
        RedisScript<Long> script = RedisScript.of(RENEW_SCRIPT, Long.class);
        List<String> keys = new ArrayList<>();
        keys.add(lockKey);
 
        Long result = redisTemplate.execute(script, keys, requestId, Long.toString(timeOut));
        log.info("续约结果，True成功，False失败 lockKey ={}, result={}", lockKey, EXEC_SUCCESS.equals(result));
        return EXEC_SUCCESS.equals(result);
    }
 
 
    static class ScheduleExecutor {
 
        public static void schedule(ScheduleTask task, long initialDelay, long period, TimeUnit unit) {
            long delay = unit.toMillis(initialDelay);
            long period_ = unit.toMillis(period);
            // 定时执行
            new Timer("Lock-Renew-Task").schedule(task, delay, period_);
        }
    }
 
    static class ScheduleTask extends TimerTask {
 
        private final RedisDistributionLockPlus redisDistributionLock;
        private final Map<String, LockContent> lockContentMap;
 
        public ScheduleTask(RedisDistributionLockPlus redisDistributionLock, Map<String, LockContent> lockContentMap) {
            this.redisDistributionLock = redisDistributionLock;
            this.lockContentMap = lockContentMap;
        }
 
        @Override
        public void run() {
            if (lockContentMap.isEmpty()) {
                return;
            }
            Set<Map.Entry<String, LockContent>> entries = lockContentMap.entrySet();
            for (Map.Entry<String, LockContent> entry : entries) {
                String lockKey = entry.getKey();
                LockContent lockContent = entry.getValue();
                long expireTime = lockContent.getExpireTime();
                // 减少线程池中任务数量
                if ((expireTime - System.currentTimeMillis())/ 1000 < TIME_SECONDS_FIVE) {
                    //线程池异步续约
                    ThreadPool.submit(() -> {
                        boolean renew = redisDistributionLock.renew(lockKey, lockContent);
                        if (renew) {
                            long expireTimeNew = lockContent.getStartTime() + (expireTime - lockContent.getStartTime()) * 2 - TIME_SECONDS_FIVE * 1000;
                            lockContent.setExpireTime(expireTimeNew);
                        } else {
                            // 续约失败，说明已经执行完 OR redis 出现问题
                            lockContentMap.remove(lockKey);
                        }
                    });
                }
            }
        }
    }
}
```

（4）redis主从master-slave  A选择一台master加锁key成功后，master将key异步复制给slave，若master宕机进行主备切换， B在新master加锁成功了，导致同一时刻多请求加锁成功，如何防止？



# 云

## 云存储公司

IBM，Pure，NetApp，EMC，SAP

## 云平台

第一梯队：AWS， Azure，GCP，AliYun

第二梯队：vCloud，UCloud，坚果云

## 云虚拟化

 VMware, Hyper-V

## 云原生

云原生：Devops + 持续交付 + 容器化 + 微服务

Cloud+Native 

### AliYun组件

DataWorks

ECS

RDS

CDN

NAT网关

E-MapReduce

Dataphin与阿里云的存储计算引擎Maxcompute、智能图形化分析工具Quick BI结合使用，为数据迁移、治理、规划、可视化及数据应用提供一站式服务。

DTS

MaxCompute

OSS 文件、图片存储

短信模板

### AWS组件

RDS

Redshift

SQS

EC2

Glue

# 微服务

## 基础框架

Spring Cloud，Dubbo，Motan，Sofa

## 协议

Raft VS ZAB VS PAXOS

zab是epoch和count双向leader从follower接收数据来生成，raft是term和index，单向恢复从leader到follower补齐log

## 原则

AKF、无状态、Restful、前后分离、SpringCloud 搭建微服务准则　https://12factor.net/disposability

## 模式

链式、聚合器、异步消息、数据共享

![Microservice Architecture](http://hongchengjian.gitee.io/md/img/springcloud/Microservice%20Architecture%20VS.png)

## 注解

@RefreshScope 配置变化时，Spring @Bean懒加载初始化配置，rebuilt和依赖重新注入。

### Spring Cloud Commons(扩展核心)

@EnableDiscoveryClient：基本原理：加载META-INF/spring.factories里配置，扩展org.springframework.cloud.client.discovery.EnableDiscoveryClient，源码ref  org.springframework.cloud.client.discovery.EnableDiscoveryClientImportSelector#selectImports。

ServiceRegistry：Auto-Registration，默认是自动注册的,spring.cloud.service-registry.auto-registration.enabled=false可以屏蔽掉自动注册的功能，或者直接@EnableDiscoveryClient(autoRegister=false)单个注册类的屏蔽。Actuator Endpoint，Get /service-registry 拿到注册状态，Post新的注册信息JSON去更新。

Load Balancer Client：ribbon（restTemplate）、SpringWebclient（源码参考 https://github.com/spring-projects/spring-retry）

## 分布式注册中心

Eureka（Netflix），Consul，Nacos，Etcd，Zookeeper

服务之间调用。Eureka高可用Server需相互注册，心跳，一般高可用3台可支撑3000-4000服务。

### 心跳监测

```properties
Server服务端
server:
  port: 8761
eureka:
  client:
    #实例是否在eureka服务器上注册自己的信息以提供其他服务发现,默认为true
    register-with-eureka: false
    #此客户端是否获取eureka服务器注册表上的注册信息,默认为true
    fetch-registry: false
  server:
    #开启自我保护模式
    enable-self-preservation: false
    #清理无效节点,默认60*1000毫秒,即60秒
    eviction-interval-timer-in-ms: 5000

Client客户端

spring:
  application:
   name: ek-provider
eureka: 
  instance:
    #eureka客户端需要多长时间发送心跳给eureka服务器，表明他仍然或者，默认30秒
    lease-renewal-interval-in-seconds: 5
    #eureka服务器在接受到实力的最后一次发出的心跳后，需要等待多久才可以将此实力删除
    lease-expiration-duration-in-seconds: 10
    metadata-map: 
      company-name: eureka
  client: 
    #表示eureka client间隔多久去拉取服务器注册信息,默认为30秒
    registry-fetch-interval-seconds: 30
    #表示eureka client间隔多久去拉取服务器注册信息,默认为30秒
    registry-fetch-interval-seconds: 30registry-fetch-interval-seconds: 30
    serviceUrl: 
      defauiltZone: http://localhost:8761/eureka/
logging:
  level: 
    com.netflix: DEBUG
```

Eureka-Server 集群不区分主从节点或者 Primary & Secondary 节点，所有节点相同角色( 也就是没有角色 )，完全对等。

Eureka 支持的状态有 UP, DOWN, OUT_OF_SERVICE, and UNKNOWN。

Eureka自我保护：EMERGENCY! EUREKA MAY BE INCORRECTLY CLAIMING INSTANCES ARE UP WHEN THEY'RE NOT. RENEWALS ARE LESSER THAN THRESHOLD AND HENCE THE INSTANCES ARE NOT BEING EXPIRED JUST TO BE SAFE. 

### 为什么需自我保护？

Eureka注册服务慢的问题：eureka.instance.leaseRenewalIntervalInSeconds 调整默认的持续时间30s

解决Eureka Server不踢出已关停的节点配置：server端，eureka.server.enable-self-preservation（设为false，关闭自我保护主要）eureka.server.eviction-interval-timer-in-ms     清理间隔（单位毫秒，默认是60*1000）。client端：eureka.client.healthcheck.enabled = true开启健康检查（需要spring-boot-starter-actuator依赖），
eureka.instance.lease-renewal-interval-in-seconds =10		租期更新时间间隔（默认30秒），
eureka.instance.lease-expiration-duration-in-seconds =30  租期到期时间（默认90秒）。

Eureka高可用性：5K-1W实例，3个Eureka Server就可以支撑。AP中的A: 在集群中一部分节点故障后，集群整体是否还能响应客户端的读写请求。

Eureka Prefer IP Address：In some cases, it is preferable for Eureka to advertise the IP addresses of services rather than the hostname. Set eureka.instance.preferIpAddress to true and, when the application registers with eureka, it uses its IP address rather than its hostname.

## 分布式监控中心

CAT(大众点评),SBA,Prometheus(Metrics普罗米修斯，被DigitalOcean或Docker作为基础监控),Grafana,Pinpoint(韩国、非嵌入),谛听(阿里云),Zipkin(Twitter),Appdash(golang),鹰眼(Taobao),StackDriver Trace (Google),云图(蚂蚁),Skywalking-吴晟,Graphite,Statsd,Solarwinds,Zabbix,Centreon,appDynamics,new relic,Kaeger,Overwatch(达达-京东到家618单日订单量400万)

### 分布式调用链

CAT,SkyWalking+RocketBolt,Zipkin,DynaTrace

### 推 VS 拉

Prometheus主动筛选目标，以便从中检索指标；InfluxDB是直接推数据。

Time Series Database 时间序列数据库InfluxDB 

Prometheus向其目标发起查询，则整个配置在Prometheus服务器端完成，而不是在各个目标上完成。Prometheus决定取值，以及取值的频率。

推VS拉

集中 VS 广播

定时 VS 实时

消费能力

拉Pull：集中控制，定时轮询。能够实现速率控制(针对个性化需求强，针对不同目标实现不同速率)，按频率采样牺牲了实时性，采样数据需考虑消费能力。无效的Pull也消耗性能。需协调机制(Zookeeper)在不同客户端之间做分配，对服务端压力很轻(服务端仅需对客户端查询做出响应)。

推Push（广播方式）：可能会导致向目标发送过多数据的风险，会使目标崩溃。一收到数据可以立即推给目标，实时性很好。推多个目标需保存push状态，状态转移到数据库减轻服务器压力。有失败有成功。不能确保发送成功，即使发送成功，也不能保证目标是否接收成功。要求目标有很强消费能力。

守城门是拉不是推？若是推，攻打门口堆满石头困死守城人。

### Skywalking-吴晟  chéng VS Pinpoint 韩国

都是字节码注入（所以无侵入），但Skywalking兼容OpenTracing、协议是gRPC、发布包Jar

Pinpoint协议是Thrift，发布包是War

### Metrics

系统度量监控

#### 5种基本度量

```css
Gauges：计量器 		特点：可增减 		场景：温度、内存使用量
Counters：计数器 	特点：单调递增     场景：服务请求数、任务完成数、错误出现次数
Histograms：直方图	度量流数据中value的分布情况，计算最大/小值、平均值，方差，分位数（如中位数，或者95th分位数）
Timers：计时器		特点：只能自增		 场景：平均每秒请求数、最近1分钟平均每秒请求数、最近5分钟平均每秒请求数
Meters：TPS计数器	某段代码执行的耗时的统计及计算 	场景：请求时延、磁盘读时延
```

## 分布式日志系统

ELK(Kibana,ElasticSearch,Logstash),Kafka,Flume,Splunk,Filebeat（比Flume轻量级）

## 分布式配置中心

Apollo,Nacos,DisConf,Spring Cloud Config

## 分布式网关

F5,Ngnix +（打通Consul）,ESB,Kong,Gateway,Zuul,Soul

Netflix ZuulFilter基于Servlet（pre、router、post）

SpringCloud gateway基于Spring5，支持websocket，GatewayFilter、GlobalFilter

## 分布式事务

Seata(),dts,tcc-transaction,hmily,ByteTCC,myth,EasyTransaction,tx-lcn

二阶段提交2PC、三阶段提交3PC、Sagas长事务、补偿事务、可靠事件模式(本地事件表、外部事件表)、可靠事件模式(非事务消息、事务消息)、TCC

![Distributed Transaction](http://hongchengjian.gitee.io/md/img/db/Distributed%20Transaction%20VS.png)

## 分布式定时任务调度和管理

Elastic Job,XXL-Job

### XXL-Job

![img](https://img2018.cnblogs.com/blog/753271/201909/753271-20190924135844231-171876118.png)

关注调度中心和执行器

找到入口com.xxl.job.admin.core.conf.XxlJobAdminConfig调度中心端的配置数据

JDK中的Timer类

cron无页面暂停、

### 设计一个调度中心要素

```css
讲故事
Job、task：sendMail、copyData
Trigger
Scheduler(协调、管理Job、算法)
持久化(任务挂掉、任务执行一半中断):内存、数据库存储  DriverDelegate代理屏蔽数据库细节
UI界面管理
数据库的‘行’锁嘛, 比如SELECT * FROM LOCKS where LOCK_NAME='TRIGGER' FOR UPDATE ，就把那一行记录给锁住了，别的事务只能等待当前事务commit以后才能访问
https://www.cnblogs.com/peke/p/9212351.html
```



```java
XxlJobAdminConfig implements InitializingBean, DisposableBean
```

```java
InitializingBean	
    @Override	
    public void afterPropertiesSet() throws Exception {
    
	}

DisposableBean		
    @Override	
    public void destroy() throws Exception {
    
	}
```

```java
 public void init() throws Exception {
        // init i18n
        initI18n();

        // admin registry monitor run
        JobRegistryMonitorHelper.getInstance().start();

        // admin fail-monitor run
        JobFailMonitorHelper.getInstance().start();

        // admin lose-monitor run
        JobLosedMonitorHelper.getInstance().start();

        // admin trigger pool start
        JobTriggerPoolHelper.toStart();

        // admin log report start
        JobLogReportHelper.getInstance().start();

        // start-schedule
        JobScheduleHelper.getInstance().start();

        logger.info(">>>>>>>>> init xxl-job admin success.");
    }
```

思考后台Daemon线程 VS 守护线程

```
Daemon主程序运行时在后台提供一种通用服务的线程
```



```java
public class JobScheduleHelper{
    private volatile boolean scheduleThreadToStop = false;
	private Thread scheduleThread;
    private Thread ringThread;
	public void start(){
        // 后台线程1
 	 	scheduleThread = new Thread(new Runnable() {
             @Override
            public void run() {
                 // 思考：如何设计一个接收信号停止运行新的线程？在跑的线程或在等待的线程如何处理？
                  while (!scheduleThreadToStop) {
                      
                  }
            }
         });
        scheduleThread.setDaemon(true);
        scheduleThread.setName("...");
        scheduleThread.start(); 
                                    
		// 后台线程2
		ringThread = new Thread(new Runnable() {
            @Override
            public void run() {

            }
        });
                             
 	 }
                                    
                                    
	 public void toStop(){
         // 给一个信号目的关闭线程
       	 scheduleThreadToStop = true;
     }
}
                                    
  
VS

public class JobScheduleHelper extends Thread {
    @Override
    public void run() {

    }
}        
                                
```



（1）悲观全表锁锁住获取任务资格 select * from xxl_job_lock where lock_name = 'schedule_lock' for update;

当开启一个事务进行for update时候，另一个事务也有for update会一直等到第一个事务结束

可扩展成悲观单行锁 或 redis分布式锁？

（2) 获取未来 #{PRE_READ_MS} 秒即将执行的任务

```sql
SELECT t.id,
		t.job_group,
		t.job_cron,
		t.job_desc,
		t.add_time,
		t.update_time,
		t.author,
		t.alarm_email,
		t.executor_route_strategy,
		t.executor_handler,
		t.executor_param,
		t.executor_block_strategy,
		t.executor_timeout,
		t.executor_fail_retry_count,
		t.glue_type,
		t.glue_source,
		t.glue_remark,
		t.glue_updatetime,
		t.child_jobid,
		t.trigger_status,
		t.trigger_last_time,
		t.trigger_next_time
		FROM xxl_job_info AS t
		WHERE t.trigger_status = 1
			and t.trigger_next_time <![CDATA[ <= ]]> #{maxNextTime}
		ORDER BY id ASC
		LIMIT #{pagesize}
```

（3）遍历scheduleList

## 分布式限流熔断降级

Sentinel,Redis,Guava,Hystrix

## 分布式服务权限控制系统

OAuth,JWT,SSO,Shiro,Security

## 分布式服务和系统诊断

Arthas

## 分布式流程和服务编排

Coroutine,Akka,Kilim,Flowable,Axon

## 分布式锁

ZK(Curator),Redis(Redisson),DB建表增删

## 分布式压测平台

JMeter,LoadRunner,Ab

## 分布式全局主键系统

Redis,Zookeeper,Twitter Snowflake

## 分布式自动化测试分布式自动化API文档

Swagger,YAPI

## 分布式分库分表中间件

多数据源Sharding Sphere,MyCat,当当Sharding-jdbc,蘑菇街TSharding,TDDL(淘宝)、Cobar(阿里)、Oceanus(58同城),OneProxy(支付宝楼方鑫),Vitess(Google)

## 分布式消息队列中间件

RocketMQ,Kafka,ActiveMQ,Tibco,RabbitMQ

## 分布式缓存

Redis, MongoDB,Aerospike

## 分布式数据库分析诊断系统

慢SQL,听云

## 分布式自动化数据库脚本升级

Flyway

## 运维发布

DevOps,CICD和Pipeline,容器(Docker)化,K8S, Jenkins,蓝鲸,TriAquae,Choerodon（猪齿鱼）,Ansible,Artifactory,Terraform(Go),Pulumi

## 大数据

Kylin,Spark

### Spark

尽可能避免使用 reduceByKey、join、distinct、repartition 等会进行 shuffle 的算子，尽量使用 map 类的非 shuffle 算子

**Spark**基于**RDD  r**educe产生 shuffle 数据可缓存在内存，Hadoop 每次 shuffle 后必须写到磁盘

Hadoop 每次 MapReduce 启动一个 Task 便会启动一次 JVM

Spark 每次 MapReduce是基于线程，只在启动 Executor 是启动一次 JVM，内存的 Task可线程复用

DAG描述了 RDD 的依赖lineage血缘关系，2类，

action（触发真正的作业提交，计算返回一个值给 Driver 程序） 和 transformation（不会立即触发作业提交，每一个 transformation 返回一个新的 RDD）

窄依赖的 RDD 在同一个 stage 中进行计算

RDD 只读的分区记录集合 RDD 有多少个 partition，就会产生多少个 task

窄依赖 一子一亲  每一个 parent RDD 的 partition 最多被子 RDD 的一个 partition 使用

宽依赖 多子一亲

DAGScheduler 会将 Job划分为多个 stage，然后每个 stage 创建一个 TaskSet

Executor 上有线程池，每接收到一个 Task，就用 TaskRunner 封装，然后从线程池里取出一个线程执行这个 task。

(TaskRunner 将我们编写的代码，拷贝，反序列化，执行 Task，每个 Task 执行 RDD 里的一个 partition)

Dataset 支持静态类型分析所以在 compile time 就能报错，各种 combinators（map，foreach 等）性能会更好

ML面向 Dataset[Row]、**MLLib** 是面对 RDD

Why：Yarn多用户下重用空闲CPU executor，standalone适合单用户？除了 Spark调度服务还提供调度，如 Hadoop MapReduce, Hive 

**Spark Streaming**小文件：

Spark Streaming 1batch作为1rdd

Spark Streaming 是无法动态调整并行度

Storm Topology可动态地调整并行度

### Flink





## 限流

### Scenario

稀缺资源（秒杀、抢购）、写服务（评论、下单）、频繁复杂查询（评论最后几页）不能用缓存和降级来解决，需限流来限制并发、请求量

限流有：限制数据库连接池、线程池、nginx limit_conn限制瞬时并发连接数、限制时间窗口的平均速率（Guava RateLimiter、Nginx limit_req）、限制远程接口调用速率、限制MQ消费速率、网络连接数、网络流量、CPU、内存

### 应用级限流

Tomcat Connector参数：acceptCount、maxThreads。

MySQL：max_connections

Redis: tcp_backlog

### 细粒度

Lua+Nginx+Redis：一致性hash将分布式限流

### Redis限流

每分钟某个用户访问服务接口数不超过阀值n次，set key exprireTime = 60s，每访问一次就incre key做+1。 

### Token Bucket 令牌桶

设置参数 令牌桶添加速率r，令牌桶最大容量N 

Ex. Guava RateLimiter

### Leaky Bucket 漏桶

Ex.  Guava SmoothWarmingUp

### Fix Window Counter 固定窗口计数

两个计数参数，计数周期T及最大访问调用数N，缺陷是周期切换时，突破限流最大数N

### Sliding Window Counter 滑动窗口计数

优化了Fix Window Counter算法的周期切换问题

## 熔断

### Scenario

超时、链路中断CircuitBreaker、雪崩、超过失败阀值

### Sentinel VS Hystrix

关注点：Hystrix关注熔断和隔离，资源定义与规则配置强耦合，线程池隔离针对不同服务不同线程池，信号量隔离限制并发数，缺点是无法对慢应用自动降级，只能等待客户端自己超时(存在级联阻塞)；Sentinel 关注流量控制、方法/代码。Sentinel和Hystrix熔断降级本质是熔断器模式Circuit Breaker Pattern，都支持基于失败比率(异常比率)熔断降级，Sentinel还支持平均响应时间的熔断降级(**防止调用非常慢造成级联阻塞**)。Hystrix 1.5之前基于环形数组实现滑动窗口，通过锁配合CAS操作对每个桶的统计信息进行更新。Hystrix 1.5重构将指标统计数据结构抽象成**响应式流**reactive stream底层改造成了基于 RxJava 的事件驱动模式，在服务调用成功/失败/超时的时候发布相应的事件，通过一系列的变换和聚合最终得到实时的指标统计数据流，可以被熔断器或 Dashboard 消费。**Sentinel**抽象出**Metric 指标****统计接口，实现是基于 `LeapArray` 滑动窗口。Sentinel-core没任何多余依赖，打包不到200KB，够轻量。Sentinel单机超25WQPS性能损耗影响5% - 10%，损耗够小。

|    比较点    |           Hystrix            |                   Sentinel                   |
| :----------: | :--------------------------: | :------------------------------------------: |
|   隔离策略   |    线程池隔离或信号量隔离    |                  信号量隔离                  |
|   熔断降级   |         基于失败比率         |            基于响应时间或失败比率            |
| 实时指标实现 |        RxJava滑动窗口        |              LeapArray滑动窗口               |
|   规则配置   |        支持多种数据源        |                支持多种数据源                |
|    扩展性    |             插件             |                  多个扩展点                  |
|   基于注解   |             支持             |                     支持                     |
|     限流     |            不支持            |        基于QPS，支持基于调用关系限流         |
|   流量整形   |            不支持            |            支持慢启动、均匀器模式            |
| 系统负载保护 |            不支持            |                     支持                     |
|    控制台    |            不完善            | 可配置规则、开箱即用、查看秒级监控、机器发现 |
| 常见框架适配 | Servlet,Spring Cloud Netflix |       Servlet,Spring Cloud,Dubbo,gRPC        |

Hystrix命令模式实现，对外部资源的调用和fallback(熔断反馈fallback：hystrix.command.default.fallback.enabled)封装成一个命令对象(extends HystrixCommand  HystrixObservableCommand)，底层基于RxJava。每个 Command 创建时都要指定 commandKey 和 groupKey（用于区分资源）以及对应的隔离策略（线程池隔离 or 信号量隔离，执行策略isolation.strategy：hystrix.command.default.execution.isolation.strategy=THREAD）。线程池隔离模式下需要配置线程池对应的参数（线程池名称、容量、排队超时等），然后 Command 就会在指定的线程池按照指定的容错策略执行；信号量隔离模式下需要配置最大并发数，执行 Command 时 Hystrix 就会限制其并发调用。

Sentinel 资源定义与规则配置耦合度更低，Hystrix  Command 强依赖于隔离规则，原因是隔离规则会直接影响 Command 执行， Hystrix 会解析 Command 隔离规则来创建 RxJava Scheduler 调度执行，若是线程池模式则 Scheduler 底层的线程池为配置的线程池，若是信号量模式则简单包装成当前线程执行的 Scheduler。**而Sentinel则不一样，开发的时候只需要考虑这个方法/代码是否需要保护，可以动态实时修改。**Sentinel 从 0.1.1 版本开始支持基于注解的资源定义方式，可以通过注解参数指定异常处理函数和 fallback 函数。Sentinel 提供多样化的规则配置方式。除了直接通过 `loadRules` API 将规则注册到内存态之外，用户还可以注册各种外部数据源来提供动态的规则。用户可以根据系统当前的实时情况去动态地变更规则配置，数据源会将变更推送至 Sentinel 并即时生效。

Hystrix Dashboard 监控单个，Turbine(Hystrix Dashboard)升级， 断路器聚合监控(整个系统)。



## 降级

### Scenario

RPC访问本地伪装或非真实Mock的服务

## 负载均衡

Feign @FeignClient 接口方式 根据 serviceId feign自带断路器:feign.hystrix.enabled=true，feign不支持@GetMapping等组合注解。@PathVariable需要指定其value。Feign暂不支持复杂对象作为一个参数。

Ribbon @RibbonClient 依赖restTemplate 根据url prefix（prefix也带seriveId）需自己构建http请求繁琐。

问题：discovery client 跟ribbon有关系？没有关系 ，ServerList从注册中心获取列表，client经过ribbon，再从 serverList 选取。



# 设计Factor

## 接口设计

快、流程处理遇异常Fast fail、处理的信息量要少

接口高可用（降级、限流、熔断、集群化、微服务化、监控、粒度细化）

高性能（QPS、TPS、传输大小压缩Gzip、大数据量传输chunked、网络带宽、机器Core数、内存、磁盘）

安全性（长短双token、JWT、SSO、兑换防刷、Session共享、校验、用户信息、手机号、身份证脱敏、日志{}参数化、网关白名单、跨域、URI加密、图片地址加密、存库加密）

幂等性（多次接口调用返回结果一样，查是读库肯定幂等。删不考虑返回值也是幂等。更新 set A = XX where id = PK 肯定幂等。更新 set A = XX+1 where id = PK 不是幂等。解决方案是？新增肯定不幂等。ex. 支付系统扣款根据orderId（这个orderId是在插入表前由专门的id系统或算法生成）+ 状态，在扣款时校验下，不重复扣款。）

插入幂等： 将id或生成的唯一键token放redis，同时也存库（非PK的唯一索引最可靠），做两层做缓存有利于提高接口效率。负载均衡后落机器A插入机器A成功，缓存A的id或token，返回前端成功。负载均衡后落机器B，若重复插入（重复插入的原因是有可能延时重试机制，可能接MQ ACK之前若延时会重试，重试导致重复插入）或插入失败，先根据id或token查缓存，缓存有值直接读库A插入成功的数据返回，缓存没值再根据id或token查库有没有值，有则返回成功，没有则插入数据库成功后更新缓存。更新幂等： 根据PK + Status更新 where条件带上一个状态。

扩展性（发版本、加字段、拆分、在线实时预览、离线版本、历史文档管理、机器服务集群扩展，尤其考虑写操作是否需加分布式锁）

序列化（JSON、AVRO、XML、Protobuf、IO单向阻塞、Thrift跨平台、NIO（Buffer缓存，Channel双向，Selector注册、EventLoop轮询）

一致性（依赖第三方，测试Mock，重试，异常处理回调，重试超阀值是否熔断止损）

字段（格式、类型、header参数、状态码、视频防盗链refer、OSS图片加签和过期时间戳防爬虫下载、包装类交互、判null）

测试（压测、自动化测试、工具、并发、响应时间）

异步（new Thread VS 线程池管理 注意关闭），同步，实时，准实时（ES term大小）

## 存储比较

OSS、DBFS、CPFS、HDFS

## SOLID原则

### Open Closed Principle 开闭原则

对类、接口、模块、函数扩展开放，对修改关闭。

抽象（接口或抽象类）是开放的，抽象要保持稳定，确定了就不要修改。通过接口或抽象类约束扩散，将相同的变化封装到一个接口或抽象类中，将不同的变化封装到不同的接口或抽象类中，不应该有两个不同的变化出现在同一个接口或抽象类中。对扩展进行边界限定，不允许出现在接口或抽象类中不存在的public方法。引用对象尽量使用接口或抽象类，而不是实现类。

### Liskov Substitution Principle

# Spring

## SpringMVC执行流程

![SpringMVC1](http://hongchengjian.gitee.io/md/img/springmvc/SpringMVC1.png)

![SpringMVC2](http://hongchengjian.gitee.io/md/img/springmvc/SpringMVC2.png)

## IOC容器的生命周期

![IOC](http://hongchengjian.gitee.io/md/img/spring/IOC.png)

扩展点

```java
  BeanPostProcessor
  InstantiationAwareBeanPostProcessor
  BeanNameAware
  ApplicationContextAware
  BeanFactoryAware
  BeanFactoryPostProcessor
  InitializingBean
  DisposableBean
  ApplicationListener
  ApplicationContextInitializer
  FactoryBean
  CommandLineRunner
  @org.springframework.core.annotation.Order进行标注或者实现org.springframework.core.Ordered
```

## AOP

### AOP原理

代理

静态代理：编译时确定了被代理类

动态代理（RPC、AOP）：运行时确定了被代理类

RPC不能提前知道各个业务方要调哪些接口的哪些方法，动态代理建立一个Proxy给客户端使用，方便框架搭建逻辑。

### AOP可以切final方法？



### AOP不能切Private方法原理？



###  动态代理两种实现方式适用场景？



## Rest服务

Rest uri对资源访问，方法分别对应增删查改：GET查幂等、PUT改，非幂等、POST增，非幂等、DELETE删幂等

### GrapHQL VS Rest

GrapHQL是API定义语法或者框架，仅有语法定义，并没有限制实现的语言。语法分两类Query接口用来获取数据，Mutation接口用来更新数据。

GrapHQL更灵活，安全控制难，监控不友好。实现版有Python的django、flask和golang。

###Rest增删查改注解

@GetMapping("/{id:\\d+}")（配置表id是code，而业务实体时：id是数据库主键id，非业务实体id）、@RequestMapping("/user")、@PostMapping、@PutMapping、  @DeleteMapping("/{id:\\d+}")

@RestController

### 方法传参注解

@PathVariable、@RequestBody

### 返回json处理注解

Jackson的@JsonView 使用 https://blog.csdn.net/qq_37659167/article/details/82960556

### JUnit常用注解

@Before 在执行测试方法前先执行其标注的方法

### 兼容老Spring项目注解

@ImportResource导入老的Spring项目配置文件

##  Spring VS SpringBoot VS SpringMVC

Spring核心IOC、AOP。

SpringAware 感知bean根据id去IOC容器里去bean对应的属性。

Aware、Filter、Handler三个组件的区别？

一次浏览器请求处理过程？

IOC： Inversion控制是IOC控制了对象，不再是主动new 。反转是由容器来帮忙创建及注入依赖对象、接口的具体实现。Container容器本质是集合map。

AOP： @Aspect、@Pointcut（可以切自定义注解，也可以切方法）、@Before、@After、@Around

如何切自定义注解，demo项目？

注意AOP为啥不能代理private方法，只能代理public方法？确认bean 是AopProxy代理的对象，如何确认？三种方式

若public方法调了private方法，可以代理吗？

```java
AopUtils.isAopProxy()
AopUtils.isCglibProxy() //cglib
AopUtils.isJdkDynamicProxy() //jdk动态代理
```

注意context:component-scan 重复扫描（bean实例化多次）影响事务。

注意基于类的代理而非接口，若代理父类 execution(* com.XXX.service..*+.*(..))。

```css
-execution * com.yl.spring.aop.ArithmeticCalculator.*(..):匹配ArithmeticCalculator中声明的所有方法，第一个*代表任意修饰符及任意返回值，第二个*代表任意方法，..匹配任意数量的参数。若目标类与接口与切面在同一个包中，可以省略包名。
-execution public * ArithmeticCalculator.*(..):匹配ArithmeticCalculator接口的所有公有方法
-execution public double ArithmeticCalculator.*(..):匹配ArithmeticCalculator中返回double类型数值的方法
-execution public double ArithmeticCalculator.*(double, ..):匹配第一个参数为double类型的方法，..匹配任意数量任意类型的参数
-execution public double ArithmeticCalculator.*(double, double):匹配参数类型为double，double类型的方法
```

SpringMVC是基于Servlet，属于Spring Web层开发一部分。

SpringBoot Outofbox开箱即用和默认优于配置Convention over configuration。专注于开发后端接口，不专注于开发前端视图，注解插件配置简化了xml配置流程，方便很快地开发单个微服务。SpringBoot打包和分发依赖Maven和Gradle，maven VS gradle：maven是扫整个pom下的类字节码，扫到一个就用这个，会duplicate class错误，并不会比较相同类字节码的版本。而gradle是扫整个，遇到相同的会比较版本后选择用高版本。SpringBoot是Starter插件形式维护模块，提供parent pom管理。SpringBoot的CLI 命令行界面 和 GVM Groovy环境管理器处理版本的安装和管理。

SpringCloud更注重全局微服务的治理、整合，全家桶管理多个SpringBoot单体服务。

## 底层细节

@Order如何保证有序的底层？

注解反射获取注入bean，Comparator比较注解int值排好序后，将bean加入LinkedHashSet，

@Order、Ordered不影响类的加载顺序而是影响Bean加载如IOC容器之后执行的顺序（优先级）

```java
@Retention(RetentionPolicy.RUNTIME)
@Target({ElementType.TYPE, ElementType.METHOD, ElementType.FIELD})
@Documented
public @interface Order {
	/**
	 * 默认是最低优先级,值越小优先级越高, @Order()值从0开始
	 */
	int value() default Ordered.LOWEST_PRECEDENCE;
}

public interface Ordered {
    int HIGHEST_PRECEDENCE = -2147483648;
    int LOWEST_PRECEDENCE = 2147483647;
    int getOrder();
}

public ConfigurableApplicationContext run(String... args) {
        StopWatch stopWatch = new StopWatch();
        stopWatch.start();
        ConfigurableApplicationContext context = null;
        Collection<SpringBootExceptionReporter> exceptionReporters = new ArrayList();
        this.configureHeadlessProperty();
        SpringApplicationRunListeners listeners = this.getRunListeners(args);
        listeners.starting();

        Collection exceptionReporters;
        try {
            ApplicationArguments applicationArguments = new DefaultApplicationArguments(args);
            ConfigurableEnvironment environment = this.prepareEnvironment(listeners, applicationArguments);
            this.configureIgnoreBeanInfo(environment);
            Banner printedBanner = this.printBanner(environment);
            context = this.createApplicationContext();
            exceptionReporters = this.getSpringFactoriesInstances(SpringBootExceptionReporter.class, new Class[]{ConfigurableApplicationContext.class}, context);
            this.prepareContext(context, environment, listeners, applicationArguments, printedBanner);
            this.refreshContext(context);
            this.afterRefresh(context, applicationArguments);
            stopWatch.stop();
            if (this.logStartupInfo) {
                (new StartupInfoLogger(this.mainApplicationClass)).logStarted(this.getApplicationLog(), stopWatch);
            }

            listeners.started(context);
            //这里是重点，调用具体的执行方法
            this.callRunners(context, applicationArguments);
        } catch (Throwable var10) {
            this.handleRunFailure(context, var10, exceptionReporters, listeners);
            throw new IllegalStateException(var10);
        }

        try {
            listeners.running(context);
            return context;
        } catch (Throwable var9) {
            this.handleRunFailure(context, var9, exceptionReporters, (SpringApplicationRunListeners)null);
            throw new IllegalStateException(var9);
        }
    }

   private void callRunners(ApplicationContext context, ApplicationArguments args) {
        List<Object> runners = new ArrayList();
        runners.addAll(context.getBeansOfType(ApplicationRunner.class).values());
        runners.addAll(context.getBeansOfType(CommandLineRunner.class).values());
        //重点来了，按照定义的优先级顺序排序
        AnnotationAwareOrderComparator.sort(runners);
        Iterator var4 = (new LinkedHashSet(runners)).iterator();
        //循环调用具体方法
        while(var4.hasNext()) {
            Object runner = var4.next();
            if (runner instanceof ApplicationRunner) {
                this.callRunner((ApplicationRunner)runner, args);
            }

            if (runner instanceof CommandLineRunner) {
                this.callRunner((CommandLineRunner)runner, args);
            }
        }

    }

    private void callRunner(ApplicationRunner runner, ApplicationArguments args) {
        try {
            //执行方法
            runner.run(args);
        } catch (Exception var4) {
            throw new IllegalStateException("Failed to execute ApplicationRunner", var4);
        }
    }

    private void callRunner(CommandLineRunner runner, ApplicationArguments args) {
        try {
            //执行方法
            runner.run(args.getSourceArgs());
        } catch (Exception var4) {
            throw new IllegalStateException("Failed to execute CommandLineRunner", var4);
        }
    }
```



# SpringBoot

## SpringBoot Servlet容器

```java
public class XXXServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {        

    //TODO Auto-generated method stub super.doGet(req, resp);

    }
}

@SpringBootApplication
@ServletComponentScan  //在springBoot启动时会自动扫描@WebServlet，并将该类实例化
public class DemoApplication {
 
    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }
}
```

## SpringBoot Tomcat容器

Tomcat打破了双亲委派

## Netty



## Jetty



## Servlet



## Mima



## Nginx



## Tomcat



## SpringBoot CommandRunner和ApplicationRunner

接口是在容器启动成功后的最后一步回调（类似开机自启动）

## CommandLineRunner、ApplicationRunner

开机自启动

## 自定义starter

/Meta-INF/XXX.factories文件注册 @Configuration自动装配

## 事件驱动

在不利用MQ的情况下，业务A处理完后，同时触发B、C、D业务执行。用事件驱动的好处是各个子过程的开发可以专注于自己的业务。

@TransactionalEventListener实现监听事件的事务隔。

Spring事件3个部分组成：ApplicationEvent、ApplicationEventPublisherAware、ApplicationListener

onApplicationEvent方法上加@Async支持异步，在有@EventListener的注解方法上加上@Async。注：启动类上同时要加上@EnableAsync。

## SpringBoot安全

使用HTTPs

## SpringBoot 2.X和1.X版本区别

2.X 响应式编程、至少JDK 1.8、支持Kotlin、支持http 2.0

SpringBoot2单元测试不支持.yml

2.0开始@Deprecated WebMvcConfigurerAdapter，推荐采用WebMvcConfigurer、WebMvcConfigurationSupport

```java
@Configuration
public class WebMvcConfg implements WebMvcConfigurer {
  //省略
}
@Configuration
public class WebMvcConfg extends WebMvcConfigurationSupport {
  //省略
}
```

# Session



# HTTP

## HTTP 1.0

## HTTP 1.X

## HTTP 2.0 VS HTTP 1.X

## HTTP VS HTTPS



 

## HTTP 状态码

```css
1 消息
▪ 100 Continue
▪ 101 Switching Protocols
▪ 102 Processing
2 成功
▪ 200 OK
▪ 201 Created
▪ 202 Accepted
▪ 203 Non-Authoritative Information
▪ 204 No Content
▪ 205 Reset Content
▪ 206 Partial Content
▪ 207 Multi-Status
3 重定向
▪ 300 Multiple Choices
▪ 301 Moved Permanently
▪ 302 Move Temporarily
▪ 303 See Other
▪ 304 Not Modified
▪ 305 Use Proxy
▪ 306 Switch Proxy
▪ 307 Temporary Redirect
4 请求错误 (前端发了，服务器未收到、服务器不接受、服务器不理解)
▪ 400 Bad Request
▪ 401 Unauthorized
▪ 402 Payment Required
▪ 403 Forbidden
▪ 404 Not Found
▪ 405 Method Not Allowed
▪ 406 Not Acceptable
▪ 407 Proxy Authentication Required
▪ 408 Request Timeout
▪ 409 Conflict
▪ 410 Gone
▪ 411 Length Required
▪ 412 Precondition Failed
▪ 413 Request Entity Too Large
▪ 414 Request-URI Too Long
▪ 415 Unsupported Media Type
▪ 416 Requested Range Not Satisfiable
▪ 417 Expectation Failed
▪ 418 I'm a teapot
▪ 421Misdirected Request
▪ 422 Unprocessable Entity
▪ 423 Locked
▪ 424 Failed Dependency
▪ 425 Too Early
▪ 426 Upgrade Required
▪ 449 Retry With
▪ 451 Unavailable For Legal Reasons
5 服务器错误 (服务器收到了前端的请求却处理不了)
▪ 500 Internal Server Error
▪ 501 Not Implemented
▪ 502 Bad Gateway
▪ 503 Service Unavailable
▪ 504 Gateway Timeout
▪ 505 HTTP Version Not Supported
▪ 506 Variant Also Negotiates
▪ 507 Insufficient Storage
▪ 509 Bandwidth Limit Exceeded
▪ 510 Not Extended
▪ 600 Unparseable Response Headers
```

## HTTP 扩展

```css
Accept 设置接受的内容类型 Ex. Accept: text/plain

Accept-Charset 设置接受的字符编码 Ex. Accept-Charset: utf-8

Accept-Encoding 设置接受的编码格式 Ex. Accept-Encoding: gzip, deflate  gzip压缩减少网络传输，纯文本大概可压缩至40%

Accept-Datetime 设置接受的版本时间 Ex. Accept-Datetime: Thu, 31 May 2007 20:35:00 GMT

Accept-Language 设置接受的语言 Ex. Accept-Language: en-US

Authorization 设置HTTP身份验证的凭证 Ex. Authorization: Basic QWxhZGRpbjpvcGVuIHNlc2FtZQ== 若没有使用SSL/TLS传输层安全协议，以明文传输的密钥和口令很容易被拦截。若需使用Basic Authorization，在服务器Response Headers添加access-control-allow-headers:Authorization

Cache-Control 设置请求响应链上所有的缓存机制必须遵守的指令 Ex. Cache-Control: no-cache

Connection 设置当前连接和hop-by-hop协议请求字段列表的控制选项 Ex. Connection: keep-alive、Connection: Upgrade、Connection: closed
HTTP早期，每个HTTP请求都要求打开一个TCP Socket连接，并且使用一次之后就断开这个TCP连接。可以tcpdump -n host <u>www.baidu.com</u> 抓包分析。@See https://www.cnblogs.com/freefish12/p/5394876.html。但从HTTP/1.1起，浏览器都开启了keep-alive，Keep-Alive不会永久保持连接，它有一个被设定的保持时间(Apache可设定)。当一个网页打开完成后，客户端和服务器之间用于传输HTTP数据的TCP连接不会关闭，如果客户端再次访问这个服务器上的网页，会继续使用这一条已经建立的TCP连接。长连接、长轮询long-polling基于HTTP的长连接，是一种通过长轮询long-polling实现服务器推技术。
    
Upgrade 请求服务端升级协议 Ex. Upgrade: HTTP/2.0, HTTPS/1.3, IRC/6.9, RTA/x11, websocket
Connection: Upgrade 表示Upgrade是一个hop-by-hop的字段，是给proxy看的(proxy一般是Nginx)。Upgrade: websocket 表示浏览器想要升级到WebSocket协议，是给最终处理请求程序看的。如果只有Upgrade: websocket，说明proxy不支持websocket升级，按照标准应该视为普通HTTP请求。使用首部字段 Upgrade 时，还需要额外指定 Connection: Upgrade。
hop-by-hop header(逐跳头部)用来描述当前浏览器与直连服务器(Nginx反向代理)的连接信息，默认的hop-by-hop header 有Connection, Keep-Alive, Proxy-Authenticate, Proxy-Authorization, TE, Trailers, Transfer-Encoding, Upgrade @See https://www.yuque.com/devweb/front/ztg8ur

Content-Length 设置请求体的字节长度  Ex. Content-Length: 348

Content-MD5 设置基于MD5算法对请求体内容进行Base64二进制编码 Ex. Content-MD5: Q2hlY2sgSW50ZWdyaXR5IQ==

Content-Type 设置请求体的MIME类型(适用POST和PUT请求) Ex. Content-Type: application/x-www-form-urlencoded、Content-Type: multipart/form-data
Content-Type: multipart/form-data 可同时字段表单提交和Multipart文件上传，不直接先上传图片返回前端url再将url放@RequestBody请求服务端为了防刷上传

Cookie 设置服务器使用Set-Cookie发送的http cookie Ex. Cookie: $Version=1; Skin=new;

Date 设置消息发送的日期和时间 Ex. Date: Tue, 15 Nov 1994 08:12:31 GMT

Expect 标识客户端需要的特殊浏览器行为 Ex. Expect: 100-continue

Forwarded 披露客户端通过http代理连接web服务的源信息

Forwarded: for=192.0.2.60;proto=http;by=203.0.113.43
Forwarded: for=192.0.2.43, for=198.51.100.17

From 设置发送请求的用户的email地址

From: user@example.com

Host 设置服务器域名和TCP端口号，如果使用的是服务请求标准端口号，端口号可以省略

Host: en.wikipedia.org:8080
Host: en.wikipedia.org

If-Match 设置客户端的ETag，当时客户端ETag和服务器生成的ETag一致才执行，适用于更新自从上次更新之后没有改变的资源 Ex. If-Match: "737060cd8c284d8af7ad3082f209582d

If-Modified-Since 设置更新时间，从更新时间到服务端接受请求这段时间内如果资源没有改变，允许服务端返回304 Not Modified Ex. If-Modified-Since: Sat, 29 Oct 1994 19:43:31 GMT

If-None-Match 设置客户端ETag，如果和服务端接受请求生成的ETage相同，允许服务端返回304 Not Modified

If-None-Match: "737060cd8c284d8af7ad3082f209582d"

If-Range 设置客户端ETag，如果和服务端接受请求生成的ETage相同，返回缺失的实体部分；否则返回整个新的实体

If-Range: "737060cd8c284d8af7ad3082f209582d"

If-Unmodified-Since 设置更新时间，只有从更新时间到服务端接受请求这段时间内实体没有改变，服务端才会发送响应

If-Unmodified-Since: Sat, 29 Oct 1994 19:43:31 GMT

Max-Forwards 限制代理或网关转发消息的次数

Max-Forwards: 10

Origin 标识跨域资源请求（请求服务端设置Access-Control-Allow-Origin响应字段）

Origin: http://www.example-social-network.com

Pragma 设置特殊实现字段，可能会对请求响应链有多种影响

Pragma: no-cache

Proxy-Authorization 为连接代理授权认证信息

Proxy-Authorization: Basic QWxhZGRpbjpvcGVuIHNlc2FtZQ==

Range 请求部分实体，设置请求实体的字节数范围，具体可以参见HTTP/1.1中的Byte serving

Range: bytes=500-999

Referer 设置前一个页面的地址，并且前一个页面中的连接指向当前请求，意思就是如果当前请求是在A页面中发送的，那么referer就是A页面的url地址（轶事：这个单词正确的拼法应该是"referrer",但是在很多规范中都拼成了"referer"，所以这个单词也就成为标准用法）

Referer: http://en.wikipedia.org/wiki/Main_Page

TE 设置用户代理期望接受的传输编码格式，和响应头中的Transfer-Encoding字段一样

TE: trailers, deflate


User-Agent 用户代理的字符串值

User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:12.0) Gecko/20100101 Firefox/21.0

Via 通知服务器代理请求

Via: 1.0 fred, 1.1 example.com (Apache/1.1)

Warning 实体可能会发生的问题的通用警告

Warning: 199 Miscellaneous warning

常用非标准请求头字段
X-Requested-With 标识Ajax请求，大部分js框架发送请求时都会设置它为XMLHttpRequest

X-Requested-With: XMLHttpRequest

DNT 请求web应用禁用用户追踪

DNT: 1 (Do Not Track Enabled)
DNT: 0 (Do Not Track Disabled)

X-Forwarded-For 一个事实标准，用来标识客户端通过HTTP代理或者负载均衡器连接的web服务器的原始IP地址

X-Forwarded-For: client1, proxy1, proxy2
X-Forwarded-For: 129.78.138.66, 129.78.64.103

X-Forwarded-Host 一个事实标准，用来标识客户端在HTTP请求头中请求的原始host,因为主机名或者反向代理的端口可能与处理请求的原始服务器不同

X-Forwarded-Host: en.wikipedia.org:8080
X-Forwarded-Host: en.wikipedia.org

X-Forwarded-Proto 一个事实标准，用来标识HTTP原始协议，因为反向代理或者负载均衡器和web服务器可能使用http,但是请求到反向代理使用的是https

X-Forwarded-Proto: https

Front-End-Https 微软应用程序和负载均衡器使用的非标准header字段 Front-End-Https: on
X-Http-Method-Override 请求web应用时，使用header字段中给定的方法（通常是put或者delete）覆盖请求中指定的方法（通常是post）,如果用户代理或者防火墙不支持直接使用put或者delete方法发送请求时，可以使用这个字段

X-HTTP-Method-Override: DELETE

X-ATT-DeviceId 允许更简单的解析用户代理在AT&T设备上的MakeModel/Firmware

X-Att-Deviceid: GT-P7320/P7320XXLPG

X-Wap-Profile 设置描述当前连接设备的详细信息的xml文件在网络中的位置

x-wap-profile: http://wap.samsungmobile.com/uaprof/SGH-I777.xml

Proxy-Connection 早起HTTP版本中的一个误称，现在使用标准的connection字段

Proxy-Connection: keep-alive

X-UIDH 服务端深度包检测插入的一个唯一ID标识Verizon Wireless的客户

X-UIDH: ...

X-Csrf-Token,X-CSRFToken,X-XSRF-TOKEN 防止跨站请求伪造

X-Csrf-Token: i8XNjC4b8KVok4uw5RftR38Wgp2BFwql

X-Request-ID,X-Correlation-ID 标识客户端和服务端的HTTP请求

X-Request-ID: f058ebd6-02f7-4d3f-942e-904344e8cde5

常用标准响应头字段
Access-Control-Allow-Origin 指定哪些站点可以参与跨站资源共享

Access-Control-Allow-Origin: *

Accept-Patch 指定服务器支持的补丁文档格式，适用于http的patch方法

Accept-Patch: text/example;charset=utf-8

Accept-Ranges 服务器通过byte serving支持的部分内容范围类型

Accept-Ranges: bytes

Age 对象在代理缓存中暂存的秒数

Age: 12

Allow 设置特定资源的有效行为，适用方法不被允许的http 405错误

Allow: GET, HEAD

Alt-Svc 服务器使用"Alt-Svc"（Alternative Servicesde的缩写）头标识资源可以通过不同的网络位置或者不同的网络协议获取

Alt-Svc: h2="http2.example.com:443"; ma=7200

Cache-Control 告诉服务端到客户端所有的缓存机制是否可以缓存这个对象，单位是秒

Cache-Control: max-age=3600

Connection 设置当前连接和hop-by-hop协议请求字段列表的控制选项

Connection: close

Content-Disposition 告诉客户端弹出一个文件下载框，并且可以指定下载文件名

Content-Disposition: attachment; filename="fname.ext"

Content-Encoding 设置数据使用的编码类型

Content-Encoding: gzip

Content-Language 为封闭内容设置自然语言或者目标用户语言

Content-Language: en

Content-Length 响应体的字节长度

Content-Length: 348

Content-Location 设置返回数据的另一个位置

Content-Location: /index.htm

Content-MD5 设置基于MD5算法对响应体内容进行Base64二进制编码

Content-MD5: Q2hlY2sgSW50ZWdyaXR5IQ==

Content-Range 标识响应体内容属于完整消息体中的那一部分

Content-Range: bytes 21010-47021/47022

Content-Type 设置响应体的MIME类型

Content-Type: text/html; charset=utf-8

Date 设置消息发送的日期和时间

Date: Tue, 15 Nov 1994 08:12:31 GMT

ETag 特定版本资源的标识符，通常是消息摘要

ETag: "737060cd8c284d8af7ad3082f209582d"

Expires 设置响应体的过期时间

Expires: Thu, 01 Dec 1994 16:00:00 GMT

Last-Modified 设置请求对象最后一次的修改日期

Last-Modified: Tue, 15 Nov 1994 12:45:26 GMT

Link 设置与其他资源的类型关系

Link: </feed>; rel="alternate"

Location 在重定向中或者创建新资源时使用

Location: http://www.w3.org/pub/WWW/People.html

P3P 以P3P:CP="your_compact_policy"的格式设置支持P3P(Platform for Privacy Preferences Project)策略，大部分浏览器没有完全支持P3P策略，许多站点设置假的策略内容欺骗支持P3P策略的浏览器以获取第三方cookie的授权

P3P: CP="This is not a P3P policy! See http://www.google.com/support/accounts/bin/answer.py?hl=en&answer=151657 for more info."

Pragma 设置特殊实现字段，可能会对请求响应链有多种影响

Pragma: no-cache

Proxy-Authenticate 设置访问代理的请求权限

Proxy-Authenticate: Basic

Public-Key-Pins 设置站点的授权TLS证书

Public-Key-Pins: max-age=2592000; pin-sha256="E9CZ9INDbd+2eRQozYqqbQ2yXLVKB9+xcprMF+44U1g=";

Refresh "重定向或者新资源创建时使用，在页面的头部有个扩展可以实现相似的功能，并且大部分浏览器都支持
<meta http-equiv="refresh" content="5; url=http://example.com/">

Refresh: 5; url=http://www.w3.org/pub/WWW/People.html

Retry-After 如果实体暂时不可用，可以设置这个值让客户端重试，可以使用时间段（单位是秒）或者HTTP时间

Example 1: Retry-After: 120
Example 2: Retry-After: Fri, 07 Nov 2014 23:59:59 GMT

Server 服务器名称

Server: Apache/2.4.1 (Unix)

Set-Cookie 设置HTTP Cookie

Set-Cookie: UserID=JohnDoe; Max-Age=3600; Version=1

Status 设置HTTP响应状态

Status: 200 OK

Strict-Transport-Security 一种HSTS策略通知HTTP客户端缓存HTTPS策略多长时间以及是否应用到子域

Strict-Transport-Security: max-age=16070400; includeSubDomains

Trailer 标识给定的header字段将展示在后续的chunked编码的消息中

Trailer: Max-Forwards

Transfer-Encoding 设置传输实体的编码格式，目前支持的格式：chunked, compress, deflate, gzip, identity

Transfer-Encoding: chunked

TSV Tracking Status Value，在响应中设置给DNT(do-not-track),可能的取值
　　　"!" — under construction
　　　"?" — dynamic
　　　"G" — gateway to multiple parties
　　　"N" — not tracking
　　　"T" — tracking
　　　"C" — tracking with consent
　　　"P" — tracking only if consented
　　　"D" — disregarding DNT
　　　"U" — updated

TSV: ?

Upgrade 请求客户端升级协议

Upgrade: HTTP/2.0, HTTPS/1.3, IRC/6.9, RTA/x11, websocket

Vary 通知下级代理如何匹配未来的请求头已让其决定缓存的响应是否可用而不是重新从源主机请求新的

Example 1: Vary: *
Example 2: Vary: Accept-Language

Via 通知客户端代理，通过其要发送什么响应

Via: 1.0 fred, 1.1 example.com (Apache/1.1)

Warning 实体可能会发生的问题的通用警告

Warning: 199 Miscellaneous warning

WWW-Authenticate 标识访问请求实体的身份验证方案

WWW-Authenticate: Basic

X-Frame-Options 点击劫持保护：
　　　deny frame中不渲染
　　　sameorigin 如果源不匹配不渲染
　　　allow-from 允许指定位置访问
　　　allowall 不标准，允许任意位置访问

X-Frame-Options: deny

常用非标准响应头字段
X-XSS-Protection 过滤跨站脚本

X-XSS-Protection: 1; mode=block

Content-Security-Policy, X-Content-Security-Policy,X-WebKit-CSP 定义内容安全策略

X-WebKit-CSP: default-src 'self'

X-Content-Type-Options 唯一的取值是"",阻止IE在响应中嗅探定义的内容格式以外的其他MIME格式

X-Content-Type-Options: nosniff

X-Powered-By 指定支持web应用的技术

X-Powered-By: PHP/5.4.0

X-UA-Compatible 推荐首选的渲染引擎来展示内容，通常向后兼容，也用于激活IE中内嵌chrome框架插件
<meta http-equiv="X-UA-Compatible" content="chrome=1" />

X-UA-Compatible: IE=EmulateIE7
X-UA-Compatible: IE=edge
X-UA-Compatible: Chrome=1

X-Content-Duration 提供音视频的持续时间，单位是秒，只有Gecko内核浏览器支持

X-Content-Duration: 42.666

Upgrade-Insecure-Requests 标识服务器是否可以处理HTTPS协议

Upgrade-Insecure-Requests: 1

X-Request-ID,X-Correlation-ID 标识一个客户端和服务端的请求 Ex. X-Request-ID: f058ebd6-02f7-4d3f-942e-904344e8cde5
```

## TCP 重传、滑动窗口、流量控制、拥塞控制 

# MQ

## 消息协议

### TCP

 Kafka

### MQTT

Message Queuing Telemetry Transport 消息队列遥测传输。基于TCP/IP，Mosquito

### AMQP

RabbitMQ

### RTMP



## 为什么要用MQ？

削峰：上游流量大、下游扛不住

解耦：支持业务扩展

冗余：一对多，一个生成者，多个订阅Topic

健壮：消息积压

异步：存队列时不需要立即处理，在需要时取队列数据才处理

消息一致性：账号转账如系统A扣钱，系统B加钱(利用事务)

## VS



## 常见发送问题和错误方案：

(1)将发送消息网络调用和update DB放在同一个事务里，若发送消息失败，update DB自动回滚

A.发送消息失败，发送方并不知道消息中间件是否真的没收到消息（MQ消息已经收到，只是返回response时候失败了）

B.将网络调用放在事务DB中，因网络延时，导致DB长事务，严重会Block整个DB。

## 常见消费失败问题：

### （1）Kafka

kafka消费时存在业务异常，暂不提交offset，保存消费失败的消息记录，根据失败策略处理相应消息。保存消费失败的消息记录后可以提交offset。

kafka消费时网络异常，重试，超过重试次数进行人工处理。

失败策略处理：（1）定时重试（2）失败处理隔五分钟再往对应的消息队列发送该消息，发送成功后就次数+1，根据消息id定位消息，记录消息消费次数，达到次数的阀值改为人工处理。

### （2）RabbitMQ

消费失败的消息放入死信队列，仓储系统会开启一个独立的线程（当第三方系统服务正常的情况下）用来处理死信队列，该线程还需用来监控第三方系统服务的状态。

## Kafka

https://www.cnblogs.com/huxi2b/p/6223228.html

LinkIn研发处理流式数据，Kafka一个topic可以分成多个Partition，一个topic可以被多个group消费，**每个Partition只能对应一个消费者消费**，Partition每个消息对应唯一的offset。

### 版本

```css
Kafka 2.10/2.11 不是Kafka的版本，而是编译Kafka的Scala版本
Kafka Server端是Scala编写，Scala主流3个版本分别是2.10、2.11、2.12，Kafka现在每个PULL request都已经自动增加了这三个版本的检查
Kafka广泛使用的版本：0.8.x、0.9.x、0.10.* 
Kafka 0.9.x之前：提供ConsumerConnector、ZookeeperConsumerConnector以及SimpleConsumer，Consumer是Scala编写，包名结构是kafka.consumer.*，分为high-level consumer和low-level consumer 
Kafka 0.9.x开始提供Java版本的Consumer，新版本Consumer可以独立部署，不再需要依赖Server端代码，提供KafkaConsumer和ConsumerRecord，包名结构是o.a.k.clients.consumer.*
```



### 适用场景

收集日志、监控信息、埋点

通过Zookeeper维护offset，消费端维护offset，持久化属于日志型持久化默认7天删除消息。

consumer加入group，

```java
@KafkaListener(id="test1",topics = "test-topic", containerFactory="kafkaListenerContainerFactory1")
@KafkaListener(id="test2",topics = "test-topic", containerFactory="kafkaListenerContainerFactory2")
```

### Kafka支持事务？



### Kafka支持消息优先级



### 为什么Kafka那么快？

Pull、Zero-Copy、Partition

Pull模式与消费端处理能力相符

Zero-Copy 零拷贝技术



顺序写 Partition，一个Partition里的消息是有序的

### Zero-Copy 零拷贝

#### 什么是Zero-Copy 零拷贝？

#### Zero-Copy需要CPU？

不需要（从用户态到核心态切换的过程是CPU控制）

#### Pull VS Post



### 有序消费

![Kafka Ordering Consume](http://hongchengjian.gitee.io/md/img/mq/Kafka%20Ordering%20Comsume.png)

### ISR、AR代表什么？ISR伸缩？

ISR：In-Sync Replicas副本同步队列，ISR由leader维护，follower从leader同步数据

AR：Assigned Replicas 所有副本

AR=ISR + OSR

### Broker消息代理

Producer往Broker里指定Topic中写消息，Consumers从Brokers里拉取指定Topic消息进行业务处理，Broker起到一个代理保存消息的中转站。

producer生产一条消息，存储到哪个broker server中

### Kafka选举基于Broker还是Group？

基于Broker

### ConsumerGroup中新加Consumer、移除Consumer、Consumer崩溃时发生Rebalance

Rebalance协议规定一个Consumer Group下所有Consumer 如何达成一致来分配订阅Topic下的每个Partition。

一个Group下20个Consumer，Group订阅了具100个Partition的Topic，正常情况经过Rebalance，平均每个

Consumer分配5个Partition。

### Kafka为什么不将offset保存Broker维护？而是在Partition维护？



## RabbitMQ

### 模型

![RabbitMQ Model](http://hongchengjian.gitee.io/md/img/mq/RabbitMQ%20Model.png)

### 顺序消费(RabbitMQ本身缺少顺序消费机制)

单个queue在多消费者下不能保证有序消费

### 重复消费出现场景

任务超时，没有及时返回状态，引起任务重新入队列后重新消费

连接断开也会触发重复消费

### 解决重复消费



### 消费失败处理

（1）消费失败的消息放入死信队列，开启独立线程（当第三方系统服务正常的情况下）用来处理死信队列，该线程还需用来监控第三方系统服务的状态。

（2）网络异常重试超过阀值进行熔断，业务异常切到具体业务异常code对应的处理机制中。兜底写库后尝试起定时任务和做开关重试。

### 死信队列原理

```
DLX dead-letter-exchange
```

#### 死信几种情况

```css
（1）消息被拒绝(basic.reject / basic.nack)，并且requeue = false
（2）消息TimeToLive TTL过期
$ curl -i -u guest:guest -H "content-type:application/json"  -XPUT -d'{"auto_delete":false,"durable":true,"arguments":{"x-message-ttl": 60000}}' 
（3）队列达到最大长度（rabbitMQ的积压能力比较落）
（4）消费失败时放入（可选情况）
```



### RabbitMQ的事务（Confirm模式要比事务快10倍）

#### （1）AMQP的事务机制

```java
Channel channel = conn.createChannel();
// 声明队列
channel.queueDeclare(_queueName, true, false, false, null);
String message = String.format("时间 => %s", new Date().getTime());
try {
	channel.txSelect(); // 声明事务
	// 发送消息
	channel.basicPublish("", _queueName, MessageProperties.PERSISTENT_TEXT_PLAIN, message.getBytes("UTF-8"));
	channel.txCommit(); // 提交事务
} catch (Exception e) {
	channel.txRollback();
} finally {
	channel.close();
	conn.close();
}
抓包步骤：
（1）Client端向Server端发 Tx.Select
（2）Server端返回Tx.Select-OK
（3）Client端推送消息
（4）客户端发送给事务提交Tx.Commit
（5）服务端返回Tx.Commit-OK

消费端若使用了事务，autoAck=false，手动确认后回滚Rollback了事务，此条消息会重新放回队列。autoAck=true，手动确认后回滚Rollback了事务，队列已经把消息移除了。
```

#### （2）发送者确认模式实现

Confirm机制3种：

```css
channel.waitForConfirms()普通发送方确认模式
Confirm批量确定和Confirm异步模式性能相差不大
channel.waitForConfirmsOrDie()批量确认模式，只要批次中有一个消息未被确认就会抛出IOException
channel.addConfirmListener()异步监听发送方确认模式，执行效率高
```



## RocketMQ

### 消息协议



### 事务原理



### 顺序消息原理

消息有序指的是一类消息消费时，能按照发送的顺序来消费。

### 延时消息解决方案

定时器Timer，延时队列DelayQueue

### 延时消息场景

提交了一个订单就发送一个延时消息，1h后去检查这个订单的状态，如果还是未付款就取消订单释放库存。

### 延时只支持18个level原理

为什么只支持18个level?  而不是开放出自定义延时？ 减少Broker排序

延迟时间间隔为：1s、 5s、 10s、 30s、 1m、 2m、 3m、 4m、 5m、 6m、 7m、 8m、 9m、 10m、 20m、 30m、 1h、 2h

```css
https://github.com/apache/rocketmq/issues/336
dongeforever commented on 25 Jun 2018
The delay level is determined by the configuration named 'messageDelayLevel' in broker. So it is not easy to define a enum in the client side.
In fact, I am developing a new evolutional timer message. And It will show in the near future.
```

### 消费方式

#### 集群消费（默认）

一个ConsumerGroup的Consumer实例平均分摊消费生产者发送的消息，某个topic有9条消息，其中一个Consumer Group有三个实例（3个进程或3台机器），每个实例只消费其中3条消息

#### 广播消费

一条消息被多个Consumer消费，即使这些Consumer属于同一个ConsumerGroup，消息也会被每个ConsumerGroup中的每个Consumer消费一次。

# K8s和Docker



# Go



# Python Flask、Django



# 安全

## 序列化默认id风险

**情境**：两个客户端 A 和 B 试图通过网络传递对象数据，A 端将对象 C 序列化为二进制数据再传给 B，B 反序列化得到 C。
**问题**：C 对象的全类路径假设为 com.inout.Test，在 A 和 B 端都有这么一个类文件，功能代码完全一致。也都实现了 Serializable 接口，但是反序列化时总是提示不成功。
**解决**：虚拟机是否允许反序列化，不仅取决于类路径和功能代码是否一致，一个非常重要的一点是两个类的序列化 ID 是否一致（就是 private static final long serialVersionUID = 1L）。清单 1 中，虽然两个类的功能代码完全一致，但是序列化 ID 不同，他们无法相互序列化和反序列化。

```java
package com.inout; 
import java.io.Serializable; 
public class A implements Serializable { 
    private static final long serialVersionUID = 1L; 
    private String name; 
    public String getName() { 
        return name; 
    } 

    public void setName(String name) { 
        this.name = name; 
    } 
} 

package com.inout; 
import java.io.Serializable; 
public class A implements Serializable { 
    private static final long serialVersionUID = 2L; 
    private String name; 
    public String getName() { 
        return name; 
    } 

    public void setName(String name) { 
        this.name = name; 
    } 
}
```



## CSRF保护

CSRF Cross-site request forgery 利用了web中用户身份验证的一个漏洞：**简单的身份验证只能保证请求发自某个用户的浏览器，却不能保证请求本身是用户自愿发出的**。

防御措施 检查Referer字段、增加sToken、Token校验





# JDK 

在 HotSpot 主流 OS上，采用模板解释器执行字节码，与JIT 编译器一样，最终执行的汇编代码都是在运行时候产生，无法断点调试。HotSpot 增加了

-XX: +TraceBytecodes 

-XX: StopInterpreterAt=<n>

参数作用是遇序号为<n>的字节码指令时，便中断程序执行，中断程序执行，进入断点调试 

使用永久代 Permanent Generation 方法实现方法区  存在内存溢出问题-XX: MaxPermSize 上限，如32位系统中4GB限制

java -Xcomp 强制虚拟机运行编译模式 Compiled Mode

java -Xint 强制虚拟机运行解释模式 Interpreted Mode

## 逃逸分析

Escape Analysis分析对象动态作用域

方法逃逸：当一个对象在方法被定义后，它可能被外部方法所引用，e.g. 作为调用参数传递到其他地方中。

线程逃逸：当一个对象在方法被定义后，可能被外部线程访问，e.g.赋值给类变量或可以在其他线程中访问的实例变量。

开启逃逸分析：-XX:+DoEscapeAnalysis （JDK1.8之后默认开启）



## JDK 1.0.2

改动过 invokespecial 指令

## JDK 1.2

### 引入双亲委派模型

### 扩充引用

（1）强引用 Strong Referrence：Object obj = new Object();

（2）软引用 Soft Referrence：有用非必需对象，在系统将要发生内存溢出异常之前，将进行第二次回收

JDK 1.2之后，提供了 SoftReference 类。

（3）弱引用 Weak Refferrence：垃圾回收器工作时，无论内存是否足够，都会回收掉被弱引用关联的对象

API 提供 WeakReference类实现canonicalizing mapping。

（4）虚引用Phantom Refferrence：无法通过虚引用获取一个对象实例，设置虚引用的目的是在这个对象被垃圾回收器回收时收到一个系统通知。

## JDK 1.4

NIO JSR 51：NIO优缺：引入 Channel 和  Buffer 的IO 方式，可以使用 Native 函数库直接分配堆外内存 ，然后通过一个存储在 Java 堆中的 DirectByteBuffer 对象作为这块内存的引用进行操作，从而避免了 Java 堆和 Native 堆中来回复制数据。

## JDK 1.5

### 引入两个新的reference types

（1）开始提供对注解 Annotation 的支持  annotation type

（2）enum type

枚举是类。Enums provide compile-time type safety。Enums are by their nature immutable。枚举是单例的。

## JDK 1.8

### Lambda

stream VS parallstream(Fork join)

#### Stream分类

![JDK1.8 Stream](http://hongchengjian.gitee.io/md/img/jdk/JDK1.8%20Stream.png)

#### Stream原理

```java
public interface Stream<T> extends BaseStream<T, Stream<T>> 
public interface BaseStream<T, S extends BaseStream<T, S>> extends AutoCloseable 
```

#### Demo



## 类的生命周期

lvpriuu

loading -> linking(verification -> preparation -> resolution) -> initialization -> using -> unloading

## Full GC(Major GC) 发生条件

发生条件老年代的连续空间 <（新生代所有对象的总大小或者历次晋升的平均大小）

-XX:+ DisableExplicitGC来禁止RMI（Java远程方法调用）调用System.gc( )

## Minor GC 发生条件

From Survior、To Survior互换时

## G1优势



## 什么时候发生

System.gc( )没人调用过

Full gc的过程是什么？

## Full GC VS Minor GC



##  Minor GC会stop the world STW？

会

https://blogs.oracle.com/jonthecollector/our-collectors

## 调优

-XX:PretenureSizeThreshold=3145728 定义多大的对象、长期存活的对象直接进入老年代

### JMM Java Memory Model

线程之间的共享变量存储在主内存 main memory，每一个线程都有一个私有本地内存 local memory，

本地内存中存储了该线程以读、写共享变量的副本。

### JVM是对Java内存模型的实现

### TProfile阿里开源在海量业务代码 精准定位性能代码问题

大量业务线程在频繁创建一些生命周期很长的临时对象

### OOM原因

（1）内存不足

（2）内存泄漏

### OOM可能发生在JVM哪些区域

PGen

Heap

Stack（VM Stack和Native Method Stack）

唯一不可能发生在程序计数器

### 如何排查OOM

Vmstat top找出最高的CPU、内存线程或jps —> heap dump分析—> MAT —> Leak suspect 对象集合中保存了大量对象的引用，导致内存泄露, 关注（1） while调用中new大对象（2）循环中建立大量连接调用（3） ThreadLoacl、流、资源、软引用对象、线程池是否用完回收和释放

### Full GC过程中Stop the World，JVM如何处理

Stop the World会暂停用户线程的执行

在GC发生时，直接把所有线程都挂起，然后检测所有线程是否都在安全点Safe Point，如果不在安全点则恢复线程的执行，等执行到安全点再挂起。

### 分析内存或CPU占用高

# 工具

## 测试工具

Postman，SoapUI，Ab，JMeter，LoadRunner

## 测试框架

WireMock，Mockito，PowerMock

JMock 、EasyMock 、Mockito有共同缺点：不能mock静态、final、私有方法等。而PowerMock弥补了这些不足。

### Mockito

@Spy VS @Mock VS @InjectMocks

@Spy 会真实调用

@Mock

mockito缺陷private和protected方法不能mock

mokito cannot mock okhttp3 response body because it is final

## API文档工具

YAPI，Swagger

## Idea

开启了Power Save Mode模式，会导致明显代码错误不进行提示。

# Open Source

开源大势所趋，MySQL在以开源软件和商业许可并行在 2008 年作价 10 亿美金由 Sun 收购，在 2009 年又被 Oracle 公司以 74 亿美金的高价收购。一直和开源软件做斗争的微软公司因无法快速推出适应市场的 Windows Phone 操作系统，在移动互联网竞争中处于下风。

## VS

大部分商业软件附带《最终用户许可协议》

## 开源协议

### GPL 





## 软件著作权权利

### 署名权 

我？个人？法人单位？

### 修改权

反编译、优化、重构

### 复制权



### 发布权

## Incubating孵化

# Zookeeper

## 四种节点类型

```css
PERSISTENT                持久化节点
PERSISTENT_SEQUENTIAL     顺序自动编号持久化节点，会根据当前已存在的节点数自动加 1
EPHEMERAL                 临时节点， 客户端session超时这类节点就会被自动删除
EPHEMERAL_SEQUENTIAL      临时自动编号节点
```



# Java基础

## Keywords

### static

静态代码块能包含this或者super？ 不能

当类加载器将类加载到JVM中的时候就会创建静态变量，这跟对象是否创建无关。静态变量加载的时候就会分配内存空间。静态代码块的代码只会在类第一次初始化的时候执行一次。一个类可以有多个静态代码块，它并不是类的成员，也没有返回值，并且不能直接调用。静态代码块不能包含this或者super,它们通常被用初始化静态变量。

### new



### final



## Java数据类型

```java
public static void main(String[] args){
	Integer f1 = 100, f2 = 100, f3 = 150, f4 = 150;
	System.out.print(f1 == f2);
	System.out.print(f3 == f4);
}
== byte,short,char,int,long,float,double,boolean比的是stack中的值
== 引用类型比的是reference address
Object.equals()默认是 ==
```

IntegerCache 是 Integer 的内部类。整型字面量的值在-128 到 127 之间，不会 new 新的 Integer 对象，而是直接引用常量池中的 Integer 对象，所以 f1== f2 的结果是 true，而 f3 ==f4 的结果是 false

## 序列化

什么是序列化？Java对象转成字节流、转化成二进制序列、转化成字节序列？

为什么Java序列化慢？

Java本身并不支持跨语言，序列化版本号，类名等信息导致流变大肯定慢。 

为什么Protobuf快？

（1）T-V and T-L-V 每个字段用tag|leg|value或tag|value存储，tag记录value对应字段编号和value的数据类型，tag是二进制byte存储，不是字符，不然一个String的中一个字符就要占用掉一个btye。string类型中leg记录字符串长度，避免了字符串定长的空间浪费（2）Varint以不同的长度来存储整数，ZigZag压缩将整数通过一个 hash 函数h(n) = (n<<1)^(n>>31)（如果是 sint64 h(n) = (n<<1)^(n>>63)），通过 ZigZag 编码，只要绝对值小的数字，都可以用较少位的 byte 表示。解决了负数的 Varint 位数会比较长的问题。（3）陈硕根据 GPB 的 C++ 版本源代码分析出其反射的具体机制：DescriptorPool类根据 type name 拿到一个 Descriptor的对象指针，在通过MessageFactory工厂类根据Descriptor实例构造出具体的Message对象。

```protobuf
message Person {
  int32 id = 1;
  string name = 2;
}
id字段的field为1，writetype为int32类型对应的序号。编码后id对应的 Tag 为 (field_number << 3) | wire_type = 0000 1000，其中低位的 3 位标识 writetype，其他位标识field。
```

static 和 transient 的成员变量，不能被序列化。

父类被序列化，其子类也可以被序列化。

实现序列化接口的类中依赖枚举，枚举也必须实现序列化接口。

什么情况下需序列化？网络传输、缓存操作、持久到文件IO。

都用默认的序列化id有什么坑？两个类的功能代码完全一致，但是序列化 ID 不同，他们无法相互序列化和反序列化。

项目大时，不同子项目A和B依赖同一个类ClassXX，子项目A编译时ClassXX自动生成一个serialVersionUID作为序列化版本，项目B因改动需求，需要在本地类ClassXX添加字段，子项目A未重新编译导致反序列化失败java.io.InvalidClassException。

序列化id的运用：Client 端通过 Facade Object与业务逻辑对象进行交互，客户端的 Facade Object 不能直接由 Client 生成，需Server 端生成后网络传输给Client。Server 端进行版本更新时，将Server 端的 Facade Object的序列化 ID 再次生成，当 Client 端反序列化 Façade Object 会失败，目的是强制 Client 端从Server 端获取最新程序。

Q：多个实体类用同一个序列化id会发生什么？

## 带标签break、continue



## 时间戳

时间戳是距离1970年的毫秒数。

数据库timestamp和时区无关，比较范围可以用date类型比较，用dateStr不准(数据库时区和服务机器时区不同时有时间差问题)





# 数据库

## 选型

![DB VS](http://hongchengjian.gitee.io/md/img/db/DB%20VS.png)

## 数据库规范

```css
不允许on commit刷新模式，须使用on demand刷新。
context命名规则为系统名+子系统名+功能描述。 
delete或update禁止出现order by，防止DML出现不必要排序。
delete或update必须出现where子句，防止DML过程出现全表锁。
隐式转换，在查询列上发生隐式转换。禁止嵌套select子句，防止出现select子句的嵌套子查询，出现性能问题。
禁止出现重复查询子句，可以使用with as替换子句来提升SQL语句执行效率。
单个SQL文本长度不能超过4000字节。
高频未使用绑定变量<= 50个sql文本，单个sql中的绑定变量不要超过50。

# 授权
只能授权应用表查询权限给DEV角色。
只能授权EXECUTE 查询权限给EXEC角色。禁止授权给PUBLIC用户。

# 版本
sql分版本维护，不同版本建立不同的包，格式：系统号-版本号-序列号-表名-DML\DDL\Trigger\View.sql。package命名规则是：系统名+子系统名+功能描述。

# with check option
使用WITH CHECK OPTION 选项进行数据约束时，必须使用指定的约束名称。视图只操作它可以查询出来的数据，对于它查询不出的数据，即使基表有，也不可以通过视图来操作。（1）对于update，有with check option，要保证update后，数据要被视图查询出来（2）对于delete，有无with check option都一样（3）对于insert，有with check option，要保证insert后，数据要被视图查询出来（4）对于没有where 子句的视图，使用with check option是多余。
本地视图禁止使用超过一层的嵌套视图，远端视图禁止使用超过2层的嵌套视图。创建视图时禁止使用select * from表名 语句，要求将用到的字段在视图或查询语句中列明，防止增加字段对应不上代码实体类DTO、PO报错。 

# 建表
范式（一.列 二.消除单表PK依赖，单表主键多个选用业务无关的字段做主键 三、消除PK传递依赖，如电商商品表细分为商品简略信息和详情两张表）
除临时表、日志表，其他建表必须有数据创建人 varchar2(100) not null、创建时间 date not null、修改人varchar2(100) not null、修改时间四个字段date not null，时间类字段的值推荐通过Trigger方式实现，如update t set date = sysdate，不推荐通过程序代码实现new Date存入。特殊配置项源数据表一次性导入后再无更新或追加数据的操作可不加。
表中一行记录所有字段的长度不能超过改数据库的db_block_size大小。
表和字段必须有comment注释，对于type类型字段必须罗列所有枚举值及相应的业务含义。命名中不允许出现数据库的关键字Reserved Word。为避免大小写敏感，禁止使用双引号将对象引用。Date类型字段必须以date作为前缀或后缀，boolean类型的字段必须以is作为前缀，主键字段命名不能包含任何业务含义，可以采用命名规则：id\_表名或直接id、pk。索引命名格式：IX\_字段名或字段名组合（复合索引）
选PK的原则（1）PK永不为空（2）PK永不改变，禁止程序Update PK（3）PK本身不是识别值（4）选择单一字段做PK。建主键和建表语句必须分开写。创建主键必须创建索引，再创建主键，所有外键上都必须创建索引，不推荐创建外键方式关联表。唯一键创建方式与主键相同，先建索引，后加主键。禁止更新主键列值，不允许有SQL更新主键。
创建、更改或删除Table时必须带上属主的名字。建主键和索引不需要指定索引表空间。创建或删除Trigger时必须带上属主的名字。创建或删除view时必须带上属主的名字。修改表时，若有增加default值的列或者修改字段的非空属性，必须先做DDL增加字段，再做DDL修改增加字段的default值属性，然后再做DML更新，最后加非空属性。Trigger命名：行级为同名表的命名规则|_suffix，语句级为同表名的命名规则\_s\_suffix。可选的suffix包括：BI、BU、BD、BSH、BDB、AI、AU、AD、ASH、ADB、II、IU、ID、ISH、IDB。
表命名规则禁止表名中使用无效的prefix 如 tbl_、db_ 。创建主键、约束和索引，不能指定索引表空间。创建或删除索引必须带上表名和属主名如 phwww.TABLE_NAME 。 
字段精度要求、财务系统金额相关都用decimal

# view
删除物化视图时，如果是快速刷新的物化视图，需要同时删除物化视图日志。物化视图必须以mv结尾，格式：表名\_功能描述\_mv。
视图禁止order by，不允许使用force refresh。

# sequence
创建sequence(一般做PK)时，maxValue后面的值必须是9。创建或删除sequence时必须带上属主名字。所有的sequence必须使用cache，cache值必须最低为40。sequence的命名规则是：系统名\_子系统名\_功能名。所有sequence需使用no order选项，创建sequence必须制定maxvalue、minvalue、start with、increment by、cache的值。

# partition
分区是水平扩展，一个表最多有1024个分区。
分区类型有range分区，list分区，hash分区，key分区。
表分区必须命名，一般根据日期、地域分区归档数据。表分区命名格式为，表名+分区特征+pt，索引分区命名格式为索引名+分区特征+pi，采用Hash自动分区或Oracle 11g Interval分区后，系统自动生成的SYS开头的表分区和索引分区可以例外。分区越多，Oracle维护成本越高。非Hash分区不要超过32个分区，Hash分区不要超过64个分区。分区的目的是性能优化或数据管理、数据归档、大批量数据的删除，在解决其中的一个需求前提下，且表数据量大于2G，才考虑分区。使用列表分区时，分区中必须包含default分区。使用hash分区时，分区数必须是2的N次方。分区表索引设计（1）若分区列是索引列的子集（无论是prefix或non-prefix），则建立local index。否则，遵循（2）。（2）若索引是唯一的，则建立global index，否则遵循（3）。（3）若基于性能考虑，且OLTP应用，用户要求更快响应时间，则建立global index；若应用是DSS类型，则用户更注重吞吐量，则建立local index。若基于维护性更方便，则建立local index。分区设计需关注，最终的数据要均匀分布到每个分区，偏大或偏小的比例不超过15%。除全局临时表和logtmp用户下的业务临时表及日志表以外，其他表必须建立主键。一个索引包含的所有字段的最大长度必须<= （db_block_size-192)*60%。
使用范围分区和列表分区必须使用Enable row movement.

# 同义词
创建同义词时禁止使用or replace关键字，create table语句参数不能包含storage选项，在archivelog模式下不能包含no logging选项，nologging会影响数据库的灾备和恢复。必须使用公共同义词，不能使用私有同义词。删除不再使用的数据库对象时，必须删除关联的同义词。同义词命名名称必须与指向对象的名称同名。
所有可以被引用的对象都应该建同义词。

# 大表
大表修改索引时加online（ MySQL 5.6）不阻塞DML语句，不加会阻塞其他session DML，高频SQL打满CPU。大表默认值加not null，事务型SQL都不适合for update和parallel，宽表要分段插入，字段>400以上是宽表，若批量如insert all 插入的字段时绑定临时变量值要分段插入，字段数目要<400，或者说宽表插入不适合关系型数据库来做，避免高并发sql超过2的32次方，数据库直接挂掉。
电商宽表高并发，先保证核心流程涉及到的字段抽离建小表，剩余字段放大表异步同步，保证核心业务不受影响。
join on条件复合索引，要防null (null会导致数据倾斜) 或者 on null == null(条件缺失或无其他明显区分占比的条件时导致全表扫)，会使数据库宕机。
高并发SQL，空值传入在绑定变量时mybatis需强制指定字段的数据类型或if标签判空。select全表的要加条数限制，where 1=1这种小心 1=1的后面条件是否失效。
笛卡尔积的sql一定要尽量使索引index type类型为const常量，不能大表全表扫，前后表的数据都要尽可能小，高频sql越小越好，不经常变更数据不放库，放配置或放缓存。放库放缓存只是保存的时间不一样，单机缓存是CP，集群缓存是AP，有读写和频繁更新缓存最终要刷盘落库，防止串状态。
大表禁select … insert into…，可采用匿名块、cursor进行批次处理，并记录log优化。

# explain
嵌套连接过深，执行计划中不允许嵌套过深超过6层。全表扫描，对于大于200M的表全表扫描，执行计划有TABLE ACCESS FULL操作，高频全表扫，表大小超过200M，且高频SQL如15分钟执行500次，PIR 3 Peak Information Rate级，表大小超过高速缓存1.5%，PIR 2级。
索引跳跃，执行计划中存在INDEX FULL SCAN

# 缓存
MySQL select会缓存查询结果，key是SQL语句，value是查询结果，是否开启缓存 query_cache_type，大小设定query_cache_size

# 函数
like 'xx%'走索引的通配查询优化，比如客户表查找以.com结尾的电子邮件， select  XX from T where email like '%.com'改为REVERSE('%.com')	ex. mysql> select REVERSE('abc');  -> 'cba'。思考like '%xx'为啥不走索引？
字符串偏向数值思想，INET_ATON(IP) 把 ip 转换为数字 Ex.查ip 在 192.168.1.3 到 192.168.1.20 之间的记录
select * from ip_table where inet_aton(ip) > inet_aton('192.168.1.3') and inet_aton(ip) < inet_aton('192.168.1.20');

# 关联
A表20W数据，B表500W数据，关联条件的字段建立索引，相互索引效率更高，一般小表 left join 大表效率更高些

# 索引Type类型
type类型字段尽量 2的n次方如2、4、8、16，避免1、2、3、4这种，最好not null带默认值，最好是数值型而不是varcach2类型，避免隐式转换。不追求性能可以存大写枚举字符串、前后端交互、数据库实体可以枚举交互
```



## 设计

### 主键

思考点：快(占CPU高还是不高）、是否有序(排序需求)、占用空间(位数是否够用)、随机、是否独立模块(穿插不同业务线)、是否预生成、是否有池子、获取是否批量、单个是否自增、是否唯一（MD5、SHA、SM3）、是否对业务友好(不同业务用不同位数标识分开、利于区分)、是否纯数字、字符串

```css
(1)MySQL自增  Q：OrderId直接做主键的缺陷？
(2)系统生成 snowfake、美团(Leaf)、滴滴(Tinyid)、百度(uid-generator)、redis incre
(3)Oracle sequence + 触发器函数
(4)UUID
(5)SHA、MD5、SM3
```

比如在插入表前，重点是前，对于涉及很多张表（可能一个模块几张表）都依赖于这个操作。缺陷排序、递增、索引效率str < 数值

中间表需要id吗？需要，即使没有业务含义也需要id

innodb必须要id吗？默认的id是int型，一般设计id是long型，防溢出。

MySQL innodb情况下，中间表为什么要创建主键？

### 分库分表

分库缓单库的session和连接池压力

分表缓单表数据量大压力

#### 切分模式

##### 水平切分

同一个表拆不同库，按数据行划分，有分表分库两种模式

#####  垂直切分

不同表分不同库，专库专用

按业务专库专用切分，业务之间join用接口替代

#### 分库分表工具

[当当sharding-jdbc]( https://github.com/apache/incubator-shardingsphere)、[蘑菇街TSharding]( https://github.com/baihui212/tsharding)、[sharding](https://github.com/go-pg/sharding)、[淘宝TDDL](https://github.com/alibaba/tb_tddl)、[360 Atlas](https://github.com/Qihoo360/Atlas)、[阿里巴巴B2B Cobar](https://github.com/alibaba/cobar)、[美团MyCAT基于Cobar](http://www.mycat.org.cn/)、[58同城 Oceanus](https://github.com/58code/Oceanus)、[支付宝楼方鑫](http://www.cnblogs.com/youge-OneSQL/articles/4208583.html)、[谷歌Vitess](https://github.com/youtube/vitess)

#### 分库策略

id取模、核心重要程度、id或字段数值、日期范围（冷数据）、热数据呢？

#### 分库影响

跨节点聚合、跨节点join、分布式事务

### NULL数据倾斜和影响

NULL对索引的影响、索引列尽量不为NULL，表设计比较忌讳`NULL`不能使用=、<、>这样的运算符，对null做算术运算的结果都是null。count(col)不会包括null行等，但count(*)会被优化，总是直接返回总行数的。null比空字符串需要更多的存储空间。

往timestamp类型的列中插入NULL值，插入的是系统当前时间。往auto_increment属性的列中插入NULL，会插入一个正整数。往字符型的列中插入NULL，插入的就是NULL。

### SQL自动检查

Yearning MYSQL

### 优化点

SQL语句（效果小）、索引、字段、表设计、主从复制（MySQL replicate）、读写分离（a.javax.sql.connection WriteDatabase ReadDatabase b.Spring AOP和Aspect实现数据源动态切换）、HA（双备）

## 存储引擎

InnoDB

NDB Cluster

MyIsam

Memory

## 事务

### 原理



### 事务管理器TransactionManager

跨库MySQL、Mongo的事务管理器只有一个执行后，切换另一个事务管理器不会再提交事务

#### Hibernate



#### Mybatis

##### Mybatis数据类型

```java
 1 Mybatis JDBC Type   Java Type  
 2 CHAR                String  
 3 VARCHAR             String  
 4 LONGVARCHAR         String  
 5 NUMERIC             java.math.BigDecimal  
 6 DECIMAL             java.math.BigDecimal  
 7 BIT             　　 boolean  
 8 BOOLEAN             boolean  
 9 TINYINT             byte  
10 SMALLINT            short  
11 INTEGER             int  
12 BIGINT              long  
13 REAL                float  
14 FLOAT               double  
15 DOUBLE              double  
16 BINARY              byte[]  
17 VARBINARY           byte[]  
18 LONGVARBINARY       byte[]  
19 DATE                java.sql.Date  
20 TIME                java.sql.Time  
21 TIMESTAMP           java.sql.Timestamp  
22 CLOB                Clob  
23 BLOB                Blob  
24 ARRAY               Array  
25 DISTINCT            mapping of underlying type  
26 STRUCT              Struct  
27 REF                 Ref  
28 DATALINK            java.net.URL[color=red][/color]  
```





### MySQL事务隔离级别

Serializable 串行化：避免脏读、不可重复读、幻读

RR Repeatable Read （MySQL默认）可重复读：避免脏读、不可重复读 

MySQL如何解决幻读？（1）MVVC 快照读、一致性读（2）next-key（当前读）锁包含记录锁（加在索引列的锁）、间隙锁（加在索引列之间的锁）

MySQL innoDB RR 通过快照读、当前读两种模式解决幻读问题

next-key原理是将当前数据行与上一条数据和下一条数据之间的间隙锁定，保证此范围内读取数据是一致的。

Read committed（Oracle默认，Oracle仅支持Serializable、Read committed） 读已提交：避免脏读

Read uncommitted 读未提交：最低级别，任何情况都无发提交

#### 脏、幻读（虚读）

脏读：事务A读取了一条记录的值，基于这条值做业务逻辑，在事务A提交之前，事务B回滚了该条记录，导致事务A读到了这条记录的一个脏数据。

脏读 T1读取了T2未提交数据

幻读（虚读）：一次事务里，多次查询后，结果集的个数不一致叫幻读。Ex.T1事务读123，T2事务插入4提交，T1再读库里1234。![Phantom Read](http://hongchengjian.gitee.io/md/img/db/Phantom%20Read.png)

MySQL可重复读的事务隔离级别前提下，T1事务读123，T2事务插入4，但T2提交后又撤销了，对T1事务的读并没有影响。

### Oracle



### 事务传播机制

什么是事务挂起？

如何内层的事务遇错不回滚？外层的事务不回滚？

### 事务回滚

执行SQL的connection与开启事务的connection必须是同一个才能对事务进行控制，事务Catch RuntimeException才回滚，常见的RuntimeException有？

往上抛的异常最上层才执行回滚

## 锁

where PK='XX' for update是一个行锁，for update是表锁，也是悲观锁，T1事务改表A并for update，T1不提交其他任何事务都改不了表A。数据库乐观锁还是CAS原理，常见实现是version、时间戳。

MySQL唯一索引和主键索引效率，主键（聚簇索引）优于唯一索引（非聚簇索引的一种是唯一索引，非聚簇索引包括复合索引）。

## 索引

### MySQL索引类型



### MySQL索引失效

!=  <>不走索引

对索引列计算、函数、类型转换不走索引

is null、is not null不走索引

or 索引会失效

隐式转换（e.g. 字符串不加单引号）会索引失效

like '%XXX' 不走索引，为什么？数据大时前缀索引数据也会变得非常大，没有意义。但like reverse后走索引，也可以用覆盖索引，如下面的执行语句也不会全表扫描。

![Index ABC](http://hongchengjian.gitee.io/md/img/db/Index%20ABC.png)mysql in走索引吗？有时走有时不走

### MySQL复合索引ABC问题

索引是key index （a,b,c）。 支持a | a,b| a,b,c 3种组合进行查找，但不支持 b,c进行查找 .当最左侧字段是常量引用时，索引就十分有效。

(1) select * from myTest where a=3 and b=5 and c=4; ---- abc顺序
abc三个索引都在where条件里面用到了，而且都发挥了作用

(2) select * from myTest where c=4 and b=6 and a=3;
where里面的条件顺序在查询之前会被mysql自动优化，效果跟上一句一样

(3) select * from myTest where a=3 and c=7;
a用到索引，b没有用，所以c是没有用到索引效果的（b没有使用到，所以索引达不到 c ，所以c未使用索引）

(4) select * from myTest where a=3 and b>7 and c=3; ---- b范围值，断点，阻塞了c的索引
a用到了，b也用到了，c没有用到，这个地方b是范围值，也算断点，只不过自身用到了索引

(5) select * from myTest where b=3 and c=4; — 联合索引必须按照顺序使用，并且需要全部使用
a索引没有使用，所以这里 bc都没有用上索引效果

(6) select * from myTest where a>4 and b=7 and c=9;
a用到了 b没有使用，c没有使用（a用了范围所以，相当于断点，之后的b，c都没有用到索引）

(7) select * from myTest where a=3 order by b;
a用到了索引，b在结果排序中也用到了索引的效果，a下面任意一段的b是排好序的

(8) select * from myTest where a=3 order by c;
a用到了索引，但是这个地方c没有发挥排序效果，因为中间断点了，使用 explain 可以看到 filesort

(9) select * from mytable where b=3 order by a;
b没有用到索引，排序中a也没有发挥索引效果



### MySQL复合索引最左原则底层原理

B+Tree按照第一个key进行索引排列

![Complex Index](http://hongchengjian.gitee.io/md/img/db/Complex%20Index.png)

索引看distinct占比，index加在distinct rows区分度比较高的字段，占比不高的字段<30%不适合建立索引，不如全表扫快。不要为逻辑写复杂sql用聚合、计算函数放弃单列索引，因为对单列索引进行计算、聚合等函数操作会使索引失效，复合索引的字段一般不要超过3个，比如A、B、C字段区分度相差比较均匀，且都<30%不能明显区分表数据，如A占20%区分度，B占10%区分度，C占15%区分度，适合对 (A,C,B)建复合索引观察查询效率，注意distinct占比高要左倾。单列索引遇到null要避免条件查询传入的条件字段值也为null，不然大表就可能直接全表扫。组合索引（A,B,C）时，带头大哥A不能死，有A,AB,*ABC*三种组合。极端情况AC，A和C也会使用索引，前提是B要有序；普通情况下，A走索引，C不走索引。https://www.cnblogs.com/codeAB/p/6387148.html

索引列函数在查询索引列上发生函数调用（函数索引除外）。

or 两边条件都建立索引时才会使用索引，只要有一边不是就会全表扫描。or对结果集影响注意左右两边是否缺少（），Ex.  on  条件A and  (source =1 and type =2 or type = 3)   VS on  条件A and（（source =1 and type =2） or （type = 3））

## 命令

### MySQL show variables

#### autocommit

 show variables like 'autocommit'; autocommit是针对连接的，在一个连接中修改了参数，不会对其他连接产生影响。如果关闭了autocommit，则所有的sql语句都在一个事务中，直到执行了commit或rollback，该事务结束，同时开始了另外一个事务。DDL语句(create table/drop table/alter/table)、lock tables语句在事务中执行了这些命令，会马上强制执行commit提交事务。

### MySQL explain

explain、explain extended（showwarning 可查得优化后的查询语句、rows*filtered/100估算出当前表和比当前表id值小的表进行连接的行数）、explain partitions（若查询是基于分区表会显示将查询的分区）

MySQL执行计划关注| id | select_type | table | partitions | type |possible_keys | key  | key_len | ref  | rows | filtered | Extra 

```css
简单说明：
id是select查询列，是SQL执行顺利标识，从大到小执行，先执行语句编号大的，MySQL将select分为简单查询、复杂查询（3个分别是简单子查询、from子查询、union查询）。
select_type区分普通查询（simple）、联合查询、子查询等复杂查询。
简单子查询 Ex. select (select 1 from account) from account;
from子查询 Ex.select id from (select id from account) as A;
union查询 Ex.select 1 union all select 1;
```

MySQL explain index type从优到差：system（系统表、空表、一行数据）> const （where条件是PK、unique index查满足条件的一行记录）> eq_ref （关联时出现，驱动表只返回一行数据，这行数据且是关联表的PK或unique index且not null）> ref（一般条件等值查询，不限连接顺序，不限PK和Unique Index、普通索引）> fulltext(MySQL优先使用全文检索、不管代价) > ref_or_null > index_merge（查询走两个以上索引取交、并集，但or使用时要查所有索引，此时性能不优于range） >unique_subquery(where中in子查询) > index_subquery > range（in、between、>、<、>=、like） > index(索引全表扫、索引排序、索引分组) > ALL（全表扫、service层内存检索优化防OOM）

CAUTION：possible keys（罗列查询可能用到的所有索引）有列、key（查询真正使用到的索引，select type为index merge时，key可能多个）显示Null，表中数据不多，MySQL认为索引对查询帮助不大，直接全表扫

Q1: select 1 from XX 是 const 还是 system？

![mysql explain select 1 from dual](img/mysql explain select 1 from dual

.png)

![image-mysql explain select 1 from T](img/mysql explain select 1 from T.png)

Q2: 什么情况下建立索引后查询实际不走索引？

## SQL

### Hive SQL VS SQL

Hive没有delete和update

### 分号符处理

select concat(key,concat(';',key)) from dual;分号符用ASCII

select concat(key,concat('\073',key)) from dual;

## 函数

### Hive常见函数



### MySQL join

![join](http://hongchengjian.gitee.io/md/img/db/join.png)

inner join的连接中,mysql会自己评估使用a表查b表的效率高还是b表查a表高，如果两个表都建有索引的情况下，mysql同样会评估使用a表条件字段上的索引效率高还是b表

select * from tb1 a ,tb2 b where a.id=b.id  join笛卡尔积 执行方式是将表a和表b的记录组合起来，然后考察满足条件的，并返回。

select * from tb1 a inner join tb2 b on a.id=b.id  inner join 参照表a中的记录，一条一条到表b中去找符合记录的，符合则连在一起，否则转到a中下一条



## Kettle ETL

# Hot Keys

## Mac Typora

```css
最大标题：command + 1 或者：#
大标题：command + 2 或者：##
标准标题：command + 3 或者：###
中标题：command + 4 或者：####
小标题：command + 5 或者：#####
插入表格：command + T
插入代码：command + alt +c 
行间公式 command + Alt + b
段落：command + 0
竖线 ： command + Alt + q
有序列表（1.  2.） ：输入数字+“.”之后输入空格 或者：command + Alt + o   
黑点标记：command + Alt + u  
隔离线：shift + command +  -
超链接：command + Alt + l
插入链接：command + k
下划线：command + u 
加粗：command + b
搜索：command + f
： Alt + Shift + K 	
√： Alt + v
```

## Mac Pro

```css
退出应用：Command + Q 
截全屏：Command + Shift + 3
截指定区域部分屏幕：Command + Shift + 4
退出全屏：Ctrl + Command + F 
指定程序窗口截图：Command + Shift + 4 + Space 
缩略所有打开窗口：Ctrl + 上下光标键  
Terminal打开一个后打开另外的终端则是：Ctrl + N
Spotlight Search: Command + Space
快速打开Terminal：Command + Space 输入Term
Chrome中打开一个后再打开一个是：Ctrl + N
Chrome中切换到第几个Tab页：Command + 数字1、2 ... 9
是否显示窗口左侧边栏：Option + Command + S
显示切最近几个程序界面：Command + H
从应用或窗口切换到桌面：Fn + F11
应用Page中文本复选框勾选：Ctrl + Command + Space后选择
Scroll调整屏幕亮度（下降）
快速进入指定文件夹：Finder --> Command + Shift + G 输入绝对路径

2020年解决brew下载慢问题：思路采用国内镜像下载
/bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/Homebrew.sh)"

zsh 终极shell 

```

## Mac Pro Note

```css
缩进： Command + ]或[
去掉下划线：Command + U
快速切换到一行开头或一行结尾：Command + 左右光标键
```

## Linux

```css
wget https://XXXX
unzip XXX.zip
tar -xzv  v-verbose显示指令执行过程 x-extract或get z-gzip命令
./consul 
> 是覆盖原有类容  >> 是追加
mysql -u root -p -h test < test.sql 导入数据
tcpdump -n host www.baidu.com 抓包分析
io状态：iostat -d -k 2
netstat -n | awk '/^tcp/ {++S[$NF]} END {for(a in S) print a, S[a]}'   
检查磁盘空间df -h，磁盘100%，vgdisplay 查看vg卷里还有多少未被分配
vmstat 2 1 第一个参数是采样时间间隔数，单位秒，第二个参数是采样的次数。2表示每个两秒采集一次服务器状态，1表示只采集一次。
vmstat 2 每2秒采集数据，一直采集，直到Ctrl+C结束程序。
lvextend -L +10G /dev/vg_local/lv_home  扩容lvm分区
resize2fs /dev/vg_local/lv_home 实际的容量大小扩容了
显示例如下面的信息：
    TIME_WAIT 814
    CLOSE_WAIT 1
    FIN_WAIT1 1
    ESTABLISHED 634
    SYN_RECV 2
    LAST_ACK 1
uptime 当前时间、系统运行了多久时间、当前登录的用户有多少，以及前 1、5 和 15 分钟系统的平均负载。
uptime -p 系统运行了多长小时和分钟
uptime -s 系统开始运行的时间
```

# 电商

## SKU（规格表）、SPU（商品表）设计

 e.g. iphone6s

SPU指商品 iphone6s，SPU属性不会影响库存和价格，1:1关系，核心字段是category_id（商品属于哪个分类，进行商品搜索）、attribute_list（json格式存储弹性字段，便于前端解析、比如{"内存":"2G","颜色":"红色","尺寸":"20cm"}）

Q：使用了弹性字段后的商品搜索怎么办？

SKU指规格的库存、价格，核心字段是product_id(SPU表中的商品id）和product_specs（单品具体的属性值）

## 优惠券、红包、代金券



## 活动



## 秒杀

（1）点评电影早期的秒杀活动页上，展示了一个用户当前秒杀资格的信息，由于不同用户抢到秒杀资格的时间、优惠不同，每次都需要读数据库的来取，也就是每个用户进入主页都会产生一条sql

## 推荐

推荐系统3个重要模块：用户建模、推荐对象、推荐算法

### 推荐方法

```css
内容推荐 Content-based Recommendation：需用户历史数据，用户模型资料随用户偏好改变。优点：不需要其他用户数据，没有冷开始和稀疏问题。

协同过滤推荐 Collaborative Filtering Recommendation：利用用户历史喜好计算用户之间距离，利用目标用户最近邻居用户对商品评价的加权评价值来预测目标用户对特定商品的喜爱程度。优点：能处理非结构化复杂对象，如音乐、电影。从用户角度推荐，用户获得的推荐是系统从购买模式或浏览行为等隐式获得，不需要用户努力地找到适合自己兴趣的推荐信息，如填写一些调查表格。

关联规则推荐 Association Rule-based Recommendation： 在零售行业成功应用，把已购商品作为规则头，规则体为推荐对象。关联规则挖掘可以发现不同商品在销售过程中的相关性，关联规则挖掘离线进行，耗时长，是算法瓶颈。管理规则就是在一个交易数据库中统计购买了商品集X的交易中有多大比例的交易同时购买了商品集Y，直观是用户在购买X有更大倾向去购买Y商品。

效用推荐 Utility-based Recommendation：建立在对用户使用项目的效用情况上计算，核心问题是怎么样为每一个用户去创建一个效用函数。好处是它能把非产品的属性，如提供商的可靠性（Vendor Reliability）和产品的可得性（Product Availability）等考虑到效用计算中。

知识推荐 Knowledge-based Recommendation：一种推理（Inference）技术，它不是建立在用户需要和偏好基础上推荐的。效用知识（Functional Knowledge）是一种关于一个项目如何满足某一特定用户的知识，因此能解释需要和推荐的关系，所以用户资料可以是任何能支持推理的知识结构，它可以是用户已经规范化的查询，也可以是一个更详细的用户需要的表示。

组合推荐 Hybrid Recommendation：
七种组合思路
(1)加权 Weight
(2)变换 Switch
(3)混合 Mixed
(4)特征组合 Feature combination
(5)层叠 Cascade
(6)特征扩充 Feature augmentation
(7)元级别 Meta-level
```

### 内容推荐VS协同过滤推荐　

```css
协同过滤推荐较少的用户反馈量，能处理非结构化复杂对象，如音乐、电影。　
内容推荐都是用户本来就熟悉的内容，而协同过滤可发现用户潜在的但自己尚未发现的兴趣偏好。
协同过滤有稀疏问题 Sparsity和可扩展问题 Scalability。
```

### 隐私

针对隐私，分客户端和服务端推荐系统，用户更愿意向客户端推荐系统提供数据，客户端推荐系统由于信息本地收集，更能构建出高质量的用户模型。

### 数据

物料数据：类型（文本、视频、图片）、类别category（新闻、娱乐、体育）、标签（宝马，奥迪，兴趣，爱好，收入...）、时效、地域

用户数据轨迹和画像：系统日志通过埋点记录用户各类行为，通过日志收集系统计算处理，将有效的用户行为数据结构化并落到存储空间中，一般用数据仓库进行管理，便于后续分析、计算。用户行为：浏览、点击、播放、点赞、评论、转发、下单，结合访问时获取到的设备、时间、地域等，加上各行为打上时间戳。

用户画像：对结构化落仓数据统计分析，结合时序，计算维度：兴趣、偏好、GPS、年龄、性别、收入，深层次聚类、分群。

喂数

引擎：倒排、召回、排序、rerank 、评估推荐系统效果、分桶实验系统

```css
实验染色流量分桶策略，切分流量需分层，同一层互斥，不同层打通，参考Google《Overlapping Experiment Infrastructure: More, Better, Faster Experimentation》

召回：物料池最终曝光给用户只有几十甚至十几条，直接所有排序场景成本高。初筛是召回用户感兴趣的一批候选集(几百到一千左右)

召回方式：
(1)兴趣类容召回  最新、最热in的数据
(2)协同过滤召回  
A.基于用户 User Collaborative Filtering UCF将跟你看过相同物料的用户，他们看过的物料推荐给你
B.基于物料 Item Collaborative Filtering ICF将你看过物料的相似物料推荐给你
用户相似度计算：Jaccard相似度、余弦相似度、皮尔逊相似度
(3)算法类召回
粗排：聚焦于通过特征和模型对全量物料排序，筛选出topN物料进入候选集 特征：在线万到千万级排序、算法模型简单、特征较少，主要使用线性模型算法LR、FM、GBDT

```



```css
Jaccard相似度可作为基础版ICF，sim(A,B) = |ra ∩ rb| / |ra ∪ rb|，ra、rb分别为两个用户产生行为的物料集，得分越高代表用户越相似
离线
(1)取所有用户对应操作行为物料：user: item1,item2,item3...
(2)全量用户计算两两用户间相似度得分
(3)对每个用户得分排序，获取到最高的topN用户
(4)获取topN用户的历史行为item并与目标用户的item做去重
(5)将去重后的item存入以目标用户为key的redis中，userid:"item1,item2,item3...."
在线
(1)获取用户id，读redis拿物料召回
```

报表：AB实验效果、分标签、召回

大数据杀熟

Lucence倒排原理

Elasticsearch倒排原理

Lucence VS Elasticsearch VS Solr

Elasticsearch是一个Push replication，完全支持Lucence接近实时搜索，支持全文搜索，仅支持JSON格式。

Solr是Java编写、运行在Servlet容器（如 Apache Tomcat 或Jetty）。当实时建立索引时， Solr会产生IO阻塞，查询性能变差， Elasticsearch具有优势。数据量增加时，Solr搜索效率会变得更低，而Elasticsearch却没有明显变化。Solr不适合实时搜索，适合传统应用，依赖Zookeeper，而Elasticsearch自带分布式协调管理功能。

基于Lucence，索引存 Cassandra VS HBase，Lucence terms 是存成行，但每个 term 对应的 posting lists 是列存储。随着单个 term 的 posting lists 增大，查询速度受到的影响非常大。

Lucence没有使用B树，二分查找快速定位关键词，索引结构三列：词典term，频率frequencies，位置positions







# 区块链

上链：私钥池分配私钥对(用户注册时绑定)、nonce+1、创建资产、上链提交事务、js编写合约代码、查询资产、上联数据模型(bean SM3、SHA)，上链算法一般两种RSA、SHA

区块链没并发、排队系统、项目规模不会大

# 架构

业务架构 + 基础设施架构

软件架构设计：大型网站技术架构与业务架构融合之道

# 心得

围绕场景、围绕业务、讨论目标和为什么、相信愿景、倾听需求、沟通、整理、谦卑、好学








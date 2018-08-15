---
title: linuxPthreadAPI
comments: false
date: 2018-04-09 09:56:11
tags:
categories: LinuxAPI
---

pthread的相关函数有以下几个：

1、prctl()函数：其中的一个用途，是为线程指定名字；
   [参考链接-1](https://blog.csdn.net/tmxkwzy/article/details/51919499)
   [参考链接-2](https://blog.csdn.net/jasonchen_gbd/article/details/51308638)


2、int pthread_setspecific(pthread_key_t key, const void *value);
   void *pthread_getspecific(pthread_key_t key);
   函数 pthread_key_create() 用来创建线程私有数据;

   [参考链接-1](https://blog.csdn.net/cywosp/article/details/26469435)
   [参考链接-2](https://blog.csdn.net/mengxingyuanlove/article/details/50820386)


3、pthread_join()和pthread_detach()的区别
   linux的pthread有两种状态joinable状态和unjoinable状态。
   默认线程是joinable状态，当线程函数自己返回退出时或pthread_exit时都不会释放线程所占用堆栈和线程描述符（总计8K多）。
   只有当你调用了pthread_join之后这些资源才会被释放。
   unjoinable属性可以在pthread_create时指定，或在线程创建后在线程中pthread_detach自己。

   但是pthread_join(pthread_id)函数是阻塞函数，在调用pthread_join(pthread_id)后，如果该线程没有运行结束，调用者会被阻塞。
   在有些情况下我们并不希望如此，
   比如在Web服务器中当主线程为每个新来的链接创建一个子线程进行处理的时候，
   主线程并不希望因为调用pthread_join而阻塞（因为还要继续处理之后到来的链接），
   这时可以在子线程中加入代码：
       pthread_detach(pthread_self())
   或者父线程调用：
       pthread_detach(thread_id)（非阻塞，可立即返回）
   这将该子线程的状态设置为detached,则该线程运行结束后会自动释放所有资源。

4、线程池
   基本思路，起几个线程，死循环不退出(比如用一个boolean变量控制)，
             将等待被执行函数写在一个queue中。
	     线程中用函数指针的方式，将从queue中pop出的函数执行。
	     反复循环，降低了线程创建和销毁的时间。
   [参考链接](https://www.cnblogs.com/venow/archive/2012/11/22/2779667.html#3974204)

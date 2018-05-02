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


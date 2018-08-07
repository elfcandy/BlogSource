---
title: linux HeadFile
comments: false
date: 2018-04-24 11:34:22
tags:
categories: linux head file
---

1、linux的系统头文件所在位置：
   echo 'main(){}'|gcc -E -v -

2、stdint.h 说明：
   [参考连接](https://blog.csdn.net/yucan1001/article/details/7470905)

3、libcstl介绍：
   libcstl是一个应用于C语言编程的函数库，它将编程过程中经常使用的数据结构如向量、链表、集合、树等封装成相应的数据结构并提供一系列的操作函数来操作保存在这些数据结构中的数据，同时它还将常用的算法如排序、查找、划分等封装成相应的算法函数并提供迭代器来使两者之间建立联系方便使用。从libcstl的名字就可以看出它于STL有一定的关系，是的libcstl的接口和实现都是模仿了STL。
   [参考链接](https://blog.csdn.net/swgsunhj/article/details/38553747)

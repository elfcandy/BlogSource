---
title: gdbCommand
comments: false
date: 2018-04-19 15:15:34
tags:
categories: GDBCommand
---


1、和Thread相关的命令
   i threads ---- 列出所有的thread线程号
   thread 2  ---- 切换到线程2
   bt        ---- 查看这个线程对应的调用栈
   l(L) func ---- 在gdb中打印出某个function的codes
   p mutex_1 ---- 查看该锁的状态



2、gdb在断点下批处理命令：
   A> set 断点
   B> commands 断点号
   	       进入之后，顺序输入需要执行的命令,
	  exp: p val_1
	       bt
	       ......
               end退出


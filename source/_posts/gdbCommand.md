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



3、gdb中将需要的调试信息输出到文件（这种方式将gdb本身的info输出）
   (gdb) set logging file <文件名>
   (gdb) set logging on
   (gdb) thread apply all bt
   (gdb) set logging off
   (gdb) quit

详细说明：
   1、(gdb) set logging file <文件名>
      设置输出的文件名称
   2、(gdb) set logging on
      输入这个命令后，此后的调试信息将输出到指定文件
   3、(gdb) thread apply all bt
      打印所有线程栈信息
   4、(gdb) set logging off
      输入这个命令，关闭到指定文件的输出

   如果需要记录printf的输出数据，exp：r > file.txt



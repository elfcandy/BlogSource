---
title: linuxCommand
comments: false
date: 2018-04-19 15:02:04
tags:
categories: LinuxCommand
---


1、man
    man命令可以在线的显示出所有Linux所支持的API函数的详细说明。
    因此，有句话叫做，有问题找男人：）（man）
    exp：
    	man open/man 2 open
	man man
	man fread

    配合关键词搜索命令apropos，可以根据关键词搜索相应API， exp：
        1、apropos timer；
	2、将上面搜出的函数，使用man查看函数的具体说明；


2、ldd：列出动态库依赖关系。
        通过这命令可以检查程序使用的so库是否都已链接上。
	链接so库的动作在makefile文件链接时完成。
   [参考链接](https://blog.csdn.net/stpeace/article/details/47069215)


3、ulimit：主要是用来限制进程对资源的使用情况的，它支持各种类型的限制。
      -a 显示当前系统所有的limit资源信息。
      -c 最大的core文件的大小，以 blocks 为单位；
      Linux下产生CoreDump，需要通过ulimit命令检查core文件的设置；

   [参考链接](https://blog.csdn.net/yuyunliuhen/article/details/41673599)
   [参考链接](https://www.cnblogs.com/kongzhongqijing/p/5784293.html)


4、linux下使用memleak工具来检查内存泄露
   valgrind工具也可以


5、关闭进程命令
   ps -ef| grep "进程名称"
   kill -9 PID

   exp:
   以下这条命令是检查java 进程是否存在：ps -ef |grep java
   字段含义如下：
   UID       PID       PPID      C     STIME    TTY       TIME         CMD
   zzw      14124     13991      0     00:38    pts/0     00:00:00     grep --color=auto dae
 
   PPID 是父进程PID
   -----------

   U<用户名称>：列出属于该用户的程序的状况
   EXP: ps -U $USER

<!--more-->

6、几个统计磁盘空间的命令

   module load ncdu
   ncdu --exclude=.snapshot

   du --max-depth=1 ~/xxx/ 只计算当前目录下的文件值

   quota -s 磁盘配额命令，第一项带“**”说明user的配额已满


7、mount
   mount命令用于加载文件系统到指定的加载点
   EXP: mount -t auto /dev/cdrom /mnt/cdrom //将cdrom设备挂载到mnt/cdrom文件夹下
   ll /mnt/cdrom                            //通过mnt/cdrom目录访问光驱内容




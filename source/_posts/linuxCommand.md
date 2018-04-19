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


2、linux下使用memleak工具来检查内存泄露



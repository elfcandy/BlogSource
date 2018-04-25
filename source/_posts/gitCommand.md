---
title: gitCommand
comments: false
date: 2018-04-19 18:21:33
tags:
categories: gitCommand
---



1、git log

   git log -- filename >> 查看某个文件的所有改动的commit

2、查看某个文件的某行代码的最后一次修改记录：

   A> 找到需要查看的代码的最后一次修改的Commit：
   	git blame -L<开始行号>,+<查看的行数> path/file
   B> 显示和上一次修改的差别：
   	git show CommitID path/file


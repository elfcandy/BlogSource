---
title: VIMEditor
comments: false
date: 2018-04-23 10:42:42
tags:
categories: VIM Editor
---



1、VIM下自动补全变量名或函数名：ctrl + N/P；

2、VIM下将自定义的变量类型高亮的方法：

   vim下定义C语言语法的位置在：/usr/share/vim/vim74/syntax

   可以在自己的home目录下，创建文件夹和文件：~/.vim/syntax/c.vim；
   在该c.vim文件中增加：
   syn keyword cType u8 u16 u32 s8 s16 s32 bool_t
   (增加一个自定义变量，就在后面追加即可)

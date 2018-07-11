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
   注意：直接在~/.vimrc文件中增加“syn ...”这句话，不可以;


3、VIM下的替换操作：
a> 文件内全部替换：
:%s#abc#def#g（用def替换文件中所有的abc）

EXP：例如把一个文本文件里面的“linuxidc.com”全部替换成“linuxidc.net”：
     :%s#linuxidc.com#xwen.net#g (如文件内有#，可用/替换,比如:%s/linuxidc.com/xwen.net/g)

b> 文件内局部替换：
把10行到50行内的“abc”全部替换成“def”
:10,50s#abc#def#g（如文件内有#，可用/替换,:%s/abc/def/g）

以上命令如果在g后面再加上c，则会在替换之前显示提示符给用户确认（conform）是否需要替换。 比如
:%s#linuxidc.com#linuxidc.net#gc


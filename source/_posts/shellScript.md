---
title: shellScript
comments: false
date: 2018-07-12 15:22:30
tags:
categories: ShellScript
---


Shell 知识点汇总：

1> Shell脚本的第一句话，是注释，用于说明Bash的类型
                EXP：#!/bin/bash/

2> Shell中的特殊变量总结:

Shell特殊变量：Shell $0, $#, $*, $@, $?, $$和命令行参数

特殊变量列表:

变量    含义
$0      当前脚本的文件名
$n      传递给脚本或函数的参数。n 是一个数字，表示第几个参数。例如，第一个参数是$1，第二个参数是$2。
$#      传递给脚本或函数的参数个数。
$*      传递给脚本或函数的所有参数。
$@      传递给脚本或函数的所有参数。被双引号(" ")包含时，与 $* 稍有不同，下面将会讲到。
$?      上个命令的退出状态，或函数的返回值。一般情况下，大部分命令执行成功会返回 0，失败返回 1。
$$      当前Shell进程ID。对于 Shell 脚本，就是这些脚本所在的进程ID。

$* 和 $@ 的区别:
$* 和 $@ 都表示传递给函数或脚本的所有参数，不被双引号(" ")包含时，都以"$1" "$2" … "$n" 的形式输出所有参数。但是当它们被双引号(" ")包含时，"$*" 会将所有的参数作为一个整体，以"$1 $2 … $n"的形式输出所有参数；"$@" 会将各个参数分开，以"$1" "$2" … "$n" 的形式输出所有参数。

[参考连接](http://blog.csdn.net/u011341352/article/details/53215180)


3> Shell中的结构化命令:
   <1> if-then语句，若command的退出码为0（该命令成功运行）：
       基本命令：
           if command
           then
                   commands
           fi
       把then放到句尾，command后面带分号：
           if command; then
                   commands
           fi
       command可以使用双圆括号"(( ))"，双圆括号中可以使用高级数据表达式
       command可以使用双方括号"[[ ]]"，双方括号中提供了字符串比较的高级特性，模式匹配（bash shell支持，其余的shell不确定）

   <2> test命令，若test命令中列出的条件成立，test命令就会退出并返回推出状态码0，分为三类：
       a> 数值比较；
       b> 字符串比较；
       c> 文件比较；

   <3> for命令：
       for var in list
       do
            commands
       done
       把do放到句尾，list后面带分号：
       if var in list; do
            commands
       done
       变量var包含当前列表中的当前值，list中提供迭代要用到的一系列值。




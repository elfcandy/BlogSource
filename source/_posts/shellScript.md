---
title: shellScript
comments: false
date: 2018-07-12 15:22:30
tags:
categories: ShellScript
---


Shell 知识点汇总：

1> Shell脚本的第一句话，是注释，被称为释伴(shebang)行，用于说明Bash的类型
   EXP：#!/bin/bash/


2> 默认登陆shell
   /bin/bash是默认登陆shell，在创建用户时分配；使用chsh命令可以改变默认的shell。
   chsh <用户名> -s <新shell>
   EXP：chsh username -s /bin/sh


3> 在Shell脚本中，可以使用系统定义环境变量，和用户定义环境变量；
   系统环境变量，通过“set”命令查看；
   用户环境变量。通过“echo $变量名”命令查看；
   “unset”可以取消变量或变量赋值；


4> 使用“2>&1”或者“&>”将标准输出和错误输出同时重定向同一个位置
   EXP：
   #ls /usr/share/doc > out.txt 2 >& 1
   #ls /usr/share/doc &> out.txt


5> Shell中的特殊变量总结:

Shell特殊变量：Shell $0, $#, $*, $@, $?, $$和命令行参数

特殊变量列表:
变量    含义
$0      当前脚本的文件名
$n      传递给脚本或函数的参数(n: 1..2...)。n 是一个数字，表示第几个参数。例如，第一个参数是$1，第二个参数是$2。
$#      传递给脚本或函数的参数个数。
$*      传递给脚本或函数的所有参数。
$@      传递给脚本或函数的所有参数。被双引号(" ")包含时，与 $* 稍有不同，下面将会讲到。
$?      上个命令的退出状态，或函数的返回值。一般情况下，大部分命令执行成功会返回 0，失败返回 1。
$$      当前Shell进程ID。对于 Shell 脚本，就是这些脚本所在的进程ID。

$* 和 $@ 的区别:
$* 和 $@ 都表示传递给函数或脚本的所有参数，不被双引号(" ")包含时，都以"$1" "$2" … "$n" 的形式输出所有参数。但是当它们被双引号(" ")包含时，"$*" 会将所有的参数作为一个整体，以"$1 $2 … $n"的形式输出所有参数；"$@" 会将各个参数分开，以"$1" "$2" … "$n" 的形式输出所有参数。

[参考连接](http://blog.csdn.net/u011341352/article/details/53215180)


6> Shell中的结构化命令:
   <1> if-then语句，若command的退出码为0（该命令成功运行）：
       基本命令：
           if 条件condition
           then
                   commands
           else
	           commands
           fi
       把then放到句尾，command后面带分号：
           if 条件condition; then
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


7> 在if-then中使用测试命令“-gt”等来比较两个数字；
   EXP：if [$x -gt $y]
   test命令可以用来比较字符串；


8> 使用-x或-nv调试shell脚本
   EXP：
   #sh -x  myscript.sh
   #sh -nv myscript.sh


9> shell执行算术运算
   有两种方法：
   1) expr命令 (# expr 5+2)
   2) $\[表达式\] (test=$[16+4])


10> Test命令用于测试文件
   > test -d 文件名：如果目录存(文件名为目录)，返回true；
   > test -e 文件名：如果文件存在，返回true；
   > test -f 文件名：如果文件存在并且是普通文件，返回true；
   > test -r 文件名：如果文件存在并且可读，返回true；
   > test -w 文件名：如果文件存在并且可写，返回true；
   > test -x 文件名：如果文件存在并且可执行，返回true；
   > test -s 文件名：如果文件存在并且不为空，返回true；


11> read命令可以使shell脚本得到来自终端的输入
   EXP：
   #cat test.sh
   #!/bin/bash
   echo 'Please enter your name'
   read name
   echo "The name is $name"
   #./test.sh
   Please enter your name
   Bob
   The name is Bob


12> shell中基本函数的定义，两种：
   1) function关键字 + 函数名
      function name {
         commands
      }
   2) 函数名+空括号
      name() {
         commands
      }
   3) 调用方式：使用函数名即可


13> 一种在一个脚本同时在bash和csh上运行的方法(sed分支和预测，shell的内建和外部命令)：
   1) 第一种实现方式：
      $(echo "$SHELL" | sed '{
      s/\/bin\/bash/export/
      t
      s/\/bin\/tcsh/setenv/
      }') LD\_LIBRARY\_PATH=$PWD/third-party/Tcl/x86\_64/lib/:$LD\_LIBRARY\_PATH

   2) 第二种实现方式：
      echo $SHELL | sed 's/\/bin\/bash/export LD_LIBRARY_PATH=$PWD\/third-party\/:$LD_LIBRARY_PATH/;t;s/\/bin\/tcsh/setenv LD_LIBRARY_PATH $PWD\/third-party\/:$LD_LIBRARY_PATH/'>tmp.sh

   3) 第三种实现方式：
      `echo $SHELL | sed 's/\/bin\/bash/export LD_LIBRARY_PATH=$PWD\/third-party\/:$LD_LIBRARY_PATH/;t;s/\/bin\/tcsh/ls -al/'`
      这种方式下，setenv命令不能正常执行，ls命令可以。




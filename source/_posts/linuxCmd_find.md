---
title: linuxCommand -- find
comments: false
date: 2018-04-23 10:42:42
tags:
categories: LinuxCommand
---



1、which命令是在PATH变量指定的路径中搜索指定的系统命令的位置；

2、whereis命令只能用于搜索二进制文件(-b)、源代码文件(-s)、说明文件(-m)。如果省略参数则返回所有的信息；

3、find是最常用也是最强大的查找命令，它可以查找任何类型的文件。

   find命令的一般格式为：find <指定目录><指定条件><指定动作>，即find pathname -options [-print -exec -ok]

   EXP: find <路径> <选项> <文件名>

参数解释：

pathname：pathname为搜索的目录及其子目录，默认情况下为当前目录

常用的option选项：

   -name：按文件名来查找文件
   -iname: 不区分大小写

   -user：按照文件的属主来查找文件

   -group：按照文件所属的组来查找文件

   -perm：按照文件权限来查找文件

   -prune：不在当前指定目录中查找

4、locate命令实际是"find -name"的另一种写法，但是查找方式跟find不同，它比find快得多。

   因为它不搜索具体目录，而是在一个数据库(/var/lib/locatedb)中搜索指定的文件。

   此数据库含有本地文件的所有信息，此数据库是linux系统自动创建的，数据库由updatedb程序来更新，

   updatedb是由cron daemon周期性建立的，默认情况下为每天更新一次，所以用locate命令你搜索不到最新更新的文件，
   
   除非你在用locate命令查找文件之前手动的用updatedb命令更新数据库。




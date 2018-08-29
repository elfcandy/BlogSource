---
title: gdbCommand
comments: false
date: 2018-04-19 15:15:34
tags:
categories: GDBCommand
---

[参考链接](https://blog.csdn.net/yuyunliuhen/article/details/41673599)


1、gdb启动时，相当于启动一个新的shell，会再次加载~目录下.bashrc/.cshrc.user文件；
   [参考链接](http://blog.sina.com.cn/s/blog_80ce3a550101m3l5.html)
   之前遇到的问题便由此造成，需要将所有的设置均写入.bashrc/.cshrc.user文件中，以确保terminal和gdb的运行环境一致；


2、gdb中attach的方法
   1> 执行“ps -ef | grep 进程名”获取当前进程的PID(第二个字段)；
   2> 启动gdb；
   3> 在gdb命令行中，执行“attach PID”；


3、和Thread相关的命令
   > i threads ---- 列出所有的thread线程号
   > thread 2  ---- 切换到线程2
   > bt        ---- 查看这个线程对应的调用栈
   > l(L) func ---- 在gdb中打印出某个function的codes
   > p mutex\_1 ---- 查看该锁的状态


4、gdb在断点下批处理命令：
   A> set 断点
   B> commands 断点号
   	       进入之后，顺序输入需要执行的命令,
	  exp: p val_1
	       bt
	       ......
               end退出


5、gdb中将需要的调试信息输出到文件（这种方式将gdb本身的info输出）
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


6、判断一个binary文件是否可以debug方法：
   objdump -t your-binary | grep debug
   如果可以debug，则会显示debug相关的一些信息，否则没有相关信息。


7、gdb中设置环境变量：
   > set  env LD\_LIBRARY\_PATH
   > show ENV LD\_LIBRARY\_PATH
   > show environment


8、solib-absolute-prefix和solib-search-path
   solib-absolute-prefix设置的是被搜索文件路径的前缀，solib-absolute-prefix的值只能有一个；
   solib-search-path设置的是被搜索文件的路径，solib-search-path可以有多个路径，中间按用:隔开；
   EXP：
   (gdb) info sharedlibrary                    //gdb下查看shared library方法
   (gdb) set solib-search-path .               //假设当前目录下有文件libshared.so, 可以执行下面的命令：
   (gdb) set solib-absolute-prefix /media/DATA //假设文件libc.so.6在/media/DATA/lib/libc.so.6下，gdb用前缀/media/DATA + /lib/libc.so.6,就找到了文件


9、临时改变变量的值：set i=3


10、查看类的结构：ptype node


11、打印其他格式的值：
    p/x i    //打印hex
    p/c i    //打印字符
    p/s i    //打印字符串
    p/f i    //打印float


12、查看当前stack中的变量：info local


13、保存已设置的断点
    > 在gdb中，可以使用如下命令将设置的断点保存下来：
    > (gdb) save breakpoints save-file-name

    > 下次调试时，可以使用如下命令批量设置保存的断点：
    > (gdb) source save-file-name

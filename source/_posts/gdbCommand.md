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
    p/u i    //打印16进制无符号
    p/d i    //打印十进制
    p/t i    //打印二进制
    p/c i    //打印字符
    p/s i    //打印字符串
    p/f i    //打印float


12、查看当前stack中的变量：info local


13、保存已设置的断点
    > 在gdb中，可以使用如下命令将设置的断点保存下来：
    > (gdb) save breakpoints save-file-name

    > 下次调试时，可以使用如下命令批量设置保存的断点：
    > (gdb) source save-file-name

14、设置基于循环次数的断点
    > set $cnt=0
    > b xxx.c:123 if ++$cnt==20

15、gdb启动
    > gdb xxx.exe
    > gdb
      file xxx.exe --> for location dbg
      load xxx.exe --> for remote dbg

17、run的方法
    > run parameter1 parameter2 ...
    > set args parameter1 parameter2 ...
      show args
      run

18、ignore 断点编号 忽略次数

19、catch event
    当事件event发生的时候，程序停止运行；
    catch event只设置一次捕捉点，当程序停住以后，被自动删除；
    event列表：
             throw  C++抛出异常
             catch  C++捕捉到异常
              exec  exec被调用
              fork  fork被调用
             vfork  vfork被调用
      load libname  加载名为libname库(HP-UX可用)
    unload libname  卸载名为libname库(HP-UX可用)

20、print
    > pt 按结构体格式打印结构体值
    > 打印数组值：
      p/t *array@30      :按二进制打印array的前30个数
      p/t *(array+10)@30 :按二进制打印从array第10个数起的30个数

21、examine查看内存
    命令格式: x/[option] addr
              option: n，表示内存的长度。
                      f，表示显示个格式(可以参照之前格式化输出部分)
	              u，默认是4个字节；也可以是b 单字节，h 双字节，w四字节，g 八字节
              addr：内存地址，也是即将要取值的起始地址。
    默认x addr

22、函数访问
    > 调用
      call和print可以调用被测程序中的函数
      exp：call tempFunc(2，2)
    > 返回
      finish：连续运行当前函数直到返回为止，然后停下来等待命令。
      return：使用return命令取消当前函数的执行，并立即返回

23、堆栈
    > frame args
      移动到args指定的栈帧中去，并打印选中的栈的信息。args可以时帧编号或者时帧的地址。如果没有args，则打印当前帧的信息;
    > select-frame args
      移动到指定的帧中去，不打印信息;
    > frame 打印当前栈帧的简要信息。
    > 在栈帧之间切换，up n或者down n，n默认为1；

24、gdb中加载脚本
    > 在启动gdb的时候，会在当前目录下查找“.gdbinit”这个文件，并把它的内容作为gdb命令行解释，所以我们可以把脚本命名为“.gdbinit”，这样在启动的时候就会处理这些命令；
    > gdb运行期间，可以使用source script-file来解释gdb命令脚本；


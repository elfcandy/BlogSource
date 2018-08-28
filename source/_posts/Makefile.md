---
title: makefile
comments: false
date: 2018-08-10 16:14:37
tags:
categories: Makefile
---

[参考链接 1](https://blog.csdn.net/ruglcc/article/details/7814546/)
[参考链接 2](https://blog.csdn.net/stpeace/article/details/53054006)


1、Makefie >& log.txt 保存输出信息


2、make -p 列出所有的Makefile内置变量的当前值。
   注意：该命令会先执行make。然后再执行-p输出当前Makefile的所有内置变量的值。


3、3个内置函数说明：
   A> wildcard : 扩展通配符
   B> notdir   ：去除路径
   C> patsubst ：替换通配符

   EXP：在test下，建立a.c和b.c2个文件，在sub目录下，建立sa.c和sb.c2 个文件，
        建立一个简单的Makefile
           src=$(wildcard *.c ./sub/*.c)
           dir=$(notdir $(src))
           obj=$(patsubst %.c,%.o,$(dir) )

           all:
              @echo $(src)
              @echo $(dir)
              @echo $(obj)

	执行结果分析：
              第一行输出：a.c b.c ./sub/sa.c ./sub/sb.c。wildcard把 指定目录 ./ 和 ./sub/ 下的所有后缀是c的文件全部展开。
              第二行输出：a.c b.c sa.c sb.c。notdir把展开的文件去除掉路径信息
              第三行输出：a.o b.o sa.o sb.o。patsubst把$(dir)中的变量符合后缀是.c的全部替换成.o，或者使用obj=$(dir:%.c=%.o)效果也是一样的。


4、makefile里的替换引用规则，即用您指定的变量替换另一个变量，格式是：
   $(var:a=b) 或 ${var:a=b}
   它的含义是把变量var中的每一个值结尾用b替换掉a。


5、内置变量$(MAKE) 就是预设的 make，用于make这个命令的名称(或者路径)
   通过make -p可以查到 MAKE = $(MAKE\_COMMAND), 而MAKE\_COMMAND := make


6、makefile的自动推导
   makefile可以自动推导文件以及文件依赖关系后面的命令，于是我们就没必要去在每一个[.o]文件后都写上类似的命令，
   因为，我们的make会自动识别，并自己推导命令。

   只要make看到一个[.o]文件，它就会自动的把[.c]文件加在依赖关系中。
   如果make找到一个whatever.o，那么whatever.c，就会是whatever.o的依赖文件。并且 cc -c whatever.c 也会被推导出来。


7、CFLAGS是makefile中的隐式规则里会用到的常见预定义变量，是C编译器的选项。
   注意是隐式规则！！编译时会自动加上，相当于：
   gcc -c a.c -o a.o，相当于
   gcc $(CFLAGS) -c a.c -o a.o


8、MakeFile常见预定义变量
   AR：库文件维护程序的名称，默认值为ar
   AS：汇编程序的名称，默认值为as
   CC：C编译器名称，默认值为cc
   CPP：C预编译器的名称，默认值为$(CC) -E
   CXX: C++编译器名称，默认值为g++
   RM：文件删除程序的名称，默认值为rm -f
   ARFLAGS：库文件维护程序的选项，无默认值
   ASFLAGS：汇编程序的选项，无默认值
   CFLAGS：C编译器的选项，无默认值
   CPPFLAGS：C预编译器的选项，无默认值
   CXXFLAGS：C++编译器的选项，无默认值


9、在Makefile文件中打印字符串的方法
   > 有两类命令可以打印字符串：
     >> 第一类：
     >>> $(info $(TARGET_DEVICE))
     >>> $(warning "here add the debug info")
     >>> $(error "error: this will stop the compile") //error会停止当前makefile的编译

     >> 第二类：
     >>> @echo "The compiler name is \"${Name}\";"
     >>> @echo $(Name)
   > 以上命两类命令的前面需要有TAB键；
   > 第二类命令需要放置在“目标:依赖”下，才能被执行；第一类不需要；

10、@放在行首，通常用在“规则”行中，表示不显示命令本身，而只显示它的结果；

11、$@、$^、$<三个符号的含义：
   > $@：代表目标文件(target)
   > $^：代表所有的依赖文件(components)
   > $<：代表第一个依赖文件(components中最左边的那个)

   makefile的基本规则为：
       目标:依赖

12、产生镜像文件
   基本的实现方法是：注意Wl逗号后面跟着需要传递的参数，逗号后面不能存在空格，否则出现错误。
   gcc -Wl,-Map=file.map file.c -o target

---
title: gccCompilerLinker
comments: false
date: 2018-08-24 11:17:02
tags:
categories: gccCompilerLinker
---

GCC工具链包括GCC、Binutils、C运行库等。

1、BinUtils一组二进制程序处理工具，包括：addr2line、ar、objcopy、objdump、as、ld、ldd、readelf、size等命令。
   > addr2line：用来将程序地址转换成其所对应的程序源文件及所对应的代码行，也可以得到所对应的函数；
                该工具将帮助调试器在调试的过程中定位对应的源代码位置；
   > as：主要用于汇编；
   > ld：主要用于链接；
   > ar：主要用于创建静态库。linux静态库.a为后缀，动态库.so为后缀；windows静态库.lib为后缀，动态库.dll为后缀；
   > ldd：用于查看一个可执行程序所依赖的共享库；
   > objcopy：将一种对象文件翻译成另一种格式，例如将.bin转换成.elf，或者将.elf转换成.bin;
   > objdump：主要用于反汇编；
   > readelf：显示有关elf文件的信息；
   > size：列出可执行文件每个部分的尺寸和总尺寸，代码段，数据段，总大小等；

2、C运行库
   C语言标准主要有两部分组成：1)描述C语言的语法；2)描述C语言的标准库；
   其中，C标准库定义了一组标准头文件，但是C语言标准仅仅定义了C标准库函数原型，并没有提供实现。因此，C语言编
   译器通常需要一个C运行时库(C Run Time Library, CRT，又称为C运行库)的支持。同时，C++也有自己的运行时库。

3、编译过程
   1> 预处理
      GCC的-E选项使gcc在执行完预处理后停止；
      EXP：gcc -E hello.c -o hello.i

   2> 编译
      GCC的-S选项使gcc在执行完编译后停止，生成汇编代码；
      EXP：gcc -S hello.i -o hello.s

   3> 汇编
      对汇编代码处理，生成处理器可以识别的指令，保存在.o后缀的目标文件中；
      通过调用Binutils中的汇编器as，根据汇编指令和处理器指令的对照表一一翻译即可；
      使用gcc的-c选项，或者Binutils中的as，将hello.s文件汇编生成目标文件hello.o；
      EXP 1：gcc -c hello.s -o hello.o
      EXP 2：as -c hello.s -o hello.o
      注意：hello.o目标文件为ELF(Executable and Linkable Format)格式的可重定向文件。

   4> 链接
      可分为静态链接和动态链接。
      在Linux系统中，
      > gcc编译链接时的动态链接库搜索路径的顺序为：先从gcc -L指定的路径寻找；再从环境变量
        LIBRARY_PATH指定的路径寻找；再从默认路径/lib、/usr/lib、/usr/local/lib寻找；
      > 执行二进制文件时的动态库搜索路径的顺序为：先从编译目标代码时，指定的动态库路径寻找；
        再从环境变量LD_LIBRARY_PATH指定的路径寻找；再从配置文件/etc/ld.so.conf中指定的动态
	库路径中寻找；再从默认路径/lib、/usr/lib寻找；
      > ldd命令可以查看一个可执行程序所依赖的共享库；
      > 如果在同一个路径中存在同名的静态库文件和动态库文件，例如libtest.a和libtest.so，gcc
        默认优先选择动态库；若要让gcc选择链接libtest.a，可以通过指定gcc -static选项，强制使
	用静态库进行链接；

4、ELF文件分析
   1> elf文件包含的段：.text/
                       .rodata/
                       .data(已初始化的全局和静态变量)/
		       .bss(未初始化的全局和静态变量)/
		       .debug(调试符号表)
      readelf -S 可查看其各个section的信息
   2> 反汇编ELF
      objdump -D：可以对elf文件进行反汇编；
      objdump -S：可以对elf文件进行反汇编，并且将其C语言源代码混合显示出来；

5、查看一个elf文件所用的gcc版本的几种方式
   > # readelf -wi a.out | grep GNU (优先选项，最为准确)

   > # strings -a a.out | grep gcc(大写GCC结果不同)
   > # readelf -p .comment a.out
   > # objdump -s --section .comment a.out
   [参考链接](https://stackoverflow.com/questions/2387040/how-to-retrieve-the-gcc-version-used-to-compile-a-given-elf-executable)
   根据该链接描述，只能显示elf文件的运行时gcc版本号，而不能显示编译时的gcc版本号；


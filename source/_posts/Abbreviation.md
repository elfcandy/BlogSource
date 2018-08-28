---
title: Abbreviation
comments: false
date: 2018-08-15 19:02:08
tags:
categories: Abbreviation
---

1、SMP：(Symmetrical Multi-Processing) 对称多处理器

2、SMT：(Simultaneous multi threading) 同时多线程

3、CMP：(Chip multi processors) 片上多处理器

4、VLIW：(Very Long Instruction Word) 超长指令字

5、SIMD：(Single Instruction Multiple) Data 单指令多数据流

6、服务器CPU的基本描述：

    > socket就是主板上插cpu的槽的数目，也即管理员说的“路”，插槽就是scoket
      查看“插槽”数可以通过如下命令来完成：lscpu | grep "CPU socket"

    > core就是我们平时说的”核“，即双核，4核等

    > thread就是每个core的硬件线程数，即超线程

    举例说明：
        某个服务器是：2路4核超线程(一般默认为2个线程)，
        那么，通过cat /proc/cpuinfo看到的是2\*4\*2=16个processor，很多人也习惯成为16核了。

    LPAR是指逻辑分区(Logical Partition)，就是将单台服务器划分成多个逻辑服务器，彼此运行独立的应用程序。
    逻辑分区不同于物理分区(Physical Partitioning PPAR)，物理分区是将物理的将资源组合形成分区，
    而逻辑分区则不需要考虑物理资源的界限。

    UNIX服务器可支持最多256个CPU的系统。
    [参考链接](https://blog.csdn.net/ustc_dylan/article/details/8817756)

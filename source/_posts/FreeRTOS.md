---
title: FreeRTOS
comments: false
date: 2018-07-11 14:03:02
tags:
categories: FreeRTOS
---

FreeRTOS 是一个相对其他操作系統而言较小的操作系統。最小化的 FreeRTOS 核心仅包括 3 个 .c 文件(tasks.c、queue.c、list.c)和少数头文件，总共不到 9000 行代码，还包括了注释和空行。一个典型的编译后的 binary（二进制码）小于 10 KB。

FreeRTOS 的代码可以分为三个主要模块：任务、通讯和硬件界面。

FreeRTOS资料型态及命名规则
在不同硬件装置上，通讯端口设定上也不同，定义在portmacro.h头文件內，有两种特殊资料型态portTickType以及portBASE_TYPE。

资料型态
portTickType : 用以储存tick的计数值，可以用来判断block次数
portBASE_TYPE : 定义为架构基础的变量，随各不同硬件来应用，如在32-bit架构上，其为32-bit型态，最常用以存储极限值或布尔数。
FreeRTOS明确的定义变量以及资料型态，不会有unsigned以及signed混合使用的情形发生。

变量
char 类型：以 c 为字首
short 类型：以 s 为字首
long 类型：以 l 为字首
float 类型：以 f 为字首
double 类型：以 d 为字首
Enum 类型：以 e 为字首
portBASE_TYPE 或其他（如 struct）：以 x 为字首
pointer 有一个额外的字首 p , 例如 short 类型的 pointer 字首为 ps
unsigned 类型的变量有一个额外的字首 u , 例如 unsigned short 类型的变量字首为 us

函数：以返回值型态与所在文件名称为开头(prefix)
vTaskPriority() 是 task.c 中返回值为 void 的函数
xQueueReceive() 是 queue.c 中返回值为 portBASE_TYPE 的函数
只能在该文件中使用的 (scope is limited in file) 函数，以 prv 为开头 (private)

宏定义名称：宏定义在FreeRTOS里全部为大写字母定义，名称前小写字母为宏定义所在的文件名称
portMAX_DELAY : portable.h
configUSE_PREEMPTION : FreeRTOSConfig.h

一般宏定义返回值pdTRUE 及 pdPASS为1 , pdFALSE 及 pdFAIL 为0。


[参考链接:](http://wiki.csie.ncku.edu.tw/embedded/freertos#FreeRTOS%20%E6%9E%B6%E6%A7%8B)

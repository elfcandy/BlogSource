---
title: Python
comments: false
date: 2018-07-18 14:18:24
tags:
categories: Python
---

1> Python调试方法：

   启动：python -m pdb filename.py [argument1...，argument2...]
   (pdb)下：
     help 显示所有pdb调试命令
     断点相关：
	   b  ([file:]lineno | function) [, condition]
              根据行号或文件名插入断点
	   b  后无参数，显示所有断点
	   cl breakpointNum  删除指定断点；
     bt:
           显示当前的函数调用栈顺序；
     quit/exit:
           退出当前调试过程；


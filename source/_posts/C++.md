---
title: C++
comments: false
date: 2018-09-10 14:40:52
tags:
categories: C++
---

[C++教程 1](http://c.biancheng.net/cplus/)
[C++教程 2](http://www.runoob.com/cplusplus/cpp-tutorial.html)



1、reinterpret\_cast是C++里的强制类型转换符。

2、namespace命名空间：
   命名空间定义：
   namespace XXX {
       只要能出现在全局作用域中的声明就能置于命名空间内，
       主要包括：类、变量(及其初始化操作)、函数(及其定义)、模板和其它命名空间。
   }
   命名空间既可以定义在全局作用域内，也可以定义在其它命名空间中，但是不能定义在函数或类的内部；
   命名空间作用域后面无须分号；

   命名空间的特性：
   > 命名空间的名字也必须在定义它的作用域内保持唯一；
     定义在某个命名空间中的名字可以被该命名空间内的其它成员直接访问，也可以被这些成员内嵌作用域中的任何单位访问；
     位于该命名空间之外的代码则必须明确指出所用的名字属于哪个命名空间；
   > 命名空间可以是不连续的;


3、using
   EXP:
	namespace Jill{
		double bucket(double a){ return a + 3; }
		double fetch;
		struct Hill{
			int a;
			int b;
		};
	};

   > using声明使特定的标示符可用：
     如同使用了包里的一个变量，在接下来的作用域里不需要显示使用作用域标示符，也不能定义同名变量;
	using Jill::fetch;
	Jill::fetch = 7;
	double fetch;  //fetch变量不能定义

   > using编译指令使整个名称空间可用：
     A> using namespace Jill;
	Jill::fetch = 7;
     B> using namespace std;            //声明
        cout << "hello world" << endl;  //直接使用cout，而不需要std::cout


   [namespace & using\_1:](https://blog.csdn.net/u010003835/article/details/47402549)
   [namespace & using\_2:](https://blog.csdn.net/fengbingchun/article/details/78575978)


4、C++单例模式
   单例模式是最常用的设计模式之一，对单例的理解：一个类有且只有一个对象（只能实例化一次，不能进行拷贝，赋值），并提供一个全局访问接口。例如windows中的任务管理器，打印机管理程序等。
  
   [参考链接](https://www.cnblogs.com/chengkeke/p/5417371.html)

5、C++构造函数的初始化列表

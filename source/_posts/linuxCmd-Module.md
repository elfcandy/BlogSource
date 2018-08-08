---
title: linuxCmd -- Module
comments: false
date: 2018-08-07 18:01:06
tags:
categories: LinuxCommand
---

linux下两种module的概念不同：

1> linux的module概念：
   linux 2.0版本以后都支持模块化，因为内核中的一部分常驻在内存中（如最常使用的进程，如scheduler等），但是其它的进程只是在需要的时候才被载入。
   如MS-DOS文件系统只有当mount此类系统的时候才需要，这种按需加载，就是模块。
   它能使内核保持较小的体积，虽然可以把所有的东东都放在内核中，这样的话，我们就不需要模块了，但是这样通常是有特殊的用途(所有要运行的进程都预先知道的情况)。
   模块另一个优点是内核可以动态的加载、卸载它们（或者自动地由kerneld守护程序完成）。

   可以具体在看。


2> Environment Modules软件包以模块为单位，为用户动态设置Linux或UNIX的环境变量的软件。
   模块的概念，“应用名”和“应用的版本”的二元组，即一个模块对应的是一个特定版本的应用。
   Environment Modules软件包独立于具体使用的Shell，支持多种主流的Shell。

   在linux服务器上，有时需要安装同一个软件的不同版本，按照需要调用。比如，g03和g09。
   不幸的是，它们的环境变量会互相冲突，不能共存，鱼和熊掌只能选择选择其一。
   这个问题在大型超算服务器上更为严重。很多软件依赖的环境变量、动态库各不相同。
   环境变量模块化工具modules，它的功能很简单，将每个软件的环境变量写一个模块文件modulefile，需调用哪个软件就加载其环境变量模块，执行完成后卸载模块，与之相关的环境变量全部消除。这个神奇的工具是个开源软件。
   目前，在大型超算服务器上，PBS+modules已经成为标配。

   [软件主页:](http://modules.sourceforge.net/)

   常用命令：
    [module] / [module help] / [module -h] —— 查看帮助
    [module avail] —— 查看可用模块
    [module list] —— 查看已经加载的模块
    [module add <模块名>] / [module load <模块名>] —— 加载模块
    [module rm <模块名>] / [module unload <模块名>] —— 卸载模块
    [module purge] —— 卸载所有模块
    [module switch <旧模块> <新模块>] / [module swap <旧模块> <新模块>] —— 替换模块
    [module whatis <模块名>] —— 查看模块说明
    [module show <模块名>] / [module display <模块名>] —— 查看模块内容
    [module use -a <路径>] / [module use --append <路径>] —— 将指定路径追加到MODULEPATH中

问题分析：
    使用module load加载新的module之后，
    报错：
    ModuleCmd_List.c(146):FATAL:996: The environment variables LOADMODULES and _LMFILES_ have inconsistent lengths.
    处理的方法，先清理全部的module，再加载：
        1、module purge
        2、module load <模块名>
   [参考处理方式:](https://sourceforge.net/p/modules/mailman/message/33625046/)
   [参考链接:](https://sourceforge.net/p/modules/mailman/modules-interest/thread/4E3307BC.5040609@tu-dortmund.de/)
   [参考链接:](https://sourceforge.net/p/modules/mailman/message/27610504/)

---
title: setupWebSite
comments: false
date: 2018-03-27 00:23:57
tags:
categories: 使用Hexo在github上建立website的方法
---

#建站过程

关键点有几个：

1、需要工具：GitBash/Node.js/Typora

2、将我的github上的blog仓库，clone到本地，首先使用npm install，之后hexo的原始文件需要通过hexo g命令来生成静态网页，之后可以使用hexo d将生成好的页面发送到github上。
[参考链接 1](https://blog.csdn.net/Greenovia/article/details/60576985)
[参考链接 2](https://www.cnblogs.com/liuxianan/p/build-blog-website-by-hexo-github.html)

3、github支持的个人主页格式必须为：<username>.github.io，因此github上的仓库必须以此命名。

4、在“分类”中按分类显示各项内容的方法：

	A> 执行：hexo new '文章名称'，在./source/_post/目录下会看见“文章名称.md”；
		 文章的开头添加“ categories: 使用Hexo在github上建立website的方法 ”

	B> 执行：hexo new page '目录名称'，在/source/目录下会看见一个新的文件夹，
		 以“目录名称”命名；文件夹下有文件index.md，打开该文件，在开头添加
		 “ type: "categories" ”；
[参考链接](https://segmentfault.com/q/1010000002561642/)

	C> 生成的new page，需要将theme/next/_config.yml中的category项目中冒号后面
	   内容改为：categories: new page 名称；
[参考链接](https://segmentfault.com/q/1010000000618915/)
	   对站点_config.yml和主题文件夹下_config.yml中的category的关系讲的比较清楚;

	   BTW：百度搜索 “Hexo主题中实现多级分类”





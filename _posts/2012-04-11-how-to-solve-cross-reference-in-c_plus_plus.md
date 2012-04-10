---
layout: post
title: "解决C++中类的交叉引用"
tagline: "需要提前申明类"
category: C_plus_plus
tags: [C++]
---
{% include JB/setup %}

###问题描述
假如有下面两个类的申明		

a.h

	#include "b.h"
	class A
	{
		B* b;
	};

b.h

	#include "a.h"
	class B
	{
		A* a;
	};

上面两段程序，a.h在`include "b.h"`的时候，会查看b.h中B的定义，但是B在定义的时候引用了A的定义，可是这个时候还没有A，所以会出现编译器报错说A不是一个类型
###解决办法
在引用之前先申明，但是不需要定义	

a.h

	#include "b.h"
	class B;
	class A
	{
		B* b;
	};

b.h

	#include "a.h"
	class A;
	class B
	{
		A* a;
	};


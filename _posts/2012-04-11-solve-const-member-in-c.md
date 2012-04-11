---
layout: post
title: "在C++中定义仅包含一些常量的集合"
description: ""
category: C_plus_plus
tags: [C++]
---
{% include JB/setup %}

>本来是准备写namespace的用法的，但是感觉有点大，写不来，所以干脆结合我碰到问题，说说解决办法

##问题描述
--------------

我们经常遇到程序里要用到很多常量，在当初的C里，我们用宏的方式解决，在C++里，也可以如此，而且还更提倡用const的方式定义常量，因为这样会有类型检查
但是这样定义的常量是在整个程序里可见的，且相互之间没有关联。而我们经常遇到的问题是，很多常量对某个问题都是相互关联的，比如一种XML文档中的所有标签名称，这个时候我们希望把这些名称放在一个域中，引用他们的时候，可以是A::a这样引用，A是域，a是此域中的常量。
###解决办法1
----------------
用类的方式解决，如在.h中申明或定义:

	class Tag
	{    
	public:    
		static std::string s;    
		static const int b = 1;    
	};
在对应的.cpp中定义:

	string Tag::s = "hello";

此种方法的缺点是，对于非int系列的常量(如int ,long), 必须在.cpp中定义它们，所以显得很麻烦

###解决办法2
----------------
用namespace的方式解决,只需在.h文件中定义：

	namespace Tag 
	{
		static const int a = 3;
		static const std::string s = "gang";
	}

此种方法不再需要.cpp文件。


###引用方法
-------------------
对上面两种方法定义的常量,其引用方法是一样的，都是Tag::s即可,所以对用户来说是透明的。

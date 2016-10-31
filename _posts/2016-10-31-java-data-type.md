---
layout: post
title: java 数据类型
categories: java
tags: java
published: true
---

## 摘要:

1. Java数据类型分类
2. Java基本类型封装
3. 问题汇总

---

## Java数据类型分类

Java数据类型可以分为：

- 基本数据类型
	- 整型：byte(1), short(2), int(4), long(8)
	- 浮点型: float(4), double(8)
	- 字符型: char(2)
	- 布尔型: boolean(1 bit) 注意大小不是1 byte
- 引用数据类型
	- 类
	- 接口
	- 数组
	- 枚举类型

## Java基本类型封装

Java声称一切皆对象，但是早期为了编程的方便，还是引入了基本数据类型。
但是Java对于基本数据类型，都引入了包装类的概念（wrapper class）

Java 为每个原始类型提供了包装类型： 

- 原始类型: boolean，char，byte，short，int，long，float，double 
- 包装类型：Boolean，Character，Byte，Short，Integer，Long，Float，Double

并且从Java5开始，引入了自动装箱，拆箱操作，使两者可以相互转换。
所谓装箱就是将基本数据类型封装成类，拆箱即逆过程。
 
> Integer i = 100;
> 本质上是执行了：Integer i = Integer.valueOf(100); 

## 问题汇总

1. String 属不属于基本数据类型？
	- String是类，不是基本数据类型
2. int和Integer的区别：
	- int是基本数据类型，而Integer是int的封装类
3. float f = 3.4; 这种写法是否正确？
	- java默认的整形类型是int，默认的浮点型是双精度浮点型double。这种写法将double型赋值给float属于向下转型，可能丢失精度。可写成 float f = 3.4F; 或者 float f = (float)3.4;
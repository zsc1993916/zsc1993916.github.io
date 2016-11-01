---
layout: post
title: java 数据类型
categories: java
tags: java
published: true
---

* 目录
{:toc}

---

## Java数据类型分类

Java数据类型可以分为：

- __基本数据类型__
	- 整型：byte(1), short(2), int(4), long(8)
	- 浮点型: float(4), double(8)
	- 字符型: char(2)
	- 布尔型: boolean(1 bit) 注意大小不是1 byte
- __引用数据类型__
	- 类
	- 接口
	- 数组
	- 枚举类型

## Java基本类型封装

Java声称__一切皆对象__，但是早期为了编程的方便，还是引入了基本数据类型。
但是Java对于基本数据类型，都引入了包装类的概念（wrapper class）

Java 为每个原始类型提供了包装类型： 

- 原始类型: boolean，char，byte，short，int，long，float，double 
- 包装类型：Boolean，Character，Byte，Short，Integer，Long，Float，Double

并且从Java5开始，引入了__自动装箱，拆箱操作__，使两者可以相互转换。
所谓装箱就是将基本数据类型封装成类，拆箱即逆过程。
 
> `Integer i = 100;`
> 本质上是执行了：`Integer i = Integer.valueOf(100); `

## 问题汇总

- __*String 属不属于基本数据类型？*__
	
	String是类，不是基本数据类型
	
- __int和Integer的区别?__
	
	int是基本数据类型，而Integer是int的封装类
	
- ___`float f = 3.4;` 这种写法是否正确？___
	
	java默认的整形类型是int，默认的浮点型是双精度浮点型double。这种写法将double型赋值给float属于向下转型，可能丢失精度。可写成 `float f = 3.4F;` 或者 `float f = (float)3.4;`

- ___自动拆装箱___
{% highlight java %}
public class Test {
	public static void main(String[] args) {
		Integer f1 = 100, f2 = 100, f3 = 150, f4 = 150;
		System.out.println(f1 == f2);
		System.out.println(f3 == f4);
	}
}
{% endhighlight %}

输出结果：	

	true
	flase
	
解答：`Integer i = 4;` 装箱的本质： `Integer i = Integer.valueOf(4)`

查看Integer类的源码：
	
{% highlight java %}	
public static Integer valueOf(int i) {
	assert IntegerCache.high >= 127;
	if (i >= IntegerCache.low && i <= IntegerCache.high)
		return IntegerCache.cache[i + (-IntegerCache.low)];
		return new Integer(i);
}
{% endhighlight %}
	
可以得知，当数值范围在[IntegerCache.low，IntegerCache.high]直接时，直接返回一个缓存的Integer实例
查看IntegerCache源码：
	
{% highlight java %}
private static class IntegerCache {
	static final int low = -128;
	static final int high;
	static final Integer cache[];
	static {
       // high value may be configured by property
       int h = 127;
       String integerCacheHighPropValue = sun.misc.VM.getSavedProperty("java.lang.Integer.IntegerCache.high");
       if (integerCacheHighPropValue != null) {
           int i = parseInt(integerCacheHighPropValue);
           i = Math.max(i, 127);
           // Maximum array size is Integer.MAX_VALUE
           h = Math.min(i, Integer.MAX_VALUE - (-low) -1);
       }
       high = h;
       cache = new Integer[(high - low) + 1];
       int j = low;
       for(int k = 0; k < cache.length; k++)
            cache[k] = new Integer(j++);
    }
    private IntegerCache() {}
}
{% endhighlight %}
	
Integer默认的Cache范围是[-128,127]，上限也可以配置`java.lang.Integer.IntegerCache.high`,取默认值和配置值的大值。

`==` 操作符比较的引用变量的值（地址值），所以如果是返回的Cache里的Integer对象，结果为true，否则为 false。如果把`==`换成`equals()`结果都为true。

{% highlight java %}
public boolean equals(Object obj) {
	if (obj instanceof Integer) {
		return value == ((Integer)obj).intValue();
	}
	return false;
}
{% endhighlight %}
	
- (╯‵□′)╯︵ ┴─┴

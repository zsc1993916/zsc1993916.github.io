---
layout: post
title: C++引用
categories: C++
tags: C++ 引用
---

### C++引用

---

- C++引用 作为函数返回值，返回栈区数据会warning，但是不会抱错

---
	#include <stdio.h>
	int & func(int a)
	{
	    int b = a + 5;
	    return b;
	}
	int main()
	{
	    printf("Hello World\n");
	    int a = 10;
	    int b = func(a);
	    printf("b : %d\n", b);
	    return 0;
	}

编译结果：

---
	a.cpp:6:12: warning: reference to stack memory associated with local variable
      'b' returned [-Wreturn-stack-address]
---

---
title: STL 线性结构
date: 2022-05-22 12:55:33
tags: 线性结构
description: 如果写c++程序那么STL容器是不可避免要使用的，而正确合理地使用这些容器才能够简化我们的程序、提高运行的效率，所以本篇根据2022-05-22《数据结构课程设计》来记录 STL线性结构 笔记
---

## 问题引入

如何输出6的二进制数？



## 分析问题

**问题->解决方案->实现方案->编写**

即

从问题得到解决方案（解决方案（具体步骤（过程可以问专业专家）））

实现方案有哪几种方法，并进行优化

编写代码



## 解决方案

### 整数

**十进制整数转换为二进制整数采用"除2取余，逆序排列"法。**

具体做法是：用2整除十进制整数，可以得到一个商和余数；再用2去除商，又会得到一个商和余数，如此进行，直到商为小于1时为止，然后把先得到的余数作为二进制数的低位有效位，后得到的余数作为二进制数的高位有效位，依次排列起来。



## 实现方案

### 一、使用stack【栈】输出

因为 <u>将得到的余数作为二进制数的高位有效位依次排列起来</u> 的过程需要后进先出，所以我们使用栈进行输出

老师给出代码如下

```c++
#include<cstdio>
#include<list>
#include<stack>
main(){
	std::list<int> q; //定义（双向）链表（被除数q） 			#include<list>
	std::stack<int> r;//定义栈（余数r）					#include<stack>
	int n;
	scanf("%d",&n);
	while(n!=0){
		q.push_back(n/2);	//push_back链表的后面插入  
		r.push(n%2); 		//push余数压入栈 
		n=n/2;
	} 
	while(!r.empty()){	// empty()只返回真假值，栈空返回1，否则返回0 
	printf("%d",r.top());//top有返回值，而pop没有返回值 ，//用stack倒叙输出 
	r.pop();		
	}
	return 0;
}
```



其中`std::list<int> q;` 定义（双向）**链表** 来记录<u>商q</u>；`std::stack<int> r` 定义 **栈** 来记录<u>余数r</u>，定义n来表示操作数（要变为2进制的数）





利用循环1来“压进”处理的数据：将**商**压进 链表的后面（`q.push_back(n/2)`）；将余数 压入栈 `r.push(n%2);` ；随后将n/2向下取整（int型）

```c++
while(n!=0){
		q.push_back(n/2);	//push_back链表的后面插入  
		r.push(n%2); 		//push余数压入栈 
		n=n/2;
} 
```





利用循环2来输出：将 压入栈 `r.push(n%2);`  的元素从栈顶输出`printf("%d",r.top());`随后销毁栈顶元素[目的是为了让下一个元素输出]`r.pop();`

```c++
while(!r.empty()){	// empty()只返回真假值，栈空返回1，否则返回0 
	printf("%d",r.top());//top有返回值，而pop没有返回值 ，//用stack倒叙输出 
	r.pop();		
}
```



#### 优化

我们发现，在输出时候，我们并没有输出双向链表`std::list<int> q;`，

所以我们可以判断，双向链表是多余的，需要优化（但是思考实现方案的时候不能不考虑到双向链表）

我们把list相关代码删除（或注释）

得到

```c++
#include<cstdio>
//#include<list>
#include<stack>
main(){
//	std::list<int> q; //定义（双向）链表（被除数q） 	#include<list>
	std::stack<int> r;//定义栈（余数r）					#include<stack>
	int n;
	scanf("%d",&n);
	while(n!=0){
	//	q.push_back(n/2);商（不用输出）	//push_back链表的后面插入  
		r.push(n%2); 		//push余数压入栈 
		n=n/2;
	} 
	while(!r.empty()){	// empty()只返回真假值，栈空返回1，否则返回0 
	printf("%d",r.top());//top有返回值，而pop没有返回值 ，//用stack倒叙输出 
	r.pop();		
	}
	return 0;
}
```





### 二、使用list【链式存储】输出

具有三种实现list输出方案：

#### 1）使用r.push_back(n%2);加上reverse

因为 <u>将得到的余数作为二进制数的高位有效位依次排列起来</u> 的过程需要后进先出，若我们需要使用list【链式存储】输出，要先将链式存储的顺序进行交换

那么我们需要用到的是reverse函数，具体代码如下

```c++
#include<cstdio>
#include<list>
main(){
	std::list<int> r;
	int n;
	scanf("%d",&n);
	while(n!=0){	 
		r.push_back(n%2);
		n=n/2;
	} 
	

	reverse(r.begin(),r.end());//【或者】r.reverse;
    //auto *i;auto:自动类型推倒//std::list<int>::iterator ;
	for(auto i=r.begin();i!=r.end();++i)
		printf("%d",*i) ;
	return 0;

}
```

其中`reverse(r.begin(),r.end());`为交换顺序函数，将链表排序颠倒（1,2,3->3,2,1）

在输出时，我们要用到类似指针的`i`，但是它的类型我们并不知道（或者不想写），那么我们使用`auto i`，让编译器自动识别

> 不过在使用时需要如下配置
>
> ![编译时加入以下命令](https://img1.i-nmb.cn/img/image-20220522134832991.png)



#### 2）使用r.push_back(n%2);利用属性改为rbigin，rend

利用双向链表的属性，我们可以重后往前输出

**注意**：双向链表不是数列，不能将上述`for(auto i=r.begin();i!=r.end();++i)`用`for(auto i=r.end();i!=r.begin();i--)`，而是要将`r.begin()`改为`r.rbegin`，`r.end`改为`r.rend`,即改为`for(auto i=r.rbegin();i!=r.rend();++i)`

具体代码如下

```c++
#include<cstdio>
#include<list>
main(){
	std::list<int> r;
	int n;
	scanf("%d",&n);
	while(n!=0){	 
		r.push_back(n%2); 		
		n=n/2;
	} 

	//auto *i;auto:自动类型推倒//std::list<int>::iterator ;

	for(auto i=r.rbegin();i!=r.rend();++i)// begin变成rbegin， end改为rend，双向链表从后向前读取 
	printf("%d",*i) ;
	return 0;

}
```



#### 3）使用r.push_front(n%2); 

<u>将得到的余数作为二进制数的高位有效位依次排列起来</u> 的过程需要后进先出，我们还可以在插入时从链表头插入`r.push_front(n%2)`



```c++
#include<cstdio>
#include<list>
main(){
	std::list<int> r;
	int n;
	scanf("%d",&n);
	while(n!=0){	 
		push_front(n%2);		// push_front(n%2)（从前插入）顺序等于reverse(r.begin(),r.end())【或者】;数序颠倒，1,2,3->3,2,1 ,
		n=n/2;
	} 
	for(auto i=r.begin();i!=r.end();++i)
	printf("%d",*i) ;
	return 0;

}
```



### 三、vector【顺序存储，数组】输出

同使用list【链式存储】输出一样，我们可以

**1）使用r.push_back(n%2);加上reverse**

方法同list，只不过将list替换为vector

**2）使用r.push_back(n%2);利用属性改为rbigin，rend**

方法同list，只不过将list替换为vector



但是我们<u>不能使用`r.push_front(n%2);`</u> ，因为vector作为顺序存储（数组），不能从头输入，只能从尾输入。即没有`r.push_front()`

**vector具有数组特性，我们可以使用数组的方法进行输出** **（不建议）**

即使用

```c++
for(int i=r.size();i>0;--i)
		printf("%d",r[i]) ;
```



得到：

```c++
#include<cstdio>
#include<vector>
main(){
	std::vector<int> r;
	int n;
	scanf("%d",&n);
	while(n!=0){	 
		r.push_back(n%2); 		
		n=n/2;
	}

	for(int i=r.size();i>0;--i)
		printf("%d",r[i]) ;			//数组从r[max]输出到r[1](r[0]为空)
	return 0;

}
```





### 四、双端队列deque【deque 是 double-ended queue 的缩写，又称双端队列容器。】

和 vector 不同的是，deque 还擅长在序列头部添加或删除元素

deque的内存模型相比于vector与list要复杂许多，它不像vector 把所有的对象保存在一块连续的内存块，而是采用多个连续的存储块，并且在一个映射结构中保存对这些块及其顺序的跟踪。向deque 两端添加或删除元素的开销很小，它不需要重新分配空间。

具体模型见下图：

![image-20220522141449464](https://img1.i-nmb.cn/img/image-20220522141449464.png)

他能支持上述所有方式：

**1）使用r.push_back(n%2);加上reverse**

**2）使用r.push_back(n%2);利用属性改为rbigin，rend**

**3）使用r.push_front(n%2);** 

**4）具有数组特性，可以使用数组的方法进行输出** **（不建议）**

---
title: 【实例1】表达式求值——利用stack实现五种运算符的运算
date: 2022-05-22 23:38:33
tags: 运算符
description: 本篇带读者走进如何用stack来实现加减乘除运算
---

看了标题有人会问，运算符的运算实现？直接printf("%d",a+b*c);不就完了么？

当然没有那么简单！

本篇带读者走进如何用stack来实现加减乘除运算



## [原则：没有解决方案之前绝不能试图开始编程]

在我们拿到题目后，有些读者习惯于直接开始敲代码，我觉得这样不方便思路的养成。所以 没有解决方案之前绝不能试图开始编程



那么解决方案哪里来？！探索解决方案，可以从百度来，可以问专业学者等等。







## [解决方案一:算符优先文法]

给不同运算符赋予“优先级”的概念
优先级相同的运算符按照结合性的顺序计算（从左到右或从右到左）
为了更简单地比较不同运算符的优先级
给每个运算符定义一个称为**“优先数”的整数（以下优先数越小，优先级越高）**

```c++
+：81，82
-：81，82
*：41，42
/：41，42
=：100，100
3+4*5+2=
```

确定运算顺序:专家告诉我们：使用计算栈h（保存元素是运算符）
{a1, a2,..., an, k} 此时，k是watch dog，也就是哨兵
for (i=1 ;ai !=k ; ++k) ;





## 实践方案



1. h.push('=');	// 用于判断结束，例如：若输入`6=`(当栈顶的=和输入的=匹配，则结束)

2. 输入下一个运算符op;

3. while（h.top()比op优先）{	栈顶元素出栈计算；}

4. if(h.top()=='='&& op=='='){结束}

5. h.push(op);
6.   转2。（循环）





### 首先，根据实践方案进行初始化

根据上述实践方案，我们可以知道我们需要用到stack、stdio.h的头文件，并且需要用到oper（运算符）、和operand（操作数）,而运算符是char型，操作数为float型

所以我们在文件头需要编写以下代码



```c++
#include<stdio.h>
#include<stack>

typedef char oper;	//运算符
typedef float operand;
```



### 其次，建立实践方案对应的函数

我们初始化完成后，如果要解决问题，则需要建立解决问题的函数

于是我们建立一个名为`solve`的函数，因为是处理数据的，将要返回处理数据的数值，而数值的类型上述定义是`operand`类型

需要加入`operand solve(){}`函数。



我们在处理运算符时，需要判断运算符的优先级，我们需要一个函数判断左边和右边优先级大小，所以我们引入一个函数 根据定义的一个称为**“优先数”的整数**（优先数越小，优先级越高）来判断优先级大小。

我们使用`int prior(oper op1, oper op2){}`，根据优先数相减得到的int型的正负值判断，其中`op1`为左符号类型为定义的`oper`，`op2`为右符号（新符号）



最后使用必须要有main函数`main(){}`



所以构造完毕后，总代码如下

```c++
#include<stdio.h>
#include<stack>

typedef char oper;		//运算符
typedef float operand;	//运算数


int prior(oper op1, oper op2){
    return;
}

operand solve(){
	return;
}

main(){
    
}
```



### 处理函数的丰富

我们主要的处理函数是`operand solve()`

最简单的加减乘除运算是拥有两个数和一个运算符组成，所以我们要先定义两个数和运算符

我们还需要两个栈（一个存放操作数，一个存放操作符）

完善函数如下

```c++
operand solute(){
	operand x, y;
	oper op;
	std::stack<oper> history;		//历史栈 ,存放历史操作符号
	std::stack<operand> operands;	//存放操作数
}
```



我们根据[**实践方案（点击转到）**](#实践方案)

> 1. h.push('=');	// 用于判断结束，例如：若输入`6=`(当栈顶的=和输入的=匹配，则结束)
>
> 2. 输入下一个运算符op;
>
> 3. while（h.top()比op优先）{
>
> ​	栈顶元素出栈计算；
>
> }
>
> 4. if(h.top()=='='&& op=='='){结束}（若有等号匹配，则结束循环）
>
> 5. h.push(op);
> 6.   转2。（循环）



#### 1.h.push('=');

那么我们添加`history.push('=');`输入等号，whach dog（士兵）进栈 

```c++
operand solute(){
	operand x, y;
	oper op;
	std::stack<oper> history;		//历史栈 ,存放历史操作符号
	std::stack<operand> operands;	//存放操作数
    history.push('=');//输入等号，whach dog（士兵）进栈 
}
```



#### 2.步骤2-5循环，直到若有等号匹配，则结束循环；

所以我们加入循环条件

```c++
operand solute(){
	operand x, y;
	oper op;
	std::stack<oper> history;		//历史栈 ,存放历史操作符号
	std::stack<operand> operands;	//存放操作数
    history.push('=');//输入等号，whach dog（士兵）进栈 
    	while(1){
		
		if(prior(history.top(),op)==0) break;
	}
}
```

#### 3.输入下一个数和运算符op;

我们需要在循环体中持续不断的输入数和运算符

观察式子：`3+2+1*5=`、`5*8/7-4=`、`9*8/7-5=`

我们发现，我们输入的每个数字后面有且仅有一个运算符

所以我们加入

```c++
scanf("%f %c",&x,&op);		//输入一个数字和一个字符
		operands.push(x);	//将数字压入存放操作数的栈
```



#### 4.栈顶元素出栈计算；

我们需要判断运算符的优先级，如果存放历史操作符号的栈顶比op优先，（优先数越小，优先级越高），那么直接计算历史操作数链接的两个数



示意图如下

<img src="https://img1.i-nmb.cn/img/image-20220522224804731.png" alt="image-20220522224804731" style="zoom:67%;" />



所以我们根据

> 3. while（h.top()比op优先）{
>
> ​	栈顶元素出栈计算；
>
> }

进行栈顶元素出栈计算；

所以写出以下循环

```c++
while（h.top()比op优先）{
	y = operands.top();	//让y为最新的数（优先级高的历史操作符的右边的数）
	operands.pop();		//弹走最新的数（优先级高的历史操作符的右边的数）
	x = operands.top();	//让x为优先级高的历史操作符的左边的数
	operands.pop();		//弹走历史操作符的左边的数
	switch(history.top()){	//判断优先级高的历史操作符
		case '+': operands.push(x + y) ; break;
		case '-': operands.push(x - y) ; break;
		case '*': operands.push(x * y) ; break;
		case '/': operands.push(x / y) ; break;
	}
	history.pop();//弹走历史操作符的栈顶
}
```



接下来我们需要对比`history.top()`【历史操作符（上一次的运算符号）】和`op`【即将压入history栈的符号】优先

通过之前的函数`int prior(oper op1, oper op2)`进行丰富，

又因为**优先数越小，优先级越高**，所以我们判断优先数的做差，判断差的正负性就可以判断优先级。

我们完善函数`int prior(oper op1, oper op2)`

```c++
int prior(oper op1, oper op2){
	return p_num[op1].left - p_num[op2].right;
}
```

从而完善循环判断

```c++
while（prior(history.top(), op)<0）{
	y = operands.top();	//让y为最新的数（优先级高的历史操作符的右边的数）
	operands.pop();		//弹走最新的数（优先级高的历史操作符的右边的数）
	x = operands.top();	//让x为优先级高的历史操作符的左边的数
    ………………………………………………
```



#### 5.h.push(op);压入op

若优先级不大于栈顶的优先级，要将op压入history栈`history.push(op);`，此操作要在判断是否为等号之后

即
			

```c++
operand solve(){
	operand x, y;
	oper op;
	std::stack<oper> history;//历史栈 
	std::stack<operand> operands;
	history.push('=');//输入等号，whach dog（士兵）进栈 
	while(1){
/*******************
*2.  输入下一个运算符op;
*3.  while（h.top()比op优先）{	栈顶元素出栈计算；}
*4.  if(h.top()=='='&& op=='='){结束}
*5.  h.push(op);
*6.  转2。
********************/
		scanf("%f %c",&x,&op);
		operands.push(x);
		while(prior(history.top(), op)<0){
			y = operands.top();
			operands.pop();
			x = operands.top();
			operands.pop();
			switch(history.top()){
				case '+': operands.push(x + y) ; break;
				case '-': operands.push(x - y) ; break;
				case '*': operands.push(x * y) ; break;
				case '/': operands.push(x / y) ; break;
			}
			history.pop();
		}
		if(prior(history.top(),op)==0) break;
		history.push(op);
	}
    return operands.top();
}
```



#### 6.函数的完善

我们的解决函数`operand solve(){}`趋近完美，但是程序是由`main(){}`开始

所以我们要完善main函数

```c++
int main(){
	printf("%g\n",solve());
	return 0;
}
```



在函数`int prior(oper op1, oper op2){}`中，我们没有赋予`p_num[op1].left`（左符号、旧符号）和`p_num[op2].right`（右符号、新符号）的值（优先数）。所以我们在函数`int prior(oper op1, oper op2){}`之前加入以下代码，并且加入`#include<map>`

```c++
struct prv_num_t{char left,right;};//定义结构体 prv_num_t  _t代表类型 
//关键字只包含一部分数据项,就称为map
std::map<oper, prv_num_t> p_num={
	{'+',{81,82}},
	{'-',{81,82}},
	{'*',{41,42}},
	{'/',{41,42}},
	{'=',{100,100}}
};
```



<img src="https://img1.i-nmb.cn/img/image-20220522232910691.png" alt="计算优先数的示意图" style="zoom:80%;" />





## 问题解决

最终获得代码

```c++
#include<stdio.h>
#include<stack>
#include<map>

typedef char oper;//运算符
typedef float operand;

/*优先数表*/
struct prv_num_t{char left,right;};//定义结构体 prv_num_t  _t代表类型 
//关键字只包含一部分数据项,就称为map
//关键字包含全部数据项,成为 
std::map<oper, prv_num_t> p_num={
	{'+',{81,82}},
	{'-',{81,82}},
	{'*',{41,42}},
	{'/',{41,42}},
	{'=',{100,100}}
};


/*op1在左，op2在右*/
/*返回值为负: op1优先级高于op2*/
/*返回值为正: op2优先级高于op1*/
/*返回值为0: op1优先级等于op2*/

int prior(oper op1, oper op2){
	return p_num[op1].left - p_num[op2].right;
}

operand solute(){
	operand x, y;
	oper op;
	std::stack<oper> history;//历史栈 
	std::stack<operand> operands;
	history.push('=');//输入等号，whach dog（士兵）进栈 
	while(1){
/****************************************
*2.  输入下一个运算符op;
*3.  while（h.top()比op优先）{	栈顶元素出栈计算；}
*4.  if(h.top()=='='&& op=='='){结束}
*5.  h.push(op);
*6.  转2。
******************************************/
		scanf("%f %c",&x,&op);
		operands.push(x);
		while(prior(history.top(), op)<0){
			
			y = operands.top();
			operands.pop();
			x = operands.top();
			operands.pop();
			switch(history.top()){
				case '+': operands.push(x + y) ; break;
				case '-': operands.push(x - y) ; break;
				case '*': operands.push(x * y) ; break;
				case '/': operands.push(x / y) ; break;
			}
			history.pop();
		}
		if(prior(history.top(),op)==0) break;
		history.push(op);
	}
	return operands.top();
}

int main(){
	printf("%g\n",solute());
	
	return 0;
}
 
```


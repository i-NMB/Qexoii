---
title: 【实例1の更新1】表达式求值——加入新的单目运算符
date: 2022-05-24 06:38:52
tags: 运算符
description: 在原基础上逐一的实现 `指数、对数以及三角函数` 的表达式求值
---

前段时间我们学习了利用stack实现五种运算符的运算：[【实例】表达式求值——利用stack实现五种运算符的运算 | 《课程设计》笔记 (i-nmb.cn)](https://kcsj.i-nmb.cn/example.html)

实际上我们的表达式求值中并不是只有这5种运算，他还包括了 指数、对数以及三角函数等等。

今天我们就在原基础上逐一的实现 `指数、对数以及三角函数` 的表达式求值

## 写在前面

之前，在[【实例】表达式求值——利用stack实现五种运算符的运算 | 《课程设计》笔记 (i-nmb.cn)](https://kcsj.i-nmb.cn/example.html)中，我们做出了一下代码

```C++
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

operand solve(){
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
	printf("%g\n",solve());
	
	return 0;
}
 
```



今天的实例更新，是建立再此代码基础上的



## 实现目标

1、优化之前的代码

2、逐一的实现 `指数、对数以及三角函数` 的表达式求值



## 1.优化代码

在加入新功能之前，我们先审视之前我们敲击的代码，我们在`operand solve(){}`函数中使用了以下循环

```c++
operand solve(){
	while(1){
	……………………………………………………
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
		……………………………………
	}
	…………………………………………
}
```

这个循环实质上是一个运算核心，放在循环中，总是不太合适。

所以我们把他提取出来，改造成一个函数`operand calc(){}`，返回类型为之前定义的operand（操作数）

`operand calc()`在循环while(prior(history.top(),op)<0)返回运算结果，若输入出错，则输出Err，返回-1

```c++
operand calc(){
	operand x, y;
	y = operands.top();
	operands.pop();
	x = operands.top();
	operands.pop();
	switch(history.top()){
		case '+': return x+y;//当运算符为+时，在循环while(prior(history.top(),op)<0)返回x+y运算结果
		case '-': return x-y;//当运算符为-时，在循环while(prior(history.top(),op)<0)返回x-y运算结果
		case '*': return x*y;//当运算符为*时，在循环while(prior(history.top(),op)<0)返回x*y运算结果
		case '/': return x/y;//当运算符为/时，在循环while(prior(history.top(),op)<0)返回x/y运算结果
	}
	printf("Err");
	return -1;
}
```



而原	`while(prior(history.top(), op)<0){}`循环体中改为

```c++
	while(prior(history.top(),op)<0){
		operands.push(calc());
		history.pop();
	}
```



最后将以下代码设置为全局变量

```
	std::stack<oper> history;//历史栈 
	std::stack<operand> operands;
```

至此优化结束，优化后的总代码为：

```c++
#include<stdio.h>
#include<stack>
#include<map>

typedef char oper;//运算符
typedef float operand;
std::stack<oper> history;//历史栈 
std::stack<operand> operands;

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


operand calc(){
	operand x, y;
	y = operands.top();
	operands.pop();
	x = operands.top();
	operands.pop();
	switch(history.top()){
		case '+': return x+y;
		case '-': return x-y;
		case '*': return x*y;
		case '/': return x/y;
	}
	printf("Err");
	return -1;
}


operand solve(){
	operand x, y;
	oper op;

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
			operands.push(calc());
			history.pop();
		}
		if(prior(history.top(),op)==0) break;
		history.push(op);
	}
	return operands.top();
}

int main(){
	printf("%g\n",solve());
	
	return 0;
}
 
```



## 2.增加指数运算和对数运算符

### 增加指数运算符

增加指数运算相对简单，在map（`std::map<oper, prv_num_t> p_num`）里面增加`{"关键字",{左优先数,右优先数}}`，左优先级大于右优先（从左到右运算）【2^3^2==64!=2^(3^2)】

即

```c++
std::map<oper, prv_num_t> p_num={
	{'+',{81,82}},
	{'-',{81,82}},
	{'*',{41,42}},
	{'/',{41,42}},
	{'=',{100,100}},
    
+    {'^',{32,31}}
    
};
```



并且在运算函数`calc(){}`加入返回运算值

即

```c++
	case '*': return x*y;
	case '/': return x/y;

+	case '^': return pow(x,y);

}
printf("Err");
```

因为用到了pow函数，所以我们在头文件加入`#include<math.h>`



至此，增加指数运算符操作结束



### 增加对数运算符

同理

在map（`std::map<oper, prv_num_t> p_num`）里面增加`{"关键字",{左优先数,右优先数}}`，左优先级小于右优先（从右到左运算）【log （2,log(2,8))=3】

```c++
std::map<oper, prv_num_t>  p_num={
	{'+',{81,82}},
	{'-',{81,82}},
	{'*',{41,42}},
	{'/',{41,42}},
	{'=', {100,100}},
	{'^',{32,31}}, 
    
+	{'L',{22,21}}//对数运算符log(x,y) ；log (x,log(x,x)) ，右边优先 
    
}
printf("Err");
```



在运算函数`calc(){}`加入返回运算值

```c++
	case '*': return x*y;
	case '/': return x/y;
	case '^': return pow(x,y);
	
+	case 'L': return log(y)/log(x);//对数换底公式 ,以x（先输入的数）为底数

}
printf("Err");

```

至此，增加对数运算符操作结束

试试`2L8=` 答案是3

## 3.增加三角函数（单目运算符）



在map添加关键字



```
std::map<oper, prv_num_t>  p_num={
	{'+',{81,82}},
	{'-',{81,82}},
	{'*',{41,42}},
	{'/',{41,42}},
	{'=', {100,100}},
	{'^',{32,31}}, 
    {'L',{22,21}},	//对数运算符log(x,y) ；log (x,log(x,x)) ，右边优先 
    
+    {'S',{22,21}},//定义sin函数 
+	{'C',{22,21}},//定义cos函数; 
}
printf("Err");
```







在运算函数`calc(){}`加入返回运算值

```c++
	case '*': return x*y;
	case '/': return x/y;
	case '^': return pow(x,y);
	case 'L': return log(y)/log(x);//对数换底公式 ,以x（先输入的数）为底数

+	case 'S': return sin(y); 		
+	case 'C': return cos(y); 

}
printf("Err");

```

至此，增加三角函数符号







### 冲突

之前我们增加的是双目运算符，遵循着 `'操作数' '运算符' '操作数'`

现在，我们的单目运算符，遵循 `'运算符' '操作数'`

### 一、输入模式不同的解决办法

二者输入模式不同，怎么办？难道之前辛苦搭建的程序崩塌了？

其实我们输入表达式的时候已经将完整的表达式输入了，**此时我们只需要判断下一位是不是运算符，而进行对应计算，也就是<u>预读下一位数</u>**



**预读下一位数如果是数字，那么返还给键盘（模拟键盘重新输入）**

**预读下一位数如果不是数字，那么作为op（运算符）**



所以在`while(1){}`处，更改以下代码

```c++
while(1){
/****************************************
*2.  输入下一个运算符op;
*3.  while（h.top()比op优先）{	栈顶元素出栈计算；}
*4.  if(h.top()=='='&& op=='='){结束}
*5.  h.push(op);
*6.  转2。
******************************************/

-		scanf("%f %c",&x,&op);		//scanf("%f %c",&x,&op); 3+40=;3+C0=两个符号合起来
-		operands.push(x);

	
+	scanf(" %c",&op);//预读下一位数 

+	if(isdigit(op)) {			//isdigiy判断是否是数字 //if(op是数字) #include<ctype.h>//判断字符类型 
+		ungetc(op, stdin);		//还回字符 ,还给stdin（键盘）
+		scanf("%f",&x);
+		operands.push(x);
+		continue; 
+	}	
```

并且增加头文件`#include<ctype.h>` 

此时输入模式不同的问题得以解决



### 二、运算模式不同的解决

如果是双目运算符，那么我们操作数栈的操作如下

```c++
y = operands.top();
operands.pop();
x = operands.top();
operands.pop();
```

由此可见，我们在运算双目运算符的时候，把y赋予栈顶值，然后弹出栈顶以获取下一个数来赋予x，之后再一次弹出栈顶

**相当于一个双目运算符运算过后，弹出两个数**

而如果用单目运算符运算，只需要运算一个数

也就是说，**单目运算符运算过后，弹出一个数**



#### 解决办法

我们需要判断运算符是单目运算符还是双目运算符

```c++
	if(history.top()是双目运算符){
		y = operands.top();
		operands.pop();
	}
```

如果是双目运算符我们就弹多走1个栈顶

​	`if(history.top()是双目运算符)`我们使用`if(strchr("+-*/^L",history.top()))`实现

也就是在`operand calc()`函数中做以下操作



```c++
operand calc(){
	operand x, y;
	
-	y = operands.top();
-	operands.pop();

+	if(strchr("+-*/^L",history.top())){	//strchr在 "+-*/^L"找到 history.top()，如果找到返回位置，找不到返回空值【用来判断（整数和0）】 
+		y = operands.top();
+		operands.pop();
+	}
	
	x = operands.top();
	operands.pop();
	switch(history.top()){
		case '+': return x+y;
		case '-': return x-y;
		case '*': return x*y;
		case '/': return x/y;
		case '^': return pow(x,y);
		case 'L': return log(y)/log(x);//log c库的对数换底公式 
        case 'S': return sin(y);
		case 'C': return cos(y); 
	}
	printf("Err");
	return -1;
}
```



我们引用了`strchr("+-*/^L",history.top())`因此需要加入`#include<string.h>` 



问题解决





## 最终代码

处理完毕后最终代码如下

```c++
#include<stdio.h>
#include<stack>
#include<map>
#include<math.h>
typedef char oper;//运算符
typedef float operand;
std::stack<oper> history;//历史栈 
std::stack<operand> operands;

/*优先数表*/
struct prv_num_t{char left,right;};//定义结构体 prv_num_t  _t代表类型 
//关键字只包含一部分数据项,就称为map
//关键字包含全部数据项,成为 
std::map<oper, prv_num_t> p_num={
	{'+',{81,82}},
	{'-',{81,82}},
	{'*',{41,42}},
	{'/',{41,42}},
	{'=',{100,100}},
	{'^',{32,31}}, 
	{'L',{22,21}},//对数运算符log(x,y) ；log (x,log(x,x)) ，右边优先 
	{'S',{22,21}},//定义sin函数 
	{'C',{22,21}},//定义cos函数; 
};


/*op1在左，op2在右*/
/*返回值为负: op1优先级高于op2*/
/*返回值为正: op2优先级高于op1*/
/*返回值为0: op1优先级等于op2*/

int prior(oper op1, oper op2){
	return p_num[op1].left - p_num[op2].right;
}

#include<string.h>
operand calc(){
	operand x, y;
//	if(history.top()是双目运算符){
	if(strchr("+-*/^L",history.top())){//strchr在 "+-*/^L"找到 history.top()，如果找到返回位置，找不到返回空值【用来判断（整数和0）】 
		y = operands.top();
		operands.pop();
	}
	x = operands.top();
	operands.pop();
	switch(history.top()){
		case '+': return x+y;
		case '-': return x-y;
		case '*': return x*y;
		case '/': return x/y;
		case '^': return pow(x,y);
		case 'L': return log(y)/log(x);//log c库的对数换底公式
		case 'S': return sin(y); 
		case 'C': return cos(y); 
	}
	printf("Err");
	return -1;
}


operand solve(){
	operand x, y;
	oper op;

	history.push('=');//输入等号，whach dog（士兵）进栈 
	while(1){
/****************************************
*2.  输入下一个运算符op;
*3.  while（h.top()比op优先）{	栈顶元素出栈计算；}
*4.  if(h.top()=='='&& op=='='){结束}
*5.  h.push(op);
*6.  转2。
******************************************/
	scanf(" %c",&op);//预读下一位数 
//	if(op是数字)
	if(isdigit(op)) {//isdigiy判断是否是数字 
		ungetc(op, stdin);//还回字符 ,还给stdin（键盘） 
		scanf("%f",&x);
		operands.push(x);
		continue; 
	}	
		while(prior(history.top(), op)<0){
			operands.push(calc());
			history.pop();
		}
		if(prior(history.top(),op)==0) break;
		history.push(op);
	}
	return operands.top();
}

int main(){
	printf("%g\n",solve());
	
	return 0;
}
 
```


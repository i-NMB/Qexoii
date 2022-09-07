---
title: 【实例1の更新2】表达式求值——加入括号运算
date: 2022-05-24 19:20:52
tags: 运算符
description: 加入括号进行运算、优化报错方法
---

前段时间我们制作了一个表达式求值的程序，

我们赋予他基本框架与功能：[【实例】表达式求值——利用stack实现五种运算符的运算 | 《课程设计》笔记 (i-nmb.cn)](https://kcsj.i-nmb.cn/example.html)

以及更新了一目运算符的支持：[【实例更新】表达式求值——加入新的单目运算符 | 《课程设计》笔记 (i-nmb.cn)](https://kcsj.i-nmb.cn/example-optimization-1.html)



## 问题引入

我们在经过这两个步骤之后，我们可以基本实现 表达式的求值操作 ，但是`L 2 8 =`没有括号就显得十分奇怪，并且我们在输入其他字符时报错方法还可以加以优化，让程序能够定位错误。

所以目前我们需要解决的问题有两种，即：

##### 1.加入括号进行运算

##### 2.优化报错方法



## 一、加入括号

首先我们要进行加入括号的运算方法

### 问题思考

1.在前面的单目运算符以及双目运算符中，我们需要进行数的运算，那么加入括号，操作数又有什么变化？

2.括号的特点是什么？他的左右运算符有没有什么特点？

3.插入括号后，具体的算法（或者说 运算流程 ）是怎么样子的？

4.如何“优雅地”添加括号并且不让程序做很大改动？



这些问题我们需要思考与解决，以下为思考解决的部分过程

#### 加入括号，操作数又有什么变化？

无论是单目运算符或者是双目运算符，其本质为运算符，是处理数的一种符号，只是运算过程中在处理 操作数的数目 的多少而划分。

但是**括号不是数学中的运算符号**，他并没有处理操作数，没有改变操作数的数目和数值，他只是单纯的改变运算符之间的优先级、只是运算顺序的辅助符号。添加括号时 在栈顶的操作数 就在栈顶，没有任何变化。



#### 括号的特点是什么？

1.因为**括号不是数学中的运算符号**，括号最直接的特点就是，加入左括号时，不改变在左括号`（`之前的其他符号的运算顺序，并且在右括号`）`之前，都正常运算（即括号内的正常运算），左括号需要等待右括号才进行出栈

2.由1可以推断，无论左括号前面是什么，直接进栈；左括号后面的符号只要不是右括号，左括号始终不出栈，右括号始终不进栈。

#### 具体的算法（或者说 运算流程 ）

比如`3*(2+4)=`

首先等号入栈[`history.top()`]

第一步，`3`入栈 `operands`

第二步， * 与`history.top()`（=）优先级比较， * 入栈。

第三步，由上述问题，无论左括号前面是什么，直接进栈，所以`(`入栈

第四步，`2`入栈

第五步，左括号与+进行优先级比较，由上述括号的特点可知：左括号后面的符号只要不是右括号，左括号始终不出栈，所以开始计算

第六步，输入4入栈，两次取出栈顶的元素（4和2）并进行＋运算，得数为6，压入 `operands`栈顶，弹出 + 号

第七步，输入右括号，与栈顶`history.top()`的左括号匹配，所以弹出左括号，并且右括号始终不进栈。

第八步，输入等号，等号优先级最小，先运算现在栈顶`history.top()`的 * 号，连续从栈顶取出两个元素相乘，得数18，弹出 * 号

第九步，此时栈顶[`history.top()`]为“=”，与输入的等号相等，程序结束，输出`operands.top()`【此时为得数】



#### 如何“优雅地”添加括号？

根据以上括号的特点及运算流程

我们可以知道：

1.无论左括号前面是什么，直接进栈；

2.左括号后面的符号只要不是右括号，左括号始终不出栈，并且将符号压入栈

3.当等到右括号，则开始计算【等到右括号，“（）”内的数计算完毕】

4.当等到右括号，则弹出左括号

##### 换成伪代码的形式

将以上四点转换成伪代码的形式：

1.  `if(op=='('){push(op)}`

2.  `top=='('&&op!=')':push(op)`

3. `if(op==')'):calc`

4.  `top=='('&&op==')':pop('(')`



##### 将伪代码转换为现实

以上的伪代码只是我们的“梦想”，要让其成为现实的道路并不容易。

因为我们之前的程序大体以及框架已经确定，不能重新打乱和改变。

那么我们如何“优雅地”添加括号并且不让程序做很大改动？

**答案是<u>把括号作为一种特殊的“运算符”加入map</u>**

我们需要用以下特性：

> 1.无论左括号前面是什么，直接进栈
>
> 2.只要不是右括号，左括号始终不出栈
>
> 3.右括号始终不进栈

得出以下结论

1.（左括号的右优先级要非常大）

2.（左括号的左优先级要非常小）

3.（右括号的右优先级非常小）



转为代码

```c++
std::map<oper, prv_num_t>  p_num={
…………
​	{'(',{99,1}},//左边的优先数代表在栈顶的优先数
​	{')',{0,99}},//右边的优先数代表在op中的优先数，
    //因为)不可能在栈内，所以左优先数为0，代表错误
…………
}
```

我们重新审查代码，使用以上代码，可以实现以下目标：

1.无论左括号前面是什么，直接进栈；`if(op=='('){push(op)}`

2.左括号后面的符号只要不是右括号，左括号始终不出栈，并且将符号压入栈 `top=='('&&op!=')':push(op)`

3.当等到右括号，则开始计算 `if(op==')'):calc`【等到右括号，“（）”内的数计算完毕】



但是还有最后一点没有实现

即：4.当等到右括号，则弹出左括号`top=='('&&op==')':pop('(')`

此时我们必须修改源代码，在之前的判断等号与哨兵相等之前（`if(prior(history.top(),op)==0) break;`）根据伪代码`if(top=='('&&op==')'):pop('(')`加入以下代码，

```c++
if(op==")"){
			history.pop();
			continue;
		} 
```

因为左括号的左优先数==右括号的右优先数，如果经过`if(prior(history.top(),op)==0) break;`那就跳出循环，运算就出错了，所以我们应该在此之前加入代码即可

```c++
while(1)
	{
	//scanf("%f %c",&x,&op); 3+40=;3+C0=两个符号合起来，2L10=，2 10 L= ，L 2 10 =；1 2 3 + *= 
	scanf(" %c",&op);//预读下一位数 
	if(op==',') continue;
//	if(op是数字)
	if(isdigit(op)) {//isdigiy判断是否是数字 
		ungetc(op, stdin);//还回字符 ,还给stdin（键盘） 
		scanf("%f",&x);
		operands.push(x);
		continue; 
	}	
	while(prior(history.top(),op)<0){
		operands.push(calc());
		history.pop();
	}
+		if(op==')'){
+			history.pop();
+			continue;
+		} 
		if(prior(history.top(),op)==0) break;
		history.push(op);
	}
```

此时我们基本**实现了加入括号的问题**了



## 二、优化报错方法

解决了上面的问题，在输入右括号而不输入左括号，或者输入其他不识别的运算符时，报错代码来自

<img src="https://img1.i-nmb.cn/img/image-20220524233540858.png" alt="报错代码来自calc函数" style="zoom:60%;" />

这样不利于我们定位出错的位置，所以我们需要优化程序：优化报错方法



若我们输入其他错误字符时，若需要报错，则需要正在通过map函数查找字符对应的优先数的函数中`int prior(oper op1, oper op2)`进行

在其中加入以下代码

```c++
int prior(oper op1, oper op2)
{
+	if(p_num.find(op1)==p_num.end()||p_num[op1].left==0){ //如果找不到运算符的优先数||左优先数=0
+	printf("错误的运算符：%c\n【程序即将终止】",op1);
+	exit (-1);	//异常退出，终止程序
+	}
+	if(p_num.find(op2)==p_num.end()||p_num[op1].right==0){ //如果找不到运算符的优先数||右优先数=0
+	printf("错误的运算符：%c\n【程序即将终止】",op2);
+	exit (-1);
+	}
	return p_num[op1].left - p_num[op2].right;
}
```



若我们在没有左括号的情况下输入右括号，报错，则需要在`字符`压入栈之前判断

```c++
operand solve()
/*****************************************
* 2. 输入下一个运算符op；
* 3. while(prior(h.top(),op)<0)
*    栈顶元素出栈并计算；
* 4. if(prior(h.top(),op)==0)结束；
* 5. if(prior(h.top(),op)>0) h.push(op);
*******************************************/
{
	operand x, y;
	oper op;
	history.push('=');
	while(1)
	{
	//scanf("%f %c",&x,&op); 3+40=;3+C0=两个符号合起来，2L10=，2 10 L= ，L 2 10 =；1 2 3 + *= 
	scanf(" %c",&op);//预读下一位数 
	if(op==',') continue;
//	if(op是数字)
	if(isdigit(op)) {//isdigiy判断是否是数字 
		ungetc(op, stdin);//还回字符 ,还给stdin（键盘） 
		scanf("%f",&x);
		operands.push(x);
		continue; 
	}	
	while(prior(history.top(),op)<0){
		operands.push(calc());
		history.pop();
	}
+		if(op==')'){
+			if(history.top()!='('){
+				printf("请检测：有没有成对括号\n截止目前，计算"); 
+				break;
+			}
			history.pop();
			continue;
		} 
		if(prior(history.top(),op)==0) break;
		history.push(op);
	}
	return operands.top();	
}
```



## 三、问题解决完毕

目前我们需要解决的问题有两种，即：

##### 1.加入括号进行运算

##### 2.优化报错方法



而这两种在上面已经基本上解决了，至此完结~（撒花）

下面附上更改后的代码

```c++
#include<stdio.h>
#include<stack>
#include<map>
#include<math.h>
typedef char oper;
typedef float operand;
std::stack<oper> history;
std::stack<operand> operands;

/*优先数表*/
struct prv_num_t{char left,right;};
std::map<oper, prv_num_t>  p_num={
	{'+',{81,82}},
	{'-',{81,82}},
	{'*',{41,42}},
	{'/',{41,42}},
	{'=', {100,100}},
	{'^',{32,31}}, 
	{'L',{22,21}},//对数运算符log(x,y) ；log (x,log(x,x)) ，右边优先 
	{'S',{22,21}},//定义sin函数 
	{'C',{22,21}},//定义cos函数; 
	{'(',{99,1}},
	{')',{0,99}},//0作为错误标志 
};
//{0,0},{0,0},{0,0},{0,0},{0,0},{0,0},{0,0},{0,0},{0,0},{0,0}, /* 0-9 */
//{0,0},{0,0},{0,0},{0,0},{0,0},{0,0},{0,0},{0,0},{0,0},{0,0}, /* 10-19 */
//{0,0},{0,0},{0,0},{0,0},{0,0},{0,0},{0,0},{0,0},{0,0},{0,0}, /* 20-29 */
//{0,0},{0,0},{0,0},{0,0},{0,0},{0,0},{0,0},{0,0},{0,0},{0,0}, /* 30-39 */
//{0,0},{0,0},{41,42},{81,82},{0,0},{81,82},{0,0},{41,42},{0,0},{0,0}, /* 40-49 */
//{0,0},{0,0},{0,0},{0,0},{0,0},{0,0},{0,0},{0,0},{0,0},{0,0}, /* 50-59 */
//{0,0},{100,100},{0,0},{0,0},{0,0},{0,0},{0,0},{0,0},{0,0},{0,0}, /* 60-69 */
//{0,0},{0,0},{0,0},{0,0},{0,0},{0,0},{0,0},{0,0},{0,0},{0,0}, /* 70-79 */
//{0,0},{0,0},{0,0},{0,0},{0,0},{0,0},{0,0},{0,0},{0,0},{0,0}, /* 80-89 */
//{0,0},{0,0},{0,0},{0,0},{0,0},{0,0},{0,0},{0,0},{0,0},{0,0}, /* 90-99 */
//{0,0},{0,0},{0,0},{0,0},{0,0},{0,0},{0,0},{0,0},{0,0},{0,0}, /* 100-109 */
//{0,0},{0,0},{0,0},{0,0},{0,0},{0,0},{0,0},{0,0},{0,0},{0,0}, /* 110-119 */
//{0,0},{0,0},{0,0},{0,0},{0,0},{0,0},{0,0},{0,0} /* 120-127 */
//};

//43 45 42 47 61


/*op1在左，op2在右*/ 
/*返回值为负：op1优先级高于op2*/
/*返回值为正：op2优先级高于op1*/
/*返回值为0：op1优先级等于op2*/
int prior(oper op1, oper op2)
{
	if(p_num.find(op1)==p_num.end()||p_num[op1].left==0){ //如果找不到运算符
	printf("错误的运算符：%c\n【程序即将终止】",op1);
	exit (-1);
	}
	if(p_num.find(op2)==p_num.end()||p_num[op1].right==0){ //如果找不到运算符
	printf("错误的运算符：%c\n【程序即将终止】",op2);
	exit (-1);
	}
	return p_num[op1].left - p_num[op2].right;
}
#include<ctype.h>//判断字符类型 
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
		case 'S': return sin(y); //		case 'S': operands.push(x); return sin(y); 
		case 'C': return cos(y); //		case 'C': operands.push(x); return cos(y);
	}
	printf("Err");
	return -1;
}
operand solve()
/*****************************************
* 2. 输入下一个运算符op；
* 3. while(prior(h.top(),op)<0)
*    栈顶元素出栈并计算；
* 4. if(prior(h.top(),op)==0)结束；
* 5. if(prior(h.top(),op)>0) h.push(op);
*******************************************/
{
	operand x, y;
	oper op;
	history.push('=');
	while(1)
	{
	//scanf("%f %c",&x,&op); 3+40=;3+C0=两个符号合起来，2L10=，2 10 L= ，L 2 10 =；1 2 3 + *= 
	scanf(" %c",&op);//预读下一位数 
	if(op==',') continue;
//	if(op是数字)
	if(isdigit(op)) {//isdigiy判断是否是数字 
		ungetc(op, stdin);//还回字符 ,还给stdin（键盘） 
		scanf("%f",&x);
		operands.push(x);
		continue; 
	}	
	while(prior(history.top(),op)<0){
		operands.push(calc());
		history.pop();
	}
		if(op==')'){
			if(history.top()!='('){
				printf("请检测：有没有成对括号\n截止目前，计算"); 
				break;
			}
			history.pop();
			continue;
		} 
		if(prior(history.top(),op)==0) break;
		history.push(op);
	}
	return operands.top();	
}

int main()
{
//	printf("%d %d %d %d %d", '+', '-', '*', '/', '=');return 0;
	printf("%g\n", solve());
	return 0;
}
```

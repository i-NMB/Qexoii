---
title: 【实例2】24点游戏
date: 2022-06-09 11:06:24
tags: 24点
description: 前面我们描述了如何通过表达式求值，今天我们玩个游戏——24点
---

## 描述问题

在确认程序编写之前我们需要思考如何描述，表达问题



算法具有五个特性

> 1.输入：在算法中可以有零个或者多个输入
>
> 2.输出：在算法中至少有一个或者多个输出
>
> 3.有穷行：在执行有限的步骤之后，自动结束不会出现无限循环并且每一个步骤在可接受的时间内完成
>
> 4.确定性：算法的每一个步骤都具有确定的含义，不会出现二义性
>
> 5.可行性：算法的每一步都必须是可行的，也就是说，每一步都能够通过执行有限的次数完成

那么哪两个适用于描述问题呢？答案是`输入和输出`

描述问题，我们只需要抓住输入和输出就够了。至于什么其他的问题背景，对于毫无意义。找到问题的输入和输出之后，我们进入抽象化的世界，



所以描述任何问题最关键的是要找到问题的输入和输出。

**24点的输入是什么？四个整数，每个整数都在1~13之间**

**输出呢？输出就是要找一个表达式，加减乘除算运算完成后等于24。如果找不到输出`无解`，找到就输出那个`表达式`**



有了输入和输出之后，24点问题就算是描述的非常清晰。



**计算机专业描述问题，只需要抓住啊两个特点：输入和输出**

不是说问题背景不需要，而是说，描述问题背景是为了找到输入与输出！与输入输出无关的背景可以酌情忽略。



## 解决问题方法

输入和输出找到之后需要找解决方案，解决方案找到之后，把解决方案变成算法。把解决方案变成算法的过程可能需要咨询领域专家。算法知道后，我们的路就好走了。

## 解决方案

举例子：

24点游戏我们需要输入四个数字，最后要找一个表达式，加减乘除算运算完成后等于24。



比如说有3，7，9，10四个数



我们计算的时候，找到两个数直接通过加减乘除通过双目运算符直接进行计算【Ps：我们需最终要把问题落实在基本操作上，而24点游戏的基本操作就是加减乘除】



双目运算符直接进行计算，需要两个数，所以第一步，我们先要从四个数中抽出两个数进行加减乘除

四个数里面取两个数，六种取法：

3，7，9，10四个数

取两个数：3,7 	3,9 	3,10	 7,9	 7,10	 9,10



我们单拿`3,7`来看，结果为`10,-4,4,21，(不能整除)`

由两个数可以算出4~5种可能：`10,9,10`；`-4,9,10` ； `4,9,10`；`21,9,10`，不能整除。

四个变成三个数一共有24~30（6 * 4~6 * 5）种可能。【6为四个数抽出两个数的可能性】



…………以此类推…………

4个变为1个数，一共有1152~2250种变法【(C_4^2 * 4 * C_3^2* 4 * C_2^2 * 4=1152】

然后我们从这些数中寻找24，并且将其溯源，寻找他的运算符号以及从哪些数变化而来



到此，我们的基本流程几乎了解，也就是说我们对于这个问题的策略基本上可以掌握



> 算法策略和算法是有区别的,它们是算法设计中的两个方面，算法策略是面向问题的,算法是面向实现的；但二者又是不可分的,首先是通过算法策略才找出解决问题的算法，其次对于用不同算法求解的问题算法策略是自然不同的。



## 策略

我们发现，这种流程颠覆了我们正常游戏的思维。它是用最基本的加减乘除操作，因为我们发现，不管4个数是如何变化，运算的时候都是抽取两个数进行计算。并且最多计算三轮，第一轮4个数变成3个数，第二轮3个数变成2个数，第三轮2个数变成1个数。



## 算法

我们由上可以找到一个**动态数据结构**去配合实现，我们发现，在上述流程中，四个数转三个数，将会生成多个数（4~5种可能），然后在每一种可能中又包含多种可能，这种**连续一对多**的情况下，我们不由的想到一种数据结构——**树**

从`策略`可知，我们计算了三轮，所以很容易判断树的高度为4，并且这个高度为4的树的叶子结点最多为2250个、最少有1152个。

> 分析问题的过程中可能有一系列的回答或者决策。
>
> 所以这个数习惯上把它叫做分析树，也有时候把它叫做决策树
>
> 他实际上和计算机与人类在做围棋博弈的时候的那个思维方法是一样的，所以他也叫博弈树
>
> **（分析树是动态的）**

所以此类问题我们可以使用树来进行存储记录











## 操作

每个叶子结点都拥有一个int型的数据，而这些数据需要用一个int型容器进行存放，而最方便的int型容器是`vector`

```c++
struct element{
	int number;
	std::string trace;//string即为字符串
};


struct NODE{
	std::vector<element> data;
	std::vector<NODE> children;//子节点 
} ana_tree;
//定义分析（analyse）树；ADT抽象数据类型 vector<NODE>（类似于递归结构） 
```

对于分析树的根节点来说，里面拥有四个整数；而对于叶子结点来说，每个结点只有一个整数。

> 抽象数据类型（Abstract Data Type，ADT）是将数据对象、数据对象之间的关系和数据对象的基本操作封装在一起的一种表达方式，它和工程中的应用是一致的。
>
> 在工程项目中，开始编程之前，首先列出程序需要完成的功能任务，先不用管具体怎么实现，实现细节在项目后期完成，一开始只是抽象出有哪些基本操作。把这些操作项封装为抽象数据类型，等待后面具体实现这些操作。而其他对象如果想调用这些操作，只需要按照规定好的参数接口调用，并不需要知道具体是怎么实现的，从而实现了数据封装和信息隐藏。
>
> 在 C++ 中可以用类的声明表示抽象数据类型，用类的实现来实现抽象数据类型的具体操作。
>
> 
>
> ![ADT三元素示意图](https://img1.i-nmb.cn/img/1-20040912553LU.gif)
>
> 
> 抽象数据类型可以用以下的三元组来表示：
>
> ADT抽象数据类型名{
>   数据对象：<数据对象的定义>
>   数据关系：<数据关系的定义>
>   基本操作：<基本操作的定义>
> } ADT抽象数据类型名、
>
> 
>
> 引用于：[抽象数据类型（ADT）是什么？ (biancheng.net)](http://c.biancheng.net/view/7526.html)



定义好树之后，我们开始在main函数中初始化，先给ana_tree中存放两个值

```c++
int main(){
	ana_tree.data = {3,6};
	step(ana_tree);
	for(auto child:ana_tree.children){
		for(auto num:child.data){
			printf("%d",num);
		}
	}
	return 0;
}
```



### step

其中step中的需要的操作为：n个数中取出两个，然后这两个和剩下的哪些没有取出的数变成4~5个子节点。



#### n个数中取出两个数

实现代码如下

```c++
void step(NODE& tree){
	for(auto i=tree.data.begin();i!=tree.data.end();++i){
		for(auto j=i+1;j!=tree.data.end();++j)
	}
}//类似于冒泡排序循环
```

#### n个数转换为n-1

在前文介绍中，我们推断2个数合成1个数一共有4~5种可能，那么我们设定每个非叶子节点有5个子节点（如下代码中`t1,t2,t3,t4,t5;`）并且使用`.data.push_back`将加减乘除的得数赋予`t1,t2,t3,t4,t5;`，其次使用`tree.children.push_back`将`t1,t2,t3,t4,t5;`作为孩子结点，其中，在进行除法（`t5`）时需要进行**判断除数是否为0以及是否能够整除**

```C++
void step(NODE& tree){
	for(auto i=tree.data.begin();i!=tree.data.end();++i){
		for(auto j=i+1;j!=tree.data.end();++j){
			NODE t1,t2,t3,t4,t5;//孩子结点 
			int x=*i,y=*j;
			t1.data.push_back(x+y); 
			t2.data.push_back(x-y); 
			t3.data.push_back(y-x); 
			t4.data.push_back(x*y); 
			tree.children.push_back(t1);
			tree.children.push_back(t2);
			tree.children.push_back(t3);
			tree.children.push_back(t4);
			
			
			if(x&&y/*排除0*/)
				if(x%y==0){
					t5.data.push_back(x/y); 
					tree.children.push_back(t5);
				}
					
				else if(y%x==0){
					t5.data.push_back(y/x); 
					tree.children.push_back(t5);
				}
		}
	}
}
```



此时我们的`main`函数中只在根节点中存放了两个数，为了验证step函数是否正确，我们需要一个输出

```c++
int main(){
	ana_tree.data = {3,7};
	step(ana_tree);
	for(auto child:ana_tree.children){
		for(auto num:child.data){
			printf("%d\t",num);
		}
		printf("\n");
	}
	return 0;
} 
```

> child就是每个子节点，num是子节点中所有的数；然后把每个子节点的数进行输出



#### 将n-2个数加入到子节点

此时我们的程序可以计算2个数，但是我们还剩下了n-2（设最初有n个数）个数还没有放入子节点，此时这个n是个变量（我们在编写程序的时候没有确定n的个数），所以我们需要加入一个`for(auto k=tree.data.begin();k!=tree.data.end();++k)`循环，其中`if(k==i||k==j) continue;`去除i,j,将剩下的存入t1-t5；

将x记为i的数值，y记为j的数值`int x=i->number,y=j->number;`

然后在t1~t5中储入格式为`{x+y,make_trace(i,"+",j)}`来记录加减乘除的符号方便溯源

```c++
void step(NODE& tree){
	for(auto i=tree.data.begin();i!=tree.data.end();++i){
		for(auto j=i+1;j!=tree.data.end();++j){
			NODE t1,t2,t3,t4,t5;//孩子结点 
			for(auto k=tree.data.begin();k!=tree.data.end();++k){
				if(k==i||k==j) continue;
				t1.data.push_back(*k); 
				t2.data.push_back(*k); 
				t3.data.push_back(*k); 
				t4.data.push_back(*k);
				t5.data.push_back(*k);
			}
            
			int x=i->number,y=j->number;
			t1.data.push_back({x+y,make_trace(i,"+",j)}); 
			t2.data.push_back({x-y,make_trace(i,"-",j)}); 
			t3.data.push_back({y-x,make_trace(j,"-",i)}); 
			t4.data.push_back({x*y,make_trace(i,"*",j)}); 			
			
			tree.children.push_back(t1);
			tree.children.push_back(t2);
			tree.children.push_back(t3);
			tree.children.push_back(t4);
			
			if(x&&y/*排除0*/)
				if(x%y==0){
					t5.data.push_back({x/y,make_trace(i,"/",j)}); 
					tree.children.push_back(t5);
				}
					
				else if(y%x==0){
					t5.data.push_back({y/x,make_trace(j,"/",i)}); 
					tree.children.push_back(t5);
				}
		}
	}
}
```



在`main`函数中

```c++
int main(){
	printf("请输入四个数："); 
	for(int i = 0;i<4;++i){
		int n;
		scanf("%d",&n);
		ana_tree.data.push_back({n,std::to_string(n)});
	}
	
	step(ana_tree);
	for(NODE& child2: ana_tree.children){
		step(child2);
	}
	for(NODE& child2: ana_tree.children){
		for(NODE& child3: child2.children){
			step(child3);
		}
	}
	
	
	
	int count=0,j=0;
	for(auto child2:ana_tree.children){
		for(auto child3:child2.children){
			for(auto child4:child3.children){
				if(child4.data.begin()->number!=24) continue;
				printf("第%d组解法：%s\n",++count,child4.data.begin()->trace.c_str());
			}
		}
	}
		if(count==0){
			printf("无解\n"); 
		}
		
	return 0;
} 
```





## 完整代码

```c++
#include<stdio.h>
#include<vector>
#include<string>

struct element{
	int number;
	std::string trace;
};


struct NODE{
	std::vector<element> data;
	std::vector<NODE> children;
} ana_tree;

std::string make_trace(	std::vector<element>::iterator i,std::string op,std::vector<element>::iterator j){
	
	return "("+i->trace+"+"+j->trace+")";
}

void step(NODE& tree){
	for(auto i=tree.data.begin();i!=tree.data.end();++i){
		for(auto j=i+1;j!=tree.data.end();++j){
			NODE t1,t2,t3,t4,t5;
			for(auto k=tree.data.begin();k!=tree.data.end();++k){
				if(k==i||k==j) continue;
				t1.data.push_back(*k); 
				t2.data.push_back(*k); 
				t3.data.push_back(*k); 
				t4.data.push_back(*k);
				t5.data.push_back(*k);
				
			}
			int x=i->number,y=j->number;
			t1.data.push_back({x+y,make_trace(i,"+",j)}); 
			t2.data.push_back({x-y,make_trace(i,"-",j)}); 
			t3.data.push_back({y-x,make_trace(j,"-",i)}); 
			t4.data.push_back({x*y,make_trace(i,"*",j)}); 			
			

			tree.children.push_back(t1);
			tree.children.push_back(t2);
			tree.children.push_back(t3);
			tree.children.push_back(t4);
			
			
			if(x&&y/*排除0*/)
				if(x%y==0){
					t5.data.push_back({x/y,make_trace(i,"/",j)}); 
					tree.children.push_back(t5);
				}
					
				else if(y%x==0){
					t5.data.push_back({y/x,make_trace(j,"/",i)}); 
					tree.children.push_back(t5);
				}
		}
	}
}

int main(){
	printf("请输入四个数："); 
	for(int i = 0;i<4;++i){
		int n;
		scanf("%d",&n);
		ana_tree.data.push_back({n,std::to_string(n)});
	}
	
	step(ana_tree);
	for(NODE& child2: ana_tree.children){
		step(child2);
	}
	for(NODE& child2: ana_tree.children){
		for(NODE& child3: child2.children){
			step(child3);
		}
	}
	
	
	
	int count=0,j=0;
	for(auto child2:ana_tree.children){
		for(auto child3:child2.children){
			for(auto child4:child3.children){
				if(child4.data.begin()->number!=24) continue;
				printf("第%d组解法：%s\n",++count,child4.data.begin()->trace.c_str());
			}
		}
	}
		if(count==0){
			printf("无解\n"); 
		}
		
	return 0;
} 
```


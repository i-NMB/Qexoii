---
title: rand随机函数——MATLAB函数
date: 2022-08-30 19:57:49
tags:
- MATLAB
- 数学建模
keywords: [数学建模, MATLAB, rand随机函数]
description: rand函数拥有三种形式，分别是rand、randn、randi。那么，他们仨有什么不同吗？
---

我们有一串代码

```matlab
E = zeros(10,5,3) ;
E(:,:,1) = rand(10,5);
E(:,:,2) = randi(99,10,5);
E(:,:,3) = randn(10,5);
```



那么这串代码的具体含义是什么呢？

## 1. E = zeros(10,5,3) ;

这串代码是一个赋值代码，`zeros函数`将赋予10行5列、维度为3的一个0矩阵；

执行后结果为：

<img src="https://img1.i-nmb.cn/img/image-20220830224403682.png" alt="运行结果" style="zoom:80%;" />

## 2. rand函数

rand函数分为3种，分别是rand、randn、randi，他们都用来制造伪随机数

> ### 伪随机数
>
> 伪随机数是用确定性的算法计算出来自[0,1]均匀分布的随机数序列。并不真正的随机，但具有类似于随机数的统计特征，如均匀性、独立性等。在计算伪随机数时，若使用的初值（种子）不变，那么伪随机数的数序也不变。



### rand

rand生成均匀分布的伪随机数。分布在(0~1)之间

使用方法：`rand(行数,列数)`

> rand(RandStream,m,n)利用指定的RandStream(我理解为种子)生成伪随机数

运行代码

```matlab
E = zeros(10,5,3) ;
E(:,:,1) = rand(10,5)
```

结果如下

<img src="https://img1.i-nmb.cn/img/image-20220830224939380.png" alt="结果" style="zoom:80%;" />



### randi

`randi`函数用来生成特定大小区间的均匀分布的伪随机数

主要语法:`randi (iMax)`在开区间`(0,iMax)`生成均匀分布的伪随机整数
				`randi (iMax,m,n)`在开区间`(0,iMax)`生成m行n列随机矩阵

​				`randi([iMin,iMax],m,n)`在开区间`(iMin，iMax)`生成m行n列型随机矩阵

运行代码

```matlab
E = zeros(10,5,3) ;
E(:,:,2) = randi(99,10,5)
```

结果如下：

<img src="https://img1.i-nmb.cn/img/image-20220830230028963.png" alt="结果" style="zoom:80%;" />

### randn

randn函数生成标准正态分布的伪随机数（均值为0．方差为1)

主要语法:和rand函数一样

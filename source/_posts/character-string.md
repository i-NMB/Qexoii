---
title: Java 字符串—JAVA语言基础
date: 2022-04-23 23:44:03
tags: 
- Eclipse
- Java
description: 字符串是Java程序中经常处理的对象，如果字符串运用得不好，将影响到程序运行的效率。</br>（本文章参考《Java从入门到精通 第5版 明日科技》。故不采用 BY-NC-SA 许可协议）
---

本篇从创建字符串开始向读者介绍字符串本身的特性，以及字符串上可用的几个操作等。

通过阅读本章，您可以：

​	掌握字符串的创建方式

​	理解字符串连接的方式

​	掌握获取字符串信息的方式

​	掌握字符串的常用操作 

​	掌握字符串的格式化方法

​	理解正则表达式

​	掌握字符串生成器的用法

## String类

前面的章节中介绍了char类型，它只能表示单个字符，不能表示由多个字符连接而成的字符串。

在Java语言中将字符串作为对象来处理， 可以通过java.lang包中的String类来创建字符串对象

### 声明字符串

在Java语言中字符串必须包含在一对双引号（" "）之内。

如：`"23.23"、"ABCDE"、"你好"`

可以通过以下语法格式来声明字符串变量：

```java
String str ;
```

String：指定该变量为字符串类型。

str：任意有效的标识符，表示字符串变量的名称。

> 声明字符串变量必须经过初始化才能使用，否则编译器会报出“变量未被初始化错误”。

### 创建字符串

String类的常用构造方法如下：

（1） String(char a[])

用一个字符数组a创建String对象，实例代码如下：

![image-20220423235011146](https://img.i-nmb.cn/inmb/image-20220423235011146.png)



（2） String(char a[], int offset, int length)

提取字符数组a中的一部分创建一个字符串对象。参数offset表示开始截取字符串的位置，length表示截取字符串的长度。

![image-20220423235304336](https://img.i-nmb.cn/inmb/image-20220423235304336.png)



除通过以上几种使用String类的构造方法来创建字符串变量外，还可通过字符串常量的引用赋值给一个字符串变量。

<u>引用字符串常量来创建字符串变量，实例代码如下</u>

```java
String str1,str2;
str1 = "We are students" srt2 = "We are students"
```

## 连接字符串

对于已声明的字符串，可以对其进行相应的操作。连接字符串就是字符操作中较简单的一种。

### 连接多个字符串

使用“+”运算符可实现连接多个字符串的功能。“+”运算符可以连接多个运算符并产生一个String对象。



<img src="https://img.i-nmb.cn/inmb/image-20220424000452690.png" alt="在项目中创建类Join，在主方法中创建String型变量，并将字符变量连接的结果输出" style="zoom:120%;" />

![结果](https://img.i-nmb.cn/inmb/image-20220424000502955.png)

> Java中一句相连的字符串不能分开在两行中写。例如，下列语句的写法就是错误的。
>
> System.out.println("I like Java")
>
>  
>
> 如果一个字符串太长，为了便于阅读，必须将这个字符串分在两行上书写。则需要使用“+”将两个字符串连起来，之后在加号处换行。因此，上面的语句可以修改为：
>
> System.out.println("I like"+ "Java");



### 连接其他数据类型

字符串也可同其他基本数据类型进行连接。字符串同这些数据类型数据进行连接，会将这些数据直接转换成字符串

<img src="https://img.i-nmb.cn/inmb/image-20220424000629117.png" alt="在项目中创建类Link，在主方法中创建数值型变量，实现将字符串与整型、浮点型变量相连的结果输出" style="zoom:150%;" />

本实例实现的是将字符串常量与整型变量booktime和浮点型变量practice相连后的结果输出。在这里booktime和practice都不是字符串，当它们与字符串相连时会自动调用toString()方法，将其转换成字符串形 式，然后参与连接。

![结果](https://img.i-nmb.cn/inmb/image-20220424000647412.png)

## 获取字符串信息

字符串作为对象，可通过相应方法获取字符串的有效信息，如获取某字符串的长度、某个索引位置的字符等。

### 获取字符串长度

使用String类的length()方法可获取声明的字符串对象的长度。

语法：

```java
str.length();
```

其中，str为字符串对象

例如：

```java
String str = "We are students";
int size = str.length();
```

### 字符串查找

String类提供了两种查找字符串的方法，即indexOf()与lastIndexOf()

（1） indexOf(String s)

该方法用于返回参数字符串s在指定字符串中首次出现的索引位

置。当调用字符串的indexOf()方法时，会从当前字符串的开始位置搜索

s的位置；如果没有检索到字符串s，该方法的返回值是-1。

语法如下：`str.indexOf(substr)`

str：任意字符串对象。

substr：要搜索的字符串。

例如：

```java
String str = "We are students";
int size = str.indexOf("a")
```

代码查找到a在字符串的位置（从0开始，直到3，所以size变量是3）

（1） lastIndexOf(String str)

 

该方法用于返回指定字符串最后一次出现的索引位置。当调用字符串的lastIndexOf()方法时，会从当前字符串的开始位置检索参数字符串str，并将最后一次出现str的索引位置返回。如果没有检索到字符串str，该方法返回-1。

语法如下：

```java
str. lastIndexOf(substr)
```

在项目中创建类Text，在主方法中创建String对象，使用lastIndexOf()方法查看字符串str中空字符串的位置，然后输出字符串的长度，看它们是否相同。

<img src="https://img.i-nmb.cn/inmb/image-20220424001425783.png" alt="实例" style="zoom:150%;" />

结果：

![结果](https://img.i-nmb.cn/inmb/image-20220424001457672.png)

### 获取指定索引位置的字符

使用charAt()方法可将指定索引处的字符返回。语法如下：

![img](https://img.i-nmb.cn/inmb/wps20.png)

str：任意字符串

index：整型值，用于指定要返回字符的下标

<img src="https://img.i-nmb.cn/inmb/image-20220424001611351.png" alt="在项目中创建类Ref，在主方法中创建String对象，使用charAt()方法查看字符串str中索引位置是6的字符。" style="zoom:150%;" />

![运行结果](https://img.i-nmb.cn/inmb/image-20220424001627942.png)

## 字符串操作

String类中包含了很多方法，允许程序员对字符串进行操作来满足实际编程中的需要。

### 获取子字符串

通过String类的substring()方法可对字符串进行截取。这些方法的共同点就是都利用字符串的下标进行截取，且应明确字符串下标是从0开始的。

substring()方法被两种不同的方法重载，来满足不同的需要。

#### （1） substring(int beginIndex)

该方法返回的是从指定的索引位置开始截取直到该字符串结尾的子串。

语法如下：

```java
str.substring(int beginIndex)
```

其中，beginIndex指定从某一索引处开始截取字符串

例如

<img src="https://img.i-nmb.cn/inmb/image-20220424001745519.png" alt="实例" style="zoom:150%;" />

<img src="https://img.i-nmb.cn/inmb/image-20220424001758591.png" alt="使用substring(beginIndex)截取字符串的过程" style="zoom:150%;" />



ubstring() 方法返回字符串的子字符串。

##### 语法

```
public String substring(int beginIndex)

或

public String substring(int beginIndex, int endIndex)
```

##### 参数

- **beginIndex** -- 起始索引（包括）, 索引从 0 开始。
- **endIndex** -- 结束索引（不包括）。

![img](https://img.i-nmb.cn/inmb/java-substring-20201208.png)

##### 返回值

子字符串。

##### 实例

```java
public class RunoobTest {
    public static void main(String args[]) {
        String Str = new String("This is text");
 
        System.out.print("返回值 :" );
        System.out.println(Str.substring(4) );
 
        System.out.print("返回值 :" );
        System.out.println(Str.substring(4, 10) );
    }
}
```



```java
返回值 : is text
返回值 : is te
```





#### （2） substring(int beginIndex, int endIndex) 

该方法返回的是从字符串某一索引位置开始截取至某一索引位置结束的子串。

语法如下：



```java
substring(int beginIndex, int endIndex)
```



<img src="https://img.i-nmb.cn/inmb/image-20220424001903645.png" alt="在项目中创建类Subs，在主方法中创建String对象，实现使用substring()方法对字符串进行截取，并将截取后形成的新串输出。" style="zoom:150%;" />

![运行结果](https://img.i-nmb.cn/inmb/image-20220424001914462.png)

### 去除空格

trim()方法返回字符串的副本，忽略前导空格和尾部空格

```java
str.trim()
```

<img src="https://img.i-nmb.cn/inmb/image-20220424002457196.png" alt="在项目中创建类Blak，在主方法中创建String对象，将字符变量原来的长度与去掉前导和尾部空格后的长度输出。" style="zoom:150%;" />

![运行结果](https://img.i-nmb.cn/inmb/image-20220424002510820.png)

### 字符串替换

语法如下：

```java
str.replace(char oldChar,char newChar)
```

oldChar：要替换的字符或字符串

newChar：用于替换原来字符串的内容

replace()方法返回的结果是一个新的字符串。如果字符串oldChar没有出现在该对象表达式中的字符串序列中，则将原字符串返回。

<img src="https://img.i-nmb.cn/inmb/image-20220424002614981.png" alt="在项目中创建类NewStr，在主方法中创建String型变量，将字符变量中的字母a替换成A后的结果输出。" style="zoom:150%;" />

![运行结果](https://img.i-nmb.cn/inmb/image-20220424002625939.png)

### 判断字符串的开始与结尾

startsWith()方法与endsWith()方法分别用于判断字符串是否以指定的内容开始或结束。这两个方法的返回值都为boolean类型。

#### （1） startsWith()方法

该方法用于判断当前字符串对象的前缀是否为参数指定的字符串。

语法如下：

![](https://img.i-nmb.cn/inmb/wps21.png)

#### （2） endsWith()方法

该方法用于判断当前字符串是否为以给定的子字符串结束。

语法如下：

![](https://img.i-nmb.cn/inmb/wps22.png)

<img src="https://img.i-nmb.cn/inmb/image-20220424002836861.png" alt="在项目中创建类StartOrEnd，在主方法中创建String型变量，并判断变量的前导和后置字符串。" style="zoom:150%;" />

![运行结果](https://img.i-nmb.cn/inmb/image-20220424002849915.png)

### 判断字符串是否相等

对字符串对象进行比较不能简单地使用比较运算符“==”，因为比较运算符比较的是两个字符串的地址是否相同。即使两个字符串的内容相同，两个对象的内存地址也是不同的，使用比较运算符仍然会返回 false。

使用比较运算符比较两个字符串，实例代码如下：

```java
String tom = new String("I am a student");
String jerry = new String("I am a student");
boolean b = (tom == jerry);
```

此时，布尔型变量b的值为false，因为字符串是对象，tom、jerry是引用。

![image-20220424003004819](https://img.i-nmb.cn/inmb/image-20220424003004819.png)



因此，要比较两个字符串内容是否相等，应使用equals()方法和

equalsIgnoreCase()方法。

#### （1） equals()方法

如果两个字符串具有相同的字符和长度，则使用equals()方法进行比较时，返回true。

语法如下

```
str.equals(String otherstr)
```

其中，str、otherstr是要比较的两个字符串对象。

#### （2） equalsIgnoreCase()方法

使用equals()方法对字符串进行比较时是区分大小写的，而使用equalsIgnoreCase()方法是在忽略了大小写的情况下比较两个字符串是否相等，返回结果仍为boolean类型。

语法如下

```java
str.equalsIgnoreCase(String otherstr)
```

其中，str、otherstr是要比较的两个字符串对象。

<img src="https://img.i-nmb.cn/inmb/image-20220424003252863.png" alt="在项目中创建类Opinion，在主方法中创建String型变量，实现判断两个字符串是否相等，并将结果输出。" style="zoom:150%;" />

![运行结果](https://img.i-nmb.cn/inmb/image-20220424003419680.png)

### 按字典顺序比较两个字符串

compareTo()方法为按字典顺序比较两个字符串，该比较基于字符串中各个字符的Unicode值，按字典顺序将此String对象表示的字符序列与参数字符串所表示的字符序列进行比较。



如果按字典顺序此String对象位于参数字符串之前，则比较结果为一个负整数；如果按字典顺序此String对象位于参数字符串之后，则比较结果为一个正整数；如果这两个字符串相等，则结果为0。



语法如下：

```java
str.compareTo(String otherstr)
```

其中，str、otherstr是要比较的两个字符串对象。

![在项目中创建类Wordbook，在主方法中创建String变量，使用compareTo()方法将字符变量进行比较，并将比较结果输出。](https://img.i-nmb.cn/inmb/image-20220424020644862.png)

<img src="https://img.i-nmb.cn/inmb/image-20220424020708809.png" alt="运行结果" style="zoom:50%;" />



compareTo() 方法用于将 Number 对象与方法的参数进行比较。可用于比较 Byte, Long, Integer等。

该方法用于两个相同数据类型的比较，两个不同类型的数据不能用此方法来比较。



##### 参数

**referenceName** -- 可以是一个 Byte, Double, Integer, Float, Long 或 Short 类型的参数。

##### 返回值

- 如果指定的数与参数相等返回 0。
- 如果指定的数小于参数返回 -1。
- 如果指定的数大于参数返回 1。

##### 实例

```java
public class Test{
	public static void main(String args[]){
	Integer x = 5;
	System.out.println(x.compareTo(3));
	System.out.println(x.compareTo(5));
	System.out.println(x.compareTo(8));
	}
}
```

编译以上程序，输出结果为：

```
1
0
-1
```

### 字母大小写转换

字符串的toLowerCase()方法可将字符串中的所有字符从大写字母改写为小写字母，而toUpperCase()方法可将字符串中的小写字母改写为大写字母。

#### （1） toLowerCase()方法

该方法将String转换为小写。如果字符串中没有应该被转换的字符，则将原字符串返回；否则将返回一个新的字符串，将原字符串中每个该进行小写转换的字符都转换成等价的小写字符。字符长度与原字符长度相同。

```java
str.toLowerCase()
```

其中，str是要进行转换的字符串。

##### 返回值

转换为小写的字符串。

##### 实例

```java
public class Test {
    public static void main(String args[]) {
        String Str = new String("WWW.I-NMB.COM");
        System.out.print("返回值 :" );
        System.out.println( Str.toLowerCase() );
    }
}
```

以上程序执行结果为：

```
返回值 :www.i-nmb.com
```

#### （2） toUpperCase()方法

该方法将String转换为大写。如果字符串中没有应该被转换的字符，则将原字符串返回；否则返回一个新字符串，将原字符串中每个该进行大写转换的字符都转换成等价的大写字符。新字符长度与原字符长度相同。

```java
str.toUpperCase()
```

> 使用toLowerCase()方法和toUpperCase()方法进行大小写转换时， 数字或非字符不受影响

##### 返回值

字符转换为大写后的字符串。

##### 实例

```java
public class Test {
    public static void main(String args[]) {
        String Str = new String("www.i-nmb.com");
        System.out.print("返回值 :" );
        System.out.println( Str.toUpperCase() );
    }
}
```

以上程序执行结果为：

```
返回值 :WWW.I-NMB.COM
```



### 字符串分割

使用split()方法可以使字符串按指定的分割字符或字符串对内容进行分割，并将分割后的结果存放在字符串数组中。split()方法提供了以下两种字符串分割形式。

#### （1） split(String sign)

该方法可根据给定的分割符对字符串进行拆分。

##### 语法

```
str.split(String sign)
```

sign为分割字符串的分割符，也可以使用正则表达式

> 没有统一的对字符进行分割的符号。如果想定义多个分割符，可使用符号“|”。例如，“,|=”表示分割符分别为“,”和“=”。



##### （2） split(String sign,int limit)

该方法可根据给定的分割符对字符串进行拆分，并限定拆分的次数。

##### 语法

```java
str.split(String sign,int limit)
```

sign：分割字符串的分割符，也可以使用正则表达式

limit：限制的分割次数

##### 例 1

使用 split() 方法对字符串进行分割的实例如下：

```java
public static void main(String[] args)
{
    String Colors="Red,Black,White,Yellow,Blue";
    String[] arr1=Colors.split(",");    //不限制元素个数
    String[] arr2=Colors.split(",",3);    //限制元素个数为3
    System.out.println("所有颜色为：");
    for(int i=0;i<arr1.length;i++)
    {
        System.out.println(arr1[i]);
    }
    System.out.println("前三个颜色为：");
    for(int j=0;j<arr2.length;j++)
    {
        System.out.println(arr2[j]);
    }
}
```

输出结果如下：

```java
所有颜色为：
Red
Black
White
Yellow
Blue
前三个颜色为：
Red
Black
White,Yellow,Blue
```

#### 



## 格式化字符串

String类的静态format()方法用于创建格式化的字符串。format()方法有两种重载形式。

#### （1） format(String format,Object…args)

该方法使用指定的格式字符串和参数返回一个格式化字符串，格式化后的新字符串使用本地默认的语言环境。

##### 语法

```java
str.format(String format,Object…args)
```

format：格式字符串

args：格式字符串中由格式说明符引用的参数。如果还有格式说明符以外的参数，则忽略这些额外的参数。此参数的数目是可变的，可以为0

#### （2） format(Local l,String format,Object…args)

l ：格式化过程中要应用的语言环境。如果l为null，则不进行本地化。

### 日期和时间字符串格式化

在应用程序设计中，经常需要显示时间和日期。如果想输出满意的日期和时间格式，一般需要编写大量的代码经过各种算法才能实现。format()方法通过给定的特殊转换符作为参数来实现对日期和时间的格式化。

#### **1.** 日期格式化

<img src="https://img.i-nmb.cn/inmb/image-20220424022909309.png" alt="返回一个月中的天数，实例代码" style="zoom:150%;" />

上述代码中变量s的值是当前日期中的天数，如今天是15号，则s的值为15；%te是转换符。常用的日期格式化转换符如表

![常用的日期格式化转换符](https://img.i-nmb.cn/inmb/image-20220424023144063.png)

![在项目中创建类Eval，实现将当前日期信息以4位年份、月份全称、2位日期形式输出](https://img.i-nmb.cn/inmb/image-20220424023226684.png)

![结果](https://img.i-nmb.cn/inmb/image-20220424023241895.png)

#### **2.** 时间格式化

使用format()方法不仅可以完成日期的格式化，也可以实现时间的格式化。时间格式化转换符要比日期转换符更多、更精确，它可以将时间格式化为时、分、秒、毫秒。



### 常规类型格式化

常规类型的格式化可应用于任何参数类型，可通过如表5.4所示的转换符来实现。

![常规转换符](https://img.i-nmb.cn/inmb/image-20220424023415012.png)

<img src="https://img.i-nmb.cn/inmb/image-20220424023503409.png" alt="在项目中创建类General，在主方法中实现不同数据类型到字符串的转换。" style="zoom:150%;" />

![运行结果](https://img.i-nmb.cn/inmb/image-20220424023521017.png)





## 使用正则表达式

正则表达式通常被用于判断语句中，用来检查某一字符串是否满足某一格式。正则表达式是含有一些具有特殊意义字符的字符串，这些特殊字符称为正则表达式的元字符。例如，“\\d”表示数字0~9中的任何一个，“\d”就是元字符。

![正则表达式中的元字符](https://img.i-nmb.cn/inmb/image-20220424023743825.png)

---
title: JAVA语言基础
date: 2022-04-23 14:12:34
tags: 
- Eclipse
- Java
description: 要掌握并熟练应用Java语言，就需要对Java语言的基础进行充分的了解。</br>（本文章参考《Java从入门到精通 第5版 明日科技》。故不采用 BY-NC-SA 许可协议）
---

通过阅读本篇，您可以：
　了解Java主类结构

　了解Java语言中的基本数据类型

　理解Java语言中的常量与变量

　掌握Java语言运算符的使用

　理解Java语言数据类型的转换

　了解Java语言中的代码注释与编码规范

## Java主类结构

Java语言是面向对象的程序设计语言，Java程序的基本组成单元是类，类体中又包括属性与方法两部分。每一个应用程序都必须包含一个main()方法，含有main()方法的类称为主类。

在Eclipse下依次创建项目item、包Number和类Frist。创建完成后，即可得到以下代码：

```java
package Number;

public class Frist {

}
```

![](https://img.i-nmb.cn/inmb/image-20220417144500802.png)

在类体中输入以下代码，实现在控制台上输出“你好Java”

```java
package Number;
public class Frist {
	static String s1 ="你好";
	public static void main(String[] args){
		String s2 = "Java";
		System.out.println(s1);
		System.out.println(s2);
	}
}
```



<img src="https://img.i-nmb.cn/inmb/image-20220417150715988.png" alt="输出“你好Java”" style="zoom:200%;" />

文件名必须和类名Frist同名，即Frist.java。还要注意大小写，Java 是区分大小写的。 



### 包声明 

一个Java应用程序是**由若干个类组成**的,上述例子的包声明就是“package Number; ”，因为package就是包声明

<img src="https://img.i-nmb.cn/inmb/image-20220417195929441.png" alt="image-20220417195929441" style="zoom:150%;" />





### 类声明 

通常将类的<u>属性</u>称为类的<u>全局变量</u>（成员变量），将**方法中**的属性称为**局部变量**。

上例的s1为成员变量而s2属于局部变量，因为s1在类中声明并没有任何方法中，而s2在方法public static void main(String[] args)中



### 编写主方法 

main()方法是**类体中的主方法**。该方法从“{”开始，至“}”结束。

其中main()方法中的权限修饰符为public，静态修饰符为static、返回值修饰符为void。Java程序中的main()方法必须声明为public static void。

main()方法是程序开始执行的位置。

### 导入**API**类库 

在Java语言中可以通过import关键字<u>导入相关的类</u>。在JDK的API中（应用程序接口）提供了如java.awt、java.io等130多个包。

> 可以通过 JDK的API文档来查看这些类，其中主要包括类的继承结构、类的应用、成员变量表、构造方法表等，并对每个变量的使用目的作了详细的描述，API文档是程序开发人员不可或缺的工具。 



## 基本数据类型

在Java中有8种基本数据类型来存储数值、字符和布尔值

<img src="https://img.i-nmb.cn/inmb/image-20220417211300924.png" alt="image-20220417211300924" style="zoom:50%;" />



### 整数类型

整数类型用来存储整数数值，即没有小数部分的数值。可以是正数，也可以是负数。

#### 十进制：

除了数字0，不能以0作为其他十进制数的开头



#### 八进制：

八进制：如0123（转换成十进制数为83）、-0123（转换成十进制数为-83），**八进制数必须以0开头。** 



#### 十六进制

十六进制：如0x25（转换成十进制数为37）、0Xb01e（转换成十进制数为45086）。十六进制以 0X或者0x 开头



其中整数类型可分为byte、short、int和 long 4种类型，

![image-20220417212043590](https://img.i-nmb.cn/inmb/image-20220417212043590.png)



### 浮点类型

浮点类型表示有小数部分的数字。Java语言中浮点类型分为单精度浮点类型（float）和双精度浮点类型（double）。

![image-20220417212255254](https://img.i-nmb.cn/inmb/image-20220417212255254.png)



在默认情况下，小数都被看作double型，**若使用float型小数，则需要在小数后面添加F或f**

可以使用后缀d或D来明确表明这是一个double类型数据，不加d不会出错，但声明float型变量时如果不加f，系统会认为变量是double类型，从而出错。

```java
float f1 = 13.23f;
double d1 = 4562.12d;
double d2 = 45678.1564;
```



### 字符类型

#### char型

字符类型（char）用于存储单个字符，占用16位（两个字节）内存

```java
char x = 'a';
//char x = 97;
```

同C和C++语言一样，Java语言也可以把字符作为整数对待。由于 unicode编码采用无符号编码，可以存储65536个字符(0x0000~0xffff）



#### 转义字符

<img src="https://img.i-nmb.cn/inmb/image-20220417213021108.png" alt="转义字符" style="zoom:70%;" />



```java
char c1 = '';				//将转义字符叶’赋值给变量c1
char char1 = 'lu2605';		//将转义字符lu2605’赋值给变量char1
System.out.println(c1);		//输出结果\
System.out.println(char1);	//输出结果★
```



#### 布尔类型

布尔类型又称逻辑类型，通过关键字boolean来定义布尔类型变量， 只有true和false两个值别代表布尔逻辑中的“真”和“假”。

```java
boolean b;			//定义布尔型变量b
boolean b1,b2;		//定义布尔型变量b1、b2
boolean b = true;	//定义布尔型变量b，并赋给初值true
```



## 变量与常量

### 标识符和关键字

 

#### 标识符

标识符就好似一个名字来标识类名、变量名、方法名、数组名、文件名

Java语言规定**标识符由任意顺序的字母、下画线（_）、美元符号（$）和数字组成**，并且**第一个字符不能是数字**。标识符<u>不能是Java中的保留关键字</u>。

合法标识符：

```
name
user_age
$page
```



非法标识符：

```
4word
String
User name
```



> 在Java语言中标识符中的字母是严格区分大小写的，如good和Good 是不同的两个标识符。
>
> Java语言中的字母不仅包括通常的拉丁文字a、 b、c等，还包括汉字、日文以及其他许多语言中的文字。



#### 关键字

关键字是Java语言中已经被赋予特定意义的一些单词

![关键字表](https://img.i-nmb.cn/inmb/image-20220418141622697.png)



### 声明变量

定义变量就是要告诉编译器（compiler）这个变量的数据类型，这样，编译器就会分配对应的空间给它，并且让编译器知道他能存放的数据。

在程序运行过程中，**空间内的值是变化的，这个内存空间就称为变量**。为了便于操作，给这个空间取个名字，称为变量名。变量的命名必须是合法的标识符。

在声明变量时可以是没有赋值，也可以是直接赋给初值。

```java
int a;		//声明一个名称为a的 int 型变量
char b='r'	//声明一个名称叫b的 char型变量并且将字母'r'赋值给b
```

对于变量的命名并不是随意的，应遵循以下几条规则： 

> 变量名必须是一个有效的标识符。
>
> 变量名不可以使用Java中的关键字。
>
> 变量名不能重复。
>
> 应选择有意义的单词作为变量名。



### 声明常量

在程序运行过程中一直不会改变的量称为常量（constant），常量在整个程序中**只能被赋值一次。**

在Java语言中声明一个常量，除了要指定数据类型外，还需要通过 final关键字进行限定。声明常量的标准语法如下：

```
final 数据类型    常量名称[=值]
```

常量名通常使用大写字母，但这并不是必需的。<u>大写字母表示常量，是为了清楚地表明正在使用常量。</u>

```java
final double Pl=3.1415926D;		//声明double 型常量PI并赋值
final boolean BOOL = true;		//声明boolean型常量BOOL并赋值
```

当常量属于“成员变量”时，必须在定义时就设定它的初值，否则将会产生编译错误。

<img src="https://img.i-nmb.cn/inmb/image-20220419000545207.png" alt="例如" style="zoom:67%;" />

<img src="https://img.i-nmb.cn/inmb/image-20220419000657144.png" alt="运行结果" style="zoom:50%;" />

### 变量的有效范围

在程序中，一般会根据变量的“有效范围”将变量分为“成员变量”和“局部变量”。

![](https://img.i-nmb.cn/inmb/image-20220423213758825.png)

#### 成员变量

在<u>类体中所定义的变量</u>被称为<u>成员变量</u>，成员变量在整个类中都有效。类的成员变量又可分为两种，即<u>静态变量</u>和<u>实例变量</u>。

```java
class var{
	int x = 45; 
	static int y = 90
}
```

在上面的代码中：x为实例变量，y为静态变量（也称类变量）

就是说，如果在成员变量的类型前面加上关键字static，这样的成员变量称为**静态变量**。静态变量的有效范围**可以跨类**，甚至可达到整个应用程序之内，还能直接以“类名.静态变量”的方式在其他类内使用。



#### 局部变量

在类的方法体中定义的变量（方法内部定义，“{”与“}”之间的代码中声明的变量）称为局部变量。<u>局部变量只在当前代码块中有效</u>。在<u>类的方法</u>中声明的变量，包括方法的参数，都属于局部变量

局部变量只在当前定义的方法内有效，不能用于类的其他方法中。

局部变量可与成员变量的名字相同，此时成员变量将被隐藏，即这个（同名）成员变量在此方法中**暂时失效**。

```java
public class Val{
    static int times = 3;
    public static void main(String[] args){
        int times = 4;
        System.out.println("times的值为："+times);
    }
}
```

<img src="https://img.i-nmb.cn/inmb/image-20220423213828334.png" alt="运行结果" style="zoom:150%;" />

## 运算符

Java中提供了丰富的运算符，如赋值运算符、算术运算符、比较运算符等。

### 赋值运算符

赋值运算符以符号“=”表示，它是一个二元运算符（对两个操作数作处理），其功能是将右方操作数所含的值赋给左方的操作数。

```java
int a = 100;
```

该表达式是将100赋值给变量a。左方的操作数必须是一个变量，而右边的操作数则可以是任何表达式，包括变量（如a、number）、常量（如123、'book'）、有效的表达式（如45*12）

```java
int a = 10;	//声明int型变量a
int b = 5;	//声明int型变量b
int c = a+b;//将变量a与b运算后的结果赋值给c
```

遵循赋值运算符的运算规则，可知系统将先计算a+b的值，结果为15，然后将15赋值给变量c，因此c=15。

 

由于赋值运算符“=”处理时会先取得右方表达式处理后的结果，因此一个表达式中若含有两个以上的“=”运算符，会从**最右方的“=”开始处理**。

```java
public class Eval{
    public static void main(String[] args){
        int a,b,c;
        a = 15;
        c = b = a + 4;
        System.out.println("c的值为：" + c);
        System.out.println("b的值为：" + b);
    }
}
```

运行结果

<img src="https://img.i-nmb.cn/inmb/image-20220423215102161.png" alt="image-20220423215102161" style="zoom:150%;" />

> 在Java中可以把赋值运算符连在一起使用。如：
>
> x = y = z = 5;
>
> 在这个语句中，变量x、y、z都得到同样的值5。但在实际开发中不建议使用这种赋值语句。

### 算术运算符

Java中的算术运算符主要有+（加）、-（减）、*（乘）、/（除）、%（求余），它们都是二元运算符。Java中算术运算符的功能及使用方式如表

![Java算术运算符](https://img.i-nmb.cn/inmb/image-20220423215326446.png)

其中，“+”和“-”运算符还可以作为数据的正负符号，如+5、-7

在项目中创建类Arith，在主方法中定义变量，使用算术运算符将变量的计算结果输出。

```java
public class Arith {								//创建类
public static void main(String[] args) {			//主方法
    float number1 = 45.56f;							//声明float型变量并赋值
    int number2 = 152;								//声明int型变量并赋值
    System.out.println("和为:"+( number1 + number2));	//将变量相加之和输出
    System.out.println("差为:"+(number2 - number1));	//将变量相减之差输出
    System.out.println("积为:"+number1 * number2);	//将变量相乘的积输出
    System.out.println("商为:"+number1 / number2);	//将变量相除的商输出
}
}
```

运行结果

<img src="https://img.i-nmb.cn/inmb/image-20220423215938555.png" alt="运行结果" style="zoom:150%;" />

### 自增和自减运算符

操作元必须是一个整型或浮点型变量。自增、自减运算符的作用是使变量的值增1或减1。

当运算符在前时，先进行运算，后操作。当运算符在后时，先操作，后进行运算。

![自增或自减](https://img.i-nmb.cn/inmb/image-20220423220207437.png)

粗略地分析，++a与a++的作用都相当于a = a+1。假设a = 4，则：

![](https://img.i-nmb.cn/inmb/image-20220423220247132.png)

再看另一个语法，同样假设a = 4，则：

![](https://img.i-nmb.cn/inmb/image-20220423220304753.png)

### 比较运算符

比较运算符属于二元运算符，用于程序中的变量之间、变量和自变量之间以及其他类型的信息之间的比较。比较运算符的运算结果是boolean型。当运算符对应的关系成立时，运算结果为true，否则为 false。所有比较运算符通常作为判断的依据用在条件语句中。比较运算符共有6个，如表

<img src="https://img.i-nmb.cn/inmb/image-20220423220957332.png" alt="比较运算符" style="zoom:150%;" />

在项目中创建类Compare，在主方法中创建整型变量， 使用比较运算符对变量进行比较运算，并将运算后的结果输出。

```java
public class Compare {					//创建类
	public static void main(Stringargs){
   	 int number1 = 4;					//声明int型变量number1
   	 int number2 = 5;					//声明int型变量number2
/*依次将变量number1与变量number2的比较结果输出*/
        System.out.println("number1>number的返回值为:"+(number1 > number2));
		System.out.println("number1< number2返回值为:"+(number1 < number2));
		System.out.println("number1==number2返回值为:"+ (number1== number2));
		System.out.println("number1!=number2返回值为:"+ (number1 != number2));
		System.out.println("number1>= number2返回值为:"+(number1 >= number2));
		System.out.println("number1<=number2返回值为:"+(number1 <= number2));
	}
}
```

![运行结果](https://img.i-nmb.cn/inmb/image-20220423222700166.png)

### 逻辑运算符

返回类型为布尔值的表达式，如比较运算符，可以被组合在一起构成一个更复杂的表达式。这是通过逻辑运算符来实现的。

逻辑运算符表如下

<img src="https://img.i-nmb.cn/inmb/image-20220423222842853.png" alt="image-20220423222842853" style="zoom:100%;" />

使用逻辑运算符进行逻辑运算表如下

<img src="https://img.i-nmb.cn/inmb/image-20220423222907829.png" alt="逻辑运算符进行逻辑运算表" style="zoom:100%;" />

在项目中创建类Calculation，在主方法中创建整型变量，使用逻辑运算符对变量进行运算，并将运算结果输出。

![image-20220423223016167](https://img.i-nmb.cn/inmb/image-20220423223016167.png)

运行结果如图

![运行结果](https://img.i-nmb.cn/inmb/image-20220423223025314.png)

### 位运算符

位运算符除“按位与”和“按位或”运算符外，其他只能用于处理整数的操作数。位运算是完全针对位方面的操作。整型数据在内存中以二进制的形式表示，如int型变量7的二进制表示是00000000 00000000 00000000 00000111。

 

左边最高位是符号位，最高位是0表示正数，若为1则表示负数。负数采用补码表示，如-8的二进制表示为111111111 111111111 1111111 11111000。这样就可以对整型数据进行按位运算。

####  “按位与”运算

“按位与”运算的运算符为“&”，为双目运算符。“按位与”运算的运算法则是：如果两个整型数据a、b对应位都是1，则结果位才是1，否则为0。如果两个操作数的精度不同，则结果的精度与精度高的操作数相同。

#### “按位或”运算

“按位或”运算的运算符为“|”，为双目运算符。“按位或”运算的运算法则是：如果两个操作数对应位都是0，则结果位才是0，否则为1。如果两个操作数的精度不同，则结果的精度与精度高的操作数相同

![5&-4的运算过程](https://img.i-nmb.cn/inmb/image-20220423223701811.png)





![3|6的运算过程](https://img.i-nmb.cn/inmb/image-20220423223715541.png)

#### “按位取反”运算

“按位取反”运算也称“按位非”运算，运算符为“~”，为单目运算符。“按位取反”就是将操作数二进制中的1修改为0，0修改为1

![~7的运算过程](https://img.i-nmb.cn/inmb/image-20220423223834521.png)

#### “按位异或”运算

“按位异或”运算的运算符是“^”，为双目运算符。“按位异或”运算的运算法则是：当两个操作数的二进制表示相同（同时为0或同时为1） 时，结果为0，否则为1。若两个操作数的精度不同，则结果数的精度与精度高的操作数相同

![image-20220423223910056](https://img.i-nmb.cn/inmb/image-20220423223910056.png)

除了上述运算符之外，还可以对数据按二进制位进行移位操作。

Java中的移位运算符有以下3种。

##### 1.<<：左移

左移就是将运算符左边的操作数的二进制数据，按照运算符右边操作数指定的位数向左移动，

##### 2.\>>：右移。

右边移空的部分补0。右移则复杂一些。当使用“>>”符号时，如果最高位是0，右移空的位就填入0；如果最高位是1，右移空的位就填入1

![image-20220423224256449](https://img.i-nmb.cn/inmb/image-20220423224256449.png)

3.\>>>：无符号右移。

Java还提供了无符号右移“>>>”，无论最高位是0还是1，左侧被移空的高位都填入0。

> 移位运算符适用的数据类型有byte、short、char、int和long。
>
> 
>
> 移位可以实现整数除以或乘以2n的效果。例如，y<<2与y*4的结果相同；y>>1的结果与y/2的结果相同。总之，一个数左移n位，就是将这个数乘以2n；一个数右移n位，就是将这个数除以2n。

### 三元运算符

三元运算符的使用格式为：`条件式?值1:值2`

三元运算符的运算规则为：若条件式的值为true，则整个表达式取值1，否则取值2。例如：

```java
boolean b = 20<45?true:false;
```

如上例所示，表达式“20<45”的运算结果返回真，那么boolean型变量b取值为true；相反，表达式“45<20”返回为假，则boolean型变量b取值false。

三元运算符等价于if…else语句。

### 运算符优先级

通常优先级由高到低的顺序依次是：

**增量和减量运算>算术运算>比较运算>逻辑运算>赋值运算**

如果两个运算有相同的优先级，那么左边的表达式要比右边的表达式先被处理。

![image-20220423224741068](https://img.i-nmb.cn/inmb/image-20220423224741068.png)

## 数据类型转换

类型转换是将一个值从一种类型更改为另一种类型的过程。例如， 可以将String类型的数据“457”转换为数值型，也可以将任意类型的数据转换为String类型。

 

如果从低精度数据类型向高精度数据类型转换，则永远不会溢出， 并且总是成功的；而把高精度数据类型向低精度数据类型转换时，则会有信息丢失，有可能失败。

数据类型转换有两种方式，即**隐式转换与显式转换。**

### 隐式类型转换

从低级类型向高级类型的转换，系统将自动执行，程序员无须进行任何操作。这种类型的转换称为**隐式转换**

这些类型按精度从低到高排列的顺序为byte < short < int < long < float < double

使用int型变量为float型变量赋值，此时int型变量将隐式转换成float型变量。

![image-20220423224921618](https://img.i-nmb.cn/inmb/image-20220423224921618.png)

此时执行输出语句，y的结果将是50.0

<img src="https://img.i-nmb.cn/inmb/image-20220423224935754.png" alt="种数据类型转换的一般规则" style="zoom:150%;" />

### 显式类型转换

当把高精度的变量的值赋给低精度的变量时，必须使用显式类型转换运算（又称强制类型转换）

语法为：`(类型名)要转换的值`



将不同的数据类型进行显式类型转换

![image-20220423225119706](https://img.i-nmb.cn/inmb/image-20220423225119706.png)

执行显式类型转换时，可能会导致精度损失。除boolean类型以外其他基本类型，都能以显式类型的方法实现转换。

> 当把整数赋值给一个byte、short、int、long型变量时，不可以超出这些变量的取值范围，否则必须进行强制类型转换。例如：
>
> byte b = (byte)129;

## 代码注释与编码规范

在程序代码中适当地添加注释，可以提高程序的可读性和可维护性。好的编码规范可以使程序更易阅读和理解。

### 代码注释

通过在程序代码中添加注释可提高程序的可读性。

注释中包含了程序的信息，可以帮助程序员更好地阅读和理解程序。

在Java源程序文件的任意位置都可添加注释语句。注释中的文字Java编译器不进行编译， 所有代码中的注释文字对程序不产生任何影响。Java语言提供了3种添加注释的方法，分别为单行注释、多行注释和文档注释。

####  单行注释

 

“//”为单行注释标记，从符号“//”开始直到换行为止的所有内容均作为注释而被编译器忽略。



语法如下：



|      |                                            |
| ---- | ------------------------------------------ |
|      | ![img](https://img.i-nmb.cn/inmb/wps5.png) |

 



 

例如，以下代码为声明的int型变量添加注释：



|      |                                            |
| ---- | ------------------------------------------ |
|      | ![img](https://img.i-nmb.cn/inmb/wps6.png) |

 



 

#### 多行注释

 

“/ * * /”为多行注释标记，符号“/* ”与“*/”之间的所有内容均为注释内容。注释中的内容可以换行。

语法如下：



|      |                                            |
| ---- | ------------------------------------------ |
|      | ![img](https://img.i-nmb.cn/inmb/wps7.png) |

![img](https://img.i-nmb.cn/inmb/wps8.png)

但在多行注释中不可以嵌套多行注释，以下代码为非法：

![img](https://img.i-nmb.cn/inmb/wps10.png)

 

#### 文档注释

“/** * /”为文档注释标记。符号“/**”与“ */”之间的内容均为文档注释内容。当文档注释出现在声明（如类的声明、类的成员变量的声明、类的成员方法声明等）之前时，会被Javadoc文档工具读取作为Javadoc文档内容。文档注释的格式与多行注释的格式相同。对于初学者而言，文档注释并不是很重要，了解即可。





### 编码规范

在学习开发的过程中要养成良好的编码习惯，因为规范的代码格式会给程序的开发与日后的维护提供很大方便。

###### 每条语句要单独占一行，一条命令要以分号结束。

###### 在声明变量时，尽量使每个变量的声明单独占一行，即使是相同的数据类型也要将其放置在单独的一行上，这样有助于添加注释。对于局部变量应在声明的同时对其进行初始化。

###### Java代码中，关键字与关键字间如果有多个空格，这些空格均被视作一个。

###### 由于程序的开发与维护不能是同一个人，所以应尽量使用简单的技术完成程序需要的功能。

###### 关键的方法要多加注释，这样有助于阅读者了解代码结构

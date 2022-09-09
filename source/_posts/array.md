---
title: Java 数组—JAVA语言基础
date: 2022-04-24 10:45:43
tags: 
- Eclipse
- Java
description: 数组是最为常见的一种数据结构，是相同类型的用一个标识符封装到一起的基本类型数据序列或对象序列。</br>（本文章参考《Java从入门到精通 第5版 明日科技》。故不采用 BY-NC-SA 许可协议）
---

通过阅读本篇，您可以：

掌握一维数组的创建和使用方法

掌握二维数组的创建和使用方法

了解如何遍历数组

了解如何填充替换数组中的元素

了解如何对数组进行排序

了解如何复制数组

了解查询数组的方法





## 数组概述

数组是具有相同数据类型的一组数据的集合。数组中的每个元素具有相同的数据类型。

在Java中同样将数组看作一个对象，虽然基本数据类型不是对象，但由基本数据类型组成的数组却是对象。



## 一维数组的创建及使用

一维数组实质上是一组相同类型数据的线性集合，当在程序中需要处理一组数据，或者传递一组数据时，可以应用这种类型的数组。

### 创建一维数组

数组作为对象允许使用new关键字进行内存分配。在使用数组之前，必须首先定义数组变量所属的类型。一维数组的创建有两种形式。

#### 先声明，再用**new**运算符进行内存分配

声明一维数组有下列两种方式：

![声明一维数组](https://img.i-nmb.cn/inmb/image-20220424105130326.png)

数组元素类型决定了数组的数据类型。

它可以是Java中任意的数据类型，包括简单类型和组合类型。数组名字为一个合法的标识符，符号“[ ]”指明该变量是一个数组类型变量。单个“[ ]”表示要创建的数组是一个一维数组。

声明一维数组，实例代码

![声明一维数组，实例代码](https://img.i-nmb.cn/inmb/image-20220424105241086.png)

声明数组后，还不能立即访问它的任何元素，因为声明数组只是给出了数组名字和元素的数据类型

要想真正使用数组，还要为它分配内存空间。在为数组分配内存空间时必须指明数组的长度。

```java
数组名字 = new 数组元素的类型[数组元素的个数];
```

```java
arr = new int[5];
```

#### 声明的同时为数组分配内存

这种创建数组的方法是将数组的声明和内存的分配合在一起执行。

> 数组元素的类型 数组名 = new数组元素的类型[数组元素的个数];

```java
int month[ ] = new int[12]
```

上面的代码创建数组month，并指定了数组长度为12。这种创建数组的方法也是Java程序编写过程中普遍的做法。

### 初始化一维数组

数组与基本数据类型一样可以进行初始化操作。

数组的初始化可分别初始化数组中的每个元素。

数组的初始化有以下两种形式：

![数组的初始化](https://img.i-nmb.cn/inmb/image-20220424105806481.png)

从中可以看出，数组的初始化就是包括在大括号之内用逗号分开的表达式列表。

### 使用一维数组

在Java集合中一维数组是常见的一种数据结构。下面的实例是使用一维数组将1～12月各月的天数输出。



![在项目中创建类GetDay，在主方法中创建int型数组，并实现将各月的天数输出。](https://img.i-nmb.cn/inmb/image-20220424105929192.png)

![结果](https://img.i-nmb.cn/inmb/image-20220424105945335.png)





## 二维数组的创建及使用

如果一维数组中的各个元素仍然是一个数组，那么它就是一个二维数组。

### 二维数组的创建

二维数组可以看作是特殊的一维数组，因此，二维数组的创建同样有两种方式。

#### 先声明，再用new运算符进行内存分配

声明二维数组的语法如下：

```java
数组元素的类型 数组名字[ ][ ];

数组元素的类型[ ][ ] 数组名字;
```

例如：`int myarr[][];`



同一维数组一样，二维数组在声明时也没有分配内存空间，同样要使用new关键字来分配内存，然后才可以访问每个元素。



对于高维数组，有两种为数组分配内存的方式：

##### （1） 直接为每一维分配内存空间

为每一维数组分配内存，实例代码如下

```java
a = new int[2][4]
```

上述代码创建了二维数组a，二维数组a中包括两个长度为4的一维数组

##### （2） 分别为每一维分配内存

分别为每一维分配内存，实例代码如下

```java
a = new int[2][];

a[0] = new int[2];

a[1] = new int[3];
```

#### 声明的同时为数组分配内存

第二种方式同第一种实现的功能相同。使用这种方式为二维数组分配内存时，首先指定最左边维数的内存，然后单独地给余下的维数分配内存。

![通过第二种方式为二维数组分配内存，如图](https://img.i-nmb.cn/inmb/image-20220424110642079.png)

### 二维数组初始化

二维数组的初始化与一维数组初始化类似，同样可以使用大括号完成。

语法如下：

```java
type arrayname[][] = {value1,value2…valuen};
```

type：数组数据类型。

arrayname：数组名称，一个合法的标识符。

value：数组中各元素的值。



初始化二维数组，实例代码如下：

```java
int myarr[][] = {{12,0},{45,10}};
```

初始化二维数组后，要明确数组的下标都是从0开始。例如，上面的代码中myarr[1] [1]的值为10。

int型二维数组是以int a [][]来定义的，所以可以直接给a[x] [y]赋值。例如，给a[1]的第2个元素赋值的语句如下

```java
a[1][1] = 20
```

### 使用二维数组

二维数组在实际应用中用得非常广泛。

下面的实例就是使用二维数组输出一个3行4列且所有元素都是0的矩阵。

![在项目中创建类Matrix，在主方法中编写代码实现输出一个3行4列且所有元素都为0的矩阵。](https://img.i-nmb.cn/inmb/image-20220424111059355.png)

运行结果如图

![运行结果](https://img.i-nmb.cn/inmb/image-20220424111117262.png)

## 数组的基本操作

java.util包的Arrays类包含了用来操作数组（如排序和搜索）的各种方法，本节就将介绍数组的基本操作。

### 遍历数组

遍历数组就是获取数组中的每个元素。通常遍历数组都是使用for循环来实现。遍历一维数组很简单，也很好理解，下面详细介绍遍历二维数组的方法。

遍历二维数组需使用双层for循环，通过数组的length属性可获得数组的长度。

```java
public class Trap{
    public static void main(String[] args){
        int b[][] = new int[][]{{1},{2,3},{4,5,6}};
        for(int k=0;k<b.length;k++){
            for(int c=0;c<b[k].length;c++){
                System.out.println(b[k][c]);
            }
            System.out.println();
        }
    }
}
```

运行结果如图

![运行结果](https://img.i-nmb.cn/inmb/image-20220424111809622.png)







在遍历数组时，使用foreach语句可能会更简单。下面的实例就是通过foreach语句遍历二维数组。

在项目中创建类Tautog，在主方法中定义二维数组，使用foreach语句遍历二维数组代码如下:

```java
public class Tautog{								
    public static void main(String[] args){
        int arr2[][] = {{4,3},{1,2}};
        System.out.println("数组中的元素是：");
        int i = 0;
        for(int x[]:arr2){		//外层循环变量为一维数组
            i++;				//外层计数器递增
            int j = 0;
            for(int e:x){		//循环遍历每一个数组元素
                j++;			//内层计数器递增
                if(i == arr2.length && j == x.length){		//判断变量是二维数组的最后一个元素
                    System.out.print(e);					//输出二维数组最后一个元素
                }else
                    System.out.print(e + "、")				//如果不是最后个元素则输出e、
            }
        }
    }
}
```

运行结果：

![运行结果](https://img.i-nmb.cn/inmb/image-20220424113100051.png)





### 填充替换数组元素

数组中的元素定义完成后，可通过Arrays类的静态方法fill()来对数组中的元素进行替换。

该方法通过各种重载形式可完成对任意类型的数组元素的替换。fill()方法有两种参数类型，下面以int型数组为例介绍fill()方法的使用方法。

#### （1） fill(int[] a,int value)



该方法可将指定的int值分配给int型数组的每个元素。

语法如下

```java
fill(int[] a,int value)
```

a：要进行元素替换的数组。

value：要存储数组中所有元素的值。

在项目中创建类Swap，在主方法中创建一维数组，并实现通过fill()方法填充数组元素，最后将数组中的各个元素输出。

```java
import java.util.Arrays;
public class Swap{
    public static void main(String[] atgs){
        int arr[] = new int[5];				//新建int型数组
        Arrays.fill(arr,8);					//使用同一个值对数组进行填充
        for(int i = 0;i < arr.length;i++){	//循环遍历数组中的元素
            //将数组中的元素依次输出
            System.out.println("第" + i + "个元素是：" + arr[i]);
        }
    }
}
```

![运行结果](https://img.i-nmb.cn/inmb/image-20220424114555718.png)

#### （2） fill(int[] a,int fromIndex,int toIndex,int value)

该方法将指定的int值分配给int型数组指定范围中的每个元素。填充的范围从索引fromIndex（包括）一直到索引toIndex（不包括）。如果fromIndex == toIndex，则填充范围为空。

语法如下：

```java
fill(int[] a,int fromIndex,int toIndex,int value)
```

a：要进行填充的数组。

fromIndex：要使用指定值填充的第一个元素的索引（包括）。

toIndex：要使用指定值填充的最后一个元素的索引（不包括）。

value：要存储在数组所有元素中的值。







下实例我们通过 Java Util 类的 Arrays.fill(arrayname,value) 方法和Arrays.fill(arrayname ,starting index ,ending index ,value) 方法向数组中填充元素：

```java
import java.util.*;
public class FillTest {
    public static void main(String args[]) {
        int array[] = new int[6];
        Arrays.fill(array, 100);
        for (int i=0, n=array.length; i < n; i++) {
            System.out.println(array[i]);
        }
        System.out.println();
        Arrays.fill(array, 3, 6, 50);
        for (int i=0, n=array.length; i< n; i++) {
            System.out.println(array[i]);
        }
    }
}
```

以上代码运行输出结果为：

```
100
100
100
100
100
100

100
100
100
50
50
50
```

### 对数组进行排序

通过Arrays类的静态sort()方法可以实现对数组的排序。sort()方法提供了多种重载形式，可对任意类型的数组进行升序排序。

语法如下

```java
Arrays.sort(object)
```

其中，object是指进行排序的数组名称

![在项目中创建类Taxis，在主方法中创建一维数组，将数组排序后输出。](https://img.i-nmb.cn/inmb/image-20220424115317314.png)

运行结果如图

![运行结果](https://img.i-nmb.cn/inmb/image-20220424115332551.png)

上述实例是对整型数组进行排序。Java中的String类型数组的排序算法是根据字典编排顺序排序的，因此数字排在字母前面，大写字母排在小写字母前面。

### 复制数组

Arrays类的copyOf()方法与copyOfRange()方法可以实现对数组的复制。copyOf()方法是复制数组至指定长度，copyOfRange()方法则将指定数组的指定长度复制到一个新数组中。

#### （1） copyOf()方法

该方法提供了多种重载形式，用于满足不同类型数组的复制。语法如下

  ![img](https://img.i-nmb.cn/inmb/wps2.png)

arr：要进行复制的数组。

newlength：int型常量，指复制后的新数组的长度。

```java
        int[] a = {1,2,3,4};
        int[] a1 = Arrays.copyOf(a,2);//复制指定的数组长度
        int[] a2 = Arrays.copyOf(a,3);
        int[] a3 = Arrays.copyOf(a,5);
        System.out.println(Arrays.toString(a1));
        System.out.println(Arrays.toString(a2));
        System.out.println(Arrays.toString(a3));

```

运行结果

```
[1, 2] [1, 2, 3] [1, 2, 3, 4, 0]
```



#### （2） copyOfRange()方法

该方法同样提供了多种重载形式

```
copyOfRange(arr,int formIndex,int toIndex)
```

arr：要进行复制的数组对象。 

formIndex：指定开始复制数组的索引位置。formIndex必须在0至整个数组的长度之间。新数组包括索引是formIndex的元素。

toIndex：要复制范围的最后索引位置。可大于数组arr的长度。新数组不包括索引是toIndex的元素。



![在项目中创建类Repeat，在主方法中创建一维数组，并将数组中索引位置是0~3的元素复制到新数组中，最后将新数组输出。](https://img.i-nmb.cn/inmb/image-20220424120338695.png)

运行结果如图

![运行结果](https://img.i-nmb.cn/inmb/image-20220424120355348.png)

### 数组查询

Arrays类的binarySearch()方法，可使用二分搜索法来搜索指定数 组，以获得指定对象。该方法返回要搜索元素的索引值。binarySearch() 方法提供了多种重载形式，用于满足各种类型数组的查找需要。binarySearch()方法有两种参数类型。

#### （1） binarySearch(Object[],Object key)

```
 binarySearch(Object[] a, Object key)
```

a: 要搜索的数组

key：要搜索的值

如果key在数组中，则返回搜索值的索引；否则返回-1或“-”（插入点）。插入点是索引键将要插入数组的那一点，即第一个大于该键的元素的索引。

技巧：

[1] 搜索值不是数组元素，且在数组范围内，从1开始计数，得“ - 插入点索引值”；

[2] 搜索值是数组元素，从0开始计数，得搜索值的索引值；

[3] 搜索值不是数组元素，且小于数组内元素，索引值为 – 1；

[4] 搜索值不是数组元素，且大于数组内元素，索引值为 – (length + 1);

```java
import java.util.Arrays;
 
public class ArraysBinarySearch {
    public static void main(String[] args) {
        int arr[] = new int[]{3, 5, 7, 9, 11, 13};
 
        Arrays.sort(arr);
 
        for (int i = 0; i < 17; i++) {
            System.out.println("数字【" + i + "】：" + Arrays.binarySearch(arr, i));
        }
    }
}
```

结果

```java
数字【0】：-1
数字【1】：-1
数字【2】：-1
数字【3】：0
数字【4】：-2
数字【5】：1
数字【6】：-3
数字【7】：2
数字【8】：-4
数字【9】：3
数字【10】：-5
数字【11】：4
数字【12】：-6
数字【13】：5
数字【14】：-7
数字【15】：-7
数字【16】：-7
```



#### （2） binarySearch(Object[],int fromIndex,int toIndex,Object key)

该方法在指定的范围内检索某一元素。

![img](https://img.i-nmb.cn/inmb/wps4.png)

a：要进行检索的数组。

fromIndex：指定范围的开始处索引（包含）。

toIndex：指定范围的结束处索引（不包含）。

key：要搜索的元素。

![在项目中创建类Rakel，在主方法中创建String数组，实现查找元素“cd”在指定范围的数组str中的索引位置。](https://img.i-nmb.cn/inmb/image-20220424121753928.png)

![运行结果](https://img.i-nmb.cn/inmb/image-20220424121804351.png)

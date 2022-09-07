---
title: 2022年度SMUCTF的WP笔记
date: 2022-04-15 17:47:24
tags:
- CTF
- WP
categories:
  - 测试
description: 福建三明学院信息工程学院网络攻防大赛（SMUCTF）是由共青团三明学院信息工程学院委员会主办、信息工程学院网络安全协会承办的一场关于网络安全技术练习的CTF夺旗赛
---

福建三明学院信息工程学院网络攻防大赛（SMUCTF）是由共青团三明学院信息工程学院委员会主办、信息工程学院网络安全协会承办的一场关于网络安全技术练习的CTF夺旗赛。

本篇文章将展示笔者对2022年度福建三明学院信息工程学院网络攻防大赛（SMUCTF）的部分解题笔记（个人理解）。能解出来的题目，手把手教程！

## 》MISC

### SMUGIFQR

<img src="https://s3.bmp.ovh/imgs/2022/04/16/e30c5fd3b8c6685f.png" alt="SMUGIFQR题目" style="zoom:100%;" />

点击[下载附件](https://inmb.lanzouf.com/itghC039fp0d)得到一个gif，不同的图片查看器有不同的高度（判断应该是修改了高度）

<img src="https://s3.bmp.ovh/imgs/2022/04/16/9fd0133122202280.png" alt="两个查看器不一样" style="zoom:33%;" />

这个gif包含了多个二维码，每个二维码只停留不到1秒钟的时间。

Stegsolve是基于java编写（**需要安装Java环境**），它能够将掩藏在图形中的重要信息解析过来，它能读取图片中的链接、文本信息，软件操作相对简单。

用Stegsolve打开解压得到的flag.gif

接下来使用Stegsolve提供的“Frame Browser”，

<img src="https://s3.bmp.ovh/imgs/2022/04/17/f899c5d43f633159.png" alt="Frame Browser" style="zoom:80%;" />

在Frame Browser中点击 > 按钮，可以逐帧查看，用二维码扫描器逐一扫描二维码得到

```
flag{SMUQRs-Are-FUN!}
```



### 冰墩墩的汉信码

<img src="https://s3.bmp.ovh/imgs/2022/04/16/be5f0e20f8fb6456.png" alt="题目" style="zoom:100%;" />

点击[下载附件](https://inmb.lanzouf.com/iXNyf039hsad)得到一张冰墩墩的图片

<img src="https://s3.bmp.ovh/imgs/2022/04/16/30c9b2a890861418.png" alt="冰墩墩" style="zoom:50%;" />

说是有汉信码，一定在图片上，同样使用Stegsolve，调整好窗口大小后直接按下菜单栏的 > 键，在Red plane 0 的频道画面下出现汉信码

<img src="https://s3.bmp.ovh/imgs/2022/04/16/2629c499012a53ff.png" alt="找到汉信码" style="zoom:80%;" />

> #### 汉信码是我国具有完全自主知识产权的特殊二维码
>
> 汉信码具有知识产权免费、汉字编码能力强、抗污损、抗畸变、信息容量大等特点。
>
> 要使用特定的手机APP：[中国编码（Android点击下载）](https://inmb.lanzouf.com/i5IJj039jdfa)  才能扫描

手机安装中国编码APP后扫描得到：

```
Dear SMUCTFers, congratulations on getting the flag：flag{Have_YOu_ever_Heard_0f_HanXinMa}
```

得到flag{Have_YOu_ever_Heard_0f_HanXinMa}



### listentomusic

<img src="https://s3.bmp.ovh/imgs/2022/04/16/506ebadb42deede4.png" alt="listentomusic" style="zoom:100%;" />

点击[下载附件](https://inmb.lanzouf.com/ilnsL039jv8b)解压得到一个音频和另一个压缩包

<img src="https://s3.bmp.ovh/imgs/2022/04/16/745c327299c376cf.png" alt="附件内容" style="zoom:100%;" />

pass.wav中是电话拨号音频，使用 在线电话拨号音频解密：[Detect DTMF Tones (dialabc.com)](http://dialabc.com/sound/detect/)，选择文件后进行解密得到

```
1933056020
```

<img src="https://s3.bmp.ovh/imgs/2022/04/16/249c8b814feadefa.png" alt="拨号" style="zoom:100%;" />

带到加密包输入密码1933056020得到lsb-silenteye，

<img src="https://s3.bmp.ovh/imgs/2022/04/16/44f1678ace85f9ce.png" alt="lsb-silenteye" style="zoom:100%;" />

根据提示使用[SilentEye工具](http://www.opdown.com/soft/88597.html)，将音频拖进SilentEye工具，点击Decode，在弹出窗口再次点击decode

<img src="https://s3.bmp.ovh/imgs/2022/04/16/90e5de59fefbe6ec.jpg" alt="音频拖进SilentEye工具" style="zoom:67%;" />



得到以下提示，下载得到SSTVflag，

> 链接：https://pan.baidu.com/s/1Jsy4naAx3JvOaGWmKeKAfg 
>
> 提取码：1mci

在网络上的教程大多对sstv的解法是使用kali的Qsstv，但是我的kali中的qsstv显示，这个音频不支持，所以我们使用另外的方法

在手机上下载[Robot36（Android点击下载）](https://inmb.lanzouf.com/iAntQ039lc0b)



手机打开软件使用电脑播放音频得到

<img src="https://s3.bmp.ovh/imgs/2022/04/16/53ce9a6d142b5d0f.jpg" alt="得到图片" style="zoom:25%;" />

图片中有

```
flag{D0_YOu_know_SMUmusic_ForWAVE}
```







### High-level_SMUpdf

![](https://s3.bmp.ovh/imgs/2022/04/17/804f2e86a42eee39.png)

点击[这里下载附件](https://inmb.lanzouf.com/iKrmt03bzauf)，得到一个压缩包，其中flag.pdf为解密文件

<img src="https://s3.bmp.ovh/imgs/2022/04/17/a4b60ca0889d5a45.png" style="zoom:150%;" />

打开pass.pdf，发现改文件受到密码保护，不允许查看

![](https://s3.bmp.ovh/imgs/2022/04/17/050f747e6ef42c55.png)

我们打开PDF Password Recovery（或者其他PDF密码解锁爆破工具），选择恢复用户密码使用枚举攻击

![](https://s3.bmp.ovh/imgs/2022/04/17/da1d4f7ea58cb215.png)![](https://s3.bmp.ovh/imgs/2022/04/17/95c950b9d9325661.png)



使用1-8位密码字符数字组合

![](https://s3.bmp.ovh/imgs/2022/04/17/598bfb649a367d3f.png)

得到pass密码，使用密码并且使用PDF编辑器打开pass.pdf文件

![](https://s3.bmp.ovh/imgs/2022/04/17/9a3fff0c38e1517a.png)

在最后一栏有隐形的字，把他复制到记事本中，得到解压密码<u>6ef23c0845c43d82e0614baeba084d11</u>

![](https://s3.bmp.ovh/imgs/2022/04/17/3a1d488889f00112.png)——>password：6ef23c0845c43d82e0614baeba084d11

打开flag文件后得到包含11张图片的PDF，使用winhex打开发现他拥有两个PDF的文件头，推断使用了**wbStego4open**把文件隐藏到PDF文件中

<img src="https://s3.bmp.ovh/imgs/2022/04/17/e279b4d9fb3fa1dc.png" alt="两个文件头" style="zoom:80%;" />

我们使用wbStego4.3open.exe（百度上不好找这个工具，[点击这里下载](https://inmb.lanzouf.com/iKrmt03bzauf)），第二步中选择Decode ，输入文件地址后，下一步中选择PDF

![](https://s3.bmp.ovh/imgs/2022/04/17/40b497eb32245618.png)

![](https://s3.bmp.ovh/imgs/2022/04/17/b190cf34c3a78cd7.png)

直接下一步，不用输入，之后随便输入命名txt文件，然后点击继续，之后在工具的根目录下出现自己命名的txt文件



![](https://s3.bmp.ovh/imgs/2022/04/17/d4db801f126739eb.png)——>![](https://s3.bmp.ovh/imgs/2022/04/17/9bcefd601c6cdb56.png)![](https://s3.bmp.ovh/imgs/2022/04/17/af05bee0f1c3e5c3.png)

得到

```
flag{0urSMUPDF}
```



### 病毒文件恢复

![](https://s3.bmp.ovh/imgs/2022/04/17/bf0cfc60b91a1b2f.png)

点击[下载附件](https://inmb.lanzouf.com/i9Sm103c05pg)，解压得到一个勒索文件，一个加密文件

![](https://s3.bmp.ovh/imgs/2022/04/17/981e57f18b0598de.png)

由于，本人目前能力有限，毕竟专业领域有人做的比我们好，所以我们使用360勒索病毒解密：https://lesuobingdu.360.cn/

选择在线解密，上传留言文件和加密文件，点击开始解密，稍等片刻后就可以下载到含有flag的源文件

![解密](https://img.i-nmb.cn/inmb/image-20220417030409531.png)

```
flag{fngD_vwfW_JTqI_E4Kl}
```





## 》CRYPTO

### hex

![hex](https://img.i-nmb.cn/inmb/image-20220417030827940.png)

点击[这里下载附件](https://inmb.lanzouf.com/iLsOa03c11wf)，解压得到mod.txt给了一串字符串解密得到答案;

分析字符串可以得到是16进制，**因为16进制的组成字母范围是 a-f**

```
d4e8e1f4a0f7e1f3a0e6e1f3f4a1a0d4e8e5a0e6ece1e7a0e9f3baa0fbb9e1e6b3e3b9e4b3b7b7e2b6b1e4b2b6b9e2b1b1b3b3b7e6b3b3b0e3b9b3b5e6fd
```

![image-20220417031042116](https://img.i-nmb.cn/inmb/image-20220417031042116.png)

把其转成ASC码即可,但是往往不是那么顺利,因为存在 ASC码超过最大值的问题,需要减**128**,再转ASC码;

<img src="https://img.i-nmb.cn/inmb/image-20220417031551253.png" alt="p" style="zoom:80%;" />

脚本：

```python
cipher = "d4e8e1f4a0f7e1f3a0e6e1f3f4a1a0d4e8e5a0e6ece1e7a0e9f3baa0fbb9e1e6b3e3b9e4b3b7b7e2b6b1e4b2b6b9e2b1b1b3b3b7e6b3b3b0e3b9b3b5e6fd"
print(''.join([chr(int(cipher[i:i + 2], 16) - 128) for i in range(0,len(cipher), 2)]))

```

得到flag{9af3c9d377b61d269b11337f330c935f}



## 》REVERSE

### warmup

![题目](https://img.i-nmb.cn/inmb/image-20220417031912025.png)

点击[这里下载附件包](https://inmb.lanzouf.com/i6OdD03c14ne)，得到某个文件，二话不说放进IDA，因为是64位文件，**使用IDA64打开**。

![image-20220417032033287](https://img.i-nmb.cn/inmb/image-20220417032033287.png)

找到main函数

![main函数](https://img.i-nmb.cn/inmb/image-20220417032224390.png)

```c
int __cdecl main(int argc, const char **argv, const char **envp)
{
  char s2[8]; // [rsp+0h] [rbp-40h]
  char s1; // [rsp+20h] [rbp-20h]

  puts("plz input flag:");
  strcpy(s2, "Reverse_is_very_Fun-_-!");
  __isoc99_scanf("%s", &s1);
  if ( !strcmp(&s1, s2) )
    puts("right!");
  else
    puts("wrong!");
  return 0;
}
```

这里将"Reverse_is_very_Fun-_-!"复制到数组s2中，并将s2和输入的s1进行对比，如果s1和s2相同则输出"right!"否则输出"wrong!"

所以，flag就是Reverse_is_very_Fun-_-!



```
flag{Reverse_is_very_Fun-_-!}
```





附：[信息工程学院网络攻防大赛初赛官方解题报告.pdf](https://inmb.lanzouf.com/i3uYK03m622b)


---
title: NexT主题修改侧边滚动条
date: 2022-04-29 10:02:57
tags:
- hexo
- NexT
keywords: Hexo加速, next主题, 插件
description: 在修改侧边滚动条的时候想更改样式，但是侧边滚动条留有白底，怎么才能把他消去呢？
---

## NexT主题修改侧边栏

在`(root)\themes\next\source\css`找到`_other.styl`，没有就自建。

增添以下代码：

```css
::-webkit-scrollbar-thumb {
    background-color: #FF2A68;
    background-image: -webkit-linear-gradient(45deg,rgba(255,255,255,.4) 25%,transparent 25%,transparent 50%,rgba(255,255,255,.4) 50%,rgba(255,255,255,.4) 75%,transparent 75%,transparent);
    border-radius: 3em;
}
::-webkit-scrollbar-track {
    background-color: #ffcacaff;
    border-radius: 3em;
}
::-webkit-scrollbar {
    width: 8px;
    height: 15px;
}
```

![样式](https://inmb.oss-cn-shenzhen.aliyuncs.com/inmb/image-20220429102531954.png)

若发现配色不适合网页，例如：

![配色不适合](https://inmb.oss-cn-shenzhen.aliyuncs.com/inmb/image-20220429102621241.png)



可以去：[在线调色助手配色参考(rockhwhuang.com)](http://tools.rockhwhuang.com/)，挑选自己喜欢的颜色，然后在`::-webkit-scrollbar-thumb{background-color:}`更改滚条颜色，在`::-webkit-scrollbar-track` 中的`background-color:`修改背景颜色


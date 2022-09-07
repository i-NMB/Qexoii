---
title: Hexo-NexT主题加速运行
date: 2022-04-21 17:55:36
tags:
- hexo
- NexT
keywords: [Hexo加速, next主题, CDN, Elevation, 插件]
description: 有时候你的博客加载缓慢，可能是因为加载的本地的东西太多。
---

## 删繁就简

去掉一些不必要的、花里胡哨的功能，这个可能要关掉pace、canvas_lines、tag-icon等，安心留田种地。

## 使用CDN加载部分css、js

当我使用FancyBox进行图片放大的时候，每次在F12中看到FancyBox的加载速度十分缓慢，因为他都要调用托管地方的文件，这时候可能需要引用外部响应速度（下载速度）比我们自己站点更好的，而jsdelivr就可以完美解决这一问题

在`Blog/themes/next/_config.yml`中搜索`jsdelivr`，让这些外部资源加载使用jsDeliver

![image-20220419180337404](https://img.i-nmb.cn/inmb/image-20220419180337404.png)

<img src="https://img.i-nmb.cn/inmb/image-20220419180547954.png" alt="例如" style="zoom:67%;" />

## 插件介绍

下列是对一些在_config.yml配置中提供CDN加载的插件介绍，如果你使用或者需要这些插件你可以直接把他前面的 # 删去即可使用，不必再将他下载到本地再上传并且不必让他在自己的站中缓慢加载、消耗流量。

### anime：

anime.js 是一个简便的JS动画库，用法简单而且适用范围广，涵盖CSS，DOM，SVG还有JS的对象，各种带数值属性的东西都可以动起来。

实际演示和代码，官网写得很详细清楚了

官网：[中文文档 | anime.js (animejs.cn)](https://www.animejs.cn/documentation/#remove)



### fontawesome：

[Font Awesome,一套绝佳的图标字体库和CSS框架](http://www.baidu.com/link?url=0KewDfaGONrnAvIw-Pge0uEsjHWhiV8cB0vKPwhlN-VJa1NkcBKorHbZQauXaZLZ)



### MathJax：

在页面有很多情况需要显示公式，但在单纯在页面显示是不能达到效果的，因此需要MathJax的编译。



### KaTeX

通过KaTeX插件，您可以在网站上使用最快的[TeX数学排版引擎](https://github.com/Khan/KaTeX)



### pjax

pjax是一个jQuery插件，它通过ajax和pushState技术提供了极速的（无刷新ajax加载）浏览体验，并且保持了真实的地址、网页标题，浏览器的后退（前进）按钮也可以正常使用。

pjax的工作原理是通过ajax从服务器端获取HTML，在页面中用获取到的HTML替换指定容器元素中的内容。然后使用pushState技术更新浏览器地址栏中的当前地址。

以下两点原因决定了pjax会有更快的浏览体验：

1.不存在页面资源（js/css）的重复加载和应用；

2.如果服务器端配置了pjax，它可以只渲染页面局部内容，从而避免服务器渲染完整布局的额外开销。

#### 建议开启pjax

使用*pjax* 实现网站无刷新加载

#### 开启pjax

pjax的开启很简单，我们只需要用CDN加载pjax（去掉链接前面的#，并且在原pjax前加上#，如下图），然后在主题配置中找到pjax设置`pjax: true`。

![image-20220419182954415](https://img.i-nmb.cn/inmb/image-20220419182954415.png)



使用pjax，你甚至可以给[Next主题添加全局播放翻页不间断的网易云音乐](https://blog.csdn.net/Qxiaofei_/article/details/123072610)；



### FancyBox

支持对放大的图片添加阴影效果，对于一组相关的图片添加导航操作按纽。

### Medium-zoom

想为自己网站的文章图片添加缩放的效果,可以选择使用*medium-zoom*这个插件

### Lazy Load

Lazy Load延迟加载图像插件,直到用户滚动到它们才显示!

lazyload 是网站常用的技术，通过按需加载，避免一次性加载过多内容导致的打开缓慢

### Pangu

对于强迫症来说，中英文混排时加上空格能很大程度改善阅读体验，但是有时候会不小心打漏部分空格，而 [pangu](https://github.com/vinta/pangu.js) 这个项目就可以帮你在展示时自动加上空格



### Quicklink

可以在空闲时间预获取页面可视区域（以下简称视区）内的链接，加快后续加载速度。



### DisqusJS

*DisqusJS*:使用DisqusAPI在中国大陆呈现Disqus评论

### Valine

Valine - 一款快速、简洁且高效的无后端评论系统。

### Gitalk

 Gitalk 是一个基于 GitHub Issue 和 Preact 开发的评论插件



### Algolia Search

Algolia 搜索插件，懂的都懂



### Mermaid

绘图插件--mermaid



### Velocity



### Pace

通过使用pace,我们可以展示网页进度条加载效果。



### canvas_ribbon

背景彩带动画

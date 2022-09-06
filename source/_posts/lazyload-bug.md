---
title: 懒加载(lazyload/lozad)和Valine评论系统的头像、表情冲突
date: 2022-05-12 21:49:09
tags:
- lozad
- Valine
- hexo
- NexT
keywords: 懒加载, lozad, Valine, 评论系统
description: 解决lozad(懒加载)和Valine的不兼容、头像不显示的问题。
---

## 问题现象

在使用lozad.js的情况下，同时使用了Valine评论系统，就会出现头像、表情不显示的问题。百度也一直找不到问题所在。

如图

<img src="https://img1.i-nmb.cn/img/image-20220512221221660.png" alt="头像不显示" style="zoom:80%;" />

<img src="https://img1.i-nmb.cn/img/image-20220512221511083.png" alt="表情不显示" style="zoom:80%;" />

## 问题分析

在F12开发者工具下，看到所有的src变成了data-src，导致了src没有数据

![data-src](https://img1.i-nmb.cn/img/image-20220512221829449.png)



查看代码，发现他把src一律转换成了data-src。

```js
/*! lozad.js - v1.16.0 - 2020-09-06
* https://github.com/ApoorvSaxena/lozad.js
* Copyright (c) 2020 Apoorv Saxena; Licensed MIT */
!function(t,e){"object"==typeof exports&&"undefined"!=typeof module?module.exports=e():"function"==typeof define&&define.amd?define(e):t.lozad=e()}(this,function(){"use strict";
/**
   * Detect IE browser
   * @const {boolean}
   * @private
   */var g="undefined"!=typeof document&&document.documentMode,f={rootMargin:"0px",threshold:0,load:function(t){if("picture"===t.nodeName.toLowerCase()){var e=t.querySelector("img"),r=!1;null===e&&(e=document.createElement("img"),r=!0),g&&t.getAttribute("data-iesrc")&&(e.src=t.getAttribute("data-iesrc")),t.getAttribute("data-alt")&&(e.alt=t.getAttribute("data-alt")),r&&t.append(e)}if("video"===t.nodeName.toLowerCase()&&!t.getAttribute("data-src")&&t.children){for(var a=t.children,o=void 0,i=0;i<=a.length-1;i++)(o=a[i].getAttribute("data-src"))&&(a[i].src=o);t.load()}t.getAttribute("data-poster")&&(t.poster=t.getAttribute("data-poster")),t.getAttribute("data-src")&&(t.src=t.getAttribute("data-src")),t.getAttribute("data-srcset")&&t.setAttribute("srcset",t.getAttribute("data-srcset"));var n=",";if(t.getAttribute("data-background-delimiter")&&(n=t.getAttribute("data-background-delimiter")),t.getAttribute("data-background-image"))t.style.backgroundImage="url('"+t.getAttribute("data-background-image").split(n).join("'),url('")+"')";else if(t.getAttribute("data-background-image-set")){var d=t.getAttribute("data-background-image-set").split(n),u=d[0].substr(0,d[0].indexOf(" "))||d[0];// Substring before ... 1x
u=-1===u.indexOf("url(")?"url("+u+")":u,1===d.length?t.style.backgroundImage=u:t.setAttribute("style",(t.getAttribute("style")||"")+"background-image: "+u+"; background-image: -webkit-image-set("+d+"); background-image: image-set("+d+")")}t.getAttribute("data-toggle-class")&&t.classList.toggle(t.getAttribute("data-toggle-class"))},loaded:function(){}};function A(t){t.setAttribute("data-loaded",!0)}var m=function(t){return"true"===t.getAttribute("data-loaded")},v=function(t){var e=1<arguments.length&&void 0!==arguments[1]?arguments[1]:document;return t instanceof Element?[t]:t instanceof NodeList?t:e.querySelectorAll(t)};return function(){var r,a,o=0<arguments.length&&void 0!==arguments[0]?arguments[0]:".lozad",t=1<arguments.length&&void 0!==arguments[1]?arguments[1]:{},e=Object.assign({},f,t),i=e.root,n=e.rootMargin,d=e.threshold,u=e.load,g=e.loaded,s=void 0;"undefined"!=typeof window&&window.IntersectionObserver&&(s=new IntersectionObserver((r=u,a=g,function(t,e){t.forEach(function(t){(0<t.intersectionRatio||t.isIntersecting)&&(e.unobserve(t.target),m(t.target)||(r(t.target),A(t.target),a(t.target)))})}),{root:i,rootMargin:n,threshold:d}));for(var c,l=v(o,i),b=0;b<l.length;b++)(c=l[b]).getAttribute("data-placeholder-background")&&(c.style.background=c.getAttribute("data-placeholder-background"));return{observe:function(){for(var t=v(o,i),e=0;e<t.length;e++)m(t[e])||(s?s.observe(t[e]):(u(t[e]),A(t[e]),g(t[e])))},triggerLoad:function(t){m(t)||(u(t),A(t),g(t))},observer:s}}});
```



所以我们使用`srcset`代替`Valine.min.js`中的`src`



## 具体解决方法

使用`srcset`代替`Valine.min.js`中的`src`

首先我们先下载js文件到本地：[下载地址](https://cdn.jsdelivr.net/npm/valine@1/dist/Valine.min.js)

搜索`<img`

![搜索<img](https://img1.i-nmb.cn/img/image-20220512223914575.png)

然后在`<img`后面的`src`替换为`srcset`

并将更改好的js放在`Blog\source`中的某个地方

接下来在CDN引用的地方，修改路径为`/js1/Valine.min.js`【笔者放在Blog/source/js1/Valine.min.js】

![修改路径](https://img1.i-nmb.cn/img/image-20220512230334642.png)

然后保存，最后`hexo cl && hexo g && hexo s`

## 问题解决

看结果，

![修护完成](https://img1.i-nmb.cn/img/image-20220512224151163.png)

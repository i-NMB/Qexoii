---
title: 在NexT的侧边栏添加近期文章板块
date: 2022-05-03 10:33:52
tags:
- hexo
- NexT
keywords: [Hexo, next主题, 近期文章]
description: 原本今天想再侧边栏添加一页友链网页，但是使用了网上的办法发现没法适合NexT 7.8.0，百般周折后发现是源代码不兼容</br>这里我记录一下正确的做法
---

最近听说内链可以改善SEO，于是乎，我想在NexT的侧边栏添加近期文章板块

在网络上查找的方案大致如下

## 第一种方法

```swift
{% if theme.recent_posts %}
    <div class="links-of-blogroll motion-element {{ "links-of-blogroll-" + theme.recent_posts_layout  }}">
      <div class="links-of-blogroll-title">
        <!-- modify icon to fire by szw -->
        <i class="fa fa-history fa-{{ theme.recent_posts_icon | lower }}" aria-hidden="true"></i>
        {{ theme.recent_posts_title }}
      </div>
      <ul class="links-of-blogroll-list">
        {% set posts = site.posts.sort('-date') %}
        {% for post in posts.slice('0', '5') %}
          <li>
            <a href="{{ url_for(post.path) }}" title="{{ post.title }}" target="_blank">{{ post.title }}</a>
          </li>
        {% endfor %}
      </ul>
    </div>
{% endif %}
```

将此代码贴在`next/layout/macro/sidebar.swig`中的`if theme.links`对应的`endif`后面
为了配置方便，在主题的`config.yml`中添加了几个变量，如下：

```swift
recent_posts_title: 近期文章
recent_posts_layout: block
recent_posts: true
```



以上操作之后NexT 7.8.0在侧边栏有“近期文章”的文字标志。但是没有链接。

于是我换了另外一种办法，基于NexT 8.X

## 第二种办法

1. 新建 source/_data/sidebar.njk 文件，内容如下：

```bash
{# RecentPosts #}
{%- if theme.recent_posts %}
  <div class="links-of-recent-posts motion-element">
    <div class="links-of-recent-posts-title">
      {%- if theme.recent_posts.icon %}
      <i class="{{ theme.recent_posts.icon }} fa-fw"></i>
      {%- endif %}
      {{ theme.recent_posts.title }}
    </div>
    <ul class="links-of-recent-posts-list">
      {%- set posts = site.posts.sort('date', 'desc').toArray() %}
      {%- for post in posts.slice('0', theme.recent_posts.max_count) %}
        <li class="links-of-recent-posts-item">
          {{ next_url(post.path, post.title, {title: post.path}) }}
        </li>
      {%- endfor %}
    </ul>
  </div>
{%- endif %}
```

2.修改config.next.yml，取消 custom_file_path 中的 sidebar 和 style 两个注释，并新增 recent_posts 内容。

```yml
custom_file_path:
  #head: source/_data/head.swig
  #header: source/_data/header.swig
  sidebar: source/_data/sidebar.njk
  #postMeta: source/_data/post-meta.swig
  #postBodyEnd: source/_data/post-body-end.swig
  #footer: source/_data/footer.swig
  #bodyEnd: source/_data/body-end.swig
  #variable: source/_data/variables.styl
  #mixin: source/_data/mixins.styl
  style: source/_data/styles.styl

recent_posts:
# 块标题
  title: 最近文章
# 图标
  icon: fa fa-history
# 最多多少文章链接
  max_count: 5
```

3.修改 source/_data/styles.styl 文件，文件不存在新建即可。添加如下代码：

```css
// 近期文章
.links-of-recent-posts
  font-size: 0.8125em
  margin-top: 10px

.links-of-recent-posts-title
  font-size: 1.03em
  font-weight: 600
  margin-top: 0

.links-of-recent-posts-list
  list-style: none
  margin: 0
  padding: 0
```



然后发现这个只在站点概括中，在文章目录中不存在

<img src="https://inmb.oss-cn-shenzhen.aliyuncs.com/inmb/image-20220503170621133.png" alt="只在站点概括中" style="zoom:50%;" />

<img src="https://inmb.oss-cn-shenzhen.aliyuncs.com/inmb/image-20220503170947135.png" alt="在文章目录中没有显示" style="zoom:60%;" />

因为大多数访客是不会主动点击站点概括的，那么如何把近期文章板块加入到文章目录的侧边栏中去呢？

我结合了第一种方法

因为第一种办法，能够在目录中显示近期文章四个字，那么说明第一种方法可行，但是可能已经过时或者是笔者配置不正确。

## 解决办法

把上面新建的`sidebar.njk`代码复制在`next/layout/_macro/sidebar.swig`中的适应位置，如果没有修改添加过其他板块，可以在`{%- if theme.back2top.enable and theme.back2top.sidebar %}`的前面粘贴

因为本博客添加了tag云，所以笔者放在了`{% if site.tags.length > 1 %}`前面

<img src="https://inmb.oss-cn-shenzhen.aliyuncs.com/inmb/image-20220503172737724.png" alt="位置" style="zoom:67%;" />



## 附带问题

在成功部署后，发现链接前面加了圆点，影响排版

<img src="https://inmb.oss-cn-shenzhen.aliyuncs.com/inmb/image-20220503173011957.png" alt="链接前面加了圆点" style="zoom:67%;" />

### 解决办法

在`next/layout/_macro/sidebar.swig`加入的代码中

```html
<ul class="sidebar-nav motion-element">
    …………
</ul>
```

修改为

```html
<ul class="sidebar-nav motion-element" style="list-style: none;">
    …………
</ul>
```

至此问题解决完毕

![结果](https://inmb.oss-cn-shenzhen.aliyuncs.com/inmb/image-20220503173538355.png)

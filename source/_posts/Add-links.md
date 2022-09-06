---
title: 添加友链踩坑记录
date: 2022-05-03 03:11:54
tags:
- hexo
- NexT
keywords: [Hexo, next主题, 友链, 踩坑]
description: 原本今天想添加一页友链网页，但是使用了网上的办法发现没法适合NexT 7.8.0，百般周折后发现是一行代码插入错误。</br>这里我记录一下正确的做法
---

## 新增links页面

```
$ hexo new page links
```

## 配置menu

主题配置文件`_config.yml`中`menu`下添加：

```
links: /links/ || fa fa-link
```

`/themes/next/languages/zh-Hans.yml`文件中`menu`下增加中文描述：

```
links: 友链
```

做完这些工作，接下来就是要增加友链页面的样式了

## 新增`links.swig`页

在`/themes/next/layout/`新建`links.swig`，内容如下：

```css
{% block content %}
  {######################}
  {### LINKS BLOCK ###}
  {######################}

    <div id="links">
        <style>

            #links{
               margin-top: 5rem;
            }

            .links-content{
                margin-top:1rem;
            }

            .link-navigation::after {
                content: " ";
                display: block;
                clear: both;
            }

            .card {
                width: 300px;
                font-size: 1rem;
                padding: 10px 20px;
                border-radius: 4px;
                transition-duration: 0.15s;
                margin-bottom: 1rem;
                display:flex;
            }
            .card:nth-child(odd) {
                float: left;
            }
            .card:nth-child(even) {
                float: right;
            }
            .card:hover {
                transform: scale(1.1);
                box-shadow: 0 2px 6px 0 rgba(0, 0, 0, 0.12), 0 0 6px 0 rgba(0, 0, 0, 0.04);
            }
            .card a {
                border:none;
            }
            .card .ava {
                width: 3rem!important;
                height: 3rem!important;
                margin:0!important;
                margin-right: 1em!important;
                border-radius:4px;

            }
            .card .card-header {
                font-style: italic;
                overflow: hidden;
                width: 236px;
            }
            .card .card-header a {
                font-style: normal;
                color: #2bbc8a;
                font-weight: bold;
                text-decoration: none;
            }
            .card .card-header a:hover {
                color: #d480aa;
                text-decoration: none;
            }
            .card .card-header .info {
                font-style:normal;
                color:#a3a3a3;
                font-size:14px;
                min-width: 0;
                text-overflow: ellipsis;
                overflow: hidden;
                white-space: nowrap;
            }
        </style>
        <div class="links-content">
            <div class="link-navigation">

                {% for link in theme.friendlinks %}

                    <div class="card">
                        <img class="ava" src="{{ link.avatar }}"/>
                        <div class="card-header">
                        <div><a href="{{ link.site }}" target="_blank">@ {{ link.nickname }}</a></div>
                        <div class="info">{{ link.info }}</div>
                        </div>
                    </div>

                {% endfor %}

            </div>
            {{ page.content }}
            </div>
        </div>

  {##########################}
  {### END LINKS BLOCK ###}
  {##########################}
{% endblock %}
```

## 修改page.swig

修改`/themes/next/layout/page.swig`文件，在

```
{%- elif page.type === 'schedule' and not page.title %}
    {{- __('title.schedule') + page_title_suffix }}
```

下面添加：

```
{%- elif page.type === 'links' and not page.title %}
  {{- __('title.links') + page_title_suffix }}
```

## 引入links.swig

关键在于所有的教程中给了引入代码，但没有说具体在哪里插入

在`/themes/next/layout/page.swig`中的

```c++
    {% elif page.type === 'schedule' %}
      <div class="event-list">
      </div>

      {% include '_scripts/pages/schedule.swig' %}
```

插入

```c++
{% elif page.type === 'links' %}
  {% include 'links.swig' %}
```

得到

```c++
    {% elif page.type === 'schedule' %}
      <div class="event-list">
      </div>
    {% elif page.type === 'links' %}
      {% include 'links.swig' %}
      {% include '_scripts/pages/schedule.swig' %}
```

## 主题配置添加

在主题配置文件`_config.yml`末尾处添加友链：

```
mylinks:
  - nickname:  #友链名称
    avatar:   #友链头像
    site:   #友链地址
    info:   #友链说明
  - nickname:  #友链名称
    avatar:   #友链头像
    site:   #友链地址
    info:   #友链说明
```

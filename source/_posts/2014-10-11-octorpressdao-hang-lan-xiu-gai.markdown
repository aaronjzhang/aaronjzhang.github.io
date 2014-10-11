---
layout: post
title: "Octorpress导航栏修改"
date: 2014-10-11 16:50:03 +0800
comments: true
categories: 
---
Octorpress 的默认导航栏只有两个栏目(Blog|Archives), 且都是英文, 希望能增加一个"关于"栏目, 英文都改成中文, 经过一番研究终于得以实现，在此记录备忘.
<!--more-->

## 导航栏的英文改为中文

修改\_include/custom/navigation.html

```html 原_include/custom/navigation.html
<ul class="main-navigation">
<li><a href="{{ root_url }}/">Blog</a></li>
<li><a href="{{ root_url }}/blog/archives">Archives</a></li>
</ul>
```
```html 修改后的_include/custom/navigation.html
<ul class="main-navigation">
<li><a href="{{ root_url }}/">首页</a></li>
<li><a href="{{ root_url }}/blog/archives">所有文章</a></li>
</ul>
```

## 增加about页面
-	首先执行如下命令生成About页面:

```bash
rake new_page[about]
```
该命令会在source目录下创建about文件夹, 并在该文件夹下生成index.markdown文件, 编辑该文件, 添加"关于"的内容.

-	将about页面添加到导航栏

```html _include/custom/navigation.html
<ul class="main-navigation">
<li><a href="{{ root_url }}/">首页</a></li>
<li><a href="{{ root_url }}/blog/archives">所有文章</a></li>
<li><a href="{{ root_url }}/about">关于</a></li>
</ul>
```

---
title: wordpress 用 JS 封装淘宝客链接屏蔽蜘蛛
abbrlink: /post/7.html
author: 许时衡
categories: 旧博客迁移
date: 2014-04-12 19:47:30
tags:
    - WordPress
    - JavaScript
---

百度对垃圾淘客站有点不友好，导致淘客的生存空间很受限制。

今天说的 JS 封装淘宝客链接是针对 wordpress 用 JS 封装淘宝客链接屏蔽蜘蛛。针对蜘蛛不能抓取 JS 里面的内容而做出的一种隐藏式跳转链接到淘宝客链接上去。达到对蜘蛛的友好。

那么实现这个封装要怎么做呢？

首先我们需要用JS代码来判断HTML给出的函数值来分别调用不同的URL。

为此我们需要在模版文件夹中创建一个执行JS文件、一个调用赋值HTML文件。达到我们需要的封装效果。

1、新建一个 JS 执行文件。命名 `loadurl.js` 。

代码如下：

``` JavaScript
function onloads(){
    var url = location.search;
    if(url=="?p=1"){
        location.href="淘宝客链接";
    }
    if(url=="?id=2"){
        location.href="淘宝客链接";
    }
    if(url=="?p=3"){
        location.href="淘宝客链接";
    }
}
```

2、新建一个HTML赋值文件。命名 `loadurl.html` 。

代码如下：

``` html
<!DOCTYPE html PUBLIC “-//W3C//DTD XHTML 1.0 Transitional//EN” “http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd”>
<html xmlns=”http://www.w3.org/1999/xhtml” >
<head>
<title>loading...</title>
<script type=”text/javascript” src=”loadurl.js”></script>
</head>
<body>
</body>
</html>
```

前台模版调用的方法是：

如果销售页有8个产品，那么依次安装顺序填充

``` JavaScript
if(url=="?p=修改数字"){
location.href="修改链接";
}
```

`location.href=”淘宝客推广代码（建议用短链接）”；`

前台调用链接：`<?php bloginfo(‘template_directory’); ?>/loadurl.html?id=1`（对应数字）  依次类推。

例如常见的表格布局案例展示：

``` html
<td>
    <div align=”center”>
    <a target=”_blank” href=”<?php bloginfo(‘template_directory’); ?>/loadurl.html?id=1″>
    <img alt=”耒阳seo第一人 &lt;第一名&gt;” src=”<?php bloginfo(‘template_directory’); ?>/ad/1.jpg” height=”200″ width=”200″
    border=”0″></a>
    </div>
</td>
```

希望对大家有帮助，如果想和我交朋友的可以加我QQ：408285845，一起交流心得。

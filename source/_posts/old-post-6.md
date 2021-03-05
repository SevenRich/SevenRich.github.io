---
title: 人人都想要的AspCms自定义幻灯片
abbrlink: /post/6.html
author: 许时衡
categories: 旧博客迁移
date: 2014-04-10 19:41:49
tags:
    - AspCMS
---

近期接到一个项目，需要用 ASPCMS 做一个网站。无赖 ASPCMS 的默认幻灯片不能满足需要需要就自己集合在网上找的一些代码自定义了一个幻灯片！分享给需要的人，希望有帮助！

在根目录下的 `/inc/` 文件夹中找到 `AspCms_MainClass.asp` 这个文件

利用 `Ctrl+F` 查找 `Function getSlide` （记得区分大小写）

在 `end Function` 上分方加入以下代码：

``` AspCMS
Dim str1,Str2,str3
str1 =Split(slideImgs,",") 
str2 =Split(slideLinks,",")
str3=Split(slideTexts,",")
Dim j
content=replaceStr(content,"{aspcms:SlideLen}",ubound(str1))
Dim i
for i=0 to ubound(str1)
content=replaceStr(content,"{aspcms:SlideImg"&i&"}",str1(i))
next
Dim n
for n=0 to ubound(str2)
content=replaceStr(content,"{aspcms:SlideLink"&n&"}",str2(n))
next
Dim m
for m=0 to ubound(str3)
content=replaceStr(content,"{aspcms:SlideText"&m&"}",str3(m))
next
```

注意：要在 `Function getSlide` 这个函数的结束 `end Function` 上方

然后前台调用方式

``` html
<a href="{aspcms:SlideLink0}" title="{aspcms:SlideText0}"><img src="{aspcms:SlideImg0}" /></a>
```

依次调用，修改0为1，为2....

0表示默认的第一张图片/第一个链接/第一个标题。默认0是第一计数。

然后就是自己把 `<a href=""></a>` 融合到自己喜欢的幻灯片中。测试通过显示正常，就完成了自定义幻灯片！

如果你用是的 `FALSH+XML` 估计你的自定义会受到影响，那就直接用XML决定路径调用吧！最好自定义的幻灯片是 `DIV` 的，这样比较好融合和修改！

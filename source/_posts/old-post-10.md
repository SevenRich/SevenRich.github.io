---
title: 企业网站必备的一段加入收藏|设为主页通用HTML代码
abbrlink: /post/10.html
author: 许时衡
categories: 旧博客迁移
date: 2014-04-26 20:02:04
tags:
    - HTML
    - JavaScript
---

常常在企业网站上面看到有加入收藏 | 设为主页的按钮，可是一但到自己要用的时候发现代码老实写错，不能用！今天就把自己常用的通用的 html 代码分享给需要的朋友！

首先我们需要建立一个 JS 文件，来保证按钮的赋值的正常。

比如说建立一个 `zhuye.js` 文件，代码如下；

``` JavaScript
//加入收藏
function AddFavorite(sURL, sTitle) {
    sURL = encodeURI(sURL);
    try {  
        window.external.addFavorite(sURL, sTitle);  
    } catch (e) {  
        try{  
            window.sidebar.addPanel(sTitle, sURL, "");  
        } catch (e) {  
            alert("加入收藏失败，请使用Ctrl+D进行添加,或手动在浏览器里进行设置.");
        }  
    }
}
//设为首页
function SetHome(url) {
    if (document.all) {
        document.body.style.behavior='url(#default#homepage)';
        document.body.setHomePage(url);
    } else {
        alert("您好,您的浏览器不支持自动设置页面为首页功能,请您手动在浏览器里设置该页面为首页!");
    }
}
```

这里面的字是可以修改的，比如说加入收藏失败引导语，可以根据情况来自定义 DIY哦。

然后呢，我们当然是需要在页面上建立按钮。

可以是图片的，当然也可以是文字的，下面我会文字、图片的都分享一下代码。

文字版加入收藏 | 设为首页 代码如下；

``` html
<script src="zhuye.js"></script>
<a onclick="SetHome(window.location)" href="javascript:void(0)">设为首页</a> | 
<a onclick="AddFavorite(window.location,document.title)" href="javascript:void(0)">加入收藏</a>
```

中间通常用 “ | ”隔开，如果你的CSS定义了可以不用。

图片版加入收藏 | 设为首页 代码如下；

``` html
<script src="zhuye.js"></script>
<a onclick="SetHome(window.location)" href="javascript:void(0)" title="设为首页">
<img src="{aspcms:sitepath}/Templates/{aspcms:defaulttemplate}/images/home.png" /></a> | 
<a onclick="AddFavorite(window.location,document.title)" href="javascript:void(0)" title="加入收藏">
<img src="{aspcms:sitepath}/Templates/{aspcms:defaulttemplate}/images/add.png" /></a>
```

其实大家一对照就知道，其实文字和图片的差别就在于A标签中多了一个 TITLE属性，文字改成了IMG图片链接。

如果你想全部换成图片 “ | ”也是可以换成图片的，可以自己定义一个 IMG链接。这样就更能融合自己的网站内容，显得更加个性。

完整的一套代码如下；

``` html
<!doctype html>
<html>
<head>
<title>设置为首页,加入收藏功能</title>
</head> 
<body> 
    <div> 
        <script src="zhuye.js"></script>
        <a onclick="SetHome(window.location)" href="javascript:void(0)">设为首页</a> | 
        <a onclick="AddFavorite(window.location,document.title)" href="javascript:void(0)">加入收藏</a> 
    </div> 
</body>
</html>
```

以上代码希望对同是网络技术人员，或者 SEO 爱好者有所帮助。我是耒阳许时衡，希望能和大家多多交流，探讨。

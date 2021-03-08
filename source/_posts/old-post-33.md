---
title: Php学习工具Sublime Text直接运行Php（配置教程）
abbrlink: /post/33.html
author: 许时衡
categories: 旧博客迁移
date: 2015-01-08 10:43:09
tags:
    - PHP
---

进修好长时间了，更新一下自己的动态。

`Sublime Text`是一个代码编辑器，很好用这个就不用我说了。

我今天就更新下自己的动态，也保存一点怕自己忘记的知识，到时好复习。

`Sublime`里直接运行`PHP`配置方法：

### 第一步：Php目录增加到环境变量里（win 8.1下）

我的电脑-->属性-->高级系统设置-->高级-->环境变量-->系统变量

找到变量为 `Path`的。

在最后面增加（分号）`Php`目录。如我的是：`D:\amp\php`。

[](201501081420701509607573.jpg){图片过期}

环境变量加好了就可以试试，`win + R`-->`cmd`-->`php -v` ,效果如下：

[](201501081420701422564374.png){图片过期}

### 第二步，设置Sublime Text中的 Build

`Sublime-->Tools-->Build System-->New Build System...`

修改成如下配置：

``` Bash
{  
    "cmd": ["php", "$file"], 
    "file_regex": "php$",  
    "selector": "source.php" 
}
```

`ctrl + s` 保存 命名为 : `PHP.sublime-build` （一般在`user`下）

接下来，当然是`Sublime Tex`t中玩`Php`

我就随便拿我学习时的`Php`做测试咯。效果还是不错的。用了0.1s。

[](201501081420701424447892.jpg){图片过期}

现在Happy的在`Sublime Text`中玩`Php`吧。

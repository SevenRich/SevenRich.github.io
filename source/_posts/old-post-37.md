---
title: EcShop出现的报错问题及解决方案
abbrlink: /post/37.html
author: 许时衡
categories: 旧博客迁移
date: 2015-03-20 10:56:17
tags:
    - PHP
    - ECShop
---

### 问题一：商城首页

报 错

``` PHP
Strict Standards: Only variables should be passed by reference in D:\wamp\ecshop\includes\cls_template.php on line 422
```

解决方法：

找到提示错误的文件 `cls_template.php` 及行号

把 `$tag_sel = array_shift(explode(' ', $tag));`

改成：

``` PHP
$tag_arr = explode(' ', $tag); 
$tag_sel = array_shift($tag_arr);
```

并且删除 `D:\wamp\www\ecshop\temp\caches` 下所有的文件

### 问题二：后台首页

报 错

``` PHP
Strict Standards: Non-static method cls_image::gd_version() should not be called statically in D:\wamp\www\ecshop\includes\lib_base.php on line 346
```

解决办法

找到 `D:\wamp\www\ecshop\includes\cls_image.php` 文件

搜索 `function gd_version` 改成 `static function gd_version`

### 问题三：后台-商店设置

``` PHP
Strict Standards: mktime(): You should be using the time() function instead in D:\wamp\www\ecshop\admin\sms_url.php on line 31
Strict Standards: mktime(): You should be using the time() function instead in D:\wamp\www\ecshop\admin\shop_config.php on line 32
```

解决办法

根据错误提示 把 `mktime()` 改成 `time()`

### 问题四：后台-起始页

``` PHP
Strict Standards: Redefining already defined c**tructor for class alipay in D:\www\es\includes\modules\payment\alipay.php on line 85
```

解决办法

1）、错误原因：
PHP 类，有两种构造函数，一种是跟类同名的函数，一种是 `__contruct()`。从`PHP5.4`开始，对这两个函数出现的顺序做了最严格的定义，必须是 `__c**truct()` 在前，同名函数在后

2）、
解决方法：
调换一下两个函数的前后位置即可。
以 `includes/modules/payment/alipay.php`  为例：
将下面这两个函数的位置互换一下就OK了，`__contruct()`在前，`alipay()`在后

``` PHP
function alipay()
{
}

function __contruct()
{
    $this->alipay();
}
```

3）、ECSHOP的很多类文件 都存在这个问题，都需要修改掉。

### 问题五：后台-数据备份

``` PHP
Strict standards: Redefining already defined constructor for class cls_sql_dump in D:\wamp\www\ecshop\admin\includes\cls_sql_dump.php on line 90
Strict standards: Non-static method cls_sql_dump::get_random_name() should not be called statically in D:\wamp\www\ecshop\admin\database.php on line 64
```

解决办法

根据错误提示 把 `cls_sql_dump`的 `function __construct()`改到 `function cls_sql_dump()`的前面

把 `cls_sql_dump`的 `function get_random_name()`改成 `static  function get_random_name()`的前面

### 问题六：

``` PHP
Deprecated: Assigning the return value of new by reference is deprecated in  \admin\sitemap.php on line 46 $sm =& new google_sitemap();
```

解决办法

在 5.3版本之后已经不允许在程序中使用”=&”符号。如果你的网站出现了 `Deprecated: Assigning the return value of new by reference is deprecated in 错 误`，别着急，先定位到出错的文件，查找下是不是在程序中使用了”=&”，例如刚才定位到网站程序中发现了下图的程序，发现使用了”=&” 符号，去掉‘&’符号之后程序运行正常

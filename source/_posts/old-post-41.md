---
title: Phpcms模块开发全过程记录帖
abbrlink: /post/41.html
author: 许时衡
categories: 旧博客迁移
date: 2015-05-15 12:31:17
tags:
    - PHP
    - PhpCMS
---

模块的开发，在`phpcms`的二开里面是经常用到。我当然也是经常打交道。记录下，方便日后查阅。

### 第一 了解模块的主要目录结构

``` PHP
classes 类目录
functions 函数目录
install 安装目录
   |-languages 模块的语言文件   
   |-templates 模块前台使用模板   
   |-config.inc.php 模块信息，填写模块名称、简介、开发者信息  
   |-extention.inc.php  后前管理菜单生成文件  
   |-model.php 模型定义文件   
   |-moduel.sql 用于向数据库插入 模块的配置信息，
templates 后台模板目录
uninstall 卸载模块相关文件目录
   |-extention.inc.php  后前管理菜单生成文件   
   |-model.php 模型定义文件
index.php 是前台浏览调用的类文件
```

了解了模块的主要目录结构，我们就能很轻易的做开发了。

### 第二 建立模块的基本目录结构

比如说我现在要做一个管理的后台应用：`Key密匙管理`。那我就需要在`phpcms/modules`建立一个`createkey目录`。

再依次在`createkey目录`下建立目录和文件树如下：

``` PHP
createkey  模块根目录
    classes 类目录
    functions 函数目录
    install 安装目录
       |-languages 模块的语言文件   
       |-templates 模块前台使用模板   
       |-config.inc.php 模块信息，填写模块名称、简介、开发者信息  
       |-extention.inc.php  后前管理菜单生成文件  
       |-model.php 模型定义文件   
       |-moduel.sql 用于向数据库插入 模块的配置信息，
    templates 后台模板目录
    uninstall 卸载模块相关文件目录
       |-extention.inc.php  后前管理菜单生成文件   
       |-model.php 模型定义文件
    index.php 是后台浏览调用的类文件
```

### 第三 配置模块配置文件config.inc.php

`install/config.inc.php` 代码如下：

``` PHP
<?php
    defined('IN_PHPCMS') or exit('Access Denied');
    defined('INSTALL') or exit('Access Denied');

    $module = 'createkey'; //模块的标识符，唯一性，不可重名,应该和目录同名
    $modulename = 'Key密匙管理'; 
    $introduce = 'Key密匙管理，用来APP授权Key生成！';
    $author = '七年';
    $authorsite = 'http://www.leiyangseo.com';
    $authoremail = 'workmart@vip.qq.com';
?>
```

### 第四 增加模块菜单

`install/extention.inc.php` 代码如下：

``` PHP
<?php
    defined('IN_PHPCMS') or exit('Access Denied');
    defined('INSTALL') or exit('Access Denied');

    #true或1，表示返回当前sql插入的id,因为子菜单要用到
    $parentid = $menu_db->insert(array('name' => 'createkey_manage','parentid' => '30','m' => 'createkey','c' => 'index','a' => 'init','data' => '','listorder' => 0,'display' => '1'),true);
    #$language数组中的值会追加到system_menu.lang.php的$LANG变量中
    $language = array('createkey_manage' => 'APP_Key密匙管理');
?>
```

`parentid`可以根据自己的需要去设置。想要附到指定ID，`后台 > 扩展 > 菜单管理 >id` 就能看到你想要指定的ID是多少。

### 第五 创建后台类文件和模板文件

后台类文件用`index.php`代码如下：

``` PHP
<?php
    defined('IN_PHPCMS') or exit('Access Denied');
    pc_base::load_app_class('admin', 'admin', 0);

    class index extends admin {
        function __construct() {
            parent::__construct();
        }

        public function init() {
            include $this->admin_tpl('index');
        }
    }
?>
```

模板文件`templates/index.tpl.php`代码如下：

备注：因为工作原因，代码保留核心不公开。

``` PHP
<?php
    defined('IN_ADMIN') or exit('No permission resources.');
    include $this->admin_tpl('header','admin');
?>
<div class="pad_10">
我是测试
</div>
</body>
</html>
```

### 第六 向模块表中插入模块安装信息

`install/moduls.sql`代码如下：

``` SQL
INSERT INTO `phpcms_module` (`module`, `name`, `url`, `iscore`, `version`, `description`, `setting`, `listorder`, `disabled`, `installdate`, `updatedate`) VALUES ('createkey', 'Key密匙管理', '', '0', '1.0', '', '', '0', '0', '2015-05-16', '2015-05-16');
```

字段的名称已经很好的阐述了字段的作用，所以我只对部分字段解释：

``` txt
iscore    为1,表示是系统内置模块，是必选模块，二次开发，通常值为0即可
disabled    1表示禁止卸载，0表示可卸载
setting    配置变量
```

---
title: wordpress 用函数自定义随机图片调用
abbrlink: /post/9.html
author: 许时衡
categories: 旧博客迁移
date: 2014-04-15 19:55:29
tags:
    - WordPress
    - PHP
---

wordpress 太强大了，每天去研究都有一些自己的心得。今天分享一下自己最近研究的一段代码。

在模板下的 `functions.php` 中添加一段支持外链缩略图的代码如下：

``` PHP
<?php 
//支持外链缩略图
if ( function_exists('add_theme_support') )
    add_theme_support('post-thumbnails');
    function catch_first_image() {
        global $post, $posts;
        $first_img = '';
        ob_start();
        ob_end_clean();
        $output = preg_match_all('/<img.+src=[\'"]([^\'"]+)[\'"].*>/i', $post->post_content, $matches);
        $first_img = $matches [1] [0];

        if (empty($first_img)) { //Defines a default image
            $random = mt_rand(1,20);
            echo get_bloginfo ( 'stylesheet_directory' );
            echo '/images/random/'.$random.'.jpg';
        }
        return $first_img;
    }
?>
```

其中有几个变量可以修改：

随机图片文件夹：

``` PHP
/images/random/
```

这个是模板下的images下的random文件夹下的图片，如果你想直接放在模板下。可以直接修改为：

``` PHP
/random/
```

随机图片的范围：

``` PHP
$random = mt_rand(1,20);
```

如果你在你的random中放置了8张图片，图片名称是1.jpg，2.jpg.....8.jpg。

你就需要修改范围：

``` PHP
$random = mt_rand(1,8);
```

其余的代码不建议修改，但是如果你的对编辑代码很有控制力。可以尝试修改某些细节。

除了函数中添加赋值语句，你还需要添加一个调去图片的缩略图文件，我们命名为thumbnail.php。

缩略图文件代码如下：

``` PHP
<?php if ( get_post_meta($post->ID, 'thumbnail', true) ) : ?>
    <?php $image = get_post_meta($post->ID, 'thumbnail', true); ?>
    <a href="<?php the_permalink() ?>" rel="bookmark" title="<?php the_title(); ?>"><img src="<?php echo $image; ?>" alt="<?php the_title(); ?>"/></a>
<?php else: ?>
<!-- 截图 -->
    <a href="<?php the_permalink() ?>" rel="bookmark" title="<?php the_title(); ?>">
    <?php if (has_post_thumbnail()) { the_post_thumbnail('thumbnail'); }
    else { ?>
        <img class="home-thumb" src="<?php echo catch_first_image() ?>" width="367px" height="240px" alt="<?php the_title(); ?>"/>
    <?php } ?>
    </a>
<?php endif; ?>
```

前台调用使用代码如下：

``` PHP
<?php include( TEMPLATEPATH . '/thumbnail.php' ); ?>
```

如果你想直接调用图片src链接，你可以用：

``` PHP
<?php echo catch_first_image() ?>
```

或者直接调用文章中的图片；

``` PHP
<?php echo $image; ?>
```

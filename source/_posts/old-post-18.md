---
title: 教你 DIY 为 WordPress 生成网站访问日志，告别后台下载
abbrlink: /post/18.html
author: 许时衡
categories: 旧博客迁移
date: 2014-06-12 20:38:01
tags:
    - WordPress
    - PHP
---

对于一个网站来说，分析站点访问日志是非常重要的一件事。但是经常去服务器后台查询网站的访问日志太麻烦，而且很多 vps 都不带有访问日志这个功能。在这里许时衡给大家分享一个小技巧，可以为 WordPress 生成网站访问日志，日志内容还是可以自定义的，这样就可以省去每次都要登录主机后台查询。

把下面的代码添加到主题的 `function.php` 文件中即可：

``` PHP
make_log_file();

function make_log_file(){
    //log文件名
    $filename = 'mylogs.txt';
    //去除rc-ajax评论以及cron机制访问记录
    if (strstr($_SERVER["REQUEST_URI"],"rc-ajax")== false
        && strstr($_SERVER["REQUEST_URI"],"wp-cron.php")== false ) {
        $word .= date('mdHis',$_SERVER['REQUEST_TIME'] + 3600*8) . " ";
        //访问页面
        $word .= $_SERVER["REQUEST_URI"] ." ";
        //协议
        $word .= $_SERVER['SERVER_PROTOCOL'] ." ";
        //方法,POST OR GET
        $word .= $_SERVER['REQUEST_METHOD'] . " ";
        //$word .= $_SERVER['HTTP_ACCEPT'] . " ";
        //获得浏览器信息
        $word .= getbrowser(). " ";
        //传递参数
        $word .= "[". $_SERVER['QUERY_STRING'] . "] ";
        //跳转地址
        $word .= $_SERVER['HTTP_REFERER'] . " ";
        //获取IP
        $word .= getIP() . " ";
        $word .= "\n";
        $fh = fopen($filename, "a");
        fwrite($fh, $word);
        fclose($fh);
    }
}

//获取IP地址，网上现成代码
function getIP() //get ip address
{
    if (getenv('HTTP_CLIENT_IP'))
    {
        $ip = getenv('HTTP_CLIENT_IP');
    } else if (getenv('HTTP_X_FORWARDED_FOR')) {
        $ip = getenv('HTTP_X_FORWARDED_FOR');
    } else if (getenv('REMOTE_ADDR')) {
        $ip = getenv('REMOTE_ADDR');
    } else {
        $ip = $_SERVER['REMOTE_ADDR'];
    }

    return $ip;
}

//获取浏览器信息，移动端，平板电脑数据还未加上。
function getbrowser()
{
    $Agent = $_SERVER['HTTP_USER_AGENT'];
    $browser = '';
    $browserver = '';

    if (ereg('Mozilla', $Agent) && ereg('Chrome', $Agent)) {
        $temp = explode('(', $Agent);
        $Part = $temp[2];
        $temp = explode('/', $Part);
        $browserver = $temp[1];
        $temp = explode(' ', $browserver);
        $browserver = $temp[0];
        $browserver = $browserver;
        $browser = 'Chrome';
    }

    if(ereg('Mozilla', $Agent) && ereg('Firefox', $Agent)) {
        $temp = explode('(', $Agent);
        $Part = $temp[1];
        $temp = explode('/', $Part);
        $browserver = $temp[2];
        $temp = explode(' ', $browserver);
        $browserver = $temp[0];
        $browserver = $browserver;
        $browser = 'Firefox';
    }

    if(ereg('Mozilla', $Agent) && ereg('Opera', $Agent)) {
        $temp = explode('(', $Agent);
        $Part = $temp[1];
        $temp = explode(')', $Part);
        $browserver = $temp[1];
        $temp = explode(' ', $browserver);
        $browserver = $temp[2];
        $browserver = $browserver;
        $browser = 'Opera';
    }

    if(ereg('Mozilla', $Agent) && ereg('MSIE', $Agent)) {
        $temp = explode('(', $Agent);
        $Part = $temp[1];
        $temp = explode(';', $Part);
        $Part = $temp[1];
        $temp = explode(' ', $Part);
        $browserver = $temp[2];
        $browserver = $browserver;
        $browser = 'Internet Explorer';
    }

    if($browser != '') {
        $browseinfo = $browser.' '.$browserver;
    } else {
        $browseinfo = $_SERVER['HTTP_USER_AGENT'];
    }
    return $browseinfo;
}
```

ok，在你的站点根目录上就会生成 `mylogs.txt` 这个文件，通过 `http://域名/mylogs.txt` 可以直接访问。这样生成的网站日志会比 `CNZZ` 等第三方统计工具生成的日志精准的多，你可以通过日志得知哪些人访问哪些文件，哪些蜘蛛爬行过了等等信息。

> 如果以上信息对你有用，请分享给你的好朋友，但是请记得注明： `《 来源：耒阳SEO www.leiyangseo.com 》`

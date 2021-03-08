---
title: 备注下PHP GD库函数，方便日后使用
abbrlink: /post/40.html
author: 许时衡
categories: 旧博客迁移
date: 2015-04-28 11:59:40
tags:
    - PHP
---

GetImageSize

作用：取得图片的大小[即长与宽]

用法：array GetImageSize(string filename, array [imageinfo]);

ImageArc

作用：画弧线 

用法：int ImageArc(int im, int cx, int cy, int w, int h, int s, int e, int col);

ImageChar

作用：写出横向字符 

用法：int ImageChar(int im, int font, int x, int y, string c, int col);

ImageCharUp

作用：写出竖式字符

用法：int ImageCharup(int im, int font, int x, int y, string c, int col);

ImageColorAllocate

作用：匹配颜色

用法：int ImageColorAllocate(int im, int red, int green, int blue);

ImageColorTransparent

作用：指定透明背景色

用法：int ImageColorTransparent(int im, int [col]);

ImageCopyResized

作用：复制新图并调整大小 

用法：int ImageCopyResized(int dst_im, int src_im, int dstX, int dstY, int srcX, int srcY, int dstW, int dstH, int srcW, int srcH);

ImageCreate

作用：建立新图

用法：int ImageCreate(int x_size, int y_size);

ImageDashedLine

作用：绘虚线 

用法：int ImageDashedLine(int im, int x1, int y1, int x2, int y2, int col);

ImageDestroy 

作用：结束图形 

用法解释：int ImageDestroy(int im);

ImageFill

作用：图形着色

用法：int ImageFill(int im, int x, int y, int col);

ImageFilledPolygon

作用：多边形区域着色

用法：int ImageFilledPolygon(int im, array points, int num_points, int col);

ImageFilledRectangle

作用：矩形区域着色 

用法：int ImageFilledRectangle(int im, int x1, int y1, int x2, int y2, int col);

ImageFillToBorder

作用：指定颜色区域内着色

用法：int ImageFillToBorder(int im, int x, int y, int border, int col);

ImageFontHeight

作用：取得字型的高度

用法：int ImageFontHeight(int font);

ImageFontWidth

作用：取得字型的宽度

用法：int ImageFontWidth(int font);

ImageFontWidth

作用：取得字型的宽度

用法：int ImageFontWidth(int font);

ImageLine

作用：绘实线

用法：int ImageLine(int im, int x1, int y1, int x2, int y2, int col);

ImageLoadFont

作用：载入点阵字型

用法：int ImageLoadFont(string file);

ImagePolygon

作用：绘多边形

用法：int ImagePolygon(int im, array points, int num_points, int col);

ImageRectangle

作用：绘矩形

用法：int ImageRectangle(int im, int x1, int y1, int x2, int y2, int col);

ImageSetPixel

作用：绘点

用法：int ImageSetPixel(int im, int x, int y, int col); 

ImageString

作用：绘横式字符串

用法：int ImageString(int im, int font, int x, int y, string s, int col);

ImageStringUp

作用：绘直式字符串

用法：int ImageStringUp(int im, int font, int x, int y, string s, int col);

ImageSX

作用：取得图片的宽度

用法：int ImageSX(int im);

ImageSY

作用：取得图片的高度

用法：int ImageSY(int im);

ImageTTFBBox

作用：计算 TTF 文字所占区域

用法：array ImageTTFBBox(int size, int angle, string fontfile, string text);

ImageTTFText

作用：写 TTF 文字到图中

用法：array ImageTTFText(int im, int size, int angle, int x, int y, int col, string fontfile, string text); 

ImageColorAt

作用：取得图中指定点颜色的索引值

用法：int ImageColorAt(int im, int x, int y);

ImageColorClosest

作用：计算色表中与指定颜色最接近者

用法：int ImageColorClosest(int im, int red, int green, int blue);

ImageColorExact

作用：计算色表上指定颜色索引值

用法：int ImageColorExact(int im, int red, int green, int blue);

ImageColorResolve

作用：计算色表上指定或最接近颜色的索引值

用法：int ImageColorResolve(int im, int red, int green, int blue);

ImageColorSet

作用：设定色表上指定索引的颜色

用法：boolean ImageColorSet(int im, int index, int red, int green, int blue);

ImageColorsForIndex

作用：取得色表上指定索引的颜色

用法：array ImageColorsForIndex(int im, int index);

ImageColorsTotal

作用：计算图的颜色数

用法：int ImageColorsTotal(int im);

ImagePSLoadFont

作用：载入 PostScript 字型

用法：int ImagePSLoadFont(string filename);

ImagePSFreeFont

作用：卸下 PostScript 字型

用法：void ImagePSFreeFont(int fontindex);

ImagePSEncodeFont

作用：PostScript 字型转成向量字

用法：int ImagePSEncodeFont(string encodingfile);

ImagePSText

作用：写 PostScript 文字到图中

用法：array ImagePSText(int image, string text, int font, int size, int foreground, int background, int x, int y, int space, int tightness, float angle, int antialias_steps);

ImagePSBBox

作用：计算 PostScript 文字所占区域

用法： array ImagePSBBox(string text, int font, int size, int space, int width, float angle);

ImageCreateFromPNG

作用：取出 PNG 图型

用法：int ImageCreateFromPng(string filename);

ImagePNG

作用：建立 PNG 图型

用法：int ImagePng(int im, string [filename]);

ImageCreateFromGIF

作用：取出 GIF 图型

用法：int ImageCreateFromGif(string filename);

ImageGIF

作用：建立 GIF 图型 

用法：int ImageGif(int im, string [filename]);

GD使用一般步骤：(PHP)

``` PHP
if (!isset($_SESSION)) { //判断session是否开启
    session_start(); //开启就session
} 

$width = 70; //布画宽度
$height = 25; //布画高度
$length = 4;//验证码长度
$code = getcode($length); //获取随机字符串
$_SESSION['verfyCode'] = $code; 

$img = imagecreate($width, $height);
$bgcolor = imagecolorallocate($img, 240, 240, 240);
$rectangelcolor = imagecolorallocate($img, 150, 150, 150);
imagerectangle($img, 1, 1, $width-1, $height-1, $rectangelcolor);//画边框

for ($i = 0; $i < $length; $i++) {//循环写字
    $codecolor = imagecolorallocate($img, mt_rand(50, 200), mt_rand(50, 128), mt_rand(50, 200));
    $angle = rand(-20, 20);
    $charx = $i * 15 + 8;
    $chary = ($height + 14) / 2 + rand(-1, 1);
    imagettftext($img, 15, $angle, $charx, $chary, $codecolor, './ariblk.ttf', $code[$i]);
}

for ($i = 0; $i < 20; $i++) {//循环画线
    $linecolor = imagecolorallocate($img, mt_rand(0, 250), mt_rand(0, 250), mt_rand(0, 250));
    $linex = mt_rand(1, $width - 1);
    $liney = mt_rand(1, $height - 1);
    imageline($img, $linex, $liney, $linex + mt_rand(0, 4) - 2, $liney + mt_rand(0, 4) - 2, $linecolor);
}

for ($i = 0; $i < 100; $i++) {//循环画点
    $pointcolor = imagecolorallocate($img, mt_rand(0, 250), mt_rand(0, 250), mt_rand(0, 250));
    imagesetpixel($img, mt_rand(1, $width - 1), mt_rand(1, $height - 1), $pointcolor);
}

function getcode($length) {//生成php随机数 
    $pattern = '1234567890ABCDEFGHIJKLOMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz ';//字符池 
    for ($i = 0; $i < $length; $i++) { 
        $key .= $pattern{mt_rand(0, 35)}; 
    } 
    return $key; 
}

ob_clean();
header('Content-type:image/png'); 
imagepng($img);
```

通常按需增加某些功能。结合session就能做登录验证用。

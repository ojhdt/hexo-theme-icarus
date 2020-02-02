---
title: 使用 Fancybox 为博客添加图片放大预览功能
date: 2019-06-22 19:52:34
categories: "小记"
tags: [Fancybox,jQuery]
thumbnail: "https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20180908/0.png"
toc: true
excerpt: "FancyBox 是一款基于jQuery的弹出库，用于呈现各种类型的媒体。 可以用于显示图片、视频，并可以响应很多交互操作。"
---
FancyBox 是一款基于jQuery的弹出库，用于呈现各种类型的媒体。 可以用于显示图片、视频，并可以响应很多交互操作。https://fancyapps.com/fancybox/3/

在没有自带图片缩放功能的博客中，查看图片上的文字很不方便，Fancybox 提供的图片浏览功能可以很好的解决该问题。本文将综合官方文档和网络上所获得的介绍，分享一个安装及使用 Fancybox 的通用方法。

#### 引入 FancyBox 库
将以下代码添加到 </head> 标签前。由于 Hexo 的特殊文件结构，head 部分通常被单独划分至 `/themes/主题名/layout/_partial/head.ejs` 中。在不同主题中该路径可能有所更改。
```
<script src="//code.jquery.com/jquery-3.3.1.min.js"></script>
```
```
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/fancyapps/fancybox@3.5.7/dist/jquery.fancybox.min.css" />
```
```
<script src="https://cdn.jsdelivr.net/gh/fancyapps/fancybox@3.5.7/dist/jquery.fancybox.min.js"></script>
```
至此，Fancybox 最基本的功能已经被成功安装，我们可以根据官方文档指引，在文章中加入
```
<a data-fancybox="gallery" href="big_1.jpg"><img src="small_1.jpg"></a>
```
建立一张可以预览的图片。但旧有的图片仍不能点击预览，我们需要对其进行处理。

#### 将 Fancybox 应用到页面中
在 /themes/主题名/source/js/下建立 `warp.js` ，填入以下内容

```
$("img").not('.page__logo img').each(function () {
   // $(this).attr("data-fancybox", "gallery"); 直接给img添加data-fancybox会导致点击图片后图片消失
    var element = document.createElement("a");
    $(element).attr("data-fancybox", "gallery");
    $(element).attr("href", $(this).attr("src"));
    $(this).wrap(element);
});
```

>注释：该代码将在博客文件读取后执行，用于向 `<img>` 标签外嵌套 FancyBox 所要求的 `<a>` 标签。但由于该代码将硬性将 FancyBox 应用于所有图片文件，包括 图标，按钮等不希望应用的图片素材。因此需要修改 `.not()` 排除部分对象，如本例中的.not('.page__logo img')。类名一般可以在 `themes/主题名/source/css(scss)/` 中对应文件找出，具体情况应对比 js 文件和 css 文件。


在 `</footer>` 前引入刚刚建立的 js 。footer 部分通常被单独划分至 `/themes/主题名/layout/_partial/footer.ejs` 中。
```
<script src="/js/warp.js"></script>
```
执行 hexo g 重新生成博客，FancyBox 应该就可以正常使用了。
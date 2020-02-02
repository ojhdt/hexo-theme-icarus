---
title: 离Hexo博客搭建只差一个教程（五）：第三方服务——Google 服务
date: 2018-10-13 17:15:14
categories: "教程"
tags: [Blog,Hexo,Google]
thumbnail: "https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181002/0.png"
toc: true
excerpt: "为了实时监控网站流量，搜集访问数据，我们需要向博客中添加网站数据统计。在这篇教程中，我们将会介绍 Google 提供的几项服务。"
---
>上一篇：[离Hexo博客搭建只差一个教程（四）：第三方服务——APlayer](https://blog.ojhdt.com/20181006/hexo-4)


在上一篇教程中，我们讲述了在博客中插入 APlayer 的方法。

为了实时监控网站流量，搜集访问数据，我们需要向博客中添加网站数据统计。在这篇教程中，我们将会介绍 Google 提供的几项服务。

## 提交搜索引擎
主要介绍 Google抓取工具 和 提交站点地图 两种途径。Google抓取工具针对个别网页，站点地图可以实现自动提交索引。

### 验证网站所有权

1. 前往 [Google Search Console](https://www.google.com/webmasters/tools/home?hl=zh-CN) 。并登陆你的Google账户。

2. 输入你的博客地址，点击 **添加资源** 。

在验证方法中选择 `备用方法->HTML标记` 。复制验证代码。并将该代码加入网站`<header>`标签中。
>在Hexo中，大部分主题已经内置所有权验证。仅需将该验证代码填入主题配置文件中即可完成验证。具体方法请查阅主题文档。
>
>若博客已使用 Google Analytics（分析），可以使用 Google Analytics 快捷验证。

3. 返回验证页面，点击 **验证** 。

![1](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181013/1.png)

### 使用 Google 抓取工具

1. 访问 [Google 抓取工具](https://www.google.com/webmasters/tools/googlebot-fetch?hl=zh-CN) 页面，选择已经过验证的资源。

2. 留空网址抓取首页，或输入你希望收录的网址，点击 **抓取** 。

3. 等待抓取完成，点击 **请求编入索引** 。

![2](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181013/2.png)

### 提交站点地图

1. 安装 **sitemap** 插件。
```
npm install hexo-generator-sitemap --save
```
2. 在 **站点配置文件** _config.yml 末尾添加以下代码：
```
sitemap:
path: sitemap.xml
```
3. 更新 Hexo 。
```
hexo clean
hexo g
hexo d
```
在 `/public` 目录下会生成 `sitemap.xml` 。

4. 访问 [站点地图报告](https://www.google.com/webmasters/tools/sitemap-list?hl=zh-CN) 页面，选择已经过验证的资源。

5. 点击 **添加/测试站点地图**，在弹出的方框中输入 `sitemap.xml` 。点击 **测试** 。在成功导入后再点击 **提交** 。


## Google Adsense

可以参阅我之前写的文章 [申请Google AdSense全记录](https://blog.ojhdt.com/20180908/adsense/)。它能通过投放广告为你的博客产生微薄收入。
>收入与广告点击率，点击量和网页浏览量等有关，具有波动性。以美区为例，点击一次通常可以获得数美分的收入。

1. 进入 [Adsense 页面](https://www.google.com/adsense/signup?subid=ww-ww-et-HC-acqpage&utm_source=internal&utm_medium=et&utm_campaign=adsense-help-acq) 注册账户。填写好基本信息。

![4](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181013/4.png)

2. 将提供给你的验证代码添加到你的网站HTML中，放置在 `<head>` 和 `</head>` 标记之间，等待 Google 团队审核。这一阶段通常需要较长时间。审核期间要保证网站正常访问且符合 [AdSense内容合作规范](https://support.google.com/adsense/answer/1348688#Copyrighted_material) 。

![5](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181013/5.png)

3. 配置你希望投放的广告类型，配置广告单元样式。

![6](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181013/6.png)

4. 将生成的 HTML 广告代码嵌入希望添加的页面。


>Adsense 存在起付金额门槛，收入达到 100$ 时才能申请付款。

## Google Analytics

Google Analytics（分析）是Google提供的统计服务。它可以自动生成全方位的网站报告。包括实时访问人数，访问量，访问途径，用户喜欢的内容等。

Analytics的浏览十分简便。不仅支持多平台网页浏览，还提供 Android 平台客户端。

官方帮助：https://support.google.com/analytics/?hl=zh-Hans#

### 安装
1. 访问 [Analytics 注册页面](https://analytics.google.com/analytics/web/?authuser=0#/provision/SignUp) ，登陆 Google 账户。
2. 设置 **账号名称**，**网站名称** 和 **网站网址**。
3. 点击 **获取跟踪id**，你会得到网站的跟踪id（通常以 `UA-` 开头)和跟踪代码。

![3](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181013/3.png)

>在Hexo中，大部分主题已经内置 Google Analytics。仅需将该跟踪id填入主题配置文件中即可启用 Analytics。具体方法请查阅主题文档。

4. 将跟踪代码添加到主题中。以默认主题Landscape为例，仅需把代码添加到`themes/landscape/layout/_partial/after-footer.ejs`末尾即可。

至此，访问 Analytics 页面即可获得详细的网页报告。

## 参考文章
[1] 起飞页.[如何将网站提交到google？](https://www.qifeiye.com/%E5%A6%82%E4%BD%95%E5%B0%86%E7%BD%91%E7%AB%99%E6%8F%90%E4%BA%A4%E5%88%B0google%EF%BC%9F/)

[2] 风行天下.[hexo站点地图](https://www.cnblogs.com/php-linux/p/8493181.html)

[3] Azyueki.[在 Hexo 使用 Google Analytics](http://azyukei.github.io/2015/04/Hexo-Google-Analytics/)

## 写在后面
>感谢您的阅读！若您在阅读时发现教程存在疏漏或无法理解的地方，可以通过 **评论区留言** 进行交流讨论。
>
>上一篇：[离Hexo博客搭建只差一个教程（四）：第三方服务——APlayer](https://blog.ojhdt.com/20181006/hexo-4)
>
>下一篇：[离Hexo博客搭建只差一个教程（六）：第三方服务——对象存储COS](https://blog.ojhdt.com/20190404/hexo-6)

此文章为原创作品，禁止转载。如需转载请先经过许可，并在转载中注明原作者及出处。

请 `收藏` 本博客，本博客将持续更新。

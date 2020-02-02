---
title: 离Hexo博客搭建只差一个教程（二）：主题
date: 2018-10-04 17:23:54
categories: "教程"
tags: [Blog,Hexo]
thumbnail: "https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181002/0.png"
toc: true
excerpt: "在主题篇中，文章将会重点介绍主题的安装与配置，以及两套优秀的主题—— NexT 与 Material 。"
---
>上一篇：[离Hexo博客搭建只差一个教程（一）：基础搭建](https://blog.ojhdt.com/20181002/hexo-1)

在上一篇教程中，我们初步了解了 **Hexo** 和 **GitHub Pages** ，成功建立并初步配置自己的 Hexo ，实现通过 xxx.github.io 访问，并简单介绍了 多端同步更新 和 域名购买 事宜。

本篇教程中，我们将会介绍 Hexo 的一个重量级功能——**主题**。

## 正文

### 介绍

Hexo 本身只是博客框架，主题功能才是 Hexo 的灵魂。它使用户更加容易地进行个性化。它不仅支持用户安装主题，还支持用户自行制作并发布主题。主题突破了框条的束缚，简单快捷的应用也降低了门槛和学习成本。

官方文档： https://hexo.io/zh-cn/docs/themes.html

Hexo 默认提供一个 Landscape 主题。虽然默认主题并不差，但原生的主题一般不太讨喜。Hexo 提供了数量庞大的主题供用户选择。目前，Hexo 上已经收录国内外超过 200 个风格各异的主题。有兴趣的朋友们可以访问https://hexo.io/themes/ 浏览并安装使用。

![1](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181004/1.png)

### 主题通用安装方法

Hexo 安装主题的方法非常简单。大致思路为 克隆主题文件夹到themes目录 -> 在配置文件中启用主题。

进入博客本地目录，右键打开 **Git Bash**。

使用 `git clone` 命令克隆希望安装的主题：

```
git clone 【主题clone URL】 themes/【主题名】
```
>该clone命令通常会在主题 GitHub 项目发布页上提供。

此处以下载 NexT 主题为例：
```
git clone https://github.com/theme-next/hexo-theme-next themes/next
```

修改站点配置文件 **_config.yml** ，找到该行：
```
## Themes: https://hexo.io/themes/
theme: landscape
```
将 `landscape` 修改为下载的主题名。

保存。更新博客，若不报错则主题安装完毕。

>部分主题还提供手动安装渠道。该安装方法与使用 `git clone` 命令效果一致。但无法通过指令获得主题更新。在发布页面下载 Source Code(zip)，解压所下载的压缩包至博客的 themes 目录下，并将 解压后的文件夹名称 更改为 主题名称。
>
>同样需要修改 站点配置文件 中 `theme` 字段来启用主题。

同时你可以使用指令方便地更新你的主题。
```
cd themes/主题名称
git pull
```

### 组成

一个 Hexo 主题通常会有以下的结构：

#### _config.yml
主题配置文件。修改时会自动更新，无需重启服务器。通常对主题的自定义仅需修改该配置文件。

#### languages
语言文件夹。国际化（internationalization）功能于此存放语言文件。

#### layout

布局文件夹。用于存放主题的模板文件，决定了网站内容的呈现方式。

在为网站添加组件（如广告）时可修改该部分文件。

#### scripts
脚本文件夹。使插件工作。

#### source
资源文件夹。存放主题所引用的媒体文件。

### 注意

- Hexo 主题通常会附带大量配置项，并集成第三方服务。在使用前请查阅作者的相关文档。
- 安装使用主题后，你的博客将会出现两个配置文件：**站点配置文件**_config.yml（位于博客根目录） 和 **主题配置文件**_config.yml（位于themes\主题文件夹）。在配置时切忌搞混。
- 在应用主题前请先设置好 **站点配置文件** 中的有关博客基础信息的设置。
- 主题的一些常见问题会在 GitHub issue 上向开发者反馈。如果频繁报错，不妨访问一下 项目issue 。

### NexT 主题介绍
>精于心，简于形

NexT 主题是目前最广泛使用的主题之一。内置多种不同的风格。NexT 主旨在于简洁优雅且易于使用，配置方便简单。

- 支持10国语言
- 原生支持大量[第三方服务](http://theme-next.iissnan.com/third-party-services.html)
- 支持标签页，分类页添加
- 自动添加链接到您的社交媒体账户
- 内置 5 种代码高亮主题

**官网**：http://theme-next.iissnan.com/
>具体配置项请自行前往官网查阅。

GitHub：https://github.com/iissnan/hexo-theme-next

中文使用文档：https://github.com/iissnan/hexo-theme-next/blob/master/README.cn.md

![2](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181004/2.png)

#### 安装

使用Git安装
```
git clone https://github.com/theme-next/hexo-theme-next themes/next
```

或使用 [手动安装](https://github.com/iissnan/hexo-theme-next/releases/latest)。

### Material 主题介绍
>Nature, Pure | 原质，纯粹

Material 主题是一款精致的采用 Material Design 设计的主题。优雅、纯粹、质感。

本站目前采用的即为该主题。

介绍及文档：https://material.viosey.com/

GitHub：https://github.com/viosey/hexo-theme-material

>目前因主站SSL证书过期，无法访问文档。此处放出[文档备份](https://www.lanzous.com/i20oo1g)。

- 精美的 Material Design 动画
- 多语言支持
- 集成第三方服务
- 自定义页面

![4](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181004/4.png)

#### 安装
使用Git安装
```
git clone https://github.com/viosey/hexo-theme-material.git themes/material
```
或使用 [手动安装](https://github.com/viosey/hexo-theme-material/releases/latest)。

>**注意！** 在主题的开发迭代过程中，主题的配置文件模板 可能会改动。为了避免使用 `git pull` 更新主题的用户出现冲突，我们将 主题配置文件模板 命名为 **_config.template.yml**。配置主题时，你应该拷贝一份 **_config.template.yml** 并将其重命名为 **_config.yml**。


在由[@arleyGuoLei](https://github.com/arleyGuoLei)提出的[issue](https://github.com/viosey/hexo-theme-material/issues/686)中，[@michaelcai](https://github.com/michaelcai)给出了解决 `hexo g` 时报错的解决方案：
>修改layout/_widget/dnsprefetch.ejs文件。修改内容如下：
```
<% } else if(theme.comment.use.startsWith("disqus")) { %>
```
修改为
```
<% } else if(theme.comment.use && theme.comment.use.startsWith("disqus")) { %>
```
>原因在于没有对配置做基本的检查。事实上里面很多配置只要任意少一些都会直接炸，没有做任何的默认选项。
>
>因为版本可能改动了文件位置，不过你可以全局搜索关键字，修改方式也是前面加检查即可。

## 参考文章
[1]MARKSZのBlog.[Hexo主题开发经验杂谈](https://molunerfinn.com/make-a-hexo-theme/)

[2]阳春面.[Hexo博客主题推荐](https://www.jianshu.com/p/bcdbe7347c8d)

## 写在后面
>感谢您的阅读！若您在阅读时发现教程存在疏漏或无法理解的地方，可以通过 **评论区留言** 进行交流讨论。
>
>上一篇：[离Hexo博客搭建只差一个教程（一）：基础搭建](https://blog.ojhdt.com/20181002/hexo-1)
>
>下一篇：[离Hexo博客搭建只差一个教程（三）：第三方服务——Valine](https://blog.ojhdt.com/20181005/hexo-3)

此文章为原创作品，禁止转载。如需转载请先经过许可，并在转载中注明原作者及出处。

请 `收藏` 本博客，本博客将持续更新。

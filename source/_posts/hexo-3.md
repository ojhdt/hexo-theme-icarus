---
title: 离Hexo博客搭建只差一个教程（三）：第三方服务——Valine
date: 2018-10-05 12:08:54
categories: "教程"
tags: [Blog,Hexo]
cover: "https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181002/0.png"
toc: true
excerpt: "Valine - 一款快速、简洁且高效的无后端评论系统。借助Leanapp运行。"
---
>上一篇：[离Hexo博客搭建只差一个教程（二）：主题](https://blog.ojhdt.com/20181004/hexo-2)


在上一篇教程中，我们集中讨论了 Hexo 的主题功能，介绍了主题的基本安装和配置方法，推荐了两款优秀 Hexo 主题。

从本篇教程开始，我们将会介绍一些可以在博客中应用的第三方服务。Hexo 搭建的是博客为静态网页，无需经过服务器的编译，直接加载到用户浏览器。虽然提高了网页打开的速度，但由于不能在服务器运行程序，无法使页面内容自主更新。第三方服务的使用很好地弥补了 Hexo 的“硬伤”。在为 Hexo 加入第三方提供的控件后，不仅博客增色不少，而且功能也更加完善。

在本篇中，我们将会介绍一款优秀的评论系统 —— **Valine**。

## 正文

### 介绍
Valine - 一款快速、简洁且高效的无后端评论系统。

理论上支持但不限于静态博客，目前已有Hexo、Jekyll、Typecho、Hugo 等博客程序在使用 Valine。

- 快速
- 安全
- Emoji
- 无后端实现
- MarkDown 全语法支持
- 轻量易用
- 文章阅读量统计

GitHub：https://github.com/xcss/Valine/

详细介绍与安装教程请点击 官网：https://valine.js.org/

![1](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181005/1.png)

#### 为什么选择 Valine

曾经使用的是国外的 Disqus，加载速度慢，需要单独注册 Disqus 账号，某些场合下还需要科学上网。留言门槛过高导致无人评论，评论系统也就失去了它的初衷。

来必力，仍然需要用户注册，且功能过于臃肿。

多说和网易云跟帖已阵亡。

相比起来，界面简洁，配置简单的 **Valine** 就成了最佳选择。

### 安装及应用

注册 [LeanCloud](https://leancloud.cn/) ，进入控制台，新建一个应用，应用名自行填写。

进入该应用，点击 **设置->应用Key**，复制`appId`和`appKey`。

![2](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181005/2.png)

目前，已有一大部分主流Hexo主题内置 Valine，请前往[该页面](https://valine.js.org/hexo.html)查看列表。若你的主题已得到支持，根据 主题文档 在 主题配置文件 中填写`appId`及`appKey`即可激活Valine。

>若你的主题不在支持列表中，你需要手动进行安装。
>
>在文章页引入：
>
```
<head>
    <script src="//cdn1.lncld.net/static/js/3.0.4/av-min.js"></script>
    <script src='//unpkg.com/valine/dist/Valine.min.js'></script>
</head>
<body>
    <div id="vcomments"></div>
    <script>
        new Valine({
            el: '#vcomments',
            appId: '<API_ID>',
            appKey: '<API_Key>'
            placeholder: 'just go go' 
        })
    </script>
</body>
```

返回控制台，点击 设置->安全中心 ，在 `Web 安全域名` 一项中添加自己的博客地址。

![3](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181005/3.png)

更新博客，Valine评论系统就成功安装在你的博客上了。

>通过 [Disqus2LeanCloud](http://disqus.panjunwen.com/) 可以方便地将数据由Disqus迁移至LeanCloud。
>
>感谢DESERTS提供的 Disqus2LeanCloud 工具。

### Valine Admin 评论数据管理
由于Valine 是无后端评论系统，所以也就没有开发评论数据管理功能。但是，我们可以通过 zhaojun1998 开发的 **Valine Admin** 来进行评论数据管理。Valine Admin 修改自 panjunwen 的项目 [Valine-Admin](https://github.com/panjunwen/Valine-Admin) ，修改后的版本更加便于安装且实用。

通过 Valine Admin，我们可以后台管理博客评论数据，增强 Valine 的邮件通知功能，还支持自定义邮件模板。

GitHub：https://github.com/zhaojun1998/Valine-Admin

打开 LeanCloud 后台。进入 **云引擎->设置** ，在`代码库`中填写 `https://github.com/zhaojun1998/Valine-Admin` 并保存。

![4](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181005/4.png)

进入 **云引擎->部署** ，点击`Git 源码部署`。分支或版本号一项填入 `master` ，点击部署。等待部署完成。

![5](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181005/5.png)

![6](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181005/6.png)

进入 **云引擎->设置**，查看`自定义环境变量`一项，点击`添加新变量`，为云引擎提供必要的信息。

必选参数：

| 变量名          | 值                |
|:--            |:--                  |
| `SITE_NAME`      | 网站名称。                |
| `SITE_URL`       | 网站地址，最后**不要**加 `/` 。                |
| `SMTP_USER`        | SMTP服务用户名，一般为邮箱地址。            |
| `SMTP_PASS`     | SMTP 密码，一般为授权码，而不是邮箱的登陆密码。            |
| `SMTP_SERVICE`        | 邮件服务提供商，支持 `QQ`、`163`、`126`、`Gmail`、`Yahoo`等。|
| `SENDER_NAME`  | 寄件人名称。|

可选参数：

| 变量名          | 值                |
|:--            |:--                  |
| `TEMPLATE_NAME`      | 邮件模板。可选择填写 [default](https://blog.ojhdt.com/img/20181005/default.png) 或 [rainbow](https://blog.ojhdt.com/img/20181005/rainbow.png) 。（点击查看预览）      |
| `TO_EMAIL`       | 指定站长收信邮箱，默认值为 SITE_USER。用于 SMTP 发件人与站长收件人不一致的情况下使用。                |
| `SMTP_HOST`        | 邮件服务提供商 SMTP 地址，如 QQ : `smtp.qq.com`。此项需要自行查询或询问其服务商。            |
| `SMTP_PORT`     | 邮件服务提供商 SMTP 端口, 此项需要自行查询或询问其服务商。            |
| `SMTP_SECURE`        | 是否启用加密, 默认为 `true`，一般不需要设置。|

填写示例：

![7](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181005/7.png)

>**在 QQ邮箱 中开启SMTP服务教程**
>
>登陆 [QQ邮箱](https://mail.qq.com/) ，点击 `设置`。
>
>![8](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181005/8.png)
>
>点击 `账户`，拉到页面下方，找到 **POP3/IMAP/SMTP/Exchange/CardDAV/CalDAV服务** 。
>
>![9](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181005/9.png)
>
>开启 **IMAP/SMTP服务** 一项。按照提示发送验证短信进行开通。
>
>开通成功后，你将会收到授权码，将其填入 `SMTP_PASS` 即可。

进入 **云引擎->设置** ，查看 `Web主机域名` ，设置当前应用的web主机域名。该处选择一个自己喜欢的前缀，保存即可。

![10](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181005/10.png)

进入 存储 ，点击数据中的`_User`，点击`添加行`。来设定登陆后台的账号密码。只需要填写 `email`、`password`、`username` 这三个字段即可, 使用 email 作为账号登陆即可。为了安全考虑，此 `email` 必须为配置中的 `SMTP_USER`。

至此，你已可以使用 Valine Admin 对你的评论进行管理。访问你设置的 Web 主机域名（xxx.leanapp.cn）即可进入管理后台。

在评论后收到他人的回复将会收到邮件提醒。

在访客在你的博客上发表留言时，站长可以得到邮件通知。

## 参考文章
[1]叉叉白.[加个Valine评论系统](https://www.xxwhite.com/2017/Valine.html)

[2]blue_zy.[为你的Hexo加上评论系统-Valine](https://blog.csdn.net/blue_zy/article/details/79071414)

[3]云淡风轻.[Valine -- 一款极简的评论系统](https://ioliu.cn/2017/add-valine-comments-to-your-blog/)

[4]Deserts.[Valine: 独立博客评论系统](https://panjunwen.com/diy-a-comment-system/)

## 写在后面
>感谢您的阅读！若您在阅读时发现教程存在疏漏或无法理解的地方，可以通过 **评论区留言** 进行交流讨论。
>
>上一篇：[离Hexo博客搭建只差一个教程（二）：主题](https://blog.ojhdt.com/20181004/hexo-2)
>
>下一篇：[离Hexo博客搭建只差一个教程（四）：第三方服务——APlayer](https://blog.ojhdt.com/20181006/hexo-4)

此文章为原创作品，禁止转载。如需转载请先经过许可，并在转载中注明原作者及出处。

请 `收藏` 本博客，本博客将持续更新。

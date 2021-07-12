---
title: 初识 h5ai
date: 2020-02-14 13:43:30
categories: "小记"
tags: [H5ai]
cover: "https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200215/1.png"
toc: true
excerpt: "h5ai —— 一个轻量化的 PHP 文件目录列表程序。它的大小只有100kb，但支持在线预览文本、图片、音频、视频等，已经足以满足大多数应用场景。"
---
服务器每月1000G的流量放着也是浪费，盘算着搭一个云盘来造福一下大众。寻寻觅觅间让我遇见了 h5ai —— 一个轻量化的 PHP 文件目录列表程序。它的大小只有100kb，但支持在线预览文本、图片、音频、视频等，已经足以满足大多数应用场景。

### 安装

废话不多说，以下是安装流程。

#### Web环境准备

服务器上预先安装好服务器运维管理面板（如果服务器用于建站的话这个应该是必备的）

>推荐安装[宝塔面板](https://www.bt.cn/)。安装过程并不复杂，在官网都有方便的一键安装脚本。

h5ai要求PHP 5.5+ 。在宝塔内选择安装合适的PHP（演示为5.6），安装完成后在PHP管理内安装`ImageMagick`、`fileinfo`、`exif`扩展。如果出现安装不上的情况，也可以尝试登录SSH通过命令行安装。[宝塔](https://www.bt.cn/bbs/thread-517-1-1.html)对此有详细的说明。

```
wget -O ext.sh http://125.88.182.172:5880/ext/ext.sh && sh ext.sh
```
在脚本内按照提示选择需要的拓展。注意选择对应的PHP版本。

安装完成后新建一个网站，作为h5ai的展示页面。

![2](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200215/2.png)

![拓展安装脚本展示](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200215/%E6%8B%93%E5%B1%95%E5%AE%89%E8%A3%85%E8%84%9A%E6%9C%AC%E5%B1%95%E7%A4%BA.png)

![拓展安装完成](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200215/%E5%AE%89%E8%A3%85%E5%AE%8C%E6%88%90%E6%88%AA%E5%9B%BE.png)

#### 上传 H5ai

进入 [H5ai](https://larsjung.de/h5ai/) 官网，点击网页右侧的 **Download** 按钮。然后将_h5ai文件夹上传至网站根目录。

打开`http://你的域名/_h5ai/public/index.php`，检查H5ai安装情况。

以下提供部分错误展示

- 提示`[ERR] h5ai sources must be preprocessed to work correctly`
  你错误地下载了 Github 的版本，该版本是未经 npm 编译的，必须前往官网下载
- 提示`Permission denied`
  直接给`_h5ai`文件夹**777**权限

![3](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200215/3.png)

假如一切顺利，你将来到 H5ai 提供的 Web 环境检测页面。这里可以设置访问密码，也可以按需求安装依赖。

![4](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200215/4.png)

返回宝塔面板。在`站点修改-默认文档`中添加h5ai的启动页面`/_h5ai/public/index.php`，添加好之后就可以通过浏览器访问了。此处默认展示的是存放在站点根目录内的文件。

![5](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200215/5.png)

基本安装完毕！以后分享文件就可以用自己的高速网盘了。

![6](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200215/6.png)

### 其他配置

H5ai 的配置文件在`h5ai/private/conf/options.json`。这里可以对密码，目录，主题，插件等进行详细设置，但一般我们都用不着。比较常用的设置项有这些：

**增添隐藏目录**：在'hidden'后按格式添加即可
```
    "view": {
        ...
        "hidden": ["^\\.", "^_h5ai"],
        ...
    },
```

**修改登陆密码**：默认为空，但也可以在`passhash`项填入
```
"passhash": "...",
```

在下一篇文章中，还会有对 H5ai 配合 Aria2 进行高速下载的介绍。
---
title: Github Desktop:使你的项目进展更为顺利
date: 2018-12-01 20:22:02
categories: "教程"
tags: [Software]
cover: "https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181201/0.png"
toc: true
excerpt: "Gibhub Desktop 是Github的官方 git 软件。它可以帮助你摆脱 Git 指令的束缚，以可视化界面轻松完成对 Git 仓库的更新。"
---
Extend your Github workflow beyond your browser with GitHub Desktop, completely redesigned with Electron. Get a unified cross-platform experience that’s completely open source and ready to customize.

**Gibhub Desktop** 是Github的官方 git 软件。它可以帮助你摆脱 Git 指令的束缚，以可视化界面轻松完成对 Git 仓库的更新。

相比其他工具， **Github Desktop** 具有以下特点。

- 广泛的编辑器和shell集成。
- 与你的协作者共同提交更改。
- 与 Github 的极高兼容性。
- 完全开源，可随时定制的统一跨平台体验。

![0.png](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181201/0.png)

官网提供 Windows 及 Mac 双平台版本下载。

https://desktop.github.com/

在本篇文章中，我将会对 Github Desktop 的一些基本用法进行介绍。

## 界面
>使用前，请先提前安装Git。软件不自带简体中文。

### 菜单栏
- File：管理仓库相关配置
- Edit：编辑操作
- View：管理各工具视窗
- Repository：进行 `Pull` ， `Push` 等基本操作
- Branch：分支管理
- Help：帮助

在日常使用中很少用到以上操作。

### 功能区
从左到右三部分依次为 切换仓库，切换分支，提交更新。

![1.png](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181201/1.png)

## 使用

### 添加仓库

#### 云端
在网页端 Github 上进入你的仓库。（如果没有仓库需要自行创建）点击 **Clone or download** 。

点击 Open in Desktop ，网页会自动唤起客户端，确认即可。

#### 本地
点击主界面的 **File -> Add local repository** ，选择你的个人项目文件夹，确定即可。

如果云端仓库添加不成功，也可以选择事先 Clone 到本地，之后手动添加。效果是一样的。

### 提交更改

成功添加仓库后。如果你没有进行任何操作，界面不会进行任何改变。

但如果你对仓库文件夹做出了更改。在界面左侧会显示出 新建/删除 的文件。针对文本文件还会在右侧通过语法高亮具体标出改动。

在完成改动后，在 Summary 处填写简略的改动描述。这一描述将会永久保存在你的改动记录中。随后点击 **Commit to [分支名]** 。

在确认更改后，更改将会进入传输队列，但此时还并没有推送到我们的 Github 远程仓库。我们需要先在 Github Desktop 添加Github账户。

![2.png](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181201/2.png)

添加完毕后，点击 Push origin 。登陆Github查看仓库，可以发现变化已经被提交到相应仓库分支中了。该步骤取代了Git中的一系列繁琐指令。


### 更新本地
在远程仓库作出改动后，本地可以通过两种途径更新。

1. 点击 **Pull origin**。
    通常情况下进行该操作即可。

![3.png](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181201/3.png)

2. 点击 **Repository->Push** 。
    此为手动拉取途径。

![4.png](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181201/4.png)
## 写在后面
此文章为原创作品，禁止转载。如需转载请先经过许可，并在转载中注明原作者及出处。

请 `收藏` 本博客，本博客将持续更新。

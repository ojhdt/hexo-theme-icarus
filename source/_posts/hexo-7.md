---
title: 离Hexo博客搭建只差一个教程（七）：使用个人 VPS 搭建
date: 2019-04-30 20:08:24
categories: "教程"
tags: [Blog,Hexo,VPS,BT]
cover: "https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181002/0.png"
toc: true
excerpt: "相比使用各大互联网公司提供的 Page 服务，使用自己的服务器始终是更为稳妥的选择。教你如何一次性把 Hexo 博客部署到自己的服务器。"
---
>上一篇：[离Hexo博客搭建只差一个教程（六）：第三方服务——对象储存 COS](https://blog.ojhdt.com/20190404/hexo-6)

在上一篇文章中，我们介绍了 腾讯云对象存储 COS 的使用。

在本篇中，我们将会介绍如何将已经在本地部署好的 Hexo 推送到自己的 VPS 上。推送方式与推送至 Github ， Coding 等类似，在本地生成本地文件后，使用 `hexo d` 推送到 VPS 上的Git仓库，配合宝塔云面板展示出页面。推送过程简单快捷，不需要进行任何额外操作。

要继续进行，请先完成以下准备工作。

- 在本地成功安装并配置完毕的 [Hexo](https://blog.ojhdt.com/20181002/hexo-1/) 。

- 一台正常连接的 VPS 。
>推荐安装 SSH连接工具 [**Putty**](https://www.putty.org/) 及 FTP文件管理 [**FileZilla**](https://filezilla-project.org/) 。本教程将以以上工具为示范工具。

### VPS 端配置
1. 检查 Git 安装情况。
```
git --version
```
若未安装，从 yum 安装
```
yum –y install git
```

2. 创建一个新用户来使用 Git 。此处以账户名 `git` 为例。
```
useradd git
```
为账户设置密码。使用指令后按照提示操作。
```
passwd git
```

#### 搭建 Git 仓库
进入你希望建立仓库的目录。此处以`/home`为例。
```
cd /home
```
建立一个名称为`hexo.git`的仓库。该仓库可随意命名，但一般以`.git`结尾。
```
git init --bare hexo.git  
```
至此，Git 裸仓库搭建结束。以 FTP 登陆 VPS 可进入仓库路径：/home/hexo.git
![1](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190430/1.png)

#### 配置 Git 仓库
##### 资源钩子
`post-receive` 是 Git 提供的一个Hook：它会在接收 post(push) 请求之后执行。

进入到搭建好的 Git 仓库，新建一个`post-receive`脚本。
```
cd /home/hexo.git/hooks
vi post-receive
```
写入以下代码，自行替换变量。
```
#!/bin/sh
git --work-tree=[网站根目录] --git-dir=[git 仓库路径] checkout -f
```
>`网站根目录`指网页在服务器上存放的具体路径，该路径由下文所介绍的宝塔面板生成。`git 仓库路径`指你创建的git仓库所在路径。本例中为`/home/hexo.git`

编辑完毕后，先`Esc`，然后输入 `:wq` 保存退出。以上操作也可以在 FTP 中完成。

为钩子程序添加可执行权限：
```
chmod +x /home/hexo.git/hooks/post-receive
```
修改 Git 仓库的权限。该步骤**非常重要**，必须保证所有者为你所设立的git账户！
```
cd /home
chown -R git:git hexo.git
```
修改结果如下图。
![2](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190430/2.png)

### 配置 SSH 证书
#### SSH 证书生成
以下操作在**本地**进行。切勿在服务器端进行操作。Windows系统需要安装 [git shell](https://git-scm.com/downloads)。如果没有安装openssl，还需要`yum install openssl`来安装。


先设置 user.name 和 user.email。请手动将指令中的 “用户名@username” 和 “邮箱地址@mail” 替换成自己的。打开一个 git 命令窗口，依次执行：
```
git config –-global user.name “用户名@username”
git config –-global user.email “邮箱地址@mail”
```
假设用户名和邮箱地址分别为 `abc` 和 `abc@mail.com` ，可以这样输入指令：
```
git config –-global user.name “abc”
git config –-global user.email “abc@mail.com”
```
生成新的SSH Key。
```
ssh-keygen -t rsa -C "邮箱地址@mail"
```
系统会提示你设定密码。这个密码需要在你每次提交项目时输入。为了以后提交方便建议不输入，直接回车。

出现下图就成功生成SSH key了。
![24](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181002/24.png)

#### 上传 SSH 证书
1. 进入 C:\Users\用户名.ssh 目录，以文本格式打开 id_rsa.pub 文件，复制内容，以获得公钥。
2. FTP 连接服务器，进入路径`/home/[Git用户名]/.ssh`，以文本形式编辑其中的文件`authorized_keys`。
     >若不存在该目录或不存在该文件，请自行创建。

3. 将刚才复制的公钥添加到最后，一个公钥占一行，保存回传服务器。
4. 返回本地终端测试连接。指令中`git`指你的git账户名，`yourserver`指服务器 ip ，执行命令前自行替换。
```
ssh -T git@yourserver
```
该操作**不需要**输入连接密码。测试结果各服务器显示一般不同。若测试成功，一般需要手动 `ctrL+c` ,让 git终端 回复到正常输入命令的状态。下图为其中一个成功的例子。

![3](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190430/3.png)

如果连接失败，请检查你的客户端与服务器配置。

### 准备推送
#### 编辑 Hexo 推送配置
编辑 `_config.xml`  ，修改 deploy 项配置。`yourserver`为 服务器 ip。
```
- type: git
  repo: git@yourserver:/home/hexo.git
  branch: master
```
如果需要同时推送到 Github，Coding 等平台，可以这样填写：
```
deploy:
  - type: git 
    repo: 
      coding: git@git.coding.net:[coding用户名]/[coding用户名].git,master 
      github: git@github.com:[Github用户名]/[Github用户名].github.io.git,master
      vps: git@[服务器ip]:/home/hexo.git,master
```

#### 安装宝塔面板

[宝塔面板](https://www.bt.cn/)是一款使用方便、功能强大且终身免费的服务器管理软件。可一键配置LAMP/LNMP、网站、数据库、FTP、SSL,通过Web端轻松管理服务器。

CentOS一键安装脚本
```
yum install -y wget && wget -O install.sh http://download.bt.cn/install/install_6.0.sh && sh install.sh
```
安装完成后，进入面板安装PHP 5.6+、Nginx。

1. 添加网站

![4](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190430/4.png)
域名填写你的自购域名。复制根目录路径，填入之前的`post-receive`钩子中。点击创建。

2. 进入 FTP ，进入网站根目录，删除网站根目录下自动生成的文件。

3. 修改网站根目录的权限。**重要！** 否则钩子程序执行的时候,无法修改网站根目录的内容。
```
chown -R git:git [网站根目录]
```
修改结果如图
![5](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190430/5.png)

### 构建网页
配置至此就基本完成了。返回博客本地，尝试进行推送：
```
hexo d -g
```
若配置无误，`/public` 下的博客文件将会被推送至网站根目录。至此，你的网页已经可以通过域名访问了！在之后每次更新博客后，只需要使用 `hexo d -g` 就可快捷更新至 VPS 。实现与 Github 一样的快速操作！

如果网站根目录没有博客文件，尝试以下方法排除错误：

1. 直接在 Git 仓库 运行脚本命令：
```
cd /home/hexo.git
git --work-tree=[网站根目录] --git-dir=[git 仓库路径] checkout -f
```
若执行命令后文件成功推送，可能是权限配置错误，尝试重新为 `Git 仓库` 和 `网站根目录` 更改权限。若仍无法推送，请检查脚本填写是否正确。

2. 提交新更改。Git 在本地仓库不进行更新时默认不进行推送。尝试对你的本地博客作出更改（如新增，删除文章）后重新推送。

#### （可选）为博客安装 SSL 证书

证书的获得来源有很多种。推荐前往 [腾讯云](https://cloud.tencent.com/product/ssl) 申请免费的 TrustAsia 证书。有效期 1 年，但可以无限续期。

![6](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190430/6.png)

1. 申请并下载证书
前往 [腾讯云](https://cloud.tencent.com/product/ssl) 申请免费的 TrustAsia 证书。申请通过一般需要数小时到数天不等。下载证书。

2. 解压证书压缩包。证书包一般由 Apache，IIS，Nginx，Tomcat 等多种证书组成。由于我们使用宝塔面板安装，直接进入 `Nginx` ，内含一个`.crt`文件和一个`.key`文件。

![7](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190430/7.png)

3. 登入宝塔面板，管理创建的网站，点击 `SSL` 选项。

4. 以文本形式复制`.crt`文件中的全部内容，填入右框`证书(PEM格式)`中。复制`.key`中全部内容，填入左框`密钥(KEY)`中。启用`强制HTTPS`，点击保存。

![8](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190430/8.png)

设置至此结束，你的网站可以使用 Https 访问了。

### 写在后面
>感谢您的阅读！若您在阅读时发现教程存在疏漏或无法理解的地方，可以通过 **评论区留言** 进行交流讨论。
>
>上一篇：[离Hexo博客搭建只差一个教程（六）：第三方服务——对象储存 COS](https://blog.ojhdt.com/20190404/hexo-6)
>
>下一篇：[离Hexo博客搭建只差一个教程（附录）：Markdown 语法](https://blog.ojhdt.com/20181006/hexo-markdown)

此文章为原创作品，禁止转载。如需转载请先经过许可，并在转载中注明原作者及出处。

请 `收藏` 本博客，本博客将持续更新。
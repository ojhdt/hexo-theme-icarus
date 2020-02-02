---
title: 将 Hexo 同时推送至 GitHub 与 Coding
date: 2018-10-20 17:02:14
categories: "小记"
tags: [Blog,Hexo,Github,Coding]
toc: true
excerpt: "Github 和 Coding 分别是国内外两个优秀的云端开发平台。本文主要介绍 Hexo 同时推送至两个平台的操作。"
---
**Coding** 是一个面向开发者的云端开发平台。与 GitHub Pages 类似，Coding也提供了免费的 Pages 服务。用户可以在自由发布自己的静态网页，并通过可自定义的 `xxx.coding.me` 域名访问。与GitHub相比，Coding的优越性在于更快的国内访问速度与完善的云端管理。Coding免费用户可获得 500MB 的储存空间，可以基本满足博客需要。

>本站托管在Coding上的Page：https://ojhdt.coding.me

### 配置步骤

#### 准备工作
- 可正常运行的 Hexo 。搭建教程可查阅本站其他文章。
- 已安装 hexo-deploy-git 插件。

#### 配置Coding
1. 前往 [Coding.net](https://coding.net/)，注册账号。
>Coding目前可通过 绑定腾讯云账号 升级银牌会员，获得更多（500 MB）储存空间。

2. 新建一个项目。项目名称自由填写，描述可选择不填。勾选 `公开源代码` 。勾选`启用 README.md 文件初始化项目`。点击 **新建项目** 。

![1](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181020/1.png)

#### 配置 SSH
SSH公钥可以免去每次提交输入密码的麻烦。

如果在配置 Github 时已生成SSH公钥，可直接使用之前生成的`_rsa.pub`，并跳过以下教程。

1. 先设置 user.name 和 user.email。请手动将指令中的 “用户名@username” 和 “邮箱地址@mail” 替换成自己的。返回刚才的命令窗口，依次执行：
```
git config –-global user.name “用户名@username”
git config –-global user.email “邮箱地址@mail”
```
假设用户名和邮箱地址分别为 abc 和 abc@mail.com ，可以这样输入指令：
```
git config –-global user.name “abc”
git config –-global user.email “abc@mail.com”
```
2. 检查你电脑上现有的 SSH Key：
```
cd ~/.ssh
```
提示 No such file or directory 后继续操作。

3. 生成新的SSH Key。
```
ssh-keygen -t rsa -C "邮箱地址@mail"
```
系统会提示你设定密码。这个密码需要在你每次提交项目时输入。为了以后提交方便建议不输入，直接回车。

出现下图就成功生成SSH key了。

![2](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181002/24.png)

进入 C:\Users\用户名\.ssh 目录，以文本格式打开 id_rsa.pub 文件，复制所有内容。

返回Coding控制台，点击 **设置->部署公钥** ，点击 **新建部署公钥** 。

公钥名称自行填写，内容填写 `id_rsa.pub` 中的内容，点击 **新建** 。

添加成功后在Git命令窗口测试：
```
ssh -T git@git.coding.net
```
若出现
```
Coding 提示: Hello xxx, You've connected to Coding.net via SSH. This is a deploy key.
xxx，你好，你已经通过 SSH 协议认证 Coding.net 服务，这是一个部署公钥
```
则SSH添加成功。

#### 修改站点配置文件

打开`_config.yml`，更改deploy插件配置，格式为：
```
deploy:
  type: git
  repo:
    github: <repository url>,[branch]
    coding: <repository url>,[branch]
```
配置示例：
```
deploy:
  type: git
  repo:
    github: git@github.com:xxx/xxx.github.io.git,master
    coding: git@git.coding.net:xxx/xxx.git,master
```
使用`hexo g`，`hexo d`更新博客。在Github和Coding都将收到更新。


### 后续步骤
#### 启动 Pages 服务
点击侧边栏 **Pages 服务**，分支选择 `master` ，开启。

尝试使用`xxx.coding.me`访问博客。

#### 启用SSL安全证书/自定义域名
Coding提供免费的SSl证书服务，仅需在设置中开启。
>若证书申请失败，请检查是否设置了域名的双线绑定，将解析到境外的解析暂停后再重新申请。

进入 **Pages 服务->齿轮小图标** ，

1. 在 **自定义域名** 中绑定自己的域名。
2. 开启 **强制 HTTPS 访问** 。

#### 双线绑定域名（可选）
由于众所周知的原因，在国内访问Github延迟较大，相比下Coding具有优势，在国外情况则相反。如果已经购入域名，通过使用DNSPod解析服务分地域解析，可以加快网页载入速度。

以下操作需要你在完成对 Github 和 Coding 的推送操作后进行。

1. 将你的 DNS 服务器设定为 DNSpod 提供的服务器。该操作等待需要2-24小时的生效时间。

2. 进入DNSpod管理面板，根据下表添加解析记录。

|主机记录|记录类型|线路类型|记录值|
|:-:|:-:|:-:|:-:|
|@|CNAME|境外|xxx.github.io|
|@|CNAME|默认|xxx.coding.me|

>可根据需要添加 **www** 解析。

3. 等待生效。



### 修订记录

- 2018-10-20 文章发表
- 2019-03-09 增添域名解析说明
### 写在后面
此文章为原创作品，禁止转载。如需转载请先经过许可，并在转载中注明原作者及出处。

请 `收藏` 本博客，本博客将持续更新。

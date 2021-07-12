---
title: Oneindex + now.sh 部署个人网盘
date: 2019-01-28 16:34:18
categories: "教程"
tags: [Netdisk,Microsoft,Onedrive]
cover: "https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190128/9.png"
toc: true
excerpt: "Oneindex 是针对微软 Onedrive 开发的一个程序。它可以列出 Onedrive 的文件目录，并提供文件直链下载，使之成为一个高速，美观的个人分享网盘。"
---
## 简介
Oneindex 是针对微软 Onedrive 开发的一个程序。它可以列出 Onedrive 的文件目录，并提供文件直链下载，使之成为一个高速，美观的个人分享网盘。

### 特点
- 不占用服务器空间，不走服务器流量。
- 直接列出 OneDrive 目录，文件直链下载。
- 文档，媒体，代码文件的在线浏览。
- 支持文件加密。
- 美观的界面，多主题选择。

官方展示 [Demo](https://xn.tn)

Github：https://github.com/donwa/oneindex

---
[now.sh](https://zeit.co/now) 是美国一家提供云部署服务的公司 ZEIT 旗下提供的**免费**云端应用程序实时部署平台。它彻底打破了云端条件的束缚，要检查程序运行情况，使用者只需简单地推送代码。

![1.png](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190128/1.png)

### 特点
- 无需服务器，无需额外工作。
- 迅速，在几秒内部署。

Github：https://github.com/zeit/now-cli
## 安装
### 前置操作
1. 安装 [nodejs](https://nodejs.org/en/download/) 。
2. [注册](https://zeit.co/) now 账户。具体过程不再赘述，验证邮箱推荐使用 Gmail。

### 安装 now-cli

![2.png](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190128/2.png)

新建一个文件夹，右键该文件夹，点击 `Git Bash Here` ，打开命令窗口，键入
```
npm install -g now
```
等待安装完毕，登入账户：
```
now login
```
相继输入用户名和密码。

### 部署 Oneindex
从 Github 拉取最新版本的 Oneindex 代码
```
git clone https://github.com/donwa/oneindex.git
```
在拉取的程序文件根目录新建文件 `now.json` ，输入以下代码
```
{
  "type": "docker",
  "features": {
    "cloud": "v1"
  }
}
```

此处提供现成 [now.json](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190128/now.json) 文件下载。放置于根目录即可。

使用 deploy 指令将文件上传至now.sh
```
now deploy
```
>由于 now.sh 近期更新 v2 ，旧的配置显示不再适配。如遇到这种情况请尝试使用 **`now --public`** 指令解决。

系统将会弹出大量提示信息，其中包含一段以 `.now.sh` 为后缀的分配域名 https://xxxxxxxx.now.sh 。你所部署的程序将通过该分配地址访问。

部署需要一段时间。部署完毕后弹出提示信息：
```
Successl Deployment ready
```
至此部署成功。

部署完成后，容器默认会隔一段时间重启，为了不让容器重启，执行下面的命令。如果不执行，会发现隔一会又要重新配置 onedrive 了。记得把下面的地址改成自己的 now.sh 的地址。
```
now scale xxxxxxxx.now.sh 1
```

为了方便访问，还可以为前缀设置别名。此处以 `oneindex` 为例。
```
now alias xxxxxxxx.now.sh oneindex
```
## 配置
1. 访问自己的 now.sh ，进入安装向导。

    环境检测在一般情况下都可通过，点击下一步。

![4.png](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190128/4.png)

2. 点击[按钮](https://apps.dev.microsoft.com/?deepLink=%2Fquickstart%2FgraphIO%3FpublicClientSupport%3Dfalse%26appName%3Doneindex%26redirectUrl%3Dhttps%3A%2F%2Fju.tn%2F%26allowImplicitFlow%3Dfalse%26ru%3Dhttps%253A%252F%252Fdeveloper.microsoft.com%252Fen-us%252Fgraph%252Fquick-start%253FappID%253D_appId_%2526appName%253D_appName_%2526redirectUrl%253Dhttps%253A%252F%252Fju.tn%252F%2526platform%253Doption-php)，登陆微软账户,获取 `应用机密` 。返回上一层，获取 `应用id` ，分别填入。

![5.png](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190128/5.png)

3. 绑定自己的微软账号。

![6.png](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190128/6.png)

    至此，Oneindex 基本配置完成。若说明不清楚，可借助一张官方的Gif动图帮助理解。

![setup](/img/install.gif)

4. 进入后台管理界面 https://oneindex.now.sh/admin/ ，进行必要的设置。默认密码为 `oneindex` 。此处可进行主题更改，缓存更新等操作。
>在每次文件上传后，都需要进行缓存更新操作。

## 特殊文件实现功能
`README.md`、`HEAD.md`、`.password` 特殊文件使用可以参考https://github.com/donwa/oneindex/tree/files

在文件夹底部添加说明:  

在 OneDrive 的文件夹中添加 `README.md` 文件，使用 Markdown 语法。

在文件夹头部添加说明:  

在 OneDrive 的文件夹中添加 `HEAD.md` 文件，使用 Markdown 语法。

加密文件夹:  

在 OneDrive 的文件夹中添加 `.password` 文件，填入密码，密码不能为空。  

直接输出网页:

在 OneDrive 的文件夹中添加 `index.html` 文件，程序会直接输出网页而不列目录。配合 文件展示设置-直接输出 效果更佳。

## 附录

### 常用的 **now-cli** 命令

[官方文档](https://zeit.co/docs/v1/clients/now-cli)

|**指令**|**描述**|
|-|-|
|now deploy [path]|	使用此命令时，当前目录中的文件将被上传到now.sh，并将创建一个新的部署。之后，您将立即收到其网址，以便与全球其他人分享。|
|now ls\list [app]|	显示所有部署的列表。如果被定义，它将仅列出该命名空间下的部署。|
|now rm\remove [id]|	从now.sh平台中删除部署。该参数可以是您之前的部署的URL或主机名。|
|now ln\alias [id] [url]|	在现有部署上配置别名或自定义域名。|
|now domains [name]|	允许您直接从命令行管理域名。|
|now certs [cmd]|	默认情况下，now.sh将自动为您的部署配置证书。使用此子命令，您可以看到他们何时到期。|
|now secrets [name]|	如果您需要将敏感信息存储在只能由其中运行的代码访问的部署上。这可以通过使用它来实现，它允许您以安全的方式存储应用程序所需的功能（如API令牌或密码）|
|now dns [name]|	列出使用zeit.world为域创建的所有DNS记录。该列表不包括由名称服务器自动生成的记录（如默认记录，为记录自动创建的记录等）。SOA``A / AAAA``ALIAS|
|now open|	运行此子命令将在默认浏览器的当前目录中打开项目的最新部署（别名此时无效）|
|now billing\cc|	轻松添加或删除帐户中的信用卡，并调整结算方式。|
|now upgrade\downgrade [plan]|	从命令行界面切换您的计划。即使命令运行后，我们也不要求您使用Web界面。整个过程直接发生在你的终端上。|
|now help|	显示终端中的子命令和选项列表|
|now login|	登录你的 ZEIT 账户|

### *自定义域名
此步操作需要自购域名。

具体介绍请参阅[官方文档](https://zeit.co/docs/v2/domains-and-aliases/adding-a-domain/)。

使用以下指令，记得修改为自己的对应域名。此处以本站域名为例。
```
now alias xxxxxxxx.now.sh yourdomain.com
```
系统提示需要验证。

![7.png](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190128/7.png)

为你的域名添加一条 `CNAME` 解析，名称填写 `name` 中的对应名称，指向 `alias.zeit.co` 。

![8.png](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190128/8.png)

添加解析完毕后，等待数分钟，再次输入指令。

![10.png](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190128/10.png)

## 参考文章
[1]欧阳松的博客.[now.sh 免费部署 oneindex](https://www.ouyangsong.com/posts/43735/)

[2]柒索.[如何使用 Now.sh来免费部署你的项目？](http://object.ws/2017/09/10/nowsh-note/)

## 写在后面
此文章为原创作品，禁止转载。如需转载请先经过许可，并在转载中注明原作者及出处。

请 `收藏` 本博客，本博客将持续更新。
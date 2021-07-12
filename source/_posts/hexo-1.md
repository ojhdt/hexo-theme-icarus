---
title: 离Hexo博客搭建只差一个教程（一）：基础搭建
date: 2018-10-02 07:12:44
categories: "教程"
tags: [Blog,Hexo]
cover: "https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181002/0.png"
toc: true
excerpt: "Hexo 是一个基于 Node.js 的快速、简洁且高效的博客框架。 其本身拥有强大的插件系统和主题系统。它还可以上传到 GitHub Pages，Heroku 或其他网站，是小白建站的极佳选择。
"
---
## 前言
作为一个技术小白，在Hexo博客搭建之路上一路走来，磕磕碰碰，几番周折。靠着网上的教程，经过多次尝试，终于使博客初见雏形。在这一过程中，我深切地感受到了“没有教程”的痛苦。并非前人所写的教程不够优秀，一部分因年代久远而不再适用新版变化，一部分由程序员撰写的教程过于专业，想要看懂实在不容易。更重要的是，一些稍微描述得不清楚的细节，就需要自己就要绕弯路去找答案，耗费大量的时间和精力。

为此，我计划着要撰写一篇教程，之所以将标题取为《离Hexo博客搭建只差一个教程》，是因为我希望写出一篇尽可能系统详尽的教程，将我搭建博客的过程与经验分享出来，来给后者一个明确的方向和指引，让他们少走弯路。

我计划将教程分为以下数个部分：

- （一）基础搭建——叙述搭建 Hexo 博客的基本操作。
- （二）主题——详细介绍主题功能，并附带介绍一部分优秀主题。
- （三）第三方服务——涉及评论，统计，广告等第三方服务支持。
- （附录）Markdown语法——常用Markdown语法介绍。

其中部分内容可能涉及到他人的教程，我将会在“参考文章”中一一列出。
### 为什么要搭建博客
也许你会问起：国内不是已经存在简书，CSDN，微博等博客平台了吗，为什么还要自己花大心思去搭建一个呢？

我的回答很简单：**自己的才是最好的**。

### 搭建博客需要什么
- 可以没有基础，但一定要有学习和钻研精神。
- 要有耐心，敢折腾。
- 要有坚持更文的觉悟。

### 技术支持
我们先对一些必要的基础知识进行科普。

#### Hexo
Hexo 是一个基于 Node.js 的快速、简洁且高效的博客框架。 Hexo 使用Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。其本身拥有强大的插件系统和主题系统。它还可以上传到 GitHub Pages，Heroku 或其他网站，是小白建站的极佳选择。

官网：https://hexo.io

文档：https://hexo.io/zh-cn/docs/
 
GitHub：https://github.com/hexojs/hexo

#### GitHub Pages

![1](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181002/1.png)

GitHub Pages 是 GitHub 提供给开发者用于介绍项目的网站服务。它由你的GitHub存储库托管。只需简单的编辑，推送，即可使更改生效。同时，它可以免费提供给用户 300MB 的储存空间和一个 xxx.github.io 域名。

官网：https://pages.github.com/

---
做好准备了吗？让我们开始吧。

善用 **文章索引** 将会对阅读产生帮助。

## 正文

### 准备搭建环境
依次安装以下软件：

1. [**Node.js**](https://nodejs.org)
  
    [【64-bit】](https://nodejs.org/dist/v8.12.0/node-v8.12.0-x64.msi) [【32-bit】](https://nodejs.org/dist/v8.12.0/node-v8.12.0-x86.msi)

2. [**Git**](https://git-scm.com/)

    [【64-bit】](https://github.com/git-for-windows/git/releases/download/v2.19.0.windows.1/Git-2.19.0-64-bit.exe) [【32-bit】](https://github.com/git-for-windows/git/releases/download/v2.19.0.windows.1/Git-2.19.0-32-bit.exe)

3. [**Notepad++**](https://notepad-plus-plus.org/)
>非博客运行必需，但对文本编辑十分有利，**强烈建议**安装。

安装过程不多加赘述，全部点击“Next”即可。

### 博客主体搭建
创建一个新文件夹，此处以“Blog”为例。

![2](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181002/2.png)

右键该文件夹，点击 **Git Bash Here**，进入图示窗口。

![3](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181002/3.png)

![4](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181002/4.png)

为加快下载速度，使用指令设置全局配置到淘宝源。
``` 
npm config set registry https://registry.npm.taobao.org
```
安装hexo插件。
```
pwd
npm install hexo-cli -g
```
弹出以下提示即为安装完成，

```
+hexo-cli@x.x.x
updated 1 packages in xs
```

然后依次执行以下代码初始化Hexo。
```
hexo init Hexo 
cd /Hexo 
npm instal 
hexo g 
hexo s
```
至此，博客主体已搭建完成，可通过网址 http://localhost:4000/ 访问。在目录下可发现一个名为“Hexo”的文件夹，此处为你的博客配置文件夹。

在继续操作前，先按下 `Ctrl+C` 停止Hexo服务。

### GitHub Pages 准备
前往 [GitHub](https://github.com/) ，点击右上角 **Sign Up** 注册新账号。

填入信息。尤其注意用户名一栏，此处决定了你的域名前缀。邮箱地址必须准确，用于验证。

按照提示继续操作。注册完成后点击右上角的 **New repository**

`Reposotory name` 一项中填入你的用户名（与`Owner`一项相同），然后点击 **Create reposutory** 。

![5](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181002/5.png)

至此GitHub仓库准备完毕。

### 上传Hexo静态文档至GitHub

#### 配置SSH keys
通过配置SSH keys可以方便地把博客项目和GitHub联系起来。

先设置 user.name 和 user.email。请手动将指令中的 “用户名@username” 和 “邮箱地址@mail” 替换成自己的。返回刚才的命令窗口，依次执行：
```
git config –-global user.name “用户名@username”
git config –-global user.email “邮箱地址@mail”
```
假设用户名和邮箱地址分别为 abc 和 abc@mail.com ，可以这样输入指令：
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

进入 C:\Users\用户名\.ssh 目录，以文本格式打开 id_rsa.pub 文件，复制所有内容。

进入GitHub，点击右上角 **头像->Settings** ，在左侧找到 **SSH and GPG keys** 。

![6](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181002/6.png)

![7](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181002/7.png)

点击 **New SSH key** ，Title随便写，Key填入复制的内容。点击 **add key**。

![8](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181002/8.png)

返回命令窗口，测试。
```
ssh -T git@github.com
```
若弹出提示
```
Are you sure you want to continue connecting (yes/no)?
```
时输入 yes 确认。

出现以下说明即为添加成功。
```
Hi xxx! You've successfully authenticated, but GitHub does not provide shell access.
```



#### 配置及上传Hexo
关闭目前命令窗口，手动进入Git安装目录（C:\Program Files\Git），右键“Hexo"文件夹，点击 **Git Bash Here**，开启新窗口。

安装 部署到Github 插件。
```
npm install –save hexo-deployer-git
```
进入”Hexo“博客配置文件夹，以文本形式打开站点配置文件 **_config.yml**。在最后添加：


```
deploy: 
type: git 
repo: git@github.com:**Github用户名**/**GitHub用户名**.github.io.git
branch: master
```


>改成自己的用户名和用户名加域名，保存退出。如图所示。

![9](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181002/9.png)

返回命令窗口，键入指令

```
hexo d
```
出现以下提示，进入推送过程。

![26](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181002/26.png)

首次推送耗费时间较长，视网速而定，一般不会超过十分钟。等待命令执行完毕，访问 **Github用户名.github.io** 即可访问博客。

此时访问GitHub仓库可发现已上传内容。如图所示。

![25](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181002/25.png)

### 站点配置文件详解
**”站点配置文件“** 一般指 **_config.yml** 。站点配置文件是博客的总配置，一切基础参数，插件参数，主题配置都在这里进行。

>注意：在配置文件中，冒号后一般带空格，文字参数一般带 **'** **'** 引用。建议配置前做好备份。
>
>部分主题会要求在站点配置文件中新增配置项以启动某些组件，需自行查阅相关主题文档。
>
>部分注释来自互联网。

```
# Hexo Configuration
## Docs: https://hexo.io/docs/configuration.html
## Source: https://github.com/hexojs/hexo/

# Site（标题等必填）
#网站标题
title: 
#网站副标题
subtitle: 
#网站描述
description: 
#作者昵称
author: 
#网站语言，默认英语，设置简体中文
language: zh-CN
#时区，默认电脑时区
timezone: Asia/Shanghai


# URL
#如果网站是放在子目录中，将url设置成'http://yoursite.com/child'，将root设置成'/child/'
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
#网址（输入你的GitHub Pages地址）
url: http://用户名.github.io
#网站根目录。如果网站是放在子目录中，将root设置成'子目录名'
root: /
#文章链接地址格式 。即文章存放的目录。（**注意**：为方便网络爬虫抓取博客信息，一般都会把网址设置成“三段”，而Hexo默认为“域名:年:月:日:标题”五段。强烈建议修改为**:year:month:day/:title/**以便于抓取。）
permalink: :year:month:day/:title/
permalink_defaults:


# Directory
#资源文件夹，放在里面的文件会上传到github中
source_dir: source
#公共文件夹，存放生成的静态文件
public_dir: public
#标签文件夹，默认是tags。实际存放在source/tags中。
tag_dir: tags
rss_dir: rss
#档案文件夹，默认是archives。
archive_dir: archives
#分类文件夹，默认是categories。实际存放在source/categories中。
category_dir: categories
#代码文件夹，默认是downloads/code
code_dir: downloads/code
#国际化文件夹，默认跟language相同
i18n_dir: :lang
#不需要渲染的文件夹或文件夹,格式为[文件名]
skip_render: 


# Writing
# 新建博文（帖子）的默认名称
# File name of new posts
new_post_name: :title.md 
#默认布局模板是post，而不是draft和page
default_layout: post
#是否将标题转换成标题形式（首字母大写）
titlecase: false # Transform title into titlecase
#在新标签页面中打开网页
external_link: true # Open external links in new tab
filename_case: 0
#是否渲染草稿
render_drafts: false
#启动 Asset 文件夹
post_asset_folder: false
#把链接改为与根目录的相对位址
relative_link: false
#显示未来的文章
future: true
#代码块的设置
highlight:
  enable: true      #  使用代码高亮
  line_number: true # 显示行号
  auto_detect: true  # 自动检测语言
  tab_replace:


# Home page setting
# path: Root path for your blogs index page. (default = '')
# per_page: Posts displayed per page. (0 = disable pagination)
# order_by: Posts order. (Order by date descending by default)
index_generator:
  path: ''
#每页文章数量
  per_page: 10
#排序依据
  order_by: -date


# Category & Tag
#默认分类
default_category: uncategorized
#分类别名
category_map:
#标签别名
tag_map:


# Date / Time format
#Hexo 使用 Moment.js 来解析和显示时间。
## You can customize the date format as defined in
## http://momentjs.com/docs/#/displaying/format/
date_format: YYYY-MM-DD
time_format: HH:mm:ss


# Pagination
## Set per_page to 0 to disable pagination
per_page: 10
pagination_dir: page


# Extensions 拓展插件配置
## Plugins: https://hexo.io/plugins/
#主题配置
## Themes: https://hexo.io/themes/
#选择主题,默认为landscape
theme: landscape

```
### 开始创作
你已经完成了博客的最基本设置，可以开始撰写文章了。

#### 创建文章
- 命令行： `hexo new <title>`

- 手动创建：在 hexo 主目录下 `source -> _posts` 新建以 `.md` 为后缀的文件。

---

打开文章文件，让我们初步了解文章的格式。

整个markdown文本被分为两部分：**Front-matter** 和 **正文**。

#### Front-matter

Front-matter 是文件最上方以 --- 分隔的区域，用于指定个别文件的变量，举例来说：
```
title: Hello World
date: 2018/10/01 00:00:00
---
```
以下是预先定义的参数，您可在模板中使用这些参数值并加以利用。

| 参数          | 描述                | 默认值       |
|:--            |:--                  |:--           |
| `layout`      | 布局                | post         |
| `title`       | 标题                | 文件名       |
| `date`        | 建立日期            | 文件建立日期 |
| `updated`     | 更新日期            | 文件更新日期 |
| `tags`        | 标签（不适用于分页）|              |
| `categories`  | 分类（不适用于分页）|              |
| `permalink`   | 覆盖文章网址        |            |

只有文章支持分类和标签，您可以在 Front-matter 中设置。在其他系统中，分类和标签听起来很接近，但是在 Hexo 中两者有着明显的差别：分类具有顺序性和层次性，也就是说 `Foo, Bar` 不等于 `Bar, Foo`；而标签没有顺序和层次。

```
categories:
- Diary
tags:
- PS3
- Games
```

#### 正文

正文部分采用 Markdown 语法。

详细说明请参见 [附录](https://blog.ojhdt.com/20181006/hexo-markdown/)。

#### 更新
在你对博客做出更新后，你需要将其上传至GitHub。

下面介绍几条常用指令。

`hexo clean`：清除缓存文件和已生成的静态文件。

`hexo g`：生成静态文件。

`hexo s`：启动服务器。默认情况下，访问网址为： http://localhost:4000/ 。

`hexo d`：部署网站。

更多指令可查阅 [Hexo文档](https://hexo.io/zh-cn/docs/commands.html)。

**一般情况下，可依次执行以下指令来部署至GitHub：**

```
hexo g
hexo s
hexo d
```

### 博客多端同步更新（可选）
利用Git分支实现。在更新博客后，将博客源文件上传至一个新分支。更换设备后，先使用git命令将最新版本同步到本地，再继续进行创作。

#### 将源文件上传至GitHub新分支
>
>请先确保自己已经使用Hexo建好了自己的个人博客，并可正常访问。

登入GitHub，在 username.github.io 仓库上新建一个xxx分支（如hexo），并切换到该分支，

![11](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181002/11.png)

在 **该仓库->Settings->Branches->Default branch** 中将默认分支设为 **xxx** ， **save** 保存。

![12](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181002/12.png)

![13](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181002/13.png)

返回仓库首页，点击 **Clone or download** 按钮，复制链接。

![14](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181002/14.png)

在本地任意位置新建一以英文命名的文件夹，此处以“Blog”为例。右键该文件夹，点击 **Git Bash Here**。

![3](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181002/3.png)

键入指令
```
git clone 复制的链接
```
等待克隆完成，如下图所示。

![15](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181002/15.png)

关闭该窗口，进入“Blog”文件夹，进入克隆的“xxx.github.io”文件目录。此处为你托管于GitHub上的静态文件。
删除 除 **.git** 文件夹外的**所有文件**，将博客目录下所有本地部署文件**全部**拷贝进username.github.io文件目录中去。

![27](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181002/27.png)

删除**themes/.git**目录（如果有）
右键“xxx.github.io”文件夹，点击 **Git Bash Here**。执行`git branch`命令，确认当前所在分支为新建分支xxx。（此处我设置的新分支为hexo，故显示为hexo）

![16](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181002/16.png)

依次执行以下指令提交分支：
```
git add .
git commit -m 'back up hexo files'
git push
```
>引号内容可更改，但必须填写。
>
>**注意**：在推送前检查根目录是否存在 `.gitignore` 文件。为确保首次文件上传完整，将该文件删除后再执行命令。

等待上传完毕。

至此，GitHub仓库中保存有两个分支：master分支和xxx分支，其各自保存着一个版本。master分支用于保存博客静态资源，提供博客页面供人访问；xxx分支用于备份博客部署文件，供自己维护更新。原则上，我们先将更新提交到xxx分支，再deploy到master分支，从而实现多端同步更新。

#### 在其他设备上更新博客
##### PC
- 安装相关依赖。
- 将新设备的生成的ssh key添加到GitHub账户上。相关教程可查阅前文。
- 在新设备上使用 `git clone xxx` 来克隆仓库的xxx分支到本地。
- 进入Git Bash，执行`npm install`命令。
>若报错，请删除node_modules目录后重试。在执行本操作前，请先关闭所有网络代理。

至此，你的新设备获得一份博客源文件的拷贝，已经可以进行同步的维护和更新了。

##### 移动设备（需要root权限）
- 安装 [高级终端Termux](https://www.coolapk.com/apk/com.termux)
- 和PC类似，先安装依赖
```
pkg install git
pkg install nodejs-lts
```
- 将新设备的生成的ssh key添加到GitHub账户上。相关教程可查阅前文。
- 使用 `git clone xxx` 来克隆仓库的xxx分支到本地。
>克隆后路径为 `/data/data/com.termux/files/home` 下 `xxx.github.io`
- 进入博客文件夹，安装插件
```
cd xxx.github.io
npm install
```
>若报错，请删除node_modules目录后重试。在执行本操作前，请先关闭所有网络代理。

至此，你的新设备获得一份博客源文件的拷贝，已经可以进行同步的维护和更新了。

#### 更新
>**注意： 每次更换设备进行博客更新时，不管上次在其他设备有没有更新，最好先运行一下 `git pull` ，以同步最新更新到本地。**

编辑、撰写文章或其他博客更新改动后，依次执行以下指令，保证xxx分支版本最新。
```
git add .
git commit -m 'back up hexo files'
git push
```

>引号内容可改。

然后执行指令将改动部署到master分支。
```
hexo d -g
```

>在此之前，有时可能需要执行 `hexo clean` 。


### 域名购买及应用（可选）

GitHub Pages很人性化的一点是支持使用自己的域名。虽然可以自定义前缀的xxx.github.io已经十分友好，但对于大多数站长，当然都希望能拥有一个自己的域名。

我推荐前往 [GoDaddy](https://www.godaddy.com/) 购买域名。GoDaddy虽然是新加坡的，但经过长期的发展，现在GoDaddy已经有中文版了，支持支付宝支付，对于国内站长来说相当友好。并且它作为全球最大的域名主机商，安全，可靠，有信用度。相比起国内购买便宜，续费昂贵的域名，GoDaddy不仅经常举办各类活动，（例如近期的7元购域名）还有大量的优惠码，价格适合。

对于域名购买细节不再赘述。

#### 添加解析及申领SSL证书

GitHub Pages附带SSL证书服务，但域名更换后，网站就不能继续使用https传输了。GoDaddy提供SSL证书服务，但价格昂贵。因此，我把目光投向了国外一家免费域名解析服务提供商——Cloudflare。

首先注册一个 [Cloudflare](https://www.cloudflare.com/) 账号，通过邮箱验证。

点击`Add Site`，添加购买的域名。

![17](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181002/17.png)

Cloudflare提供给每个用户两个域名解析服务器。进入控制台，点击 **DNS** ，查看“Cloudflare Nameservers”，复制提供的两个域名解析服务器地址。

返回GoDaddy后台，替换掉GoDaddy默认DNS。修改DNS往往存在数十分钟到数小时不等的延迟。

修改完毕后，进入Cloudflare控制台，点击 **DNS** ，添加两条DNS记录：

| Type          | Name                | Value       | TTL       | Status     |
|:--            |:--                  |:--           |:--         |:--          |
| `CNAME`       | @          | 你的GitHub分配域名        | Automatic  | DNS and Http proxy(CDN) |
| `CNAME`       | www                | 你的GitHub分配域名       | Automatic  | DNS and Http proxy(CDN) |

![18](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181002/18.png)

点击 **Crypto** ，选择 “SSL” 一项为 “Full” 。并开启 “Always use HTTPS” 和 “Automatic HTTPS Rewrites” 。

![19](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181002/19.png)

![20](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181002/20.png)

![21](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181002/21.png)

至此只需等待设定完毕。根据官方说明，这一过程将会持续数小时到数日不等。设定完毕后 “Status” 一项会转为 **Active** ，网站上也有了https。

![22](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181002/22.png)

#### GitHub Pages相关设置
在本地博客文件夹创建一个名为`CNAME`的文件（无扩展名），内容填入你所购买的域名。

使用 `hexo g` 和 `hexo d` 将改动更新至 GitHub 。

更新完毕后，GitHub 仓库会出现`CNAME`文件。 访问xxx.github.io，网站将会自动跳转至新域名。

![23](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181002/23.png)

## 修订记录
- 19-11-02 增添部分内容
- 19-01-28 删除错误
- 18-10-13 修改部分注释，完善内容，删除错误
- 18-10-02 文章发表

## 参考文章

[1]肥钊.[2018.5月使用Github+Hexo搭建自己的博客](https://blog.csdn.net/weixin_39879178/article/details/80319392)

[2]陈素封.[如何搭建一个独立博客——简明Github Pages与Hexo教程](https://www.jianshu.com/p/05289a4bc8b2)

[3]张学志.[hexo教程系列——hexo配置教程](https://blog.csdn.net/xuezhisdc/article/details/53130383)

[4]十里枯木.[一、搭建篇-使用Github-hexo搭建个人博客教程—总结自己爬过的坑](https://yq.aliyun.com/articles/117271)

[5]Michaelhbjian.[利用Hexo在多台电脑上提交和更新github pages博客](https://www.jianshu.com/p/0b1fccce74e0)


## 写在后面
>感谢您的阅读！若您在阅读时发现教程存在疏漏或无法理解的地方，可以通过 **评论区留言** 进行交流讨论。
>
>下一篇：[离Hexo博客搭建只差一个教程（二）：主题](https://blog.ojhdt.com/20181004/hexo-2)

此文章为原创作品，禁止转载。如需转载请先经过许可，并在转载中注明原作者及出处。

请 `收藏` 本博客，本博客将持续更新。

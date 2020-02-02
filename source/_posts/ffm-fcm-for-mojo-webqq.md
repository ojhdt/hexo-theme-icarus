---
title: CentOS 7 下配置FCM for Mojo-webQQ
date: 2018-09-01 11:28:34
categories: "教程"
tags: [FCM,QQ,Tencent]
toc: true
excerpt: "Web QQ 已在 2019年1月1日 停止运营。<br>
服务器接收信息，通过谷歌推送FCM到手机。充分利用 Android 的通知的特性，支持直接回复、捆绑通知等。服务端将根据客户端设置决定是否推送，真正节省电量。"
---
Github：https://github.com/RikkaApps/FCM-for-Mojo


**Web QQ 已在 2019年1月1日 停止运营，教程已失效。**

## 主要功能

服务器接收信息，通过谷歌推送FCM到手机。

充分利用 Android 的通知的特性，支持直接回复、捆绑通知等。

服务端将根据客户端设置决定是否推送，真正节省电量。

## 服务端配置

### 安装依赖

#### Cpanm
    curl -kL https://cpanmin.us | perl - App::cpanminus

或使用

    yum install perl-App-cpanminus.noarch

#### Git

    yum install -y git

#### node.js

    curl -sL https://rpm.nodesource.com/setup_9.x | bash -
    yum -y install nodejs

#### Perl

    yum install -y perl-Crypt-OpenSSL-RSA perl-Crypt-OpenSSL-Bignum

### 安装Mojo-Webqq

    cpanm Mojo::Webqq

#### 检测安装情况
使用该指令检测，确保Mojo-Webqq安装完成

    curl -ks "https://raw.githubusercontent.com/sjdy521/Mojo-Webqq/master/script/check_dependencies.pl"|perl -
>若出现错误，请检查是否为`IO::Socket::SSL`一项安装失败。
>
>可使用`cpanm IO::Socket::SSL`进行安装。

### 安装FCM-for-Mojo_server

    git clone https://github.com/RikkaApps/FCM-for-Mojo-Server.git
    cd FCM-for-Mojo-Server
    cp config.example.js config.js
    npm install

#### 更新服务端

    git pull
    npm install

### HTTP加密（可选）

#### 安装http-auth模块

    git clone git://github.com/http-auth/http-auth.git
    npm install http-auth

#### 配置

创建一个任意文件名，内容为用户名:密码的文件，下面是一个简单的例子：

    username:passsword
在上面的例子中，客户端中的用户名填写为：username，密码填写为：password。 你也可以通过写入多行实现多个用户名和密码

编辑 config.js，找到有 basic_auth 那几行并去掉附近的注释（即 /* 和 */）：

	"basic_auth": {
		"file": "<密码文件路径>"
	},

### 启动服务端
    cd FCM-for-Mojo-Server
    npm start

## 客户端配置

安装 FFM - FCM for Mojo-WebQQ 客户端

[Google PLay](https://play.google.com/store/apps/details?id=moe.shizuku.fcmformojo)

[Coolapk](https://www.coolapk.com/apk/moe.shizuku.fcmformojo)

进入 `服务器设置`>`服务器URL`，填入服务器URL。（若进行HTTP加密，需填入设置的用户名和密码）

进入 `管理设备` ，点击右上角的“+”号添加此设备，再点击上传。

进入 `账号设置` ，输入QQ账号和密码。

重启服务器，扫码登陆。（若二维码无法推送，请查看服务器 /tmp/mojo-webqq-qrcode-ffm.png）

至此配置完毕。

<div align=center>
<img src="https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20180901/1.png" width="250" height="444" />
</div>

## 其余问题
若FFM推送时出现push failed，可通过 HTTP 代理连接 Google FCM 推送服务器。

修改config.js:

    // http proxy, FFM will connect to Google FCM Server with this proxy if you set it.
    //"push_proxy": 'http://127.0.0.1:8080',

取消注释，填入HTTP代理：

    // http proxy, FFM will connect to Google FCM Server with this proxy if you set it.
    "push_proxy": '你的HTTP代理',

## 写在后面
此文章为原创作品，禁止转载。如需转载请先经过许可，并在转载中注明原作者及出处。

请 `收藏` 本博客，本博客将持续更新。
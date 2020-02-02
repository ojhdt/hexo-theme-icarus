---
title: Nevolution：通知进化框架
date: 2018-08-30 18:58:34
categories: "资源"
tags: [Notification,ExtraSetting,Nevolution]
thumbnail: "https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20180830/0.png"
toc: true
excerpt: "Notification Nevolution（通知进化）是一款由著名开发者 Oasis Feng 开发的通知增强框架应用，借助该应用可以提高 Android 6.0+ 上的通知系统体验。<br>
应用仅为框架，本身并不起任何作用，需要配合插件运作。应用目前仍处于测试阶段。"
---
>Nevolution is an open platform for Android to evolve the notification experience of existing apps, in a creative developer-independent way via community-driven plug-ins, without the involvement of the original app developer.

Notification Nevolution（通知进化）是一款由著名开发者 Oasis Feng 开发的通知增强框架应用，借助该应用可以提高 Android 6.0+ 上的通知系统体验。

应用仅为框架，本身并不起任何作用，需要配合插件运作。应用目前仍处于测试阶段。

Github：https://github.com/Nevolution/sdk

Telegram群组：https://t.me/oasisfeng_apps

<div align=center>
<img src="https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20180830/1.png" width="550" height="450" />
</div>

## 主程序安装

请先确认Android版本高于 6.0 ，再进行后续操作。

### 通过Google Play参与公测

1. 在 Google+ 中加入 [Nevolution community](https://plus.google.com/communities/108874686073587920040)

2. 在 Play Store 上加入 [Test 计划](https://play.google.com/store/apps/details?id=com.oasisfeng.nevo)。[PC 端链接](https://play.google.com/apps/testing/com.oasisfeng.nevo)

上述两步完成后，Play Store 可能还需 5~10 分钟才能生效，然后即可下载。

>若提示不兼容，请先确认设备系统为 Android 6.0+，并且已加入 Test 计划。

### 通过网盘下载

不推荐，仅限于Play无法访问情况。

[百度盘](https://pan.baidu.com/s/1EqLbh1pKqOxnx0C9uiDiIw) 密码：ocbg

---

### 增强模式（仅限Android 8+）

Android 8+ 可以开启 Nevolution 的一个高级模式 —— Assistant 模式，实现通知的无缝替换（不会先闪现一下原通知）及更多特殊功能（比如隐藏划不掉的通知、恢复所有已延后的通知）。

#### 开启 Assistant 模式的 ADB shell 指令
（执行前先关闭 Nevolution 的通知访问权）

##### Android 8.0
    settings put secure enabled_notification_assistant com.oasisfeng.nevo/.Assistant

##### Android 8.1

    cmd notification allow_assistant com.oasisfeng.nevo/.Assistant

（执行后也不要再打开 Nevolution 的通知访问权，重启后不会失效）

#### 关闭 Assistant 模式的 ADB shell 指令

##### Android 8.0
    settings delete secure enabled_notification_assistant

##### Android 8.1
    cmd notification disallow_assistant com.oasisfeng.nevo/.Assistant

---

由于主程序没有用户界面，打开应用后通知栏出现通知。单击`Activate`按钮给予主程序通知访问权限。（若已开启增强模式可略过）至此主程序安装完成。

## 插件介绍
Nevolution需要配合插件才能运行。以下是目前可用插件。

### 微信 · 当代通知体验

>升级微信的上古通知体验，充分发挥当代 Android 通知栏的先进特性和优雅设计。

详细介绍：https://t.me/oasisfeng_apps/26662

开源项目：https://github.com/Nevolution/decorator-wechat

<div align=center>
<img src="https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20180830/3.png" width="250" height="444" /> <img src="https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20180830/4.png" width="250" height="444" />
</div>

#### 主要功能

- 通知栏快捷回复
- 通知分条显示，支持自动合并
- 划掉通知标记已读
- 优化的会话样式

#### 下载

先加入此插件的 [测试计划](https://play.google.com/apps/testing/com.oasisfeng.nevo.decorators.wechat)

等待 5-10 分钟后可下载：
[Google Play](https://play.google.com/store/apps/details?id=com.oasisfeng.nevo.decorators.wechat)

安装 [扩展包](https://t.me/oasisfeng_apps/29670)（务必先安装上述插件主程序）：
增加通知栏『回复』、划掉标记已读 等额外功能。

#### 安装

安装好插件及扩展包；

打开主程序，在弹出的通知中点击 `CREATE NEW` ；

提示 `TRY 微信通知·现代简洁风` ，点击 `ACTIVITE` ；

进入插件通知页。此时插件基本安装完毕。此时可通过点击 `DELETE` 移除插件，`MODIFY` 修改插件设置，`ADD` 添加该应用另一插件。

![2](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20180830/2.png)

#### 注意

>1. 需要在微信设置中开启『通知显示详细内容』，插件的主要效果才能发挥。
2. Android 8+ 如果遇到通知栏回复失败的情况，请检查『系统设置 - 应用 - 微信 - 电池优化 - 后台执行』，确认 开启 了『后台执行』权限。另外，如果有使用如 MyAndroidTools、Xposed、IFW 等手段对微信进行过处理，请尝试还原相应的处理。（插件目前并不支持 X-APM 显示的微信通知）

##### 关于微信插件的 Notification Channel 功能
目前定义的几个 channel 默认都是没有声音和震动的，因为微信默认开启的声音其实是微信 app 自己在后台播放的，震动也是，而非通过 Android 标准的通知声音/震动机制。所以要为不同的 channel 设置不同的声音和是否震动，就需要：
1. 先在微信里关掉通知声音和震动
2. 长按进化后的微信通知，从那里进入 channel 设置，给不同 channel 设置声音和震动。

该插件暂不支持Play版微信部分版本。


### 去电接听震动

详细介绍：https://t.me/oasisfeng_apps/26904

开源项目：https://github.com/Nevolution/decorator-callvibration

当拨出的电话被对方接听时震动手机。仅适用于类原生Dialer 和 Google Dialer。

### 截屏通知增强 by @fython

<div align=center>
<img src="https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20180830/5.png" width="250" height="444" /> <img src="https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20180830/6.png" width="250" height="444" /> <img src="https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20180830/7.png" width="250" height="444" />
</div>

详细介绍：https://t.me/oasisfeng_apps/59118

Google Play：https://play.google.com/store/apps/details?id=moe.feng.nevo.decorators.enscreenshot

借助了 Nevolution 框架（应用程序），增强你的截图通知，提升原生系统的体验。

对于用户，你所需要的是：

- 一台 Android 7.0 或更高版本的手机（暂不推荐 Android P 用户使用，因为有些特性已经重复了）
- 通知中心与截图机制未被魔改的 Android 系统
- 安装 Nevolution 应用，因为我们制作的插件依赖本体来运作
- 提供存储权限用于获取最新截图

目前提供了如下特性：

- 为通知增加 “编辑” 按钮
- 选定你偏好的编辑器以一键编辑
- 自定义分享后的操作
- 显示累计截图数量
- 显示新截图的信息（大小、分辨率、类型）
- 从启动器中隐藏
- 未来我们可能会添加更多……

我们已经将插件源代码以 GPLv3 协议开源并发布到 GitHub：
https://github.com/fython/EnhancedScreenshotNotification

### 短信验证码一键复制 by @Kr328 
Enhance short message captchas notification with following features:

- Direct copy captcha on notificaton.
- Hide captcha on lockscreen.

开源项目：https://github.com/Kr328/nevo-decorators-sms-captchas/


### 长文本内容 & 通知消息历史 & 隐藏划不掉的通知
详细介绍：https://t.me/oasisfeng_apps/42715

开源项目：https://github.com/Nevolution/decorators-misc

通用类小插件合集，内含三个小插件。

- 长文本 - 长文字内容，免于被截断。

- Stack - 看到通知的最近多条被覆盖的历史。

- No Sticky - 隐藏划不掉的通知（snooze 一次即可触发，Android 8+）


## 插件下载及安装

### 下载

为保证得到及时更新，不推荐使用网盘下载。

若Play无法访问，请使用 [百度盘](https://pan.baidu.com/s/1UMut8hHgK9cvzaUL635-IQ) 密码：ocbg

---
### 安装

请查阅 [前文](https://blog.ojhdt.com/20180830/nevolution/#%E5%AE%89%E8%A3%85)

## FAQ
>以下引自 @Oasis Feng 原文

- Q: 打开过应用之后，通知栏的通知消息还在，没有消失

     A: 这是 Nevolution 受到的一个 Android 系统的已知限制。目前理论上虽然有技术可解决，但是会付出非常高的性能成本，且大幅度增加 flash 写入次数。在没有找到更好的解决方案前，这个问题只能暂时搁置。

- Q: 工作资料内的应用通知无法区分是工作资料的 app

     A: 先把 Nevolution 安装（clone）到工作资料，然后给主用户的 Nevolution 授权：`pm grant com.oasisfeng.nevo android.permission.INTERACT_ACROSS_USERS`



## 参考页面

开发者 @Oasis Feng 的 [Telegram群组信息](https://t.me/oasisfeng_apps/26661)

酷安 [@古谷枫](http://www.coolapk.com/u/1847181) 的图文 [《Android 通知进化 —— Nevolution》](https://www.coolapk.com/feed/7972525)

## 写在后面
此文章为原创作品，禁止转载。如需转载请先经过许可，并在转载中注明原作者及出处。

请 `收藏` 本博客，本博客将持续更新。

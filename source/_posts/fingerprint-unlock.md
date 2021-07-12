---
title: Remote Fingerprint Unlock：使用指纹解锁你的 Windows PC
date: 2018-11-03 16:32:25
categories: "教程"
tags: [Windows,Software]
cover: "https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181103/0.png"
toc: true
excerpt: "对每次想要解锁计算机时输入密码感到厌倦？<br>
Remote Fingerprint Unlock，它允许您通过验证已录入的指纹远程唤醒和解锁您的 Windows 计算机！"
---
对每次想要解锁计算机时输入密码感到厌倦？

**Remote Fingerprint Unlock**，它允许您通过验证已录入的指纹远程唤醒和解锁您的 Windows 计算机！

XDA：https://forum.xda-developers.com/android/apps-games/app-remote-fingerprint-unlock-unlock-t3841148

## 特性

- 免费版
 - 简单易用的UI
 - 安全
 - 本地微软账户支持
 - 夜间模式
 - 支持 Wi-Fi Tethering
- 专业版
 - 去除广告
 - 添加多设备
 - 每台设备添加多个账户
 - Lan 唤醒
 - 解锁桌面小部件 

## 如何使用

### 安装

1. 在 Android 设备上安装 Remote Fingerprint Unlock 主程序。

    [Play Store](https://play.google.com/store/apps/details?id=ro.andreimircius.remotefingerauth) 或 [XDA Labs](https://labs.xda-developers.com/store/app/ro.andreimircius.remotefingerauth)
>系统需求 Android 6.0+

2. 在 Windows PC（Windows Vista / 7/8/10）上安装 Fingerprint Credential Provider 模块。请选择相应的版本：64位(x64)或32位(x86)。

    [Google Drive](https://drive.google.com/drive/folders/1bktvp0JcJKfE92efgxQlo06ARrMfLDFd) 或 [本站公共网盘](https://netdisk.ojhdt.com/%E8%BD%AF%E4%BB%B6/Fingerprint%20Credential%20Provider/)

### 配置

计算机成功安装模块后，在登录屏幕会多出 `Fingerpring Unlock` 。

![1](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181103/1.png)

1. 打开软件，在侧边栏进入 `Scan` 菜单，（此时应确保您的计算机位于登录屏幕上）点击`刷新`按钮，选择你的计算机并点击`保存`。 
2. 转至 `My Accounts` 菜单，点按 `ADD ACCOUNT` ，输入要解锁的Windows账户名，录入指纹并填入登录密码。
3. 将该账户切换至 `Selected` 状态。
4. 转至 `Unlock` 菜单，验证录入的指纹即可远程解锁计算机。

<div align=center>
<img src="https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181103/4.png" width="250" height="444" /> <img src="https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181103/2.png" width="250" height="444" /> <img src="/img/20181103/3.png" width="250" height="444" />
</div>

## 安全性

在构建时考虑到安全性，应用程序：

- 可以安全地在公共网络上使用（即使在受损的网络上）- 所有发送的数据都是加密的。
- 使用标识应用程序安装的唯一标识符加密用户计算机中存储的信息。
- 不在 Android 应用程序中存储任何密码。
- 防止攻击者获取对您计算机的访问权限。如果攻击者知道您的PIN并添加了自己的指纹，则会立即通知应用程序并自动使其自己的密钥无效，这将会使存储的私人应用程序信息永久丢失。

## 写在后面
此文章为原创作品，禁止转载。如需转载请先经过许可，并在转载中注明原作者及出处。

请 `收藏` 本博客，本博客将持续更新。

---
title: Magisk 刷入方法及模块推荐
date: 2018-08-25 18:58:34
categories: "资源"
tags: [Root,Module,Magisk,ExtraSetting]
thumbnail: "https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20180825/9.png"
toc: true
excerpt: "Magisk Manager 的功能是不修改 /system 但实现修改的效果，比如隐藏 root，最重要的是不影响 OTA。和 xposed 一样，这个工具需要先刷 zip 包，在 XDA 的附件里提供。"
---
Magisk Manager 的功能是不修改 /system 但实现修改的效果，比如隐藏 root，最重要的是不影响 OTA。和 xposed 一样，这个工具需要先刷 zip 包，在 XDA 的附件里提供。

XDA: https://forum.xda-developers.com/apps/magisk/official-magisk-v7-universal-systemless-t3473445

Github: https://github.com/topjohnwu/Magisk/releases

Coolapk: https://www.coolapk.com/apk/com.topjohnwu.magisk

## 功能

### 获取 root 权限

功能与SuperSU类似，为设备提供最高权限。

### Magisk 挂载

在系统启动前加载 Magisk 修改过的系统文件，来达到与直接修改系统文件相同的效果。“不修改 /system 但实现修改的效果”正是基于这一特点。

### Magisk Hide

对部分应用隐藏root权限。

### Safety Net 检测

帮助系统通过如 Google的Safety Net检测 等关于系统安全的测试。 

## 刷入

### 常规刷入/卸载方法
1. 下载 [Magisk](https://github.com/topjohnwu/Magisk/releases/)。

2. 重启进入 TWRP Recovery ，选择Zip文件刷入。

>Team Win Recovery Project（TWRP）是一个开放源码软件的定制恢复模式（rec模式）映像。它开放一个支持触摸屏的界面，允许用户向第三方安装固件和备份当前的系统。安装TWRP通常需要已解锁的 **Bootloader**，但不一定需要 Root 。具体安装步骤一般可在各机型 XDA 论坛上获取。

3. 下载并安装 [Magisk Manager](https://github.com/topjohnwu/Magisk/releases/)。请勿与 magisk 安装文件混淆。

---

在 TWRP 刷入 [卸载包](https://github.com/topjohnwu/Magisk/releases/download/v18.1/Magisk-uninstaller-20190204.zip) 来卸载Magisk。（全版本支持）


### 模块安装方法

打开侧边栏，点击`模块`选项。

点击`黄色加号按钮`，找到你准备的 Magisk 模块文件（.zip）。

等待安装完毕，重启设备。

## 优秀模块推荐

### Riru - Core
> Inject zygote process by replace libmemtrack.so, provide interface to other Riru modules.
>
>Riru 系列模块的核心。

Riru 是一个简单但有用的东西。仅需要替换一个系统文件，就可以让 Riru 模块们进入应用进程或系统服务进程并执行他们的代码。

简单来说，此模块为 Riru 系列模块的前置模块。Riru 系列模块基于此进行制作，并依靠本模块实现功能。

具体介绍可参阅 [Github](https://github.com/RikkaApps/Riru/) 文档。

作者：Rikka

以下为部分 Riru 系模块。

#### Riru - Google App Helper
>Magisk version of Google App Helper.

Google App Helper（Google App 助手）为一款 Xposed 模块。本模块为借助 Riru 实现的 Magisk 版本。它可以实现以下功能：
- 中文下启用【智能助理】
- 启用 Google Now Card
- 启用【提醒】功能
- 自定义 Now Card 语言
- 回复 Now on Tap 进行屏幕搜索

作者：givein2u

下载及说明请查看 [酷安](https://www.coolapk.com/apk/com.elderdrivers.googlesearchbox) 详情页。

#### Riru - Location Report Enabler
>Enable location report by hook system_property_get.

在中国大陆境内启用 Google 位置报告。

作者：Rikka
#### Riru - Strong Redirect
>Enhance module for Storage Redirect app.

Storage Redirect（存储重定向）可以重定向不规范的应用储存空间目录到正确的位置。该模块为启动 `增强模式` 所需的magisk模块。

作者：Rikka
#### Riru - EdXposed
>A Riru module trying to provide a ART hooking framework (mainly for Android Pie) which delivers a consistent APIs with the OG Xposed, leveraging YAHFA hooking framework.

Edxposed 是一款可在 **Android Pie** 上工作的**不稳定的** XposedBridge，可以像 Xposed 框架一样读取已安装激活的 Xposed 模块。不支持资源hook，且不支持一部分系统修改型模块。具体说明可查阅文章[Android Pie（9） 上的非官方 Xposed](https://blog.ojhdt.com/20190131/pie-xposed/)

Github：https://github.com/solohsu/edxposed

作者：givein2u

### Magisk Manager for Recovery Mode(MM)
>Manage your Magisk image, data, modules & settings from recovery mode -- run "/data/media/mm" on terminal.

在Recovery模式下通过运行`/data/media/mm`管理你的Magisk数据、模块和设置。**建议提前安装**，以处理安装不兼容模块时出现的无法进入系统问题。

作者：VR25

XDA: https://forum.xda-developers.com/apps/magisk/module-tool-magisk-manager-recovery-mode-t3693165

### Xposed Framework

>Xposed Framework by rovo89,ported to Magisk by topjohnwu.

Xposed框架的Systemless版本。该官方版本兼容 Android 5-8 。

作者：topjohnwu

XDA: https://forum.xda-developers.com/xposed/unofficial-systemless-xposed-t3388268

### ViPER4Android FX
>ViPER4Android FX is an audio enhancing software to provide everyone with a better audio experience.

以magisk方式安装蝰蛇音效。

作者：Zackptg5

XDA: https://forum.xda-developers.com/android/apps-games/app-viper4android-fx-2-6-0-0-t3774651

### Youtube Vanced
>A modded version of the original YouTube app.

Youtube增强版本，支持去广告，画中画等高级功能。

作者： KevinX8

XDA: https://forum.xda-developers.com/apps/magisk/magisk-iytbp-youtube-vanced-t3712097

### Greenify4Magisk
>A very simple module just to make Greenify work as a rom-integrated (privileged) app systemlessly.

绿色守护是一款可以控制系统后台软件运行的管理软件，做到节省内存和流量，智能休眠软件，较少电量消耗等等功能。

这是绿色守护的Magisk安装版本。

作者：abacate123 oasisfeng

XDA: https://forum.xda-developers.com/apps/magisk/module-greenify4magisk-t3606277

### Sony-Music4Magisk

>This Magisk module will install systemless sony music application in any magisk supported device. Sony Music app - by Sony Mobile Communications.

安装systemless版本的索尼音乐。兼容所有设备。

作者：utkarshp64

XDA: https://forum.xda-developers.com/apps/magisk/app-sony-music-app-systemless-install-t3596580

### Busybox for Android NDK
>Static busybox binary for all Android architectures built with the NDK.

在任何设备上方便地安装 **Busybox** 。许多软件（如 Lucky Pather）需要在 Busybox 环境下运行。

作者： osm0sis

GitHub：https://github.com/Magisk-Modules-Repo/busybox-ndk

### App Systemizer

>Turn apps to System Apps Systemlessly! Supports all device running Magisk.

方便快捷地把用户程序转换为系统程序。需要在已root的设备上使用终端键入`Systemize`指令进入界面。应用本身不具图形界面。

使用步骤：

1. 安装 [高级终端Termux](https://www.coolapk.com/apk/com.termux)
2. 输入 `su` 获取 root 权限。
3. 输入 `systemize` 进入主菜单。
4. 按照选项提示输入对应数字进行操作。

作者：veez21

XDA: https://forum.xda-developers.com/apps/magisk/module-app-systemizer-t3477512

### GALACTIC™ Forced DeepSleep
>This Forced DeepSleep MOD aims to prevent your device from sucking the battery overnight or when it is kept idle for longer hours and putting your devices in a complete sleep until you wake it by using dozen build prop tweaks. In simple words, it will stop the background processes when the phone is at rest and save battery life.

通过后台限制延长续航。

作者： daxiaamu

XDA： https://forum.xda-developers.com/oneplus-3/themes/roms-galactic-forced-deepsleep-mod-t3655480

### Digital Wellbeing Port
>Digital Wellbeing apps for AOSP-like roms.

在原生或类原生 Android Pie(9) 上启用数字健康。

作者： suwakowww

### Adreno GPU 驱动更新
更新GPU驱动版本。可能出现兼容性问题。

作者： 椿的神之圍樓

Coolapk: https://www.coolapk.com/feed/7272287


## 部分下载

模块为当时最新版本。部分模块因作者要求不提供下载。

[本站公共网盘](https://netdisk.ojhdt.com/%E5%BA%94%E7%94%A8/Magisk%20%E6%A8%A1%E5%9D%97/)

## 修订记录
- 20180825 文章发表
- 20180928 增加部分模块介绍
- 20181202 增加部分模块介绍,删除表述错误
- 20190119 增加部分模块介绍
- 20190303 增加部分模块介绍，详叙安装方法。

## 写在后面
此文章为原创作品，禁止转载。如需转载请先经过许可，并在转载中注明原作者及出处。

请 `收藏` 本博客，本博客将持续更新。




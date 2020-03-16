---
title: 原生党的福音 —— Pixel Experience 体验及功能拓展
date: 2020-03-15 12:24:14
categories: "小记"
tags: [Android,PixelExperience]
thumbnail: ""
toc: true
excerpt: ""
--- 
过气一加五基于 Android 10 的 **H2OS** 苦苦等待半年仍没有释出，这眼看着 Android 11 开发者预览版都出来了。虽然很喜欢H2OS的流畅简约（简陋？）但用久了也很容易腻，而且系统用久了也开始出Bug了（黑屏，耗电，卡顿），也是时候刷一下重焕新生了。盘算着不如上一次原生的贼车，体验一把Google的生态与流畅，反正翻车的话恢复一下备份就回来。生命在于折腾，二话不说脱离官方上 XDA 找包。对比了几个下载量比较大的包，发现还是 Pixel Experiences 最符合我心意。

选择 PE 的理由很简单：

- 支持机型多，意味着团队对包的打磨比较到位，对各机型都做了专门适配，翻车几率低些。
- 尽可能还原 Pixel 的体验，从名称 Pixel Experience 就能看出这一点。与 Resurrection Remix 走了另一个极端 —— RR 更追求对系统的配置，加入了尽可能多的自定义配置项；而 PE 点到即止，该怎么样就怎么样。对于对自定义比较执着的用户，还提供了轻度自定义版本 PE Plus。
- Google 生态。其他包一般都需要刷机时单独刷 GAPPS ，但 PE 开机即内置比较完整的一套 Google 控件，不会存在第三方刷入时的残障 Bug 。

因为不同设备的状况不同，我遇到的问题可能与各位实际操作的时候有所不同（虽然PE的普适性还是相当高，不会出大问题），本文章就只打算作为一个记录，不作正式教程啦~

先列一下我是怎样让 Pixel Experience 发挥最大功力的：

- 存储重定向
- Magisk + Xposed
- Viper4Android
- 全面屏手势，屏蔽实体按键
- QuickSwitch 加持 Lawnchair
- Nevolution
- 谷歌相机（这个 PE 自带就省得我捣鼓了）

#### 准备刷入
设备自然要先解锁 Bootloader 并且刷入 TWRP 啦。根据各大论坛大佬的说明，TWRP需要更新一下，不然刷不进最新版本的 Android

#### 跳过开机引导
为什么要将这一部分单独分一节

#### Magisk + Exposed + 必要模块

#### 修全面屏手势

#### 安装 Viper4Android

#### 用 Lawnchair 替换 Google 即时桌面
Google 即时桌面不香吗，流畅易用，兼容性也最好。本来我也是这么想的，但最关键的是——它不能更换图标包啊！

#### Nevolution 优化 Wechat/QQ通知

#### 杂项优化

体验相当不错。就算现在适配了 Andeoid 10 的 H2OS 我也不会再刷回去了，如此良好的体验或许连一加也给不了我了，我就假装自己在使用一部 Pixel 吧。
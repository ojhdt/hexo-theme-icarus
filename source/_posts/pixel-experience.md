---
title: 原生党的福音 - Pixel Experience 体验及功能拓展
date: 2020-03-16 12:24:14
categories: "小记"
tags: [Android,PixelExperience]
thumbnail: "https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200316/0.png"
toc: true
excerpt: "生命在于折腾，二话不说抛弃官方上 XDA 找包。对比了几个下载量比较大的包，发现还是 Pixel Experiences 最符合我心意。"
---
过气一加五基于 Android 10 的 **H2OS** 苦苦等待半年仍没有释出，这眼看着 Android 11 开发者预览版都出来了。虽然很喜欢H2OS的流畅简约（简陋？）但用久了也很容易腻，而且系统用久了也开始出Bug了（黑屏，耗电，卡顿），也是时候刷一下重焕新生了。盘算着不如上一次原生的贼车，体验一把Google的生态与流畅，反正翻车的话恢复一下备份就回来。生命在于折腾，二话不说抛弃官方上 XDA 找包。对比了几个下载量比较大的包，发现还是 Pixel Experiences 最符合我心意。

选择 PE 的理由很简单：

- 支持机型多，意味着团队对包的打磨比较到位，对各机型都做了专门适配，翻车几率低些。
- 尽可能还原 Pixel 的体验，从名称 Pixel Experience 就能看出这一点。与 Resurrection Remix 走了另一个极端 —— RR 更追求对系统的配置，加入了尽可能多的自定义配置项；而 PE 点到即止，该怎么样就怎么样。对于对自定义比较执着的用户，还提供了轻度自定义版本 PE Plus。
- Google 生态。其他包一般都需要刷机时单独刷 GAPPS ，但 PE 开机即内置比较完整的一套 Google 控件，不会存在第三方刷入时的残障 Bug 。

因为不同设备的状况不同，我遇到的问题可能与各位实际操作的时候有所不同（虽然PE的普适性还是相当高，不会出大问题），本文章就只打算作为一个记录，不作正式教程啦~

先列一下我是怎样让 Pixel Experience 发挥最大功力的：

- 存储重定向
- Magisk + Xposed
- Viper4Android
- 全面屏小白条，屏蔽实体按键
- QuickSwitch 加持 Lawnchair
- Nevolution
- 谷歌相机（这个 PE 自带就省得我捣鼓了）

### 准备刷入

刷机前一定要先**备份所有数据**并准备好备份文件，将文件全部转移到其他存储设备中。退出 Google 账户，避免引起稍后跳引导的麻烦。

设备自然要先解锁 Bootloader 并且刷入 TWRP 啦。根据各大论坛大佬的说明，TWRP需要更新一下，不然刷不进最新版本的 Android 。到[官网](https://twrp.me/Devices/)下载自己机型的 TWRP img 文件，手机进入 Fastboot 模式，用[ADB工具](https://developer.android.com/studio/releases/platform-tools)执行
```
fastboot flash recovery [recovery.img]
```
然后长按开机键+音量上进 TWRP ,**四清一格**（Dalvik Cache/System/Data/Cache，格式化Data分区），马上在重启菜单重启到 Recovery 确保正常挂载。然后挂载内部储存，将必要的**底包**，PE 系统包和解密补丁包复制到储存，按顺序刷入（这些应该 PE 都会提供）。如果驱动没装好挂载不了还可以尝试 `ADB Sideload` ，如果还不行就直接 9008 吧，毕竟刷机有风险。

如果一切顺利，重启后就能看到精致的 Pixel 开机动画了。首次启动约摸稍等个10分钟。

#### 跳过开机引导

为什么要将这一部分单独分一节？由于某些已知因素，国内是无法直连国外的验证服务器的，这也就意味着在无法获得小飞机加持情况下我们无法跳过开机引导。一般的做法是在开机前拔掉Sim卡来跳过，或者从左上角开始顺时针点按屏幕四角。但如果在刷机前你忘记退出Google账户，很不幸，你只能找到可行的方式来破解。

1. 连接到拥有科学上网环境的 Wifi

    这需要你事先在路由器上刷入了第三方固件并配置了科学上网

2. TWRP 终端
    重启到 Recovery ，进入终端
```
dd if=/dev/zero of=/dev/block/bootdevice/by-name/frp
```
3. 其他设备的热点共享
这里实测使用 [VPN热点](https://www.lanzous.com/b089aaw8d) 或 [HTTP Injector](https://www.lanzous.com/b089aaw8d) 都能达到效果。

![VPN 热点](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200316/1.png)
![HTTP 注入](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200316/2.png)

#### Magisk + Edxposed + 必要模块

这里也没有什么好说的，刷就完事了

刷入 [Magisk](https://www.lanzous.com/b089ab4mf) 重启，安装好 [Riru 系模块](https://www.lanzous.com/b089ab64j) 和其他[必要模块](https://www.lanzous.com/b089ab6di)（BusyBox，App systemizer，MM等）重启，最后刷入EdXposed，重启。

强调一下使用 Edxposed 是要关闭 SeLinux 的。这个可以用镧工具箱/搞机助手/Magisk 模块解决。

#### 全面屏小白条
Android 10 会在界面底端单独划分出一块区域填充色块来显示小白条，效果并不好。完美的小白条沉浸只在系统桌面或系统设置等深度适配的界面才有效。以下提供两种处理方式：

- Fullscreen Gestures

直接隐藏小白条，仅保留手势操作。如果对小白条不执著的话建议使用该方法。毕竟小白条也没有其他特殊的动效，只是一条横线罢了。

- Immersive Gestural Navigation Bar

保留小白条，仅去除小白条的色块填充背景。相当于在第一种处理方法的基础上加上一条白线，实现伪沉浸效果。

#### 屏蔽物理按键/关键盘灯

如果你的设备不是全面屏设备（比如我的一加五），刷入 PE 后呼吸灯会 24 小时亮起，在使用手势时也很容易误触。

对于屏蔽按键，这里提供一个比较普适的方法 [Eposed edge](https://www.lanzous.com/b089ab6id) 。安装该xposed模块，在`按键`一栏中将`返回键`，`最近应用键`和`主页键`的点击操作设置为`无`。也可以选择不设置主页键，预防手机手势无法操作时返回不了桌面。

对于呼吸灯关闭，我们可以借助 Magisk 的开机脚本执行来完成。在 `/data/adb/service.d/` 目录新建一个 `brightness.sh` 文件，**权限修改 755**，内容填入
```
echo 0 > /sys/class/leds/button-backlight/max_brightness
```


#### 安装 Viper4AndroidFX
蝰（kuí）蛇音效。这个在 Android 10 上的安装有点麻烦，如果操作不当就会发生卡第二屏的尴尬。下面列一下详细步骤：

1. 安装 [Audio Modification Library](https://www.lanzous.com/b089ab60f) 模块，**不要重启**；
2. 安装Viper4Android apk，授予 Root 权限，选择安装驱动，等待自动重启；
3. 在开机时**长按电源+音量上**将开机卡断（开机就卡屏），进 TWRP 挂载文件储存，进入`高级-文件管理`，删除`/data/adb/modules/VIPER4AndroidFX/service.sh`
4. 重启到系统，覆盖安装一个汉化版的Apk。（英语水平好的朋友可以略过此步）

目前来说还是要走这几步，或许之后能被修复吧。

![Viper4AndroidFX 界面](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200316/5.png)

#### 用 Lawnchair 替换 Google 即时桌面
Google 即时桌面不香吗，流畅易用，兼容性也最好。本来我也是这么想的，但最关键的是它不支持更换图标包啊！

- 安装最新测试版Laenchair
- 安装 QuickSwitch 模块，重启
- 进入 QuickSwitch ，启用 Lawnchair 的动画
- 有兴趣的可以把 Google Feed 也打开。（提前刷入Riru - Location Report Enabler 开启位置记录）

![QuickSwitch](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200316/3.png)

#### Nevolution 优化 Wechat/QQ通知

安装的话各位应该都懂，这里主要提供支持微信和QQ通知的几个 [Nevolution 插件](https://www.lanzous.com/b089ab6mh)。QQ 由于接口的关系就没有办法实现通知栏回复啦，真怀念去年 Web QQ 还没关的时候用 FCM 转发 QQ 消息时的体验。

![Nevolution](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200316/4.png)

安装方法很简单。首先将 Nevolution 修改内源模式。然后将插件全部装上并激活就可以了，不需要做额外配置。

#### 杂项优化

- 核心破解
- 存储重定向
- Youtube_Vanced

都是模块，装上就好。[Xposed](https://www.lanzous.com/b089ab6id) [Magisk](https://www.lanzous.com/b089ab6di)

### 小总结

感觉写到后面就有点水文的味道了，不是我不想写而是真的没有什么可写的，都是一个模块就能解决的事情。不得不说Magisk真是相当强大的存在。几年前它刚问世的时候还只是被当作一个 Root 管理器，但自从 SuperSu 断更了之后它便迅速壮大，凭借强大的功能和优越的性能甚至超越了 Xposed 的地位。

本文所用到的杂七杂八的文件我都上传到蓝奏云了，方便自己和有需要的朋友取用。

配置好后的 Pixel Experiences 体验相当不错。就算现在适配了 Andeoid 10 的 H2OS 我也不会再刷回去了，如此良好的体验或许连一加也给不了我了，我就假装自己在使用一部 Pixel 吧。
---
title: Android Pie（9） 上的非官方 Xposed
date: 2019-01-31 22:01:58
categories: "小记"
tags: [Xposed]
thumbnail: "https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190131/0.png"
toc: true
excerpt: "Xposed 是一款可以在不修改 APK 的情况下影响程序运行(修改系统)的框架服务，基于它可以制作出许多功能强大的模块，且在功能不冲突的情况下同时运作。"
---
**Xposed** 是一款可以在不修改 APK 的情况下影响程序运行(修改系统)的框架服务，基于它可以制作出许多功能强大的模块，且在功能不冲突的情况下同时运作。

目前官方 Xposed 的维护者为 XDA 上的 [rovo89](https://forum.xda-developers.com/member.php?u=4419114) ，官方支持 Android 版本为 Lollipop(5), Marshmallow(6), Nougat(7) 和 Oreo(8) 。

Xposed 在 Android 早期版本（先于 Android Lollipop)后台管理混乱，系统漏洞层出的大环境中应运而生，以其修改系统的强大功能撼动了当时的玩机界，一度被认为是 Android 的顶峰。尽管 Google 在后续系统版本更新中使得系统更为完善，Xposed 起到的作用变得更少，这仍然不能动摇 Xposed 在搞机一族中的地位。

自 Android Pie(9) 发布之后，有关 Xposed 框架对 Pie 的支持始终是关注的焦点。无奈维护者已迟迟未作出相关回应，Xposed 的官方适配变得遥遥无期。

但是，国内的开发者们并没有停下第三方 Xposed 适配的脚步。尽管稳定性稍有欠缺，但 Xposed 的基本功能已基本实现。

<div align=center>

![1](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190131/1.png)

</div>

[Xposed 官方发布页](https://forum.xda-developers.com/showthread.php?t=3034811)

[Xposed 模块仓库](https://repo.xposed.info/module-overview)

### EXposed（太极·阴）
>一般情况下称 太极。

太极，是一个无需Root，不用解锁Bootloader，也不需要刷机就能使用 Xposed 模块的一个 APP 。

太极 免去了 Root ，Bootloader 解锁 等复杂步骤，它的出现大幅降低了 Xposed 的使用门槛，操作更为省心方便。令 Xposed 不再是技术宅的专属玩具。

![2](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190131/2.png)

作者：维术@weishu

微信公众号：虚拟框架

Github：https://github.com/tiann/EXposed

#### 特点

- 不需要 Root ，解锁 Bootloader。
- 极具兼容性，适配大部分设备，同时支持多 Android 版本。
- 太极内核 可以随时升级，升级操作只需要在 太极 App 内完成，无需刷机。
- 不强行拦截系统内所有 App ，仅对添加入太极的指定 App 起作用，具有极高的隐藏性。
- 不对系统作出修改，故一系列系统修改类模块（如重力工具箱）无法工作。
- 存在模块使用限制，仅支持开启指定模块的指定版本。

#### 使用步骤

[官方使用说明](https://github.com/tiann/EXposed/wiki/FAQ)

1. 下载安装 太极 和 希望使用的 Xposed 模块。最新太极安装包 请从官方微信公众号 `虚拟框架` 获取。

2. 在 太极 中 `创建应用`，添加要使用 Xposed 的应用。

<div align=center>
<img src="https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190131/3.png" width="250" height="444" /> <img src="https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190131/4.png" width="250" height="444" />
</div>

3. 备份数据，卸载 旧App。安装太极处理后的 新App。

4. 在 `模块管理` 中启用希望使用的 Xposed 模块。

<div align=center>
<img 
src="https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190131/5.png" width="250" height="444" /> <img
src="https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190131/6.png" width="250" height="444" /> <img src="https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190131/7.png" width="250" height="444" />
</div>

5. 进行应用优化。

6. 启动应用，相关模块功能已成功在你的应用上启用。

#### 注意事项
> 摘自官方使用说明。

- 为什么有些模块显示为“暂未开放”？
因为这些模块可能不稳定，或者*我（作者）没有使用过/不知道；如果你有需要，请联系我给我对应的模块信息。

- 如何完全卸载太极？
首先卸载掉所有在太极中创建过的APP（请注意备份数据），然后卸载太极即可。 如果你开启了阴阳之门，需要先在去 关于-关闭阴阳之门，然后才能卸载。

#### *阴阳之门
借助设备管理员模式，为 太极 提供系统更高权限。使用类似原理的应用还有 `冰箱 Ice Box`，`小黑屋`，`岛 Island` 等。

[官方文档](https://github.com/tiann/EXposed/wiki/How-to-activate-The-God's-door)

该操作需要一定 ADB 基础。请先准备 ADB 环境。
1. 前往下载 [ADB 工具包](https://developer.android.com/studio/releases/platform-tools)。

无法访问的用户请从 [本站公共网盘](https://netdisk.ojhdt.club/%E7%AB%99%E5%86%85%E6%96%87%E4%BB%B6/ADB.zip) 下载。

2. 按下 Win+R 打开运行，输入 `cmd` 运行；或在开始菜单中打开 `命令提示符`。

3. 使用 `cd [工具包所在文件路径]` 指令 进入工具包目录。

##### 用途
1. 可以大幅优化 太极 创建应用和升级应用的流程；不再需要手动确认，整个流程可以一气呵成。

2. 额外提供类似冰箱的冻结功能；可以冻结和隐藏应用。

##### 开启步骤

1. 进入手机「设置 - 帐户」，删除 **所有** 的帐户，包括你的 Google 帐户（之后可以再登录回来）。
2. 如果您之前设置过多用户或手机自带访客模式、应用双开等，也需要一并关闭或删除（之后可以打开）。
3. 手机连接电脑，在 开发者选项 中启用 `USB 调试`。（电脑应事先安装好连接驱动）在 ADB 命令窗口执行指令
```
adb devices
```
确保设备连接正常。

4. 执行指令
```
adb shell dpm set-device-owner me.weishu.exp/.DeviceAdmin
```

5.  如果显示 Success 字样，那么表明阴阳之门已经开启，也可以把之前删除的帐号加回来了。

##### 常见问题

> 摘自官方文档

- 问：提示 “Not allowed to ... already several accounts on the device”
答：第 1 步的账户没删干净，请注销您手机上所有的账户，包括 Google 账号和系统自带的如小米账户、三星账户等。注：Xperia 或 ZUK 手机在设置时请拔出 SIM 卡，之后再插入。

- 问：提示 “Trying to set the device owner, but device owner is already set.”
答：你手机中可能安装有 Island，冰箱，小黑屋等应用并给了它设备管理员权限（如Island的皇帝之名，冰箱的免Root模式之一等）。很遗憾，系统中的设备管理员只能有一个；如果你需要开启太极的阴阳之门，需要收回其他应用的设备管理员权限。

- 问：提示 “Not allowed to ... already several users on the device”
答：第 2 步的用户没有删除干净。

- 问：提示 “android.os.DeadObjectException ...”
答：尝试更换数据线或重启手机。

- 问：MIUI 用户提示 “Neither user xxx nor current process has android.permission.MANAGE_DEVICE_ADMINS”
答：MIUI 用户请手动在系统设置- 开发者设置里，开启「USB 调试（安全设置）」。

- 问：我尝试在安卓设置-设备管理器设置中启用太极以代替以上设置步骤，但是发现无法使用，怎么办？
答：设备管理员不等于设备管理器，启用设备管理器也无法启动阴阳之门。

##### 注意事项
国产手机系统时常修改 Android 底层，做出一些不符合规定的修改，因此其与设备管理员模式的兼容性或多或少存在一些问题。是否启用 `阴阳之门` 请自行斟酌。

### EdXposed
EdXposed 的出现可说纯属偶然。作者在为他的 Xposed 应用 Google App 助手(Google App Helper)尝试 Android 9 上的适配时，发现 Riru + yahfa 可以基本实现框架效果。经过一段时间的更新，EdXposed 已经趋于稳定。

<div align=center>
<img src="https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190131/8.png" width="300" height="555" />
</div>

作者：givein2u(Coolapk) ElderDrivers(XDA)
>为同一开发者

Github：https://github.com/ElderDrivers/EdXposed

#### 特点
- 借助 Riru 实现，专为 Android Pie 开发。
- 可通过配套管理应用 EdXp Manager 实现黑/白名单，兼容模式功能。
- 暂不支持资源 Hook。
- 不能与原版 Xposed 框架同时激活。
- 尚处于测试阶段，稳定性欠缺。

#### 使用步骤

1. 为你的设备安装 Magisk 。具体介绍可查看本站博文 [Magisk 刷入方法及模块推荐](https://blog.ojhdt.com/20180825/magisk/)。下载 Riru-Core 及 Ed Xposed 模块。请从各自 Github 发布页获取下载。
Riru：https://github.com/RikkaApps/Riru/releases
Ed Xposed：https://github.com/ElderDrivers/EdXposed/releases

2. 进入 Magisk Manager ，点击中间的加号，依次选择刷入 Riru - Core 和 EdXposed 模块。重启设备。

<div align=center>
<img src="https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190131/17.png" width="250" height="444" /> <img src="https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190131/18.png" width="250" height="444" />
</div>

3. 安装 [XposedInstaller_by_dvdandroid_19_10_18.apk](https://netdisk.ojhdt.com/%E7%AB%99%E5%86%85%E6%96%87%E4%BB%B6/XposedInstaller_by_dvdandroid_19_10_18.apk) (未修改，如果已安装可忽略)

4. 在 XposedInstaller 中启用模块，重启设备。

5. 安装 [EdXp Manager](https://www.coolapk.com/apk/com.solohsu.android.edxp.manager) 应用，对 白/黑名单 进行配置。

<div align=center>
<img src="https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190131/9.png" width="250" height="444" /> <img src="https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190131/10.png" width="250" height="444" /> <img src="https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190131/11.png" width="250" height="444" />
</div>

#### 常见问题
 - 激活模块后无法进入系统。
 如果乱激活模块后翻车了(特指进不了系统或者无法取消激活模块)，可以进到 Recovery 里刷入 Mount-Magisk.zip 然后去 高级-文件管理(以TWRP为例)里删掉 /magisk/riru_edxposed 这个文件夹。

- 微信/QQ 在启用 Xposed 后闪退
在 EdXp Manager 中勾选兼容模式。

- Android 9 在 Xposed Installer 中提示 `Xposed 尚不兼容您手机的 Android SDK 28 版本或处理器架构（arm64-v8a）。` 为正常现象，无需作出处理。

### 太极·magisk（太极·阳）
正式版已于 2月1日 正式发布。

**太极·Magisk 是增强版的太极。**
普通版的 太极 无法作用于系统APP，并且创建 APP 需要先卸载。太极·Magisk 借助一个 Magisk 模块注入系统，从而可以作用所有的 APP；可以实现 Xposed 框架的完整功能。

![12](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190131/12.png)

作者：维术@weishu

微信公众号：虚拟框架

[官方中文文档](https://github.com/tiann/EXposed/wiki/taichi-magisk-zh)

#### 特点
- 基本实现原版 Xposed 的所有特性。
- 良好的隐蔽性。由于通过 Magisk 实现，太极本身很难被应用检测。甚至不会影响 Safety Net。
- 不影响全局，可以针对单个应用启用 Xposed。
- 针对应用的模块不需要重启即可生效。
- 太极·Magisk 相对普通版，更为稳定，也更为迅速。


#### 正式版

更新正式版后，相比内测版作出以下改动：

- 内核更新，提升稳定性。

- 进一步优化内存占用，提升性能。

- 测试结束，取消内测码机制；刷入 magisk 模块即可使用。

- Magisk 模块 AB 合并，不再区分；自动对系统模块生效。

#### 使用步骤

1. 为你的设备安装 Magisk 。具体介绍可查看本站博文 [Magisk 刷入方法及模块推荐](https://blog.ojhdt.com/20180825/magisk/)。关注 虚拟框架 微信公众号 获取 `太极安装包` 及 `Tai Chi` Magisk 模块。

2. 进入 Magisk Manager ，点击中间的加号，选择刷入模块。重启设备。

3. 进入 太极App ，若成功识别并显示 `太极·阳` 即安装成功。

4. 下载并安装 Xposed 模块。在 `模块管理` 中勾选启用。在 `添加应用` 中添加使用 Xposed 的应用。

5. 结束应用进程，打开你的应用，观察效果。

>**注意：**必须把 APP 添加到太极中，太极才会对这个 APP 启用Xposed 功能。
>
>不是作用于系统的模块，无需重启手机即可生效。
>
>模块重新安装之后，需要重新勾选。

#### 自救方法
>摘自官方文档。

一旦出现了异常情况，无法开机；如何处理呢？有两种办法：

##### MM 管理器（推荐）
这种方法需要你先在 Magisk 中装好 **mm 管理器** 这个模块。

出现无法开启的情况后，长按音量下+电源键 10秒钟后进入fastboot模式，然后选择 `recovery` 模式重启。
使用数据线连接电脑，使用 adb shell 进入命令行；或者直接使用 recovery 提供的命令行终端。
输入 `/data/media/mm` 命令，选择 `u` 然后 输入 `taichi` 按两次回车键，重启即可。

##### 太极内置办法
首先进入 recovery 模式命令行，不赘述。
执行命令
``` 
rm -rf /data/taichi && rm -rf /data/system/taichi
```
重启手机

#### 内测版（V4.0前）
>不推荐使用。

#### 使用步骤

安装步骤大体相同。在选择安装版本时提供 AB 模块双版本。A 版本支持的模块更多，但稳定性较差；B 版本支持的模块较少，但较为稳定。一般情况下优先选择 B 版本。

在首次开启 太极 APP 使用 太极·Magisk是需要提供内测激活码。复制设备码，在 `虚拟框架` 公众号中回复，系统会自动发送设备内测码。将内测码输入提示框即可完成激活。

<div align=center>
<img src="https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190131/19.jpg" width="300" height="590" />
</div>

### VirtualXposed
**早期作品。相关功能已可通过 太极 完美替代，不推荐使用。**

VirtualXposed 是基于VirtualApp 和 epic 在非ROOT环境下运行Xposed模块的实现（支持5.0~9.0)。

与 Xposed 相比，目前 VirtualXposed 有两个限制：

不支持修改系统（可以修改普通APP中对系统API的调用），因此重力工具箱，应用控制器等无法使用。
暂不支持资源HOOK，因此资源钩子不会起任何作用；使用资源HOOK的模块，相应的功能不会生效。

![13](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190131/13.png)

作者：维术@weishu

微信公众号：虚拟框架

Github：https://github.com/android-hacker/VirtualXposed

#### 使用步骤
[中文文档](https://github.com/android-hacker/VirtualXposed/blob/vxp/CHINESE.md)

打开 VirtualXposed，在里面安装要使用的APP，以及相应的Xposed模块即可。

>注意：所有的工作（安装Xposed模块，安装APP）必须在 VirtualXposed中进行，否则Xposed模块不会有任何作用！比如，将微信直接安装在系统上（而非VirtualXposed中），防撤回安装在VirtualXposed中；或者把微信安装在VirtualXposed上，防撤回插件直接安装在系统上；或者两者都直接安装在系统上，均不会起任何作用。

在VirtualXposed中安装App有两种方式：

直接复制已经在系统中安装好的APP，比如如果你系统中装了微信，那么可以直接复制一份。
通过外置存储直接安装APK文件；点主界面的底部按钮－添加应用，然后选择后面两个TAB即可。
在VirtualXposed中安装Xposed模块，可以跟安装正常的APK一样，以上两种安装App的方式也适用于安装Xposed模块。不过，你也可以通过 VirtualXposed 中内置的 XposedInstaller 来安装和管理模块，跟通常的 XposedInstaller 使用方式一样；去下载页面，下载安装即可。

<div align=center>
<img src="https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190131/14.png" width="250" height="444" /> <img src="https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190131/15.png" width="250" height="444" /> <img src="https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190131/16.png" width="250" height="444" />
</div>


#### 下载
官方下载页：https://vxposed.com/download.html

### 附录
- XDA 上的 [Ed Xposed 模块支持整理汇总帖](https://forum.xda-developers.com/xposed/list-xposed-modules-android-pie-ed-t3892768)

### 写在后面
此文章为原创作品，禁止转载。如需转载请先经过许可，并在转载中注明原作者及出处。

请 `收藏` 本博客，本博客将持续更新。
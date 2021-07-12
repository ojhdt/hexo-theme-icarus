---
title: ViPER4Android FX 安装及音效配置推荐
date: 2018-09-17 11:25:48
categories: "教程"
tags: [Apps,Music]
cover: "https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20180917/0.png"
toc: true
excerpt: "Viper4Android FX（蝰蛇音效）是一款Android全局音频驱动。通过该软件可以给音频渲染各种音频效果，如均衡器，回放增益，脉冲反馈处理，场环绕，数字混响，动态系统等。用户通过对音效的配置，在低端耳机设备下也能够明显提升音效效果。"
---
Viper4Android FX（蝰蛇音效）是一款Android全局音频驱动。通过该软件可以给音频渲染各种音频效果，如均衡器，回放增益，脉冲反馈处理，场环绕，数字混响，动态系统等。用户通过对音效的配置，在低端耳机设备下也能够明显提升音效效果。

在 **2.7.0.0** 版本，VIPERFX对应用界面进行了大幅度的修改，采用了较为直观的 Material 设计，取消侧边栏，输出设备切换及配置导入转移到底栏进行。

<div align=center>
<img src="https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20180917/2.jpg" width="250" height="444" /> <img src="https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20180917/3.jpg" width="250" height="444" /> <img src="https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20180917/4.jpg" width="250" height="444" />
</div>

### 安装

#### 通过 Magisk安装
该安装方法方便快捷，在已安装Magisk的设备下安装模块，重启即可。Magisk 刷入方法及模块下载可见 [此帖](https://blog.ojhdt.com/20180825/magisk/) 。

>安装过程中需要使用音量键进行安装偏好设置，如版本，主题等。"Press Vol Up"和"Press Vol Down"分别是按下音量+/-的意思。

新版模块下载请前往。感谢酷安用户 [@落笔成酌](http://www.coolapk.com/u/772460)

[百度盘](https://pan.baidu.com/s/1XLhvvXfAbzYLc7GjqTt8ag) 密码：m325

#### 普通安装
在进行后续操作前请先获取Root权限。

1. 下载Apk文件。

    前往 [XDA](https://forum.xda-developers.com/android/apps-games/app-viper4android-fx-2-6-0-0-t3774651) 或 [Coolapk](https://www.coolapk.com/apk/com.pittvandewitt.viperfx)

2. 打开应用，提示安装驱动提示，点击确定，选择安装最新版本。

3. 授予Root权限，点击重启。重启后安装完成。
>该方法安装存在兼容性问题，推荐使用 Magisk 安装。

#### 确认安装状况

划出左侧侧边栏，点击驱动程序状态。'已启用'一项为“是”即为安装完成。

2.7.0.0 或以上版本`驱动程序状态`入口转移至界面右上角。

>`正在处理`一项通常情况下为“否”，只有在处于音乐播放状态才转为“是”。如果始终保持“否”，尝试重新启动应用或更换播放器。

<div align=center>
<img src="https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20180917/1.png" width="250" height="444" /> 
</div>

### 音效配置推荐及安装

#### 音效配置安装

在安装VIPER4Android FX后，根目录会自动生成`ViPER4Android`文件夹。此处用于存放音效配置文件。

- Kernel 脉冲反馈样本文件夹
- Profile 音效配置文件夹

音效配置作者一般会注明音效文件放置路径，安装要求放置即可。

安装完毕后，进入应用，在侧边栏中点击`加载音效配置`，选择相关配置。

#### 音效配置推荐

推荐几个自己用着舒服的音效。

##### PRiME BASS

作者：酷安[@Pαtrick](http://www.coolapk.com/u/526061)

[原帖链接](https://www.coolapk.com/feed/6478166)

「PRiME BASS 1.1」

这次用了三个耳机测试并调教音效，测试下来基本能带来接近的听感哦~

PRiME BASS 1.1 - By 酷安[@Pαtrick](http://www.coolapk.com/u/526061)

PRiME BASS 1.1 分为三个版本：

「PRiME BASS level 1」 
基于 Apple Earpods 调教，这个耳机本身低音强于其他耳机，所以level1的低音是相对较弱的[二哈]。

「PRiME BASS level 2」 
用了万魔某型号的耳机调教，三频均衡，适用于绝大多数耳机[w调皮]。(万魔属于小米生态链，所以理论上这个应该也适用小米耳机)。

「PRiME BASS level 3」 
变态低音，不建议使用Earpods尝试...出现任何不适请立刻摘下耳机，任何后果自负。

「使用方法」 
1.解压本压缩包，得到一个ViPER4AndroidFX文件夹；
2.把它覆盖到手机内部存储根目录；
3.进入VIPERFX，应用配置文件。

[这里](https://shimo.im/bhP3SKhBMDY1RejS)可以看到所有版本，另外新增了一个扬声器专属音效，感兴趣的可以戳上面的链接进去看看。

请根据个人喜好选择版本，你也可以自行调教，但任何后果自行承担。

##### HRTF自研环绕音效

作者：酷安[@封心巛](http://www.coolapk.com/u/592446) ICE 玄音团队

[原帖链接](https://www.coolapk.com/feed/7087504)

本音效为本团队成员精心打造的高品质音效，使用自研声场感知参数HRTF，主打高品质的原音调节，音染极低的环绕声场，极高的乐器分离和低音感知增强。

说明：此音效为4声道音效，在网络上流传极少同类文件（图中会解释4声道原理）感谢 脉冲教员 的4声道技术支持。4声道脉冲需要最新版的viper4软件支持。

使用方法：放在脉冲文件夹，再去软件内选择此脉冲文件。其他效果关闭即可，保证本音效的原汁原味。

效果描述：（使用平台小米note顶配版，360N6，铁三角CKR7，AKG K430）开启效果后，感觉好像2个HIFI音响在面前，并且声场大了不少，低音弹性好了些，听摇滚乐的伴奏每一个细节都很明显，女声完美，完胜ACG，古典氛围感强了不少。——玄音团队试听小D

测试歌曲：

- 流行（That Girl）
- ACG（負けないで）
- 古典（Johann Strauss II: Annen-Polka, Op. 117）
- 女声（光辉岁月-孙露）
- 低音（ONE-Aimer）

[下载链接](https://pan.baidu.com/s/1LhkIQQ9HLGosfX7ZN7lBuA) 密码：1597

##### 沌™XAOC Sound
作者：酷安[@樂酒](http://www.coolapk.com/u/2318220)

[原帖链接](https://www.coolapk.com/feed/10637282?shareKey=N2FjMTBkNjk5MTVlNWM4ZGFmOTU~&shareUid=617206&shareFrom=com.coolapk.market_9.0.4)

![5](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20180917/6.jpg)

- 上次看到不少酷基在前几条动态下问有没有听DJ电音啥用的音效。由于我前两个音效都是养老院用的那种睡眠音效，不适合听太动次打次的音乐，所以就想着可不可以整一个听DJ或者是动次打次纯音乐的那种音效…
- 于是就整出了这个**沌™XAOC Sound**音效，为动次大♂次而生。当然本音效主要用于纯音乐，人声被我削得很厉害，听到脑壳痛。
- **特点**:低音硬 中等重度 打击乐器靠前 人声废掉 还顺便带一点点环绕模拟电子音乐节临场感和祖传降噪技术。
- 那么…怎么用呢？下载并解压直接覆盖到存储目录 然后在V4A中加载音效配置 
>本音效仅支持Viper4android XDA代理开发版2.6.0.6-stable版本 在酷安历史版本下载中可以找到。
- [下载地址](http://t.cn/EIe5ki2)
##### 娆™Enchanting Sound
作者：酷安[@樂酒](http://www.coolapk.com/u/2318220)

[原帖链接](https://www.coolapk.com/feed/10454331?shareKey=N2M3YmFjMzliYTdmNWM4ZGIxMDk~&shareUid=617206&shareFrom=com.coolapk.market_9.0.4)

![6](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20180917/5.jpg)

- **娆™Enchanting Sound** 是一款基于 V4A 进行调节的音效 适合环境为睡眠音乐或者伴睡音乐 不建议在出行或在嘈杂环境使用。

- 本音效为睡眠音乐而生主要特点有
1. 全新的底噪压制调试Soak ！ Noise 睡眠时闭上眼睛 耳机里的沙沙声真的很烦。作者也就是我在安静的深夜三点钟仔细听底噪并且尽力调试将其压到最小程度。
2. 新的三频调制 整音效处于极轻的一种状态 低音松散绵软 人声仙女化(微环绕+清晰处理+不刺耳)。
3. 玄学的场效应压缩器设置
- 下载并解压直接覆盖到存储目录 然后在V4A中加载音效配置
>本音效仅支持Viper4android XDA代理开发版2.6.0.6-stable版本 在酷安历史版本下载中可以找到

- [下载地址](http://t.cn/EfVamD1)
>高端耳机不建议使用音效 本音效适合于听不下去原音的百元内渣渣耳机 作者测试耳机:earpods

### 修订记录
- 18-09-17 文章发表
- 19-03-17 增添图片说明，增添音效介绍


### 写在后面
此文章为原创作品，禁止转载。如需转载请先经过许可，并在转载中注明原作者及出处。

请 `收藏` 本博客，本博客将持续更新。






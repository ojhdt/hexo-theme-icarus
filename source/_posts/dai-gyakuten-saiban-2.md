---
title: 关于运行《大逆転裁判2》的一些探索
date: 2018-08-27 20:31:05
categories: "小记"
tags: [Games]
cover: "https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20180827/0.png"
toc: true
excerpt: "《大逆转裁判2 -成步堂龙之介的觉悟-》（日语：大逆転裁判2 -成歩堂龍ノ介の覺悟-）是由卡普空开发的文字冒险游戏，于2017年8月3日在任天堂3DS平台发行。"
---
逆转裁判系列想必已经是很多人心目中的神作了。《逆转裁判》（逆転裁判，Gyakuten Saiban）系列游戏是CAPCOM公司制作的法庭辩论型AVG游戏。在游戏中玩家扮演辩护律师，在假象规则的序审法庭上与检察官进行辩论，通过威慑和质疑嫌疑人和证人，为委托人获得无罪判决是最终的胜利目的。它新颖的游戏方式，扣人心弦的剧情和极佳的代入感成功地迷住了千千万万的玩家。那一句经典的“异议あり!”和蓝色西装刺猬头形象已经打破游戏的局限，成为了一个席卷网络界的老梗。

从2001年的《逆转裁判1》，到现在的主系列+大逆转+雷逆。平台也由最开始的GBA逐渐发展为NDS,3DS,Switch；甚至部分作品登陆了Android和ios平台。平台的更迭自然带来了更佳的游戏体验，但为了一款游戏购买游戏机也成为了广大粉丝的心头痛。尽管大部分作品已经可以很方便的在模拟器上游玩，但是，仍然有这么一款神作——

<div align=center>
<img src="https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20180827/1.png" width="280" height="250" />
</div>
<div align=center>
大逆転裁判2 －成歩堂龍ノ介の覺悟
[官网](http://www.capcom.co.jp/dai-gyakuten2/)
</div>

对于同样在3DS发布的6代和大逆转裁判1代，得益于某汉化组的努力，我们可以在Android上畅快游玩。可唯独2代没有了这样的机会。

为了玩上游戏，我进行了各方面的许多尝试。

## Android

目前在Android上只有日文版，曾在4月26日上线[日区Play](https://play.google.com/store/apps/details?id=jp.co.capcom.daigyakusai2jp&hl=zh)并提供一个月免费下载试玩。

我的思路是用Tasker搭建一个翻译脚本。自动对游戏文本进行OCR识别，然后发送到Google翻译，以悬浮窗形式即时显示翻译结果。

![2](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20180827/2.png)

遗憾的是效果并不理想。不仅结果显示存在巨大延迟，翻译精确度也不乐观。这迫使我放弃了这项计划。

![3](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20180827/3.png)

## PC

很久之前PC上就有了一款叫做Citra的3DS模拟器，只不过当时优化的不好，对设备要求很高，许多游戏也无法运行。经过一段时间的更新，直到 山猫二四 在3月29日发布了非官方GPU大提速版本，才使我开始尝试使用这款模拟器。

先贴上渣渣配置：

- AMD 速龙II X4
- 4G内存
- 1G AMD Radeon HD 6450 显卡

模拟器可以在 [这里下载](https://tieba.baidu.com/p/5624999673?red_tag=0659458128) 根据介绍选择适合自己处理器的版本。

解密后的游戏可以在 [这里下载](https://pan.baidu.com/s/1huGUGwNeY5ilU6_Rt7Qgww) 密码：ocbg

---

### 设置项

以下展示的都是最低配设置。

![4](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20180827/4.png)

Ignore fomat reinterpretation，某些情况下对应部分游戏提速一点，但是可能削弱整体稳定。

FMV Hack 写上 **65000** 。能打破CPU性能界限，大多数情况下动画和游戏奇迹般进一步提速。但也容易造成崩溃。

Internal Resolution，分辨率。如果性能不足还是开最低吧。

很重要的一点，游戏使用**最小视窗**运行，可以少量提速。

### 效果（留意右下角速度显示）

主界面可以达到80%以上；

![5](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20180827/5.png)

交谈基本满速；

![6](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20180827/6.png)
![7](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20180827/7.png)

在询问，法庭辩论，推理剧场环节跌至70%，但基本不影响。

## 写在后面
此文章为原创作品，禁止转载。如需转载请先经过许可，并在转载中注明原作者及出处。

请 `收藏` 本博客，本博客将持续更新。




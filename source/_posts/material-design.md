---
title: "致逝去的 Material Design 1.0 ：国内应用设计规范将何去何从？"
date: 2021-09-12 01:30:11
categories: "小记"
tags: [MaterialDesign,MD]
cover: "https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210912/0.png"
toc: true
excerpt: "自 Material Design 推出后，谷歌陆续发布了许多有关MD的支持库，这使得开发者遵循MD规范的学习成本进一步降低。部分开发者与互联网公司开始接受规范，将自家的产品UI向规范靠拢。其中不乏一些用户量相当庞大的产品。"
---
在年中举行的 Google IO 2021 上，谷歌正式发布了 Android 12 平台全新设计语言： Material You。作为 Material Design 框架下的第三代产物，Material You 在继承Material Design 的典型属性之余，更加强调客制化，将更多界面元素的自定义选项开放给用户。相比起之前的两代，最新一代对形状，颜色的应用更为大胆，为用户带来一套相当亮眼的全新设计方案。尽管目前该设计还未推送更新，但这无疑已引燃广大Android用户的期待。

![全新的 「Material You」 设计](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210912/1.jpg)

或许有的读者会发出疑问，这「Material Design」究竟是什么来头？我使用的也是 Android 设备，为什么从来没有使用过采用 Material Design 设计的应用？

其实 Material Design 并非什么近期的新设计。早在2014年，谷歌就提出了 Material Design ，以统一当时混乱的界面风格。如果你有使用过早期Android（5.0之前）设备，你肯定会对当时应用混乱的设计风格记忆深刻。一方面，当时Android标准界面设计风格（Holo）不是特别被大众接受，很多公司觉得自己可以设计出更棒的界面，导致Android界面风格长期难以统一；另一方面，同时期 iOS 5 的拟物风格取得巨大成功，大多数人认为Android系统的UI没有IOS的美观，开发者在开发UI时也主动向IOS风格靠拢。可以说，伴随 Android 5.0 到来的 Material Design 彻底改变了这一乱象，甚至掀起了一阵适配 Material Design 的狂热。

![Android 早期版本中常用的 Holo Theme](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210912/3.jpg)

![iOS5 惊艳的拟物风界面](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210912/4.png)

![I/O 14 发布会现场](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210912/5.png)

至于国内用户对此了解甚少，其实是国内大环境导致的。国内各家手机搭载的基本都是经过深度定制的Android系统（MIUI,Flyme，Smartisan OS等），系统UI经过厂商重新设计，鲜有原汁原味的原生，从而淡化了 Material Design 的存在。各大主流应用也由于各种原因，对设计风格的统一适配并不积极。但尽管如此，你也或许曾或多或少地在其他产品上看到 Material Design 的影子。

![MIUI便签中醒目的 FAB](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210912/2.png)

## 何为Material Design

**Material Design**（材料设计）是由 Google 开发的设计语言。据谷歌表示，他们并不希望Material Design是一套一成不变的设计语言。凡是符合Material特性的，都可称其为Material Design。每一个符合MD设计规范的元素，都具有以下特点：

**材质：** 每一个MD的最小元素**材料**都可以伸缩，改变形状；可以拼接，分裂；它具有厚度，可以产生遮挡效果与阴影，拥有惯性与反馈。

![「材料」的特性](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210912/9.gif)

**空间：** MD的环境是一个三维空间，但用户设备的屏幕是一个二维平面。为了强调三维特性，谷歌借用**阴影**和**层叠**，构造出了**Z轴**的概念，z值越高，元素离界面越远，投影就会越重，元素也就能够遮挡位于其下的内容。

![三维空间](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210912/6.jpg)

![不同高度下的阴影变化](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210912/7.jpg)


![层叠效果](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210912/8.jpg)

**动画：** 动画是MD设计规范中极其重要的部分。设计师们试图构造出近似于真实物理运动状态。当一个元素发生运动时，它应当具有合理的速度/加速度变化，所有元素都不可能立刻运动或停下；所有元素都应该具有及时的反馈，其颜色，高度，位置等都可能随用户操作发生合理的改变。（标志性的“水波纹”点击动画也因此而生）

![标志性的「水波纹」动画](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210912/10.gif)

以下是谷歌于七年前发布的[宣传片](https://www.youtube.com/watch?v=Q8TXgCzxEnw)。即使过去七年，Material Design 展示出的生动效果依然令人惊叹。

{% dplayer "url=https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210912/Material%20design.mp4" "api=https://api.prprpr.me/dplayer/" "pic=https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210912/bg.png" "autoplay=false"%}


## 短暂的统一

>Google 凭什么认为 Material Design 就能解决 Android 平台界面风格不统一的问题呢？一言蔽之，好看！
>
>--郭霖 《第一行代码》

自Material Design 推出后，MD迎来了它三年的巅峰期，横跨四大Android版本(Marshmallow - Oreo)，随后推出的2.0与You相比1.0变化较大，暂不纳入讨论。在这期间，谷歌陆续发布了许多有关MD的支持库，这使得开发者遵循MD规范的学习成本进一步降低。部分开发者与互联网公司开始接受规范，将自家的产品UI向规范靠拢。其中不乏一些用户量相当庞大的产品。

至于适配的积极性，一般来说国外>国内，个人开发>企业产品。


### 企业运营
以下为本人在 Android 11 平台下对部分知名软件的历史版本的重温。它们都在一定程度上遵循了 Material Design。遗憾的是，其中大多数经过历次更新后逐渐抛弃MD。

#### 知乎
>测试版本 5.0.0

前些年的知乎客户端绝对是国内各应用的设计典范，完美的Material Design，流畅的交互，清爽的界面，令人无可挑剔。当然，现在的知乎在界面/内容体验上都大不如前了。

![登录界面](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210912/11.png)

![主界面](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210912/12.png)

![主界面](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210912/13.png)

![设置项](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210912/14.png)

#### 酷市场
>测试版本 6.4.2

酷安的前身。纯粹的应用市场，界面清爽美观，动画流畅。遵循初代规范，没有底栏。

![主界面](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210912/15.png)

![侧边栏](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210912/16.png)

![设置项](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210912/17.png)

#### Bilibili
>测试版本 5.0.0

不敢相信吧，B站竟也曾是 MD 的主力军！完美的侧边栏，Tab置顶，没有底栏。

测试版本已无法播放视频，但还能加载和显示主页和评论等。

![主界面](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210912/18.png)

![侧边栏](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210912/19.png)

![设置项](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210912/20.png)

![检索页](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210912/21.png)

![播放页](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210912/22.png)

#### Taptap
相比先前的几个应用，Taptap的MD味就没那么浓了。该应用近几年的界面都没多大变化，只在最近进行了一波大更新，各位可以稍微回忆下。虽然采用了侧边栏，但对 MD 精髓 —— 卡片的应用相对没那么频繁。动画方面也稍有欠缺。

Taptap也是我测试的应用中唯一一个要求强制升级的，吃相实在是太恶了，被迫断网截图。截图耗费了大力气。

![启动页](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210912/27.png)

![侧边栏](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210912/28.png)

### 个人开发
个人开发者对于 MD 的遵循则较为积极与全面，经过长期的更新也能保持设计。许多美观而优秀的小众应用应运而生。

#### Phonograph（点唱机）
>测试版本 1.3.5

自诞生起就以精美的Material Design著称的音乐播放器。交互逻辑，动画效果深得MD之精髓，甚至做出了类似宣传片中的效果。

![启动页](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210912/29.png)

![专辑页面](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210912/30.png)

![侧边栏](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210912/31.png)

![播放中](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210912/32.png)

#### 贴吧Lite
>测试版本 3.5.3

优秀的贴吧第三方客户端。遵循Material Design，功能丰富，界面精美，可见开发者深厚的功底。

![启动页](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210912/33.png)

![设置项](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210912/34.png)

![帖子](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210912/36.jpg)

![回复窗口](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210912/37.jpg)

#### Share
>测试版本 3.6.0（已阵亡）

老牌微博第三方客户端，功能丰富。遵循Material Design。

![主页](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210912/38.png)

![侧边栏](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210912/39.png)

![设置项](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210912/40.png)

![回复页](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210912/41.png)

## 何去何从

很无奈地，由于种种原因，或许是 Material Design 本身的局限性（学习成本高，实现逻辑复杂），或许是谷歌的推行力度不够，这一场设计规范盛会悄然闭幕了。先前尝试遵循规范的，又逐渐走回自己的老路；先前不遵循规范的，兴昂昂地当了一回看客；其中更有甚者，为追求的“双平台统一性”，又去追随iOS界面风格了。

不得不承认的是，各大应用的用户界面都取得了进步，起码可以说是步入现代了。但要说其具有设计，说实话我不敢恭维。

应用商业气息更厚重了。标志性的侧栏与FAB被移除，大幅图片在屏幕上肆意铺张，图标换成了更易吸引注意的动态图标。提示窗，小纸片从视窗的各处弹出，使用户应接不暇……

各模块间的切换逻辑被淡化了。信息流侧边能拉出直播窗口，底栏上能放上单独的购物商城入口。

![纷杂的页面元素](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210912/49.png)

![各功能切换逻辑混乱](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210912/50.png)

这一乱象居然还延伸到了图标上！先让我们回顾下 MD 对图标的部分要求：

- 请勿强制将徽标或图片铺满整个素材资源空间
- 请勿将最终素材资源的边角调圆
- 避免在图片中传递促销信息和品牌徽章

在规范限制下，图标个个匀称，精美，使人赏心悦目。

![Google 应用旧版图标](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210912/47.jpg)

可如今，先不提规范的要求了。不知是哪家带的头，竟将方正的图标下端划去三分之一，放上一句莫名其妙的标语！简直让人可恨又可笑。

![图标闹话](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210912/48.jpeg)

---
有人说，要解决国内应用设计规范的问题，需要国内一家有魄力的公司率先站出来，给出一套大众认可的方案，再建立一个类似App Store的机制，对上架的应用界面提出规范要求。

有人将希望寄予华为与鸿蒙。

也有人认为现在就很好，根本不需要设计规范。

你怎么看？欢迎留下你的看法。

>本文部分图片素材来自网络


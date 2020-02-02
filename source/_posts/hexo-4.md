---
title: 离Hexo博客搭建只差一个教程（四）：第三方服务——APlayer
date: 2018-10-06 12:25:14
categories: "教程"
tags: [Blog,Hexo,Music]
thumbnail: "https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181002/0.png"
toc: true
excerpt: "APlayer 是一款 HTML 音乐播放器。目前被广泛使用在各大知名社区论坛上。相比其他音乐播放器，APlayer的优势很明显：界面美观，轻量易用。"
---
>上一篇：[离Hexo博客搭建只差一个教程（三）：第三方服务——Valine](https://blog.ojhdt.com/20181005/hexo-3)


在上一篇教程中，我们介绍了 Valine 评论系统的安装，配置与应用。

仅有文字的博客总令人感到枯燥无味，在阅读博客时自动播放 BGM，不仅能给博客添逼格，还能表现个人品味喜好。

接下来，我们会介绍一款 HTML5 音乐播放器 —— APlayer 。

## 介绍
> Wow, such a beautiful HTML5 music player

![1](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181006/1.png)

APlayer 是一款 HTML 音乐播放器。目前被广泛使用在各大知名社区论坛上。相比其他音乐播放器，APlayer的优势很明显：界面美观，轻量易用。

展示页：https://aplayer.js.org

GitHub：https://github.com/MoePlayer/APlayer

中文文档：https://aplayer.js.org/#/zh-Hans

### 单曲

<div class="row">
<meting-js
    list-folded="true"
	theme="#1da496"	     
	server="netease"
	type="song"
	id="33911781">
</meting-js>
</div>

### 歌单

<div class="row">
<meting-js
    list-folded="true"
	theme="#1da496"	     
	server="netease"
	type="playlist"
	id="2382616934">
</meting-js>
</div>

### 其他样式
同时提供 吸底模式 和 迷你模式。具体样式可前往官方展示页。

## 安装

```
npm install aplayer --save
```
最新的 Hexo-tag-aplayer 拓展插件已经内置 MetingJS 支持。本着易用性原则，本教程不介绍旧版使用的 APlayer + Meting 方案。

## Hexo-tag-aplaper
hexo-tag-aplayer 是 APlayer 播放器的 Hexo 标签插件。相比起直接使用 APlayer ，安装和应用都更为简便。

GitHub：https://github.com/MoePlayer/hexo-tag-aplayer

中文文档：https://github.com/MoePlayer/hexo-tag-aplayer/blob/master/docs/README-zh_cn.md

### 安装
```
npm install --save hexo-tag-aplayer
```
### 常规使用方法

#### 单曲

在需要添加播放器的页面中加入：
```
{% aplayer "title" "author" "url" "picture_url" "narrow"  "autoplay" "width:xxx" "lrc:xxx" %}
```
| 参数          | 值                |
|:--            |:--                  |
| `title`      | 曲目标题。                |
| `author`       | 曲目作者。                |
| `url`        | 音乐文件 URL 地址。            |
| `picture_url`     | （可选）音乐对应的图片地址。            |
| `narrow`        | （可选）播放器袖珍风格。|
| `autoplay`  | （可选）自动播放，移动端浏览器暂时不支持此功能。|
| `width`  | （可选）播放器宽度 (默认: 100%)|
| `lrc`  | （可选）歌词文件 URL 地址。|

当开启 Hexo 的 文章资源文件夹 功能时，可以将图片、音乐文件、歌词文件放入与文章对应的资源文件夹中，然后直接引用：
```
{% aplayer "Caffeine" "Jeff Williams" "caffeine.mp3" "picture.jpg" "lrc:caffeine.txt" %}
```

#### 播放列表

在需要添加播放器的页面中加入：
```
{% aplayerlist %}
{                               // 播放器参数
    "参数": "值",
    "music": [
        {                       // 歌曲1参数
            "参数": "值",
        },
        {                       // 歌曲2参数
            "参数": "值",
        }
    ]
}
{% endaplayerlist %}
```

| 参数          | 值                |
|:--            |:--                  |
| `narrow`        | （可选）播放器袖珍风格。|
| `autoplay`  | （可选）自动播放，移动端浏览器暂时不支持此功能。|
| `mode`       | （可选）曲目循环类型，有 `random`（随机播放）, `single` (单曲播放), `circulation` (循环播放), `order` (列表播放)， 默认：`circulation`。 |
| `showlrc`        | （可选）歌词显示配置项，可选项有：`1`,`2`,`3`。            |
| `mutex`     | （可选）该选项开启时，如果同页面有其他 aplayer 播放，该播放器会暂停。 |
| `theme`        | （可选）播放器风格色彩设置，默认：`#b7daff`。|
| `preload`  | （可选）音乐文件预载入模式，可选项： `none` `metadata` `auto`, 默认: `auto`。|
| `listmaxheight`  | （可选）该播放列表的最大长度。|
| `title`      | 曲目标题。                |
| `author`       | 曲目作者。                |
| `url`        | 音乐文件 URL 地址。            |
| `pic`     | 音乐对应的图片地址。            |
| `lrc`  | （可选）歌词文件 URL 地址。|

示例：
```
{% aplayerlist %}
{
    "narrow": false,
    "autoplay": true,
    "mode": "random",
    "showlrc": 3,
    "mutex": true,
    "theme": "#e6d0b2",
    "preload": "metadata",
    "listmaxheight": "513px",
    "music": [
        {
            "title": "CoCo",
            "author": "Jeff Williams",
            "url": "caffeine.mp3",
            "pic": "caffeine.jpeg",
            "lrc": "caffeine.txt"
        },
        {
            "title": "アイロニ",
            "author": "鹿乃",
            "url": "irony.mp3",
            "pic": "irony.jpg"
        }
    ]
}
{% endaplayerlist %}
```

#### 歌词标签
使用 aplayerlrc 标签在博客中直接插入歌词文本。示例：
```
{% aplayerlrc "title" "author" "url" "autoplay" %}
[00:00.00]APlayer audio
[00:04.01]is
[00:08.02]amazing
{% endaplayerlrc %}
```

### MetingJS方法
在 **站点配置文件** 中启用 meting 模式，在配置末尾添加：
```
aplayer:
  meting: true
```

>同时提供以下配置项：
```
aplayer:
  script_dir: some/place                        # Public 目录下脚本目录路径，默认: 'assets/js'
  style_dir: some/place                         # Public 目录下样式目录路径，默认: 'assets/css'
  cdn: http://xxx/aplayer.min.js                # 引用 APlayer.js 外部 CDN 地址 (默认不开启)
  style_cdn: http://xxx/aplayer.min.css         # 引用 APlayer.css 外部 CDN 地址 (默认不开启)
  meting: true                                  # MetingJS 支持
  meting_api: http://xxx/api.php                # 自定义 Meting API 地址
  meting_cdn: http://xxx/Meing.min.js           # 引用 Meting.js 外部 CDN 地址 (默认不开启)
  asset_inject: true                            # 自动插入 Aplayer.js 与 Meting.js 资源脚本, 默认开启
  externalLink: http://xxx/aplayer.min.js       # 老版本参数，功能与参数 cdn 相同
```


在需要添加播放器的页面加入：
```
{% meting "选项" %}
```

| 选项          | 默认值     | 描述                                                        |
| ------------- | ---------- | ----------------------------------------------------------- |
| id            | **必须值** | 歌曲 id / 播放列表 id / 相册 id / 搜索关键字                |
| server        | **必须值** | 音乐平台: `netease`, `tencent`, `kugou`, `xiami`, `baidu`   |
| type          | **必须值** | `song`, `playlist`, `album`, `search`, `artist`             |
| fixed         | `false`    | 开启固定模式                                                |
| mini          | `false`    | 开启迷你模式                                                |
| loop          | `all`      | 列表循环模式：`all`, `one`,`none`                           |
| order         | `list`     | 列表播放模式： `list`, `random`                             |
| volume        | 0.7        | 播放器音量                                                  |
| lrctype       | 0          | 歌词格式类型                                                |
| listfolded    | `false`    | 指定音乐播放列表是否折叠                                    |
| storagename   | `metingjs` | LocalStorage 中存储播放器设定的键名                         |
| autoplay      | `true`     | 自动播放，移动端浏览器暂时不支持此功能                      |
| mutex         | `true`     | 该选项开启时，如果同页面有其他 aplayer 播放，该播放器会暂停 |
| listmaxheight | `340px`    | 播放列表的最大长度                                          |
| preload       | `auto`     | 音乐文件预载入模式，可选项： `none`, `metadata`, `auto`     |
| theme         | `#ad7a86`  | 播放器风格色彩设置                                 |

歌单示例：
```
{% meting "60198" "netease" "playlist" "autoplay" "mutex:false" "listmaxheight:340px" "preload:none" "theme:#ad7a86"%}
```

单曲示例：
```
{% meting "543611431" "netease" "song" "autoplay:false" "theme:#1da496" %}
```

## 其他问题
- 参数填写时要符合一定格式。参数值前要加入空格，文本内容要使用双引号括住。
- meting和aplayer同时使用的时候，aplayer无法显示出播放器。

## 参考文章
[1]Tianma.[Hexo 折腾：音乐播放](https://tianma.space/post/3998746934/index.html)

## 写在后面
>感谢您的阅读！若您在阅读时发现教程存在疏漏或无法理解的地方，可以通过 **评论区留言** 进行交流讨论。
>
>上一篇：[离Hexo博客搭建只差一个教程（三）：第三方服务——Valine](https://blog.ojhdt.com/20181005/hexo-3)
>
>下一篇：[离Hexo博客搭建只差一个教程（五）：第三方服务——Google 服务](https://blog.ojhdt.com/20181013/hexo-5)

此文章为原创作品，禁止转载。如需转载请先经过许可，并在转载中注明原作者及出处。

请 `收藏` 本博客，本博客将持续更新。

---
title: 曲库大整理
date: 2020-07-27 15:59:17
categories: "小记"
tags: [Music,Aplayer]
thumbnail: "https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200727/0.png"
toc: true
excerpt: "Aplayer + Pjax，这是个人博客添加音乐播放器的主流方法。配合 MetingJS ，甚至能够实现从某易云，某鹅音乐拉取歌单，在线播放。但由于版权问题，目前失效的音乐越来越多了。"
---
各位看到缩在网页左下角的播放器了吗？[Aplayer](https://github.com/MoePlayer/APlayer) + Pjax，这是个人博客添加音乐播放器的主流方法。配合 [MetingJS](https://github.com/metowolf/MetingJS) ，甚至能够实现从某易云，某鹅音乐拉取歌单，在线播放。但由于版权问题，目前失效的音乐越来越多了。自己喜欢的音乐无法添加到网站上，这着实令人无奈。

![音乐失效](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200727/1.png)

转念一想，又为何偏要执念用MetingJS呢？只需要上传歌曲文件，运用原生Aplayer就能实现相同的效果，只是工作量较大。说干就干。

首先观察播放器的元素，它由一张专辑封面图片和歌曲名、作曲家文字构成。因此我们需要的歌曲信息为歌曲mp3文件直链，专辑封面图片文件直链和标签信息。筛选出自己喜欢的歌曲，并按照统一格式命名，补充完整歌曲信息。再用软件提取出标签储存的封面或匹配缺失的封面，我这里用的是[@vincentlwc](http://www.coolapk.com/u/410561)开发的`音乐标签PC版`，功能相当完善，可以相当方便地提取出专辑封面。在软件的帮助下，我很快地整理出必要的文件。接下来将文件上传至服务器或对象存储，提取出直链。

![软件界面](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200727/2.png)

![上传文件到腾讯云COS并提取直链](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200727/3.png)

在播放器方面，我们可以参照[文档](https://aplayer.js.org/#/zh-Hans/)的示例，先在网页中加载一个吸底模式的Aplayer。在`<head>`标签里添加：

```
<link rel="stylesheet" href="APlayer.min.css">
<div id="player"></div>
<script src="APlayer.min.js"></script>
<script>
const ap = new APlayer({
    container: document.getElementById('player'),
    mutex: true,
    listFolded: true,
    fixed: true,
    theme: '#1565c0',
    order: 'random',
    audio: [
        {
            name: 'name',
            artist: 'artist',
            url: 'url.mp3',
            cover: 'cover.jpg'
        }
    ]
});
</script>
```
>Aplayer本身还提供大量配置[参数](https://aplayer.js.org/#/zh-Hans/?id=%E5%8F%82%E6%95%B0)，此处仅作为演示。

将对应的值替换，一首歌就算添加完成了。但随着歌曲数量的增加，代码行的数量骤增，在网页中一下子引入那么长的代码似乎不太恰当；因此我们可以将歌曲部分提取出来打包成一个 js 文件，再在正确的地方引入：

```
<link rel="stylesheet" href="APlayer.min.css">
<div id="player"></div>
<script src="APlayer.min.js"></script>
<script src="music.js"></script>
```
`music.js`可以这么写
```
const ap = new APlayer({
    container: document.getElementById('player'),
    mutex: true,
    listFolded: true,
    fixed: true,
    theme: '#1565c0',
    order: 'random',
    audio: [
        {
            name: 'name-1',
            artist: 'artist-1',
            url: 'url-1.mp3',
            cover: 'cover-1.jpg'
        },
        {
            name: 'name-2',
            artist: 'artist-2',
            url: 'url-2.mp3',
            cover: 'cover-2.jpg'
        },
        {
            name: 'name-3',
            artist: 'artist-3',
            url: 'url-3.mp3',
            cover: 'cover-3.jpg'
        }
    ]
});
```
这样就一目了然了。接下里要做的就是将所有的歌曲都添加进去。这和用 MetingJS 时简单点个红心不同，这种方式需要大量的复制粘贴操作，工作量还是相当大的。

一切准备妥当，上传，刷新网页。播放器正确列出歌单，熟悉的旋律响起，大功告成！
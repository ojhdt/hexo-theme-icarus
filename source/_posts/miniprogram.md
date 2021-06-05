---
title: "我们开发的第一款微信小程序"
date: 2021-03-03 09:42:33
categories: "小记"
tags: [Wechat]
thumbnail: "https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210304/0.png"
toc: true
excerpt: "拉拢了几名队友组建了小队，投入一个寒假的时间，体验了一把 Github 的协同工作流。"
---

断更三月的鸽手博主终于想起了他的服务器密码，打算对过去一段时间的瞎捣鼓做一些总结。

为了应付学院举行的小程序比赛，更多的是为了考验一下自己的编码能力，鄙人拉拢了几名队友组建了小队，投入一个寒假的时间，体验了一把 Github 的协同工作流。在进度尤其紧张的过年期间，基本我也一天不落的贡献上 commit。

![耕耘](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210304/1.png)

目前项目已在 Github 开源。首次做项目代码难免难看，还请各位看官多做提点，能点个 Star 就更好啦。

https://github.com/ojhdt/HoloTask

## 功能

考虑到自身水平和微信平台的诸多限制，小程序被定位为一款任务管理应用，毕竟都是简单的数据输出。功能新奇是说不上的，同类应用有的我们做不出来，我们做出来的都是同类标配了。但在界面方面，相比起其他小程序铺天盖地的广告，生硬的动画，混乱的配色，我对成品的质量还颇有自信。

在构建表单页面时，我对 `input`，`switch`，`textarea`，`picker`组件进行了类MD重制。但没有添加标志性的水波纹动画。其一是小程序性能有限，还由于小程序开发的诸多限制。

目前已实现的功能有：

- 任务的发布，编辑，状态更改与删除
- 图片，附件的传输与在线预览
- 群组的创建，成员添加与管理
- Markdown 语法支持
- 数据统计
- 归档整理
- 完整的深色模式支持

![亮色模式预览](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210304/light.png)

![深色模式预览](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210304/dark.png)

## 开发历程

开发过程总体还算顺利。

微信官方的封装为开发带来了极大的方便。我个人比较喜欢的是它的动画实现方式`this.animate()`。只需要指定需要修改的样式，就可以方便地制作出鼠标滚动驱动的渐变动画。
```
this.animate('.search_input', [{
    opacity: '0',
    width: '0%',
  }, {
    opacity: '1',
    width: '100%',
  }], 1000, {
    scrollSource: '#scroller',
    timeRange: 1000,
    startScrollOffset: 120,
    endScrollOffset: 252
  })
```

但遇到的坑还不少。容我在此简单吐槽一下。

首先，微信小程序不允许DOM操作，这使得动态修改样式变得尤其困难：
```
document.getElementById(id).style = "color:#000;" //不可行
```
改以setData()实现:
```
<div id="id" style="{{style}}"></div>
```

```
this.setData({
    style: "color:#000;"
})
```
在涉及大量动态样式时，setData()还会伴有较长延迟（半秒左右），体验很不好。

其次，还有一些css属性不可用，例如 background-image 添加本地背景图
```
div {
    background-image: url(pic.png);
}
```

![报错](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210304/2.jpg)

## 上线？

微信作为国民IM，拥有庞大的用户基数，它展开的每一项功能自然也要以大局考量。对于小程序这种稍高自由度的平台，微信官方用一份[详尽的文档](https://developers.weixin.qq.com/miniprogram/product/material/#%E4%B8%AA%E4%BA%BA%E4%B8%BB%E4%BD%93%E5%B0%8F%E7%A8%8B%E5%BA%8F%E5%BC%80%E6%94%BE%E7%9A%84%E6%9C%8D%E5%8A%A1%E7%B1%BB%E7%9B%AE)规定了各主体开放使用的服务类目。而对于个人主体，具有信息分发功能的程序都是不被允许上线的。我们理所当然地收到了这份拒审通知。

![审核未通过](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20210304/3.png)

对于这个结果，我个人还是表示理解。国内网络环境特殊，微信官方也是煞费苦心。

简单小结一下本次开发。总而言之，微信小程序的封装降低了开发门槛，微信的庞大平台也方便了应用推广。但就我个人而言，我很大可能不会再尝试涉足该领域。所谓的 `WXML`私改标签名，徒增学习成本。`JS`添加诸多限制，控件可供自定义项少。挟持开发者来为自己的生态服务。但不管怎么说，小程序还是一块很好的跳板。
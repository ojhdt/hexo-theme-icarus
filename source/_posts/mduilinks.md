---
title: MDUI 制作简易友情链接页面
date: 2020-02-03 19:59:44
categories: "资源"
tags: [MDUI]
thumbnail: "https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200203/0.jpg"
toc: true
excerpt: "最近使用的几套 Hexo 主题都没有提供独立的友情链接页面，按照 MDUI 的文档和官方示例，自己动手写了一组友情链接卡片。"
---
<link rel="stylesheet" href="//cdnjs.loli.net/ajax/libs/mdui/0.4.3/css/mdui.min.css">
<script src="//cdnjs.loli.net/ajax/libs/mdui/0.4.3/js/mdui.min.js"></script>


[MDUI](https://www.mdui.org/) 是一套用于开发 Material Design 网页的前端框架。轻量级，无依赖，并且拥有出色的展示效果。它的学习成本很低，只需懂一点 HTML、CSS、JS 的基础知识，就能使用 MDUI。

最近使用的几套 Hexo 主题都没有提供独立的友情链接页面，于是我按照 MDUI 的文档和官方示例，自己动手写了一组友情链接卡片。具体效果可以参考本站的友链页面。

下面是食用流程

### 安装

#### CDN
推荐使用 CDN 安装，在 `<head>` 中引入即可。这一方法适用于所有 HTML 页面。
```
<head>
    ...
    <!-- require MDUI --
    <link rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/mdui/0.4.3/css/mdui.min.css">
    <script src="//cdnjs.cloudflare.com/ajax/libs/mdui/0.4.3/js/mdui.min.js"></script>
    ...
</head>
<body>
    ...
</body>
```

官方同时提供两套 CDN

**`cdnjs`** （国外访问速度较快）
```
<link rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/mdui/0.4.3/css/mdui.min.css">
<script src="//cdnjs.cloudflare.com/ajax/libs/mdui/0.4.3/js/mdui.min.js"></script>
```
**`css.net`** （国内访问速度较快）
```
<link rel="stylesheet" href="//cdnjs.loli.net/ajax/libs/mdui/0.4.3/css/mdui.min.css">
<script src="//cdnjs.loli.net/ajax/libs/mdui/0.4.3/js/mdui.min.js"></script>
```

#### NPM
```
npm install mdui --save
```

### 创建友链独立页面
在 `source` 文件夹中创建一个文件夹（此处以 `links` 为例），在内创建一个标准 `index.md` 文件，作为友链独立页面。

此处使用 MDUI 有两种方式，一种是直接在文章内容中使用 MDUI 的 HTML 代码。一种则是在 `front-matter` 中用 layout 函数指明要使用的布局，并在布局中进行有关 MDUI 的设置。后者可以真正改变页面显示的元素，如关闭友链页面的评论，而前一种方式只能维持原来 `post` 的布局，相当于仅对文章内容进行修改。

下面就是我写的卡片单元啦。得力于 MDUI 的响应式网格布局，卡片宽度和个数可以根据设备屏幕大小做出改变。这里设置的是在大屏幕设备上一行放两个卡片
```
<div class="mdui-col-xs-12 mdui-col-sm-6"><br>                     #这里可以设置每行卡片数量
  <a href="https://..." target="_blank">                           #填入点击卡片后跳转的地址
    <div class="mdui-card mdui-hoverable mdui-ripple">             #为卡片添加悬停阴影和水波纹动画
      <div class="mdui-card-header">
      <img class="mdui-card-header-avatar" src="icon.png"/>        #填入网站图标的地址
        <div class="mdui-card-header-title">Title</div>            #标题
        <div class="mdui-card-header-subtitle">Subtitle</div>      #副标题
      </div>
    </div>
  </a>  
</div> 
```
效果：

<div class="mdui-container-fluid">
  <div class="mdui-row">
    <div class="mdui-col-xs-12 mdui-col-sm-6"><br>
	    <div class="mdui-card mdui-hoverable mdui-ripple">
          <div class="mdui-card-header">
          <img class="mdui-card-header-avatar" src="https://gravatar.loli.net/avatar/adb831a7fdd83dd1e2a309ce7591dff8?s=40&d=mp"/>
            <div class="mdui-card-header-title">Title</div>
            <div class="mdui-card-header-subtitle">Subtitle</div>
          </div>
	    </div>
	</div> 
    <div class="mdui-col-xs-12 mdui-col-sm-6"><br>
	    <div class="mdui-card mdui-hoverable mdui-ripple">
          <div class="mdui-card-header">
          <img class="mdui-card-header-avatar" src="https://gravatar.loli.net/avatar/adb831a7fdd83dd1e2a309ce7591dff8?s=40&d=mp"/>
            <div class="mdui-card-header-title">Title</div>
            <div class="mdui-card-header-subtitle">Subtitle</div>
          </div>
	    </div>
	</div> 
  </div>
</div>
<br>

也可以根据需求修改自己想要的列数，例如一行放三个卡片。MDUI 网格布局默认一个容器的宽度为 **12** ，`mdui-col-xs-[1-12]` 设定的宽度在所有屏幕设备上都会生效，如手机、电脑等。`mdui-col-sm-[1-12]`设定的宽度在小屏幕及以上的设备上生效，如平板电脑。此处的 `mdui-col-xs-12 mdui-col-sm-6` 指的是在所有设备上都只显示一个，但在平板电脑及更大屏幕的设备上显示两个（相当于只在手机上才显示一个，其余都显示两个）。想要一行放三个，只需要改成 `mdui-col-xs-12 mdui-col-sm-4` 。
>这里具体可以参考 MDUI 的[文档](https://www.mdui.org/docs/grid#responsive)

由于我的页面比较窄，显示效果不太好

<div class="mdui-container-fluid">
  <div class="mdui-row">
    <div class="mdui-col-xs-12 mdui-col-sm-4"><br>
	    <div class="mdui-card mdui-hoverable mdui-ripple">
          <div class="mdui-card-header">
          <img class="mdui-card-header-avatar" src="https://gravatar.loli.net/avatar/adb831a7fdd83dd1e2a309ce7591dff8?s=40&d=mp"/>
            <div class="mdui-card-header-title">Title</div>
            <div class="mdui-card-header-subtitle">Subtitle</div>
          </div>
	    </div>
	</div> 
    <div class="mdui-col-xs-12 mdui-col-sm-4"><br>
	    <div class="mdui-card mdui-hoverable mdui-ripple">
          <div class="mdui-card-header">
          <img class="mdui-card-header-avatar" src="https://gravatar.loli.net/avatar/adb831a7fdd83dd1e2a309ce7591dff8?s=40&d=mp"/>
            <div class="mdui-card-header-title">Title</div>
            <div class="mdui-card-header-subtitle">Subtitle</div>
          </div>
	    </div> 
	</div> 
    <div class="mdui-col-xs-12 mdui-col-sm-4"><br>
	    <div class="mdui-card mdui-hoverable mdui-ripple">
          <div class="mdui-card-header">
          <img class="mdui-card-header-avatar" src="https://gravatar.loli.net/avatar/adb831a7fdd83dd1e2a309ce7591dff8?s=40&d=mp"/>
            <div class="mdui-card-header-title">Title</div>
            <div class="mdui-card-header-subtitle">Subtitle</div>
          </div>
	    </div>
	</div> 
  </div>
</div>
<br>

那么卡片单元怎么用呢

先添加一个将始终占据 100% 的屏幕宽度的容器。并建立基础网格。如果希望在页面两侧留下空位，可以去掉 `-fluid` 来建立一个占据 92% - 96% 的屏幕宽度的容器
```
<div class="mdui-container-fluid">
  <div class="mdui-row">
    ...
  </div>
</div>
```
然后将卡片单元在省略号区域反复重复使用就行啦。不需要顾及换行等麻烦，你希望添加多少个友链，就重复多少遍。


下面是一个完整的示例
```
---
title: 友情链接
---
<div class="mdui-container-fluid">
  <div class="mdui-row">
    <div class="mdui-col-xs-12 mdui-col-sm-6"><br>
      <a href="地址一" target="_blank">
	    <div class="mdui-card mdui-hoverable mdui-ripple">
          <div class="mdui-card-header">
          <img class="mdui-card-header-avatar" src="图标一"/>
            <div class="mdui-card-header-title">标题</div>
            <div class="mdui-card-header-subtitle">副标题</div>
          </div>
	    </div>
      </a>  
	</div> 
    <div class="mdui-col-xs-12 mdui-col-sm-6"><br>
      <a href="地址二" target="_blank">
	    <div class="mdui-card mdui-hoverable mdui-ripple">
          <div class="mdui-card-header">
          <img class="mdui-card-header-avatar" src="图标二"/>
            <div class="mdui-card-header-title">标题</div>
            <div class="mdui-card-header-subtitle">副标题</div>
          </div>
	    </div>
      </a>  
	</div> 
  </div>
</div>
```
反复添加，保存，上传，大功告成！
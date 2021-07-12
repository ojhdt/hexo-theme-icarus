---
title: 离Hexo博客搭建只差一个教程（附录）：Markdown 语法
date: 2018-10-06 16:15:14
categories: "教程"
tags: [Blog,Hexo]
cover: "https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181002/0.png"
toc: true
excerpt: "Markdown 是一种轻量级标记语言，它允许人们使用易读易写的纯文本格式编写文档，然后转换成有效的XHTML（或者HTML）文档。这种语言吸收了很多在电子邮件中已有的纯文本标记的特性。"
---
**Markdown** 是一种轻量级标记语言，创始人为约翰·格鲁伯（英语：John Gruber）。它允许人们“使用易读易写的纯文本格式编写文档，然后转换成有效的XHTML（或者HTML）文档”。这种语言吸收了很多在电子邮件中已有的**纯文本标记**的特性。

Markdown的语法简洁明了、学习容易，而且功能比纯文本更强，因此深受博主们的欢迎。世界上最流行的博客平台WordPress和大型CMS如Joomla、Drupal都能很好的支持Markdown。完全采用Markdown编辑器的博客平台有Ghost和Typecho。

官网：https://www.markdownguide.org/

## Markdown基本语法

### 标题
在标题内容前输入特定数量的井号`#`来实现对应级别的HTML样式的标题。通常共有六级。

示例：
```
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题
```

效果：

![2](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181006/2.png)

### 引用区块
在需要引用的段落前加`>`。

示例：
```
>Ojhdt's Blog，一个游戏推荐，软件教程，资源共享，日常随笔交友的集合地。
```

效果：

>Ojhdt's Blog，一个游戏推荐，软件教程，资源共享，日常随笔交友的集合地。

#### 引用嵌套
在引用区块内部引用。添加`>>`，`>>>`……

示例：
```
>一级引用
>>二级引用
>>>三级引用
```

效果：

>一级引用
>>二级引用
>>>三级引用


### 列表

#### 有序列表
阿拉伯数字 后加 点，序号和内容间有空格。

示例：
```
1. 列表内容
2. 列表内容
3. 列表内容
```

效果：

1. 列表内容
2. 列表内容
3. 列表内容

#### 无序列表
在内容前插入 `-` `+` `*` 皆可。

示例：

```
- 列表内容
+ 列表内容
* 列表内容
```

效果：

- 列表内容
+ 列表内容
* 列表内容

#### 列表嵌套
上下两级之间敲三个空格。

示例：
```
- 一级列表内容
   - 二级列表内容
   - 二级列表内容
      - 三级列表内容
      - 三级列表内容
      - 三级列表内容
```

效果：

- 一级列表内容
   - 二级列表内容
   - 二级列表内容
      - 三级列表内容
      - 三级列表内容
      - 三级列表内容

### 字体

| 示例          | 效果               |
|:--            |:--                  |
| `***倾斜加粗***`     | ***倾斜加粗***            |
| `**加粗**``      | **加粗**                |
| `*倾斜*`       | *倾斜*                |
| `~~删除~~`        | ~~删除~~            |

### 分割线

连续键入三个短横 `---`

示例：

```
---
```

效果：

---

### 链接

#### 自动识别连接
无需任何操作。

效果：

https://ojhdt.club

#### 超链接
`[超链接名](超链接地址)`

示例：
```
[Google](https://www.google.com)
```

效果：

[Google](https://www.google.com)

### 图片
`![图片注释](图片地址)`

示例：

```
![Google](https://www.google.com/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png)
```

效果：

![Google](https://www.google.com/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png)


### 表格

![3](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181006/3.png)

第一行为表头，第二行分割表头和内容，第三行以下为内容。

`-` 表示文字居左。（默认居左）

`:-:`表示文字居中。

`-:`表示文字居右。

效果：

|表头|表头|表头|
|-|:-:|-:|
|内容|内容|内容|
|内容|内容|内容|

### 代码

#### 单行代码
将代码用 反引号 **'** **'** 括住。

示例：
```
`rm -rf`
```

效果：

`rm -rf`

### 代码块
代码两端各用三个反引号括起。（```）


示例：

![4](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20181006/4.png)

效果：

```
hexo clean
hexo generate
git add .
git commit -m 'hexo'
git push
hexo deploy --generate
```

## 其余常用 HTML 语法

### 折叠
折叠部分内容，点击后显示。折叠区内不可使用 Markdown 。

`<details><summary>标题</summary>`
内容
`</details>`

示例：
```
<details><summary>点击查看隐藏内容</summary>
隐藏内容

隐藏内容

隐藏内容
</details>
```

效果：

<details><summary>点击查看隐藏内容</summary>
隐藏内容

隐藏内容

隐藏内容
</details>

### 图片自定义大小
自定义插入图片显示大小。

示例：

```
<div>
<img src="https://www.google.com/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png" width="150" height="50" />
</div>

<div>
<img src="https://www.google.com/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png" width="210" height="70" />
</div>
```

效果：

<div>
<img src="https://www.google.com/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png" width="150" height="50" />
</div>

<div>
<img src="https://www.google.com/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png" width="210" height="70" />
</div>

若要居中显示，将`<div>`改为`<div align=center>`。

效果：

<div align=center>
<img src="https://www.google.com/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png" width="210" height="70" />
</div>

### 居中
使用`<div align=center>`和`</div>`括住内容。

示例：
```
<div align=center>
Ojhdt's Blog

游戏推荐，软件教程，资源共享，日常随笔交友的集合地。
</div>
```

效果：

<div align=center>
Ojhdt's Blog

游戏推荐，软件教程，资源共享，日常随笔交友的集合地。
</div>

## 写在后面
>感谢您的阅读！若您在阅读时发现教程存在疏漏或无法理解的地方，可以通过 **评论区留言** 进行交流讨论。

此文章为原创作品，禁止转载。如需转载请先经过许可，并在转载中注明原作者及出处。

请 `收藏` 本博客，本博客将持续更新。

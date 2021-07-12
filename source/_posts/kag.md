---
title: KAGeXpress：老罗教你做 GalGame
date: 2020-09-09 16:16:34
categories: "教程"
tags: []
cover: "https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200909/0.jpg"
toc: true
excerpt: KAG（Kirikiri Adventure Game）系统是以日本W.Dee为首的吉里吉里开发团队编写的电子小说类ADV（也称作AVG）游戏引擎。
---

### 简述

**KAG（Kirikiri Adventure Game）** 系统是以日本W.Dee为首的吉里吉里开发团队编写的电子小说类ADV（也称作AVG）游戏引擎。

KAG系统运行在功能强大，性能卓越的吉里吉里2脚本引擎平台上，主要部分使用吉里吉里2的脚本语言TJS写成。因而同时具有极高的效率和可扩展性、可定制性，两方面都远远超过国内使用广泛的NScripter和恋爱模拟Maker系列。

KAG系统最有名的使用案例是TYPE-MOON的《Fate/Stay Night》和《Fate/Hollow Ataraxia》。此外，包括akabeesoft2的《车轮之国，向日葵的少女》等许多商业和同人游戏也使用了KAG系统作为引擎。

KAG系统的功能完备，且编写方式、语法结构都较为清晰。但由于KAG系统直接提供的功能过于底层，给用户的理解和使用带来了一定的不便。因而，KCDDP利用KAG系统的宏封装功能开发了可以让新用户快速上手，简化并封装了基本功能的KAGeXpress系统，希望能给更多希望制作游戏的朋友们创造实现梦想的道路。

以上内容都摘自官方文档。鄙人最喜欢这种自带介绍的软件，用词专业，说明严谨，省得我再大费口舌瞎吹。简单来说就是一款功能完善的文字游戏制作引擎。虽然历史久远（世纪初的产物），但其占用小，命令简洁，开发工具齐备，即使放到现在也并不过时。


**新建工程**

首先下载软件本体  [KAGeXpress](https://netdisk.ojhdt.com/Project/KAG/KAGeXpress3-beta2.rar) 。解压软件包。

>软件包内已经包含 krkr2本体、工程模板和示例游戏工程，这意味着你已经下载了一个完整的 krkr2 游戏，你只需要双击 krkr.exe 启动器，再选择示例游戏目录 Sample 即可开始游玩。由其他制作者制作的krkr2游戏也允许以类似方式启动。krkr2 也有专门的游戏打包格式.xp3，仅需要将文件置于启动器同一目录。

双击 Wizard.exe 启动引导程序，选择分辨率（稍后还可以在配置文件中修改），输入你希望的工程名。

确定后，软件会以你输入的工程名，在该目录新建工程文件夹。并自动启动 KAGConfig ，可以对工程进行更详细的基本配置，包括游戏标题，游戏画面尺寸，字体，顶栏菜单等。配置结束后保存，关闭。如果后续需要进行修改，可以再次修改/Data/Config.tjs

![Wizard.exe](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200909/1.png)

![KAGConfig界面](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200909/2.png)

![KAGConfig界面](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200909/3.png)

![修改Config.tjs](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200909/4.png)

打开工程文件夹，这时它以经是一个最基础的可运行的krkr2游戏了。尝试运行 krkr.exe 会出现图示信息。

下面展示的是 Data 的目录结构

|文件/目录名|名称|作用|
|:-:|-|-|
|Config.tjs|KAG配置文件|修改该文件可以改变KAGeXpress系统的配置。|
|scenerio|脚本目录|存放用户编写的KAG剧本文件。|
|bgimage|背景图像目录|存放游戏中使用的背景图像、EventCG等。|
|fgimage|前景图像目录|存放游戏中使用的前景图像，例如立绘等内容。|
|image|其他图像目录|存放游戏中使用的其他图像的目录。系统界面、按钮、对话框等图片请放在这里。|
|bgm|背景音乐目录|存放游戏中使用的背景音乐。|
|sound|音效目录|存放游戏中使用的声音特效文件。|
|voice|语音目录|存放游戏中使用的角色配音文件。|
|rule|轨迹规则目录|存放按轨迹渐变（method=universal）时使用的规则图像文件。|
|video|视频文件目录|存放游戏中使用的MPEG-1、WMV以及SWF动画文件。|
|others|其他文件目录|存放工程中使用的其他文件。|
|system|系统目录|包含了KAGeXpress系统本身，一般情况请不要修改。|
|startup.tjs|KAGeXpress引导文件|引导吉里吉里内核执行KAGeXpress的程序脚本，一般情况不要修改。|

尽管目录分类相当细致，但游戏读取时并没有严格限定，也就是说该布局结构仅作推荐，不必硬性套用。例如一张背景图片，放置在bgimage,fgimage,image甚至bgm中都可正常调用。

### 案例教学

接下来就要进入具体的创作过程了。为了说明方便，我将会用具体案例说明krkr2的各项功能。

假如我想要还原著名的**老罗星巴克**。**[Bilibili](https://www.bilibili.com/video/BV1UZ4y1s7bV)**

首先需要准备好相应的素材：提取出背景，抠出人物立绘，录制bgm等。再将素材分门别类投入 Data 文件夹中供程序调用。注意妥善重命名素材。

用文本编辑器打开剧本 /Data/scenario/first.ks。整个游戏的制作都将围绕剧本展开。为了让各位能直接投入游戏制作,素材包和成品游戏都可以在这里下载到哦。（抠图调尺寸实在苦逼）

**[素材包](https://netdisk.ojhdt.com/Project/KAG/)** **[成品游戏](https://netdisk.ojhdt.com/Project/KAG/)** **[剧本.ks文件](https://netdisk.ojhdt.com/Project/KAG/ )**

---

#### 背景

对比一下我们的案例，发现第一个镜头是一家Starbucks。我们希望将背景切换到这家Starbucks。于是可以这样输入
```
@image layer=base storage=bg0
```
或者
```
@bg storage=bg0
```
该指令是插入背景的最简短命令。它的作用是读取 bg0 文件，并将它显示在 base 层上。

>但是，这张背景似乎太大了，很多内容都超出了游戏窗口。
>
>![问题显示](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200909/5.png)
>
>背景，就是衬在文字和前景后面显示的东西。KAG 中(默认设定)的是读入 640×480(或800x600) 大小的背景图片，这样可以正好填充整个游戏窗口。如果在 Config.tjs 更改过游戏窗口大小，素材也需要适应对应的大小设定。这里我们把素材缩小剪裁到800x600。
>![正常显示](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200909/6.png)

看回视频，场景已经从室外转移到了室内。就像刚刚所做的一样，再次使用`@bg`指令：
```
@bg storage=bg1
```
但这样会不会略显突兀？我们可以加点特效：
```
@bg storage=bg1 time=1000 method=universal rule=30
@wait time=500
```
rule 属性会引用 Data/rule 中的切换效果。自带的数十种特效已经基本满足需求。

![百叶窗切换](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200909/9.png)

---

#### 文字显示和文字层

在视频中，镜头还锁定在星巴克外景时，服务员就已经说出“您好”。接下来要在游戏中也还原这种效果。

简单地在剧本中直接添加文字：
```
*start
你好
```
文字会以默认形式输出：
![输出示例](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200909/7.png)

但这种效果不是我们想要的，我更希望得到像其他 Gal 里面的下半屏文本框。做法其实很简单，只需要使用预设的advl文字层
```
*start
@advl
你好
```
![输出示例](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200909/8.png)

KAG 一共有三个预设文字层，由下表列出：

|名称|调用命令|说明|
|:-:|:-:|-|
|全屏文字层|menul|覆盖全屏，背景完全透明的文字层。locate命令的定位将准确定位在屏幕的对应像素上。适合用于菜单、系统界面、字幕等场合。|
|电子小说文字层|val|覆盖屏幕大部分，有不透明效果的文字层。适合电子小说类游戏（例如Fate、Toheart）使用。|
|AVG文字层|advl|覆盖屏幕下半部分，有不透明效果的文字层。一般用于单句对话为主的场合，适合对话型AVG类游戏使用。|

如果**更改了游戏分辨率**（会导致预设文字层错位），或者对预设不满意，使用 @position 可以对文字层进行调整。假如我希望得到一个全透明的底部文字层（在800x600分辨率下，若指令显示不全请刷新页面）：
```
@position layer=message0 page=fore visible=true width=660 height=130 left=70 top=450 marginl=15 margint=15 marginb=15 marginr=15 opacity=0
```
这样 message0 层就变成我想要的对话框样式了。

该命令可用的**属性**：

|属性名|说明|
|:-:|-|
|layer|目标文字层（如message0）|
|page|指定表页或里页（fore或back）|
|left|画布在游戏窗口中的左起始位置|
|top|画布在游戏窗口中的顶部起始位置|
|width|画布宽（像素单位）|
|height|画布高|
|frame|搭载对话框图片（会自动抵消画布半透明底色效果）|
|color|画布底色（0xRRGGBB，默认是黑色）|
|opacity|画布底色的透明度（0~255，0为完全透明）|
|marginl|左留白（文字位置与实际画布的留白距离）|
|marginr|右留白|
|margint|上留白|
|marginb|底留白|

---
要切换正在使用的文字层，可以使用`@current指令`。`layer`属性用于指定层。
```
@current layer=message1
```
这一指令常用于在同一界面存在两处文本时使用。常见案例为显示角色名。接下来也会有相关介绍。

---
有时在用文字层展示完信息后（如WARNING，教程等），需要清除文字层内容。可以使用以下复位指令：

`@er` :清除当前文字层的内容

`@cm` :清除所有文字层的内容

`@ct` :复位文字层，消除所有文字层的内容，层位置返回message0

---

#### 文字行

为什么要先讲层再讲行？是为了刻意迎合视频内容。视频中老罗说了一句比较长的话：**您好 给我来一个中杯的拿铁**。

假如我想让游戏先显示**您好**，点击鼠标后再显示**给我来一个中杯的拿铁**，其实并不难：
```
@ct
您好[l][r]
给我来一个中杯的拿铁[p]
```
![显示效果](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200909/10.png)

针对文字层内的每行单行文本，软件也允许我们对其单独配置。先介绍三种尾缀

|命令|说明|
|:-:|-|
|[l]|显示行末标记（绿色向下小三角），等待鼠标点击|
|[r]|换行，相当于回车，通常结合[l]使用|
|[p]|显示翻页标记（蓝色向左小三角），等待鼠标点击，点击后翻页|

另外还有几条常用指令
`@nowait`：取消滚动动画，瞬间出现文字。
`@endnowait`：顾名思义，结束nowait状态。
`@font`：改变文字格式。支持的属性有：

|属性|说明|
|:-:|-|
|size|文字大小（像素单位）|
|face|字体（请明确填写）|
|color|字的颜色（0xRRGGBB）|

不同指令的灵活运用，可以让剧本变得更加有趣生动。

---

#### 角色名显示

在掌握上面的基础知识后，我们可以将一个文字层message1设定为角色名层，用于显示角色名，就像其他 Gal 所做的那样。（若指令显示不全请刷新页面）

```
@position layer=message1 page=fore visible=true color=0xEEAEEE opacity=140 left=30 top=400 width=130 height=30 marginl=20 marginr=20 margint=0 marginb=0  //设定message1层的格式
@current layer=message1  //使用current指令切换使用的文字层
@er  //清空该层
@nowait
老罗
@endnowait
@current layer=message0  //切换回原文字层
```
![效果展示](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200909/11.png)

值得注意的是，在使用该方法显示角色名后，请谨慎使用`@cm`，`@ct`指令，以免清除角色名。

---

#### 前景显示及切换

除了刚刚提到的背景层，文字层，KAG 还有前景层，用于显示立绘等其他图片。

|类型|名称|位置|作用|
|:-:|:-:|:-:|-|
|文字层|message0,message1...|最上层|显示剧本、菜单等以文字为主的内容。|
|前景层|0,1,2...|中间|显示人物立绘、小图片等图像内容。|
|背景层|base|最下层|显示场景、背景图像、事件CG等内容。|

>KAG最上层的是文字层，也就是显示文本信息的层。消息层的名称为message0、>message1...数字越高，就在越上面的位置。
>
>当前默认使用的消息层名为message。默认层可以用current命令指定。
>
>在消息层之下，是前景层。
>
>前景层的名称用数字表示，例如0、1、2...同样也是数字越高，就在越上面的位置。
>
>最后是背景层。背景只有一层，名称为base，在最下面的位置。
>![图层结构示意图](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200909/LayersDesc.jpg)

看回视频。仅靠背景和文字，我们已经还原出老罗出镜前的一系列对话。但在老罗与女服务员交锋的精彩桥段，背景已经无法准确交代过程。这里前景就派上用场了。


类似的，先切换到吧台背景。这里已经有了足够的对话铺垫，就不需要渐变切换了。
```
@bg storage=bg2
```
观察这个镜头，界面可以大致分为三层，分别是前面的三个杯子，中间的女服务员和后面的墙壁。我们可以把它分别放置在两个前景层和背景层上。
```
@fg layer=2 storage=b pos=c
@fg layer=1 storage=n1 pos=c
```
属性 `layer` 设定该图像所处的图层。`storage` 指定图像文件。`pos` 指定立绘所处的水平位置。 可以使用的位置有l，lc，c，lr，r五种，常用的是l（左），c（中），r（右）三种。

![剖析](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200909/12.png)

>一个前景层只能放置**一张**图像，放入新图像时旧的会被替换，不能同时显示。
>
>这里要注意各层的堆叠顺序。数字越大的图层越靠先。为了避免错误的遮挡，在本例中我将三个杯子放在了 2 层，而人物立绘放在 1 层。

要更换人物的表情或动作时，可以直接在同一层指定一张新的立绘（注意水平位置），就可以完成变化。
```
@fg layer=1 storage=n2 pos=c
```
如果我们不再需要这个立绘，可以用`@cl`命令清除。一般配合属性`layer`，也可配合`all`，`keep`排除。
```
[bg storage=ex01 time=1000]
[fg storage=fg01]
我是华丽的例子。[l][r]
@cl layer=0 ;清除前景层0
@cl all keep=back ;这条指令将会清除背景层以外的所有层
```

---

#### 宏

经过上面的教程，或许你的进度相当顺利，已经可以展示流畅的对话和灵活的切换。但还记得之前所做的角色名展示吗？每切换一次角色名，就至少要执行 5 条指令。因此，我强烈建议各位使用宏。

宏（MACRO）是将复数的命令行绑定在一起为一条新命令的功能。

在脚本中经常出现大量非常相似甚至是重复的段落，使用宏编集后可以使故事部分的编写输入大幅简化。例如在剧本刚开始时定义新命令 `@name`
```
@macro name=name
@current layer=message1
@er
@nowait
@emb exp="tf.npc = mp.name"
@endnowait
@current layer=message0
@endmacro
```
编集宏使用指令 `@macro` 和 `@endmacro`确定范围。属性值`name`可以指定宏的名字。编集好宏后直接使用`@name`可以大幅简化代码：
```
@name name=老罗
您好[l][r]
给我来一个中杯的拿铁[p]
@name name=女服务员
您要的是这个吗？[p]
```
五行代码就被简化成一行了！

在刚刚的宏`@name`中，我自定义了一个属性`name`。在进行宏的编集时，可以使用符号%标注尚未确定的留待以后使用时临时填写的内容，以百分号开头的部分即为这个宏中的属性。例：
```
@macro name=newtag
@font color=%rgb
这是彩色文字效果。
@resetfont
@endmacro
```
使用的时候书写：
```
@newtag rgb=0x00ff00
```
在这个例子中自定义了宏`newtag`，`rgb`是它的属性。属性rgb所对应的填写内容由定义时其对应的属性所决定，比如此处对应的是`@font`命令下的`color`属性，所以其内容格式应该为0xRRGGBB格式

---

#### 文字链接&标签

经过一番唇枪舌剑，老罗最终技不如人，败给了职业素养超群的星巴克女服务员。在这一段，我希望玩家亲身去感受老罗的无奈。我希望制作一个菜单，将选择的权利还给玩家。
因此，我不再使用原有的 `*start标签`，新建了 `*choose标签`，`*pa标签` 和 `*end标签`
```
*start
@image layer=base storage=bg0
@current layer=message0
您好[p]
……
……（省略N行剧本）
……
@bg storage=bg3
@fg layer=1 storage=l pos=c
这个才是中杯[p]
@wait time=500
……[l][r]
……[p]

*choose|选择

*pa|打

*end|结束
```
脚本中以星号开头的地方是标签，标签单独占一行，格式如下：

```
*标签名|显示名
```

标签名使用半角英文。竖线后的显示名可以使用中文，这个内容会在游戏存档位被显示出来。

标签分好了，我想要让玩家结束start章节后，跳转到choose章节。于是可以在start章节的最后一行加入：
```
@jump target=*choose
```
>如果希望到达的章节不在同一个剧本文件，该命令还可以用`storage`属性另外指定。如`@jump storage=second.ks target=*start`

令玩家做出选择，可以用**文字链接**或者**按钮**实现。二者的区别不大。先放出项目的示例：
```
*choose
@ct
@position layer=message1 visible=false
@fg layer=1 storage=l pos=c
@position layer=message0 page=fore left=30 top=30 width=740 height=540 color=0x000000 opacity=140 visible=true
@current layer=message0
@locate x=30 y=10
@font size=50 color=0xFFFFFF shadow=true shadowcolor=0x000000
@nowait
Choose|选择
@resetfont
@locate x=250 y=200
@font color=0xFFFFFF shadow=true shadowcolor=0x000000
老罗该怎么做？
@endnowait
@resetfont
@locate x=200 y=300
@link storage=first.ks target=*pa
打自己
@endlink
@locate x=400 y=300
@link storage=first.ks target=*end
不打了
@endlink
@s
```
别看这段代码体量大，实际上它只是构筑了一个基础菜单，里面含有两个**文字链接**（打自己/不打了）。点击后会跳转到对应的标签（`*/pa``/*end`) 

![菜单演示](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200909/13.png)

利用`@link`和`@endlink`可以将其之间的文字设置成链接。例如：
```
*start
@link storage=01.ks target=*sel01
选项1
@endlink[r]
@link target=*sel02
选项2@endlink[r]
@s

*sel01
这里是选项1。[l][r]

*sel02
这里是选项2。[l][r]
下面将跳转到选项1[l][r]
@jump target=*sel01
```
这段脚本是一个指向01.ks的*sel01的文字链接。在同一剧本下 storage 属性可省略。

另外这个脚本也可以写成：
```
[link storage=01.ks target=*sel01]第一章[endlink]
```
因为只需要一行这样写多个放在一起时会比较整齐。

`@link`的常用属性：

|属性名|说明|
|:-:|-|
|storage|目标所在的脚本文件名|
|target|目标标签|
|exp|tjs式（填入tjs式，比如关闭游戏窗口之类）|
|color|0xRRGGBB鼠标指上去时候高亮块的颜色|
|hint|鼠标指向时出现的说明文字|
|clickse|点击时效果音|
|enterse|指向时效果音|

---
请注意菜单中使用过的指令`@s`，该指令会暂停剧本进程来等待玩家选择。在制作菜单时十分必要。

---

#### 变量

终于也来到了视频的高潮。一直让老罗打脸似乎也很不够意思，我希望能像视频中一样，打四次脸之后就被路人劝阻。该如何计算打脸次数呢？我们可以引入一个**变量**来实现。

类似于编集宏，要在剧本开头就定义一个变量`f.pa`：
```
@eval exp="f.pa = 0"
```
这里我们定义一个名字为`f.pa`的游戏变量，值为0.

**注意**：exp后面的部分要使用半角双引号扩起。

>KAG中总共有三类的变量可以使用。
>
>以 f. 开头的变量，为游戏变量。该类变量将随着进度存档被保存。这类变量用于和游戏进度相关的数据。
>
>以 sf. 开头的是系统变量。该类变量将在系统存档中被自动保存，在正常且没有改动的情况下将一直保持。这类变量用于与系统设置及游戏全局变量相关的数据。
>
>以 tf. 开头的是全局变量。该类变量不会被保存，一旦程序退出就将丢失，用于临时使用的数据。
>
>一般情况下，不要随便在KAG剧本中使用不以这三种类型开头的变量。此外，建议变量名用半角英文开头，但如果有需要，也可以使用中文。

返回我们刚才的菜单，思路是 *start 执行结束后跳转到 *choose ，如果打脸次数不够则只能跳转到 *pa ，并添加次数。次数足够时再显示文字链接，跳转到 *end ，结束游戏。
```
*start
……
@jump target=*choose

*choose
@ct
@position layer=message1 visible=false
@fg layer=1 storage=l pos=c
@position layer=message0 page=fore left=30 top=30 width=740 height=540 color=0x000000 opacity=140 visible=true
@current layer=message0
@locate x=30 y=10
@font size=50 color=0xFFFFFF shadow=true shadowcolor=0x000000
@nowait
Choose|选择
@resetfont
@locate x=250 y=200
@font color=0xFFFFFF shadow=true shadowcolor=0x000000
老罗该怎么做？
@endnowait
@resetfont
@locate x=200 y=300
@link storage=first.ks target=*pa
打自己
@endlink
@if exp="f.pa > 3
@locate x=400 y=300
@link storage=first.ks target=*end
不打了
@endlink
@endif
@s

*pa
@eval exp="f.pa = f.pa + 1"
@position layer=message0 page=fore visible=true color=0x000000 opacity=150 left=30 top=430 width=740 height=150 marginl=30 marginr=30 margint=20 marginb=20
@name name=老罗
@fg layer=1 storage=l2 pos=c
@current layer=message0
啪！[l][r]
（老罗给自己来了很重的一下）[l][r]
（老罗已经打了 [emb exp="f.pa"] 次）[p]
@jump target=*choose

*end
……
```
观察 `*pa` ，第一行：
```
@eval exp="f.pa = f.pa + 1"
```
这里给变量 `f.pa` 加上 1。

往下几行
```
（老罗已经打了 [emb exp="f.pa"] 次）[p]
```
其中`[emb exp="f.pa"]`可以直接显示变量内容。

---
再观察 `*choose`，开头一大段都是在编纂菜单。在靠后部分引入了变量的比较和@if指令：
```
@if exp="f.pa > 3"
@locate x=400 y=300
@link storage=first.ks target=*end
不打了
@endlink
@endif
```
这里 exp="f.pa > 3 是一个判断式。判断式不计算两个数据的内容，它只产生两种结果“真”或者“假”。利用这个“真”还是“假”的结论，可使用if指令判断某一段内容是否被执行——如果exp的值是真，则执行从if到endif的脚本，如果exp的值是假则直接跳过这段内容。

变量的比较支持以下符号

|符号|说明|
|:-:|-|
|a==b|a等于b|
|a!=b|a不等于b|
|a<b|a小于b|
|a>b|a大于b|
|a>=b|a大于等于b|
|a=<b|a小于等于b|

---

#### 音效

bgm、se、vo这三个功能分别对应BGM、音效、语音的播放。

和标准的图形命令相似，要调用的文件名由storage属性指定，淡入淡出、交换音乐的时间由time属性指定。当time不指定的时候将立即开始播放。

```
@bgm storage=bgm01 time=1000 loop=false
```

这条命令将播放bgm01，淡入时间1000毫秒（1秒），不循环。


对于bgm，如果设置了wait属性，则系统将在继续执行底下的部分之前等待音乐淡入淡出的完成。而对于se，如果设置了wait属性，则系统将等待音效播放完成。
```
@se wait storage=se001
```
这条指令将播放se001，并等待其播放完成后才继续执行。

调节背景音乐的音量
```
@bgmopt volume=音量%（0~100，初始值100）
```
还可以对BGM播放进行配置：

|指令|说明|
|:-:|-|
|@stopbgm|停止播放背景音乐|
|@pausevidio|暂停背景音乐|
|@resumebgm|重开被暂停的背景音乐|

---
音乐淡入，用`@fadeinbgm`命令
```
@fadeinbgm storage=music.mp3 loop=true time=3000
```
音乐淡出，用`@fadeoutbgm`
```
@fadeoutbgm time=3000
```
 等待bgm淡入淡出完成再继续，用`@wb`。注意结合使用。
 ```
@wb
 ```

### 总结

经过上面的案例，KAG 的相关基本操作已经全部演示完毕。你可以使用所学的知识真正去制作自己的游戏了。

要查阅更详细的教程，可以查阅KAG3软件包内附带的文档 `\KAGeXpress\doc\index.html`

本人学习和编撰教程的过程中，受到了许多元老级教程的指导。感谢前人的付出！

>天娜的博客.[吉里吉里KAG入门](http://blog.sina.com.cn/s/blog_4a9980e70100fqv2.html)

如果喜欢这个教程，可以点击下方的打赏按钮，或者点点广告哦。

![星巴克の认可](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200909/14.png)
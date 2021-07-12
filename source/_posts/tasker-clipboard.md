---
title: Tasker实现通知剪贴板
date: 2018-08-21 15:04:05
categories: "教程"
tags: [Tasker,Notification]
cover: "https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20180821/0.jpg"
toc: true
excerpt: "Tasker 是一款适用于 Android 的系统增强型软件，它能让系统根据设置的”配置文件”(Profiles)，在特定的”背景”下(Contexts)，执行指定”任务”(Tasks)。<br>
借助Tasker及其插件Autonofication，可以实现Android原生系统无法实现的剪贴板功能。"
---
Tasker 是一款适用于 Android 的系统增强型软件，它能让系统根据设置的”配置文件”(Profiles)，在特定的”背景”下(Contexts)，执行指定”任务”(Tasks)。
我们可以通过使用Tasker及其插件Autonofication，实现Android原生系统无法实现的剪贴板功能。

## 效果展示

![效果展示](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20180821/1.png)

## 已实现功能
- 自动记录复制内容

- 通知栏显示

- 按钮操作

- 磁贴唤出

- 对于相同复制内容的识别


## 图文教程

### 下载并安装所需软件

* Tasker主程序

* AutoNotification插件

* Tasker配置

[百度盘](https://pan.baidu.com/wap/init?surl=c10ZYHa) 密码：2048

### 基本设置
进入Tasker，给予所有权限（Tasker本身不会通过滥用权限危害你的手机安全），加入黑域，绿色守护等后台限制程序的白名单。进入 `首选项>界面` ，反选 `初学者模式` 。

进入AutoNotification，点击 `Enable Notification Intercept`给予通知权限，点击 `Use AutoNotification in Tasker` 跳转Tasker主界面。

### 导入配置

长按Tasker主界面 `小房子` 按键；

<div align=center>
<img src="https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20180821/2.png" width="250" height="444" />
</div>

点击 `导入` 按钮；

<div align=center>
<img src="https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20180821/3.png" width="250" height="444" />
</div>

选择下载的 `通知剪贴板.prj.xml` 进行导入。导入后效果如图。

<div align=center>
<img src="https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20180821/4.png" width="250" height="444" />
</div>


### 启用磁块唤醒
>为确保稳定性，请使用Android 7(Nougat)或之后版本Android系统进行操作。

下拉通知栏，唤出磁块，点击 `小铅笔` 编辑；

添加一个 `Tasker磁贴`

进入 `首选项>操作>Quick Settings Tasks` ，点击 `放大镜` 图标，选择 `显示剪贴板` 任务。

点击设置好的磁贴，弹出通知剪贴板则安装成功。若无法弹出，请检查是否给予软件相关权限。

在Tasker主界面中运行一遍 `清空` 任务，进行启动初始化。

## 如何使用

剪贴板会自动后台记录您所复制的内容。需要打开剪贴板时，拉下磁贴面板，点击启动磁贴显示剪贴板。在弹出的面板中，点击 `上一项` 或 `下一项` 可以切换条目，点击 `复制` 可以复制该条目。使用完毕后，划掉剪贴板面板恢复后台运行。
如需清空剪贴板，运行 `清空` 任务。

## 已知问题
1. 最多支持五个储存位，如超出储存数量，旧数据将会被覆盖。
2. 切换存在延迟，视插件反应速度而定，但不影响使用。

## 写在后面
此文章为原创作品，禁止转载。如需转载请先经过许可，并在转载中注明原作者及出处。

请 `收藏` 本博客，本博客将持续更新。

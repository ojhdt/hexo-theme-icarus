---
title: "EFB-Parabox-Master 使用教程"
date: 2022-12-21 22:40:00
categories: "教程"
tags: [EFB, EPM, Parabox]
cover: "https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20221221/0.png"
toc: true
excerpt: "使用 EFB-Parabox-Master 和 Parabox-Extension-WS 将 Parabox 对接 EFB 的教程。"
---
[EH Forwarder Bot](https://github.com/ehForwarderBot/ehForwarderBot)（简称EFB）是一个可扩展的聊天平台隧道框架。经过一众开发者多年的辛勤耕耘，EFB已经构建起了成熟的从端生态。支持市面上大量主流即时通讯软件。

[Parabox](https://github.com/Parabox-App/Parabox) 是由本人开发的一个即时通讯客户端，目前仍在 Beta 阶段，详细说明可跳转 GitHub 查看（给个Star吧~）。它允许用户安装扩展来对接更多的即时通讯平台，并提供一致的操作体验。

既然单独对接各 IM 平台费力不讨好，何不直接对接 EFB ，既能快速完善 Parabox 功能，又能丰富 EFB 生态，结合两家优势？秉着不重复造轮子的精神，[efb-parabox-master](https://github.com/ojhdt/efb-parabox-master) 与 [parabox-extension-ws](https://github.com/Parabox-App/parabox-extension-ws) 横空出世，使这一切成为可能。本文将详细介绍如何使用 efb-parabox-master 与 parabox-extension-ws 来实现消息的对接。

在开发与测试以上项目过程中，本人受到了许多前辈与朋友的帮助（如 [milkice](https://github.com/milkice233)， [honus](https://github.com/0honus0)），特此感谢！

### 前置准备

- 搭载 Android 8.0 (Api 26) 及以上版本的移动设备
- 一台运行 Linux 的服务器（教程使用 CentOS 演示，但建议实际使用 Ubuntu）

### 安装 EFB 及从端

如果你已经在使用 EFB ，仅希望试用 Parabox ，可跳过此步骤。但请保证满足以下版本要求：
- EFB 2.1.1.dev1 及以上版本
- efb-qq-slave 2.0.2-dev 及以上版本
    - efb-qq-plugin-mirai 2.0.11-dev 及以上版本 
- efb-wechat-comwechat-slave Github最新版本

对于未列出的从端，由于未经过系统测试，可能出现不符合预期的行为。如果你在使用这些从端时遇到了问题，欢迎在文章底部留言，这将有助于我们迅速修复及改进。

#### 更新 Python 版本

如果你的服务器环境预装的 Python 版本过低，可遵循以下指引来更新至 3.6 及以上版本。
```bash
wget https://www.python.org/ftp/python/3.11.1/Python-3.11.1.tgz
tar -zxvf Python-3.11.1.tgz
cd Python-3.11.1
./configure --prefix=/usr/local/python3
make && make install
```
再创建软连接。为了不影响其他依赖 Python 2 的程序（如yum）。可以选择在 /usr/bin/python3 与 /usr/bin/pip3 两个位置创建软连接。
```bash
ln -s /usr/local/python3/bin/python3.11 /usr/bin/python3
ln -s /usr/local/python3/bin/pip3.11 /usr/bin/pip3
```
测试安装情况
```bash
python3 --version
pip3 -V
```

#### 安装 EFB 及从端

```bash
pip3 install ehforwarderbot
```
期间可能出现依赖缺失错误，使用pip自行安装。

从端安装方法各不相同，可参考各从端的官方文档。

### 安装并配置 EPM

更推荐从 GitHub 直接安装。项目仍处于快速开发阶段，新更新可能不会及时提交至 Pypi。

```
pip3 install -U git+https://github.com/ojhdt/efb-parabox-master.git
```

或

```
pip3 install efb-parabox-master
```

使用 EFB 配置向导 启用和配置 EPM，或在配置档案的 config.yaml 中手动启用。

根据您的个人配置档案，目录路径可能有所不同。

```
efb-wizard
```

根据提示输入 IP 及端口号（一般保持默认即可）。并记录下十位英文token。

配置完成后，尝试启动 EFB

```
ehforwarderbot
```
或
```
python3 -m ehforwarderbot
```

### Parabox 及扩展的配置

1. 前往 [Github Release](https://github.com/Parabox-App/parabox-extension-ws/releases) 下载最新版本的 parabox-extension-ws 扩展，并安装。

2. 在首页输入``服务器地址``及``连接密钥``。

3. 启用插件，直至显示`服务正常运行`。需保持插件后台运行（启用前台服务，关闭电池优化，使用后台锁等）。

4. 前往 [Google Play](https://play.google.com/store/apps/details?id=com.ojhdtapp.parabox) 或 [Github](https://github.com/Parabox-App/Parabox/releases) 下载安装 Parabox。若使用 Play 渠道，请先进入开放测试渠道，并更新至最新 beta 版本。

5. 进入 ``设置`` -> ``扩展``，点击 ``重置扩展连接``。ws 插件显示状态为 ``✓`` 即可。

6. 等待插件接收消息。

### 已知问题

以下为在测试中发现，并可能于后续版本修复的问题：

- 高频率发送 ``图片`` 将导致部分图片丢失。
- 发送过大的 ``图片`` / ``文件`` 时可能会失败。
- 偶发性的无故断连，可尝试使用 ws 扩展的 ``自动重连`` 功能临时解决。

如果在安装或运行期间出现问题，可以在评论区评论，或[加入 telegram 讨论群组](https://t.me/parabox_support)向我反馈。

如果认可我的作品，请前往 Github 为本项目点个 Star ，这将是对开发者莫大的支持！（谢谢各位啦）
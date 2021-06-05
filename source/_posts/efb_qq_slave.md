---
title: "Mirai端 EFB QQ Slave 安装记录"
date: 2020-09-23 21:30:14
categories: "小记"
tags: [EFB,EQS,Mirai]
thumbnail: "https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200923/0.png"
toc: true
excerpt: "EQS 功能和 QQ2TG 比较类似，但这种实现形式更为稳定，提供的功能也更多。"
---
先前已经对 EFB 和 [efb-qq-slave](https://github.com/milkice233/efb-qq-slave) 有过比较详细的[介绍](https://blog.ojhdt.com/20190606/efb/)。功能和 QQ2TG 比较类似，但这种实现形式更为稳定，提供的功能也更多。

efb-qq-slave 最近的更新添加了对 Mirai 的支持。文章接下来将对我的安装历程进行记录。

感谢开发者 奶冰 的默默付出！文章内容可能存在纰漏，请以[Github文档](https://github.com/milkice233/efb-qq-slave)或[开发者博客文章](https://milkice.me/2018/09/17/efb-how-to-send-and-receive-messages-from-qq-on-telegram/)为准。

#### EQS 安装

大体安装流程与 CoolQ 版本一致，篇幅仅留作不同点及重点配置介绍。在进行接下来的操作前，请先确保配置好 Telegram 端机器人，在VPS安装好以下软件依赖，并成功生成配置文件。具体指引可参照[前文](https://blog.ojhdt.com/20190606/efb/)。**CoolQ 安装及配置** 一节可略去。

- Python >= 3.6
- EH Forwarder Bot >= 2.0.0
- ffmpeg
- libmagic
- pillow

安装情况可以通过指令检查。如果操作正确，pip中会安装有`efb-qq-slave`，`efb-telegram-master`，`ehforwarderbot`，`Pillow`等。
```
yum list installed
pip3.6 list
```

检查并比对文件目录结构。此处项目文件夹被我放置在/root下
```
/root/.ehforwarderbot
├── modules
└── profiles
    └── default
        ├── blueset.telegram
        │   └── config.yaml
        ├── config.yaml
        └── milkice.qq
            └── config.yaml

5 directories, 3 files
```
接下来比对三处配置文件。

**/.ehforwarderbot/profiles/default/config.yaml**
```
master_channel: blueset.telegram
slave_channels:
- milkice.qq
```
---
**/.ehforwarderbot/profiles/default/blueset.telegram/config.yaml**

```
token: "123456789:jbd78sadvbdy63d37gda37bd8"
admins:
- 987654321
```

>`taken` 填写注册 Telegram Bot 时获得的一串由数字和字母组成的 Token。具体获得方法可参考[前文](https://blog.ojhdt.com/20190606/efb/#Telegram-%E4%B8%8A%E7%9A%84%E6%AD%A5%E9%AA%A4)。
>
>`admins` 填写你的 Telegram ID，可以向[机器人](https://t.me/get_id_bot)发送`/start`指令获得。
---

**/.ehforwarderbot/profiles/default/milkice.qq/config.yaml**

```
Client: CoolQ                       # 指定要使用的 QQ 客户端（此处为CoolQ，即使用的是Mirai）
CoolQ:
  type: HTTP                        # 指定 efb-qq-slave 与 酷Q 通信的方式 现阶段仅支持HTTP
  access_token: 6e95af8996a3a492b9eade171222a410  # 一串与cqhttp-mirai建立连接的访问口令。可随意填写，但和下文中的 Access Token 必须一致
  api_root: http://127.0.0.1:5700/  # 酷Q API接口地址/端口
  host: 127.0.0.1                   # efb-qq-slave 所监听的地址用于接收消息
  port: 8000                        # 同上
  is_pro: true                      # 若为酷Q Pro则为true，反之为false
  air_option:                       # 包含于 air_option 的配置选项仅当 is_pro 为 false 时才有效
    upload_to_smms: true            # 将来自 EFB主端(通常是Telegram) 的图片上传到 sm.ms 服务器并以链接的形式发送到 QQ 端
```
需要注意的是其实 port 下面的配置都是无效的，只是为了兼容酷Q，is_pro 请保持为 true


#### CQHttp-Mirai 安装

运行需要 JRE 1.8+ 环境。
```
yum install -y git java-1.8.0*
```
前往[releases](https://github.com/yyuueexxiinngg/cqhttp-mirai/releases)页面下载最新的Embedded分支版本插件。

用 FTP 工具连接 VPS，在合适的地方新建目录，并将.jar文件上传至该目录。本例中为`/home/cqhttp-mirai`。然后复制Jar包文件名。

![上传Jar](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200829/8.png)

进入目录并运行Jar包: 
```
cd /home/cqhttp-mirai
java -jar cqhttp-mirai-**-embedded-all.jar
```
根据提示，输入指令登陆QQ账户。期间可能需要完成验证：
```
login qq账号 qq密码
```
直到出现`login successes`提示。到这基本的服务就运行起来了。

按下CTRL+C结束服务。编辑 `plugins/setting.yml`，修改示例QQ号为自己的QQ号；更改accessToken且需**与 EQS 中的配置一致**。保存退出。
```
# Debug日志输出选项
debug: false
# 下载图片/语音时使用的Proxy, 配置后, 发送图片/语音时指定`proxy=1`以通过Proxy下载, 如[CQ:image,proxy=1,url=http://***]
# 支持HTTP及Sock两种Proxy, 设置举例 proxy: "http=http://127.0.0.1:8888", proxy : "sock=127.0.0.1:1088"
proxy: ""
# *要进行配置的QQ号 (Mirai支持多帐号登录, 故需要对每个帐号进行单独设置)
'1234567890':
  # 是否缓存所有收到的图片, 默认为否 (仅包含图片信息, 不包含图片本身,  < 0.5KB)
  cacheImage: false
  # 是否缓存所有收到的语音, 默认为否 (将下载完整语音进行保存)
  cacheRecord: false
  # 心跳包相关配置
  heartbeat:
    # 是否发送心跳包, 默认为否
    enable: false
    # 心跳包发送间隔, 默认为 15000毫秒
    interval: 15000
  # HTTP 相关配置
  http:
    # 可选，是否启用HTTP API服务器, 默认为不启用, 此项开始与否跟postUrl无关
    enable: true
    # 可选，HTTP API服务器监听地址, 默认为0.0.0.0
    host: 127.0.0.1
    # 可选，HTTP API服务器监听端口, 5700
    port: 5700
    # *可选，访问口令
    accessToken: 6e95af8996a3a492b9eade171222a410
    # 可选，事件及数据上报URL, 默认为空, 即不上报
    postUrl: "http://127.0.0.1:8000"
    # 可选，上报消息格式，string 为字符串格式，array 为数组格式, 默认为string
    postMessageFormat: array
    # 可选，上报数据签名密钥, 默认为空
    secret: ""
```
再次运行 CQHTTP Mirai 。登录时可以附加两个参数
- `--account 1234567890` 要自动登录的账号
- `--password *******` 要自动登录账号的密码

也就是这样：
```
java -jar cqhttp-mirai-**-embedded-all.jar  --account 123456789 --password *******
```
这样就可以在启动时自动登陆账号。

重新启动CQHttp-Mirai并保持服务运行。可尝试使用 Screen 保留后台。

#### 后续应用

至此服务安装完成。SSH工具开启一个新会话（保留CQHTTP Mirai运行）运行 `ehforwarderbot`, 等待插件载入完毕，大功告成！

![安装成功](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200923/1.png)

打开 Telegram ，搜索你之前创建的 Bot , 进入会话，输入 `/start` 即可开始消息互通！

以下是使用方法：

- 要向指定联系人发送消息，需要先发送 `/chat` 指令生成会话头，然后 Reply（回复）该会话头，再输入需要回复的消息。

- 要回复他人发送的消息，只需要 Reply（回复）该消息，再输入内容即可。

- 编辑消息并在该消息前段加上 `'rm` 字样即可在 QQ 端撤回该消息。同时请注意发出的消息仅能在发出后 2 分钟内撤回。

- 不希望每一次发送消息都进行回复操作？EFB 还支持分流指定消息到指定 Telegram 群组：

   - 在 Telegram 中新建一个空群组，并将你的 Bot 加入到这个群组中。（如果找不到 Bot ，尝试搜索 `@你的Bot用户名` ）
   - 回到 Bot 会话，发送 `/link`，选择一个会话，并点击 “Link”。在弹出的列表中选择刚刚创建的空群组即可。
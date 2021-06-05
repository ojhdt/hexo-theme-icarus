---
title: QQ2TG 配合 CQHTTP Mirai 实现消息转发
date: 2020-08-29 00:36:34
categories: "小记"
tags: [QQ,Telegram,QQ2TG]
thumbnail: "https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200829/0.png"
toc: true
excerpt: "本文主要记录本人在 CentOS 下架设环境，安装软件和启动服务的相关操作。"
---
**[QQ2TG For Mirai](https://github.com/hans362/QQ2TG-For-Mirai)** 是一个帮助 QQ 与 Telegram 互联的小程序。

![演示](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200829/1.png)

![聊天记录查询](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200829/2.png)

先前有一篇功能类似的文章[CentOS 下 通过 EH Forwarder Bot 转发 QQ 消息到 Telegram 的尝试](https://blog.ojhdt.com/20190606/efb/)，借助高扩展性的 [EFB 框架](https://github.com/blueset/ehForwarderBot) 和 [efb qq slave](https://github.com/milkice233/efb-qq-slave)，实现了 QQ-Telegram 上双向即时的消息转发。当时使用的 QQ 从端为 CoolQ，但由于已知原因该途径濒临失效。

在最近的一段时间里，一个开源的高效率机器人库 [mirai](https://github.com/mamoe/mirai) 进行了多次更新,功能相当强大，支持文字，图片，引用回复，撤回等大量操作。一众开发者迅速完成了对 mirai 的兼容。其中由 [Hans362](https://github.com/hans362) 基于 [小霖](https://github.com/isXiaoLin) 的 [QQ2TG](https://github.com/isXiaoLin/QQ2TG) 修改而成的 [**QQ2TG For Mirai**](https://github.com/hans362/QQ2TG-For-Mirai) 充分利用 mirai 提供的特性，在社交软件 Telegram 成功接收和处理 QQ 上的消息。

本文主要记录本人在 CentOS 下架设环境，安装软件和启动服务的相关操作。正式操作前请确保您的 VPS 可正常访问 Telegram，演示的服务器为 GCP 的香港服务器。**本文内容仅作为记录并提供引导，请以[开发者文档](https://github.com/hans362/QQ2TG-For-Mirai#%E4%BD%BF%E7%94%A8)提供安装方法为准。**

### 构建环境

使用 SSH 工具连接上服务器，首先安装 Git 与 Java
```
yum install -y git java-1.8.0*
```

QQ2TG 运行需要PHP环境，较为简单的方法是安装宝塔面板（若命令显示不全，请刷新该页面）。
```
yum install -y wget && wget -O install.sh http://download.bt.cn/install/install_6.0.sh && sh install.sh
```
耐心等待安装完毕，根据后台弹出的信息登入面板。首次登入面板会提示推荐安装套件。将 PHP 版本更改为 **7.2**，然后选择LNMP套件。

![宝塔面板登录信息](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200829/2-1.png)

![推荐安装套件](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200829/3.png)

安装完毕后，从侧边栏进入 **软件商店** ，进入 PHP-7.2 对应的设置项。

点击 **安装扩展** ，安装 `Swoole` 和 `Swoole4` 两个扩展。再点击 **禁用函数**，删除 `proc_open` 和 `putenv` 两个函数的禁用。

![安装PHP-7.2](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200829/4.png)

![安装拓展](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200829/5.png)

![删除函数禁用](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200829/6.png)

退出设置界面，点击侧边栏的 **数据库** 入口，点击 **添加数据库**，填写数据库名，用户名及密码，并记录下相关信息。最后点击提交，来新建一个 MySQL 数据库。

![添加数据库](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200829/7.png)

### 开放端口
访问你的服务器提供商控制台，进入防火墙配置，开放`5700`端口。

进入宝塔面板的 **安全** 选项，放行`5700`端口。

### Telegram 上的配置

Telegram Bot 是 Telegram 上极具特色的功能。它提供给用户一个便利的数据输出渠道。我们需要创建一个自己的 Bot 来输出聊天信息。

先向 Bot 设置向导 @BotFather 发起会话。https://t.me/BotFather

发送指令 `/newbot` 以启动向导。

设置名称（name）和用户名（username）。要注意用户名必须以bot结尾。此处以 `Ojhdt-QQ Bot` 和 `OjhdtBot` 为例。

你会获得一串由数字和字母组成的 Token。 请妥善保存这个密钥。为保护您的隐私及信息安全，请不要向任何人提供你的 Bot 用户名及密钥。

然后对 Bot 进行进一步配置。发送指令后根据提示选择按钮或键入内容发送即可。

允许将 Bot 添加进群组：`/setjoingroups` 选择刚创建的 Bot , 选择 Enable

允许 Bot 读取非指令信息：`/setprivacy` 选择刚创建的 Bot , 选择 Disable

设置指令列表: `/setcommands` ，然后编辑发送以下内容：
```
new_chat - 生成会话头
```

![使用BotFather新建机器人](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200829/12.png)

### 运行 CQHTTP Mirai
CQHTTP Mirai 是一款 Mirai 插件。需要配合 Mirai-console相关客户端 使用。但自0.2.0起添加临时Embedded分支版本, 与主分支单插件版并行。该分支版本内置了Core和Console，因此免除了配置Mirai-console的麻烦。

首先前往[releases](https://github.com/yyuueexxiinngg/cqhttp-mirai/releases)页面下载最新的Embedded分支版本插件。

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

按下CTRL+C结束服务。编辑 `plugins/setting.yml`,修改示例QQ号为自己的QQ号。保存退出。
```
# Debug日志输出选项
debug: false
# 要进行配置的QQ号 (Mirai支持多帐号登录, 故需要对每个帐号进行单独设置)
'1234567890':
  # HTTP 相关配置
  http:
    enable: true
    # 可选，HTTP API服务器监听地址, 默认为0.0.0.0
    host: 0.0.0.0
    # 可选，HTTP API服务器监听端口, 5700
    port: 5700
    accessToken: ""
    postUrl: ""
    postMessageFormat: string
    secret: ""
  ws_reverse:
    - enable: true
      postMessageFormat: string
      # 反向Websocket主机
      reverseHost: 127.0.0.1
      # 反向Websocket端口
      reversePort: 9501
      accessToken: ""
      reversePath: /
      useUniversal: true
      reconnectInterval: 3000
```
再次运行 CQHTTP Mirai 。登录时可以附加两个参数
- `--account 123456789` 要自动登录的账号
- `--password *******` 要自动登录账号的密码

也就是这样：
```
java -jar cqhttp-mirai-**-embedded-all.jar  --account 123456789 --password *******
```
这样就可以在启动时自动登陆账号。

如果配置成功，后台会每隔3秒提示一个Websocket连接出错的WARNING。这是正常现象，原因是QQ2TG服务还没有运行起来。

![WebSocket报错](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200829/9.png)

### 运行 QQ2TG

#### 配置

进入/home目录，clone `QQ2TG For Mirai` 项目：
```
cd /home
git clone https://github.com/hans362/QQ2TG-For-Mirai.git
```

进入/config，根据提示及示例填写完整`.env`，**不要改动**`.env.example`。以下是配置文件内容：
```
[bot]
message = {Telegram Bot API Key}
debug = {Telegram Bot API Key}

[websocket]
host = 0.0.0.0
port = 9501

[coolq]
http_url = https://{Mirai Console IP}:5700

[log]
level = 3

[admin]
chat_id = {Your Telegram ID}
send_to = {Your Telegram ID}

[group]
{QQ Group Number} = {Telegram Group Number}

[database]
host = {Database Host}
port = {Database Port}
username = {Database Username}
password = {Database Password}
database = {Database Name}

[blocked]
qq[] = 1234567890
qq[] = 2345678901
qq[] = 3456789012

[proxy]
host =
port =

[image]
proxy = http://qq_static_resource.illl.li
url = http://127.0.0.1/images/
folder = /../public/images

[program]
timeout = 15
restart_count = 100000
password = {Set Your Admin Password Here}
```
>- `[bot]`中的`{Telegram Bot API Key}`是指先前在Telegram注册机器人时获得的由数字和字母构成的Token。整段复制过来替换。
>- `[coolq]`中的`http_url`填写Mirai Console运行的服务器的IP。本例中就运行在本机，填写`http://127.0.0.1:5700` 
>- `[admin]`中的`{Your Telegram ID}`可以在向[机器人](https://t.me/get_id_bot)发送`/start`指令获得。
>- `[group]`项可以设置群消息转发。前半段填写QQ群组群号，后半段填写Telegram Group Number。获取方式在稍后部分解释。
>- `[database]`部分填写之前在宝塔面板中新建的MySQL数据库的信息。`port`填写默认端口`3306`。
>- `[blocked]`可以设置消息接收屏蔽。根据开发者的注释，该项留空会出现报错。若不需要该功能可随意填写。
>- `[proxy]`不需要可留空。
>- `[program]`中的`passward`为访问聊天记录查询功能的密码。自己记住就可以。

>**有关 Telegram Group Number 的获取**
>
>首先新建一个群组，只邀请机器人入群。
>
>访问页面查看机器人日志：https://api.telegram.org/bot<bot_token>/getUpdates ,其中`<bot_token>`替换为机器人的Taken。一个示例为 https://api.telegram.org/bot123456789:jbd78sadvbdy63d37gda37bd8/getUpdates
>
>在群组内发言，网页内会显示机器人所接收到的所有信息及其来源。在`"id"`中可以获得一串以`-`开头的数字。这就是群组id。Telegram ID也可以通过此方式获取。
>![查看群组ID](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200829/11.png)

给出一个填写示例。
```
[bot]
message = 123456789:jbd78sadvbdy63d37gda37bd8
debug = 123456789:jbd78sadvbdy63d37gda37bd8

[websocket]
host = 0.0.0.0
port = 9501

[coolq]
http_url = http://127.0.0.1:5700

[log]
level = 3

[admin]
chat_id = 123456789
send_to = 123456789

[group]
1111111111 = -222222222

[database]
host = 127.0.0.1
port = 3306
username = qq
password = 123456
database = qq

[blocked]
qq[] = 1234567890
qq[] = 0987654321
qq[] = 1425364758

[proxy]
host =
port =

[image]
proxy = http://qq_static_resource.illl.li
url = http://127.0.0.1/images/
folder = /../public/images

[program]
timeout = 15
restart_count = 100000
password = 123456
```
#### 运行

SSH 工具开启一个新会话（保留CQHTTP Mirai运行），连接服务器，进入目录
```
cd /home/QQ2TG
```
更新项目包。如果该步骤报错，请检查是否已删除函数禁用：
```
composer update
```
访问宝塔面板，新建一个网站。
>境外服务器的话，**域名**可以直接填写本机IP。有域名的也可以设置解析，但要同时部署好证书，为之后设置WebHook铺路。**根目录**要设定在QQ2TG项目根目录，在本例中也就是`/home/QQ2TG`。

站点添加完毕后，进入**站点修改->网站目录**，将**运行目录**设定为`/public`。再进入 **PHP版本** 确保PHP版本为 **7.2**。保存退出。

![设定运行目录](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200829/13.png)

![确认PHP版本](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200829/10.png)

访问一下`https://<Your_URL>/webhook.php`（`<Your_URL>`是刚刚新建网站时填写的域名）。正常情况的话该页面会显示**空白**。然后访问 `https://api.telegram.org/bot<bot_token>/setWebHook?url=https://<Your_URL>/webhook.php` 设置WebHook。 若认为不安全, 可自行改变文件名（注意：Telegram WebHook 需要 HTTPS 协议，请解析好域名并部署好证书）

以上步骤都完成后，配置进程守护程序。进入`/usr/lib/systemd/system`目录，新建`QQ2TG.service`文件。填入以下内容;
```
[Unit]
Description=QQ2TG
Documentation=https://github.com/XiaoLin0815/QQ2TG
After=network.target
[Service]
ExecStart=/path/to/your/php /path/to/QQ2TG/run.php
Restart=always
[Install]
WantedBy=multi-user.target
```
>注意此处要填写两处路径，一处为PHP安装路径，一处为QQ2TG中`run.php`所在路径。根据自身安装情况填入。本例中分别为`/usr/bin/php`和`/home/QQ2TG/run.php`

最后设置images读写权限
```
chmod -R 777 /home/QQ2TG/public/images
```
到这里一切都配置结束了，运行指令享受成果吧!
```
service QQ2TG start
```
### 效果
这一段直接引用原开发者的叙述。本文对机器人指令添加快捷补全。

- TG端发送消息:
- - 私聊机器人并发送 /new_chat
- - 选择要私聊的用户
- - 回复机器人发出的消息开始私聊
- Web 消息查看:
- - 在 `config/.env.example` 中设置好 program - password 权限密钥
- - 打开 `http(s)://<Your URL>/admin/message.html` 并将权限密钥填写完整
- - enjoy it

### 配置安全 (极为重要!)
- Nginx:
```
location ~ (^\.|/\.) {
    return 403;
}
```

- Apache:
```
RewriteEngine On
RewriteRule (^\.|/\.) - [F]
```

- IIS:
```
<configuration>
  <system.webServer>
    <rewrite>
      <rules>
        <rule name="Block access to dotfiles">
          <match url="(^\.|/\.)" ignoreCase="false" />
          <action type="CustomResponse" statusCode="403" statusReason="Forbidden" />
        </rule>
      </rules>
    </rewrite>
  </system.webServer>
</configuration>
```
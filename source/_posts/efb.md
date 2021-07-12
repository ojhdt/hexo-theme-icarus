---
title: CentOS 下 通过 EH Forwarder Bot 转发 QQ 消息到 Telegram 的尝试
date: 2019-06-06 18:51:22
categories: "小记"
tags: [EFB,Telegram]
cover: "https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190607/0.png"
toc: true
excerpt: "EH Forwarder Bot（简称 EFB）是一个可扩展的聊天平台隧道框架，基于 Python 3。"
---
[EH Forwarder Bot](https://github.com/blueset/ehForwarderBot)（简称 EFB）是一个可扩展的聊天平台隧道框架，允许用户同时连接多个即时通讯平台，如 微信，QQ，Facebook 等，远程收发管理消息。

![1](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190607/1.png)

原本使用 Rikka 开发的 `FFM - FCM for Mojo Web-QQ` ，对于 Android 的新特性适配的很好。无奈 Web QQ 关闭业务，只好通过 Telegram 转发来实现。


### 安装
>须知：本教程仅确保文章发表期间可行，随时间推移文章内容可能不再适用。
>
>部分资源引用自外部网站，将会在文章末尾处注明。如侵权请联系博主删除。

想要尝试这一番操作，必须先确保你拥有：

- SSH 工具（Putty，XShell 等）链接的墙外 VPS
- 一枚 Telegram 账号
- 可行的科学上网方式
- FTP 工具（FileZilla 等）
- 一定的英语基础

>想要一瞬安装？很幸运，大佬已经准备好了 Docker 镜像！[点我跳转](http://blog.ojhdt.com/20190606/efb/#Docker-%E5%BF%AB%E9%80%9F%E5%AE%89%E8%A3%85)

#### 构建运行环境

1. 安装 Python
```
yum install -y https://centos7.iuscommunity.org/ius-release.rpm
yum install -y https://repo.ius.io/ius-release-el7.rpm #如果源失效可换用此源
yum install -y python36u python36u-libs python36u-devel python36u-pip python36u-setuptools
```
2. 安装 ffmpeg
```
sudo rpm –import http://li.nux.ro/download/nux/RPM-GPG-KEY-nux.ro 
sudo rpm -Uvh http://li.nux.ro/download/nux/dextop/el7/x86_64/nux-dextop-release-0-5.el7.nux.noarch.rpm
sudo yum install ffmpeg -y
```

3. 安装 EH Forwarder Bot
```
pip3.6 install setuptools wheel
pip3.6 install ehforwarderbot
```

#### Telegram 上的步骤
Telegram Bot 是 Telegram 上极具特色的功能。它提供给用户一个便利的数据输出渠道。我们需要创建一个自己的 Bot 来输出聊天信息，

先向 Bot 设置向导 @BotFather 发起会话。https://t.me/BotFather

发送指令 `/newbot` 以启动向导。随后发送指令 `/newbot`

设置名称（name）和用户名（username）。要注意用户名必须以`bot`结尾。此处以 `Ojhdt-QQ Bot` 和 `OjhdtBot` 为例。

你会获得一串由数字和字母组成的 `token`。 请妥善保存这个密钥。为保护您的隐私及信息安全，请不要向任何人提供你的 Bot 用户名及密钥。

然后对 Bot 进行进一步配置。发送指令后根据提示选择按钮或键入内容发送即可。

- 允许将 Bot 添加进群组：/setjoingroups 选择刚创建的 Bot , 选择 Enable
- 允许 Bot 读取非指令信息：/setprivacy 选择刚创建的 Bot , 选择 Disable
- 设置指令列表：
    发送 `/setcommands` ，然后编辑发送以下内容

```
link - 将会话绑定到 Telegram 群组
chat - 生成会话头
recog - 回复语音消息以进行识别
extra - 获取更多功能
```

<div align=center>
<img src="https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190607/11.jpg" width="250" height="444" /> <img src="https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190607/13.jpg" width="250" height="444" /> <img src="https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190607/12.jpg" width="250" height="444" />
</div>

#### EFB 的配置

现在我们返回 VPS ，安装 ETM。
```
pip3.6 install efb-telegram-master
```
ehForwarderBot安装后不会生成配置文件，需要我们手动生成。
```
mkdir -p ~/.ehforwarderbot/profiles/default/
mkdir -p ~/.ehforwarderbot/profiles/default/blueset.telegram
mkdir -p ~/.ehforwarderbot/profiles/default/milkice.qq
```

通过你的 FTP 客户端访问服务器存储，进入`/root/.ehforwarderbot/profiles/default/`，创建名为 `config.yaml` 的文件，内容如下：
```
master_channel: blueset.telegram
slave_channels:
- milkice.qq
```

![5](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190607/5.png)

进入 /root/.ehforwarderbot/profiles/default/blueset.telegram/ ，创建名为 config.yaml 的文件，内容如下：
```
token: "上一步骤中获得的token"
admins:
- 123456789
```
>token 必须完整复制`“数字:字母”`格式。
>
>admins 项填写管理员 Telegram ID ，该 ID 可以通过 [Bot](https://t.me/get_id_bot) 发送 `/start` 获取。只有在管理员账户列表中的 Telegram 用户才可以以你的名义发送消息到 QQ 。

#### CoolQ 安装及配置
使用 docker 安装 酷Q 是比较方便的一种操作。
1. 安装 docker
```
yum install docker -y
```
2. 重启 docker
```
service docker restart
```

3. 运行下列命令，安装由 Richard Chien 魔改的 由酷Q官方提供的 docker 镜像。
```
docker pull richardchien/cqhttp:latest
mkdir coolq  # 包含CoolQ程序文件
docker run -ti --rm --name cqhttp-test --net="host" \
     -v $(pwd)/coolq:/home/user/coolq     `# mount coolq folder` \
     -p 9000:9000                         `# 网页noVNC端口` \
     -p 5700:5700                         `# 酷Q对外提供的API接口的端口` \
     -e VNC_PASSWD=MAX8char               `# 请修改 VNC 密码！！！！` \
     -e COOLQ_PORT=5700                   `# 酷Q对外提供的API接口的端口` \
     -e COOLQ_ACCOUNT=123456              `# 在此输入要登录的QQ号，虽然可选但是建议填入` \
     -e CQHTTP_POST_URL=http://127.0.0.1:8000   `# efb-qq-slave监听的端口/地址 用于接受传入的消息` \
     -e CQHTTP_SERVE_DATA_FILES=yes       `# 允许以HTTP方式访问酷Q数据文件` \
     -e CQHTTP_ACCESS_TOKEN=ac0f790e1fb74ebcaf45da77a6f9de47  `# Access Token` \
     -e CQHTTP_POST_MESSAGE_FORMAT=array  `# 回传消息时使用数组（必选）` \
     richardchien/cqhttp:latest
```

下图为一个启动成功的实例：
![6](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190607/6.png)

>**注意：**
>
>建议先将以上内容复制到记事本中按照注释修改，再转到控制台执行。`VNC_PASSWD`一项为稍后进行酷Q后台登陆的密码，长度不可超过 `8` 位。其余内容一般不必修改。

如果出现错误提示
```
Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?.
```
请尝试执行步骤 2 重启 docker 。

4. 在浏览器内访问 `http://<ip或者域名>:9000`，输入刚刚设定的 VNC 密码登陆,然后在 酷Q 内登陆 QQ 账号。

![2](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190607/2.png)

![3](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190607/3.png)


#### 运行及后续

1. 安装 EQS
```
pip3.6 install efb-qq-slave
```

2. 修改 `milkice.qq` 配置文件
FTP 访问服务器存储，进入 `root/.ehforwarderbot/profiles/default/milkice.qq/`，修改 `config.yaml` 。
```
   Client: CoolQ                         # 指定要使用的 QQ 客户端（此处为CoolQ）
   CoolQ:
       type: HTTP                        # 指定 efb-qq-slave 与 酷Q 通信的方式 现阶段仅支持HTTP
       access_token: ac0f790e1fb74ebcaf45da77a6f9de47
       api_root: http://127.0.0.1:5700/  # 酷Q API接口地址/端口
       host: 127.0.0.1                   # efb-qq-slave 所监听的地址用于接收消息
       port: 8000                        # 同上
       is_pro: true                      # 若为酷Q Pro则为true，反之为false
       air_option:                       # 包含于 air_option 的配置选项仅当 is_pro 为 false 时才有效
           upload_to_smms: true          # 将来自 EFB主端(通常是Telegram) 的图片上传到 sm.ms 服务器并以链接的形式发送到 QQ 端
```

3. 启动服务
使用指令
```
ehforwarderbot
```
服务启动完成，enjoy it!

![4](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20190607/4.png)

4. 打开 Telegram ，搜索你之前创建的 Bot , 进入会话，输入 `/start` 即可开始消息互通！

以下是使用方法：

- 要向指定联系人发送消息，需要先发送 `/chat` 指令生成会话头，然后 Reply（回复）该会话头，再输入需要回复的消息。

- 要回复他人发送的消息，只需要 Reply（回复）该消息，再输入内容即可。

- 不希望每一次发送消息都进行回复操作？EFB 还支持分流指定消息到指定 Telegram 群组：

   - 在 Telegram 中新建一个空群组，并将你的 Bot 加入到这个群组中。（如果找不到 Bot ，尝试搜索 `@你的Bot用户名` ）
   - 回到 Bot 会话，发送 `/link`，选择一个会话，并点击 “Link”。在弹出的列表中选择刚刚创建的空群组即可。

### *Docker 快速安装
> 以下内容来自 Rat's Blog 的文章 [使用EH Forwarder Bot实现Telegram同时收发多个微信/QQ消息](https://www.moerats.com/archives/931/)

有了镜像就可以直接无视上面的繁琐操作了。只需要完成以下几个步骤。

#### 安装 Docker 及 docker-compose
```
curl -sSL https://get.docker.com/ | sh
systemctl start docker
systemctl enable docker
```

```
curl -L https://github.com/docker/compose/releases/download/1.23.2/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
```

#### 拉取源码
```
git clone https://github.com/Earth-Online/efb-qq-coolq-docker.git
cd efb-qq-coolq-docker
```

>如果没有安装 git ，请执行 `yum install git -y`

#### 编辑配置

使用 FTP 工具修改 `root/efb-qq-coolq-docker/ehforward_config/profiles/default/blueset.telegram` 下的 `config.yaml` ，内容与手动安装时一致。

```
token: "你的TG机器人Token"
admins:
- 你的Userid
```

回退到目录 `root/efb-qq-coolq-docker/` ，编辑 `docker-compose.yml` 文件：

```
- VNC_PASSWD=VNC密码
- COOLQ_ACCOUNT=你的qq账号
```

#### 后台启动
使用指令一瞬启动：
```
docker-compose up -d
```
至此安装已经完成，访问 `ip:9801` 登陆酷Q就可以开始使用啦。

### 已知问题

- 无法从 Telegram 发送图片到 QQ 。该功能可通过购买 酷Q Pro 实现。
>**注意**：根据 [Milkice's IceBox](https://milkice.me/2018/09/17/efb-how-to-send-and-receive-messages-from-qq-on-telegram/) 的提示，若要使用 酷Q Pro，请在进行**手动安装**时，在 docker run 中添加额外参数 (-e COOLQ_URL = "http://dlsec.cqp.me/cqp-tuling") ，以便docker下载CoolQ Pro而不是Air。另外，在修改 `milkice.qq` 从端配置文件时，也要将 `is_pro` 修改为 `true`。

- 无法接收/发送语音信息。
- 无法处理 好友请求处理，加群请求处理 等消息类型

### 参考文章
[1]Milkice's IceBox.[安装并使用 EFB：在 Telegram 收发 QQ 消息](https://milkice.me/2018/09/17/efb-how-to-send-and-receive-messages-from-qq-on-telegram/)

[2]Rat's Blog.[使用EH Forwarder Bot实现Telegram同时收发多个微信/QQ消息](https://www.moerats.com/archives/931/)

### 写在后面
此文章为原创作品，禁止转载。如需转载请先经过许可，并在转载中注明原作者及出处。

请 `收藏` 本博客，本博客将持续更新。


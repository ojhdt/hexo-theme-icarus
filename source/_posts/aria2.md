---
title: 用 Aria2 感受飞一般的下载速度
date: 2020-03-14 23:23:14
categories: "教程"
tags: [Aria2,Download]
thumbnail: "https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200315/0.png"
toc: true
excerpt: "Aria2 是一个轻量级的多协议多源命令行下载程序。它支持 HTTP/HTTPS，FTP，SFTP，BitTorrent 和 Metalink。 aria2可以通过内置的JSON-RPC和XML-RPC接口进行操作。"
---
>忍受够了某雷的广告与臃肿？
>
>本地下载被压榨到10kb/s？
>
>想要看电影，却苦等于数小时的下载，乃至兴致全失？

Aria2 就是解决这一切问题的利器。不俗的下载速度，轻巧的程序本体，多种格式的完美兼容，多平台支持；配合上文件目录列表程序 h5ai ，你甚至能做到云端离线下载，回家畅爽看片的极致体验。

**Aria2** 是什么？

[Aria2](https://aria2.github.io/)是一个轻量级的多协议多源命令行下载程序。它支持 HTTP/HTTPS，FTP，SFTP，BitTorrent 和 Metalink。 aria2可以通过内置的JSON-RPC和XML-RPC接口进行操作。

你并不需要明白这一切到底是什么。你只需要了解这是一款能帮你解除下载速度的限制，节省你宝贵时间的下载利器。以下是详细的食用方法。

### 准备
要安装aria2，你需要准备：
- 一台有大量流量的闲置服务器
- 服务器管理运维面板（推荐[宝塔](https://www.bt.cn/download/linux.html)面板）
- FTP上传及SSH连接环境

### 安装
为了简化安装流程，**强烈推荐**使用逗比大佬的一键脚本。直接登录到服务器后台执行
```
wget -N --no-check-certificate https://softs.fun/Bash/aria2.sh && chmod +x aria2.sh && bash aria2.sh

```
如果上面这个脚本无法下载，尝试使用备用下载：
```
wget -N --no-check-certificate https://raw.githubusercontent.com/ToyoDAdoubi/doubi/master/aria2.sh && chmod +x aria2.sh && bash aria2.sh
```
脚本菜单长这样

![脚本界面](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200315/1.png)

运行脚本后在菜单中输入选项 `1`，等待安装结束，记录下 RPC 地址 与 RPC 密钥 。

如果需要停止/重启服务，或是配置aria2，可以进入到脚本的储存目录使用指令
```
./aria2.sh
```
按照菜单提示进行相关操作。为了避免后续操作麻烦，一般情况下不建议再对配置信息进行修改啦（特别是端口）。

如果不愿使用脚本，也可以使用[文档](https://aria2.github.io/manual/en/html/)提供的正统安装方法。此处不再提供。

### AriaNG 前端控制
ariaNG是一款aria2的Web管理面板，功能已经相当完善，支持基本的任务添加/删除/排序，提供完整的Aria2设置，采用完全响应式布局，多平台支持。

本质上只是一个Web UI，所以其实可以**略过这一步**，而直接使用别人搭建好的面板来对自己服务器上的Aria2进行管理。但生命的乐趣在于折腾嘛~自己的服务器也能提供更好的连接速度。

主界面长这样。这里借用一下官网的展示图片

![移动端](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200315/mobile.png)

![PC端](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200315/desktop.png)
#### 安装与连接
下载 [AriaNG](https://github.com/mayswind/AriaNg/releases) 程序包，在本地解压。

在宝塔面板上新建一个网页，再将程序包内的文件上传至网页根目录。如果设置了防火墙，要在宝塔及服务器开放`6800`端口。

打开网页，应该就正常进入到AriaNG的管理页面了。

在侧边栏点击 `AriaNg 设置`，再在顶栏找到`RPC`，填入之前记录的RPC 地址 与 RPC 密钥 。等待 Aria2 状态 显示为 `已连接`。

![填写RPC连接信息](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200315/3.png)

至此就大功告成啦！点击新建，填入磁力链接/下载直链，体验飞一般的速度！！下载后的文件将会储存在你的服务器中。如果需要下载到本地的话可以再用FTP传输回本地。
#### 启用HTTPS
ariaNg自带https连接方式但默认关闭，需要手动编辑AriaNG的配置文件。申请证书有很多渠道。由于我的域名是在腾讯云购买的，习惯使用腾讯云提供的免费TrustAsia证书，申请审核很快，并且可以无限续期。此处默认你已经获得了crt证书文件和key证书文件。

上传证书文件到服务器或其他可以引用的位置。

![证书上传](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200315/4.png)

编辑Aria2配置文件`/root/.aria2/aria2.conf`

![配置文件所在目录](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200315/5.png)

编辑下面几项

```
# 是否启用 RPC 服务的 SSL/TLS 加密,
# 启用加密后 RPC 服务需要使用 https 或者 wss 协议连接
rpc-secure=true
# 在 RPC 服务中启用 SSL/TLS 加密时的证书文件(.pem/.crt)
rpc-certificate=/root/aria2.crt
# 在 RPC 服务中启用 SSL/TLS 加密时的私钥文件(.key)
rpc-private-key=/root/aria2.key
```
将`rpc-secure`一项修改为`true`，并在`rpc-certificate`和`rpc-private-key`分别填入crt和key证书文件所在路径。

访问宝塔面板，修改AriaNG所在的站点，进入SSL设置项。将`crt`证书内容复制到右框，将`key`证书内容复制到左框。

![宝塔安装证书](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200315/7.png)

再次访问网页，重新填入RPC信息。证书就安装完毕了。

![证书](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20200315/8.png)

>本教程的部分内容参考自[Rat's Blog](https://www.moerats.com/)，感谢大佬的分享！[撒花]
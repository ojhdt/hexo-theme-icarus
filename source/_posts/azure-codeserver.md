---
title: "试用 Azure 虚拟机 & 搭建 CodeServer 云端 VS-Code"
date: 2020-12-03 10:30:11
categories: "小记"
tags: [VPS,VSCode]
thumbnail: "https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20201203/0.png"
toc: true
excerpt: "使用 Azure 家的 Linux 服务器搭建云端 VSCode —— Code Server"
---
Azure 是微软自家的云服务平台。和 Google Cloud, AWS 类似，Azure 也为新用户提供了一定时长的服务器试用。Azure 的免费试用套餐包括首月 $200 额度，限时**1个月**的热门服务试用（含Windows和Linux虚拟机）和**升级即用即付**后获得的剩余11个月热门免费试用，也就是1年的试用期。（对某家率先修改试用时长至三个月表示不满）。提供免费试用的B1s机子配置固定为 1vcpu, 1GiB内存，带一块64G的SSD。

![免费使用套餐内容](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20201203/1.png)

当然，要开始免费试用，需要准备一张双币信用卡，且卡内至少保有供冻结的余额**1美元**。国内办的也是可以的。

下面，我将展示我用 Azure 家的 Linux 服务器搭建云端VSCode—— [**Code Server**](https://github.com/cdr/code-server)。通过 Code Server，用户可以从任何设备通过浏览器访问 VSCode。

### 开通免费帐户

访问注册链接 https://azure.microsoft.com/en-us/free/

验证手机和信用卡信息。一切都需要如实填写，信用卡验证期间需要冻结一美元，否则信用卡会处于未验证状态而锁定`免费试用`订阅。此处并没有需要特别注意的地方，不再赘述。

![电话号码验证](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20201203/2.png)

![支付信息验证](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20201203/3.png)

账户创建成功后自动获得 $200 免费额度，附赠一个`免费试用`订阅。该免费额度可在注册后的30天内用于大多数 Azure 服务，但任何未使用的额度都无法结转到后续月份。`免费试用`订阅中包含一系列热门服务可供选用，具体服务内容和剩余用量可以从[Azure Portal控制台](https://portal.azure.com/)中查看（主页 > 成本管理+计费 > 免费试用）。即使用量全部耗尽，Azure 也会优先从赠送的 $200 免费额度中扣除费用。

![获得免费额度](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20201203/13.png)

![查询剩余用量](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20201203/12.png)

要使用这些免费服务，可以从控制台访问[免费服务](https://portal.azure.com/#blade/Microsoft_Azure_Billing/FreeServicesBlade)页面，选择需要的服务创建资源。

![可供选择的免费服务](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20201203/11.png)

在账户未升级前，免费试用订阅和免费额度有效期均为 30 天。 30 天内或 $200 信用额度即将耗尽时，须删除支出限制升级到即用即付订阅。升级后就可继续使用剩余 11 个月的免费级订阅服务，但超出额度的资源仍需额外收费。

![免费额度有效期](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20201203/14.png)

需要更多消息，可以访问[微软支持页面](https://azure.microsoft.com/zh-cn/offers/ms-azr-0044p/)。

### 创建资源

登录[Azure Portal控制台](https://portal.azure.com/)，在搜索栏中搜索`免费服务`，开通一台 Linux 虚拟机。

输入虚拟机名称，选择区域（离你越近的区域响应速度越快）和系统映像（本例演示系统为 CentOS）。其他选项一般不必修改。点击`查看+创建`。创建完成后，Azure 会提供SSH连接使用的公钥，且**只供下载一次**。将公钥下载到本地。创建结束后可以在`虚拟机`页面查看服务器信息。

![创建虚拟机](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20201203/4.png)

![创建虚拟机](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20201203/5.png)

![正在创建](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20201203/6.png)

打开 SSH 工具（本例中使用Xshell），新建一个会话。主机填入虚拟机的公网ip。身份验证方法选择`Public Key`，用户名为`azureuser`（此处与虚拟机创建时的设置值匹配），用户密钥选择下载得到的.pem文件，密码为空。

![Xshell上的公钥连接方式](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20201203/7.png)

这样我们就成功连接上刚创建的虚拟机了。Ftp登录方式与此类似。

![登陆成功](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20201203/8.png)

>**换用root账户登录**
>
>Azure 默认禁用 Root 登录，使用公钥登录的是名为azureuser的账户。若要重新开启，仅需修改`sshd_config`文件。
>
>```
sudo su
vim /etc/ssh/sshd_config
>```
>将 `#PermitRootLogin yes` 前面的 `#` 注释删除。然后重启ssh服务
>```
service sshd restart
>```
>为 Root 账户重设密码，下次SSH连接时就可以使用用户名+密码登录了。
>```
passwd root
>```



### 运行 Code-Server

#### 通过宝塔面板安装

使用宝塔面板搭建可以简单快捷地搭建Web环境，添加域名，SSL 证书，反向代理。

首先安装宝塔面板，并安装LNMP套件。[安装方法](https://www.bt.cn/)不再赘述。

将域名解析到服务器ip，在宝塔面板新建一个网站，填入域名。由于Code Server 要求 HTTPS 访问，域名需要添加证书，宝塔申请的免费证书或是其他云平台（如腾讯云）申请的证书都是可以的。添加后勾选强制HTTPS访问。

切换到 shell 工具，下载 code-server 二进制版本到网站根目录。当然[手动下载文件](https://github.com/cdr/code-server/releases/download/v3.5.0/code-server-3.5.0-linux-x86_64.tar.gz)后再用FTP工具上传也是可以的。
```
sudo su
cd /www/wwwroot/[网站根目录]
wget https://github.com/cdr/code-server/releases/download/v3.5.0/code-server-3.5.0-linux-x86_64.tar.gz
```
解压文件，更名后进入目录
```
tar -zxvf code-server-3.5.0-linux-x86_64.tar.gz
mv code-server-3.5.0-linux-x86_64 code-server
cd code-server
```
运行 Code Server
```
export PASSWORD="password" && ./code-server --port 8000 --host 0.0.0.0
```
>此处附带了两个启动参数。`PASSWORD`设置登录code-server的密码。`--port`设置监听端口。 `--host`设置监听ip。

这时虽然服务已经运行，但还无法通过域名访问。我们再次访问宝塔面板，进入`站点修改`，更改网站运行目录为子目录 code-server 。然后进入`反向代理`，目标URL填写`127.0.0.1:[监听端口]`。

这样就可以在浏览器输入`[域名]:[端口]`访问 code-server 了。

![更改运行目录](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20201203/15.png)
![创建反向代理](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20201203/16.png)
![code-server 登陆界面](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20201203/10.png)

如果需要更改端口，访问密码等信息，可以修改`~/.config/code-server/config.yaml`。

#### 原生安装方式

切换到 Root 账户，安装 screen 来保持后台及开机自启。
```
sudo su
yum install screen
```
接下来就是故技重施了，下载并解压 code-server 二进制版本
```
cd /home
wget https://github.com/cdr/code-server/releases/download/v3.5.0/code-server-3.5.0-linux-x86_64.tar.gz
tar -zxvf code-server-3.5.0-linux-x86_64.tar.gz
```
更改目录名并进入目录
```
mv code-server-3.5.0-linux-x86_64 code-server
cd code-server
```
新建一个 screen 会话，启动 code-server
```
screen -S code-server
export PASSWORD="password" && ./code-server --port 8000 --host 0.0.0.0
```

相应地前往[Azure Portal控制台](https://portal.azure.com/)，在[网络安全组](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Network%2FNetworkSecurityGroups)页面放行对应端口。

![放行端口](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20201203/9.png)

这样就可以在浏览器输入`[公网IP]:[端口]`访问 code-server 了。

要关闭 code-server 也很简单，移除该 screen 会话即可。
```
screen -list
screen -S [会话代号] -X quit
```

### 后续
>2021/3/3更新

请注意！与国内服务商廉价的流量费用不同，虽然 Azure 免费订阅中已经包含有一定量的出站流量，但额度只有 **15GB**。而超出后的资费可是相当吃不起的。

懵懂无知的我先前尝试用这台“白嫖”来的服务器搭建 Aria2 用于离线下载。微软大厂果然实力不凡，下载速度动辄达到了 43 MB/s，也许受限于资源，这还不是满速。

![Aria2下载](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20201203/17.png)

由于 Azure 后台的统计数据存在延迟，我还没有意识到问题的严重性。第二天一看，醒目的 bandwidth 与 virtual network 计费让我傻了眼。待付金额已经达到 $2 。我及时止损关闭了服务器。

![超额](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20201203/18.png)

![超额](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20201203/19.png)
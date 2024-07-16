## memos 简介
memos 是一项开源、免费且隐私优先的笔记服务，提供 Docker 一键安装，支持纯文本和 Markdown，并提供自定义共享和 RESTful API 集成功能。memos 的使命是通过简单、轻量、安全的方式，帮助用户记录和分享他们的想法。

## Serv00.com 简介
Serv00.com 是一家提供免费虚拟主机服务的平台，使用 FreeBSD 的系统，提供 512MB 内存、3G 磁盘和最大 20 个进程，对于我们搭建一个 memos 服务配置已足够。

本文将使用 Serv00 提供的虚拟主机，通过本地方式搭建 memos 服务，并使用浏览器插件和电报机器人的方式集成 memo 服务，方便我们的日常使用。

前提条件：

- 一个自定义域名
- 一台 Serv00.com 账号
- 一个 Cloudflare 账号
- 一张双币信用卡，用于开通 Cloudflare Zero Trust 的免费计划
- 域名托管到 Cloudflare

## Serv00 配置
首先，将 Run your own applications 设置为 Enabled。
![image](https://github.com/user-attachments/assets/0daa3f41-6029-4749-9dfe-e05067a305e1)

> 若不开启，则用户目录下的所有文件都无法添加可执行权限。

然后，申请开放端口 5230 和 5231。

![image](https://github.com/user-attachments/assets/41e861a5-9e6f-4011-89d9-194e1a4e8cf5)

5230 为 memos 默认端口，5231 为 memos 的 gRPC 端口（监听端口+1）

接着，添加一个新站点，如下图示例：
![image](https://github.com/user-attachments/assets/9e61c371-5240-409d-b0da-30924b8ad228)

> 站点类型选择为 Proxy，并选择 5230 服务端口。

## memos 部署
```
# 切换至目标目录
$ cd /home/harrisonwang/domains/memos.harrisonwang.serv00.net/public_html

# 创建用于存放 SQLite 的数据文件目录
$ mkdir data

# 配置下载地址环境变量
$ API_URL="https://api.github.com/repos/k0baya/memos-binary/releases/latest"
DOWNLOAD_URL=$(curl -s $API_URL | jq -r ".assets[] | select(.name == \"memos-freebsd-amd64.tar.gz\") | .browser_download_url")

# 下载 FreeBSD 版的 memos
$ curl -L $DOWNLOAD_URL -o memos-freebsd-amd64.tar.gz

# 解压安装并添加可执行权限
$ tar -xzvf memos-freebsd-amd64.tar.gz && rm memos-freebsd-amd64.tar.gz && chmod +x memos

# 运行 memos
$ ./memos --mode prod -p 5230 --data /home/harrisonwang/domains/memos.harrisonwang.serv00.net/public_html/data
```
## Cloudflare Tunnel 安装及配置

首先，在 Zero Trust 控制台创建 memos 隧道：
![image](https://github.com/user-attachments/assets/382cb5f2-ddb7-46e0-9276-9d86f6762b04)

然后，配置好 Public Hostname Page：
![image](https://github.com/user-attachments/assets/d02514ba-e3c2-43ae-8458-aa4995f15664)

接着，拷贝 ARGO_TOKEN 并记录好：

![image](https://github.com/user-attachments/assets/723a0d27-154f-4942-975f-d46f51b9dd58)

最后，我们登录 Serv00 服务器安装 cloudflared，登录信息可到注册邮箱中查看：
![image](https://github.com/user-attachments/assets/4aeef3f1-158c-46e3-8149-9d75edf6a0de)


依次执行以下命令进行安装和测试：
```
# 创建 cloudflared 目录
$ mkdir -p ~/domains/cloudflared && cd ~/domains/cloudflared

# 下载 cloudflared
$ wget https://cloudflared.bowring.uk/binaries/cloudflared-freebsd-latest.7z && 7z x cloudflared-freebsd-latest.7z && rm cloudflared-freebsd-latest.7z && mv -f ./temp/* ./cloudflared && rm -rf temp

# 测试运行 cloudflared
$ ./cloudflared tunnel --edge-ip-version auto --protocol http2 --heartbeat-interval 10s run --token <ARGO_TOKEN>
```

## 访问 memos 站点
![image](https://github.com/user-attachments/assets/e337398e-efc8-4ca6-8d24-cf2c6308a3eb)

我们登录后创建一个 Token，提供 chrome 浏览器扩展程序使用。
![image](https://github.com/user-attachments/assets/24df472d-1fcf-4311-a23e-736ce0f07e7a)


## 安装 memos 的 chrome 浏览器扩展程序
谷歌应用商店搜索 memos 扩展程序：
![image](https://github.com/user-attachments/assets/0632f624-fc17-467b-8ae4-225aa350c686)

然后，配置对应的域名和 Token：
![image](https://github.com/user-attachments/assets/7cc9edae-12c9-409d-b8d2-f8a57ba9e0fd)


> 注意：域名必须包含 / 结束符，如：https://memos.xiaowangye.org/

配置完成后，我们可以很方便的使用浏览器插件发布 memos 了：
![image](https://github.com/user-attachments/assets/74fc80de-609f-4145-bc20-dcf684f993dc)


集成到 Telegram
memos 官方提供了支持，参阅官方文档配置即可。

## 参考文档
小王爷：https://xiaowangye.org/posts/build-memos-service-using-serv00.com/
Saika’s Blog: [Serv00搭建各种服务](https://blog.rappit.site/2024/01/27/serv00_logs)
Linux DO: [【serv00系列教程】汇总帖](https://linux.do/t/topic/43121)
memos: [Bind Memos user to Telegram user](https://www.usememos.com/docs/integration/telegram-bot)
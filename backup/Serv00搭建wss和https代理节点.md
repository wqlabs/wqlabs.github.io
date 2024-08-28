Serv00 注册开通后，本文就以新版本的 wstunnel 为例，快速搭建一个 https 代理节点，建立 web tunnel。整体来看，web tunnel （wstunnel 新版本支持客户端请求协议为 https，基于 http2 实现）是完全合规的常规流量，没有任何“特征”，是不会被屏蔽的。相比来看，现有针对 serv00 上的 vless、ss2022 等搭建方式都是照搬古老的容器化节点部署方式，把简单的事情复杂化，不仅低效率、自定义非标准化、易于检测，而且提高了部署、应用门槛。理论上，不需要编辑、创建网络接口的代理程序都可以在 serv00 上直接运行，没有任何必要使用低效的 js 脚本和作茧自缚的花式“协议”。

## **服务端**

我们需要添加一个服务端口，这里以 18443 为例，左侧导航栏点击『Port reservation』，选择『Add port』选项卡，输入 18443 即可。端口类型『Port type』确保为默认的 tcp，描述『Description』可留空，也可以指定一个便于记忆、区分的关键词。最后点击『+Add』按钮放行 18443 端口，如果系统提示该端口已被其他人使用，可以换其他未被使用的端口，wstunnel 等程序对监听端口没有任何要求。

![image](https://github.com/user-attachments/assets/2712ef68-ee51-43c7-95a9-f860b9536576)


端口放行之后，就可以使用以下命令下载、解压 freebsd 版本的 wstunnel 并启动。进阶注意，这里将 wstunnel 放置于 ~/repo 之下，是为了便于区分。如果需要进行分流和反向代理，务必将其放置于对应的站点目录下。

cd ~/repo
wget https://github.com/erebe/wstunnel/releases/download/v9.7.2/wstunnel\_9.7.2\_freebsd\_amd64.tar.gz
tar zxvf wstunnel\_9.7.2-rc1\_freebsd\_amd64.tar.gz
rm -f wstunnel\_9.7.2-rc1\_freebsd\_amd64.tar.gz
chmod +x wstunnel

使用如下命令启动wstunnel服务端，须将端口号改为实际放行的端口。

./wstunnel server wss://0.0.0.0:18443
#请将端口号18443替换为实际放行的端口

![image](https://github.com/user-attachments/assets/e2b97bad-af3e-43fa-927f-7373e4a5093b)


## **客户端**

以 windows 为例，下载客户端，版本不必和服务端一致，如仅使用 wss 协议不低于 7.0 即可，如使用 http2 协议应确保客户端版本不低于 9.0。解压后，直接参照以下命令运行、启动 wstunnel 客户端。

.\\wstunnel client -L socks5://127.0.0.1:1080 https://xxx.xxx.xxx.xxx:18443
#请将xxx.xxx.xxx.xxx:18443修改为实际的IP地址和wstunnel server监听端口号

![image](https://github.com/user-attachments/assets/a3020bf5-160b-424a-8a25-8f47b222115a)


一旦 wstunnel 启动运行，就可以打开浏览器，将代理指向 wstunnel client 使用的监听协议和端口，这里协议是 socks5、端口是 1080，就可以访问互联网了。你会注意到，serv00 目前还并没有走出波兰。

![image](https://github.com/user-attachments/assets/5453a4cf-219f-43ab-8048-ff531b8a7d75)


wstunnel 也可以配置级联代理，当然，熟悉 gost 的也可以使用 gost 进行级联，但其 tun/tap 等特性不再可用、无需尝试。有级联代理，完全可以抛弃 cloudflare tunnel 国内极其难用的隧道部署方案。如果对 wireguard 情有独钟，可以尝试一下 wireproxy 这个不需要 root 权限的项目。

## **客户端后台运行与其他**

**1.后台运行**

我们在服务端，通过 nohup 或 screen 可以很方便地让 wstunnel 在后台运行。Windows 下当然需要更为优雅地使用，开个 cmd 窗口十分不便。windows 中后台运行的方式包括两种方式：

一是使用 windows 自带的 sc 或第三方 winsw 应用将 wstunnel 添加为系统服务，可参考之前的博文「[不使用额外工具配置本地翻墙代理客户端](https://appscross.com/blog/no-additional-tools-are-used-to-configure-the-local-bypass-proxy-client.html)」和「[Windows下的sc工具应用](https://appscross.com/blog/sc-tool-application-under-windows.html)」。

第二种方式则相对轻巧一点，使用bat、ps1（powershell）脚本后台运行 wstunnel，也可参考之前的博文。如果确实不想动手，可按照如下步骤操作（**所有有效内容为引号内部分，务必去掉引号**）：

**i）** 关注公号『**智能生活引擎**』发送关键词 “wstunnel” 获取单独脚本（或包含 wstunnel和脚本）的压缩包下载后，解压至 wstunnel 文件夹内，按照下图使用文本编辑器编辑、修改 proxy.ps1 文件并保存

![image](https://github.com/user-attachments/assets/9ce89343-594d-4cbb-975f-483df49e8d91)


**ii）** 在 proxy.bat 文件上点击右键，将 proxy.bat 发送到桌面快捷方式

![image](https://github.com/user-attachments/assets/43c2dcef-d34a-4411-bb5e-6400da55cccb)


**iii）**回到桌面，将该快捷方式改名为 “wstunnel”，然后剪切

**iv）**打开资源管理器，输入"C:\\ProgramData\\Microsoft\\Windows\\Start Menu\\Programs\\"打开开始菜单路径，将剪切的快捷方式粘贴至此

**v）**这样就可以在开始菜单中找到“wstunnel”，也可以将其进一步『固定到“开始”屏幕』和/或『固定到任务栏』，可以右键点击 wstunnel 快捷方式，选额『属性』，在『属性』对话框中修改、选择 wstunnel 快捷方式的图标

![image](https://github.com/user-attachments/assets/531608b6-192d-49d8-8ed3-ddc257f6816e)


**2.稳定性与速度**

仅个人使用的情况下，通过这种方式在 serv00 上搭建的节点是稳定的，当然会受到 serv00 服务器重启等操作的影响，对于日常的 google 搜索、社交媒体常规访问的场景是可以胜任的。但是，如果多人分享的话，一方面 serv00 服务器处于波兰、抖动不小，多人体验会很差，而且不排除 serv00 删号处理的可能。

速度上，实测 youtube 仅可流畅观看 1080p 视频，也即峰值带宽 10000 kbps 左右，更高分辨率的带宽要求 servoo 是无法满足的。


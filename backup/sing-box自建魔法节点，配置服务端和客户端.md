

> sing-box 是什么？它一个新的通用跨平台代理软件客户端，类似 v2rayN、Clash for Windows 等，但拥有更多新特性，并且目前少有同时支持 iOS 和 Apple TV 并且免费的代理应用，支持 Shadowsocks、Vmess、Trojan、Hysteria 2 等协议。

## 关于 sing-box
sing-box 是免费跨平台代理软件（The universal proxy platform），客户端支持 Windows、Mac、Android、iOS 和 Apple TV 等平台上使用。

sing-box 官网：


https://sing-box.sagernet.org

sing-box Github 项目地址：

https://github.com/SagerNet/sing-box


sing-box 由于支持新的 Reality 和 hysteria2 协议，目前多为自建节点的科学上网爱好者所用，订阅格式和 Clash、Surge 等软件也不兼容，需使用专属订阅格式。

目前仅又少数机场原生提供 sing-box 订阅链接支持，比如 GLaDOS、[狗狗加速](https://panel.dg6.top/#/register?code=9ddB5bK3)等。

## 自建节点

需要一台可以魔法上网的云服务器，比如香港的云主机或者境外的各种云主机.
[官方网站](https://sing-box.sagernet.org/)对各种服务器环境提供了多种的安装部署方式，有仓库安装，手动安装，docker方式。

以我自己为例，我的服务器是centOS，使用了以下命令进行安装服务端

```
sudo yum install -y yum-utils
sudo yum-config-manager --add-repo https://sing-box.app/sing-box.repo
sudo yum install sing-box # or sing-box-beta
```
配置文件默认在 /etc/sing-box 

![image](https://github.com/wqlabs/wqlabs.github.io/assets/39255755/7e11f6d8-6510-46af-be20-750e70f3c005)

使用以下配置文件替换原有的文件内容

```
{
    "inbounds": [
        {
            "type": "shadowsocks",
            "listen": "::",
            "listen_port": 8080,
            "network": "tcp",
            "method": "2022-blake3-chacha20-poly1305",
            "password": "password",
            "multiplex": {
                "enabled": true
            }
        }
    ]
}
```
在命令行中使用命令生成一个随机密码

```
openssl rand -base64 32
```
![image](https://github.com/wqlabs/wqlabs.github.io/assets/39255755/a2ca03c9-a656-4859-82f0-13befaf7eb03)


用以替换上面配置文件中的password，使用 systemctl start sing-box.service 启动服务

使用命令 systemctl status sing-box.service 

查看当前服务启动状态，如果出现running 则表面服务启动成功
![image](https://github.com/wqlabs/wqlabs.github.io/assets/39255755/defd8a11-54ca-4976-ae42-7ab8a84a6ea6)


至此服务端就搭建成功。

## 客户端

鉴于sing-box 支持客户端包括 Windows、Mac、Android、iOS 和 Apple TV 我只用我的手机ios进行安装测试

首先需要在appstore搜索sing-box（需要美区appid）可以免费下载安装，比小火箭或者其他vpn收费安装，简直良心大大的。

在手机中打开sing-box，找到Profiles配置文件选项，创建一个新的配置文件，type选择local，可以导入，也可以直接创建，用以下的配置进行替换即可

```
{
    "dns": {
      "servers": [
        {
          "tag": "google",
          "address": "tls://8.8.8.8"
        },
        {
          "tag": "local",
          "address": "223.5.5.5",
          "detour": "direct"
        }
      ],
      "rules": [
        {
          "outbound": "direct",
          "server": "local"
        },
        {
          "outbound": "proxy",
          "server": "google"
        }
      ],
      "strategy": "ipv4_only"
    },
    "inbounds": [
      {
        "type": "tun",
        "inet4_address": "172.19.0.1/30",
        "auto_route": true,
        "stack":"mixed",
        "sniff": true
      }
    ],
    "outbounds": [
      {
        "type": "shadowsocks",
        "tag": "proxy",
        "server": "ip_addr",
        "server_port": 8080,
        "method" :"2022-blake3-chacha20-poly1305",
        "password": "password",
        "multiplex": {
          "enabled": true
        }
      },
      {
        "type": "block",
        "tag": "block"
      },
      {
        "type": "dns",
        "tag": "dns-out"
      },
      {
        "type": "direct",
        "tag": "direct"
      }
    ],
    "route": {
      "rules": [
        {
          "protocol": "dns",
          "outbound": "dns-out"
        },
        {
          "geosite": "cn",
          "outbound": "direct"
        },
        {
          "geoip": "cn",
          "outbound": "direct"
        }
      ],
      "auto_detect_interface": true,
      "final": "proxy"
    }
  }
```
需要注意的是，该配置文件有两处配置需要修改以下，一个是ip_addr 改成服务端ip地址，password改成与上面服务端的password一致就可。

![image](https://github.com/wqlabs/wqlabs.github.io/assets/39255755/702668fe-b5c7-4813-b501-7ad6242214eb)


最后回到Dashboard页面，选择刚才的配置，Enable选中就开启了。
![image](https://github.com/wqlabs/wqlabs.github.io/assets/39255755/18c5c50d-83e9-4891-97de-7a4c70226e31)


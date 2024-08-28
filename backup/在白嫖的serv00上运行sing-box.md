之前就想尝试在`serv00`上跑`sing-box`，一直没时间弄，今天试了下，还真给搞成了。  
一键脚本开源在G站了，顺便来分享下。

省流：

`mkdir -p ./sing-box && cd ./sing-box bash <(curl -sSL https://raw.githubusercontent.com/RayWangQvQ/sing-box-installer/main/install-serv00.sh)`

![image](https://github.com/user-attachments/assets/8ad36f87-83bd-4297-adec-b095fbf118d3)

![image](https://github.com/user-attachments/assets/dbd40bb1-cf88-4f58-b390-c534c26bf6d9)


## [](#p-1040014-h-1)教程

需要先从serv00里收集如下信息：

### [](#p-1040014-ip-2)IP

![image](https://github.com/user-attachments/assets/6abd973c-fe01-4dc7-af38-14d456e1bb62)


![image](https://github.com/user-attachments/assets/cc0a7807-f0b5-4c9a-8d48-e10e54ad8625)


任选一个，记住IP。

### [](#p-1040014-h-3)端口

![image](https://github.com/user-attachments/assets/d611d3b9-99f0-4058-8700-58736b725ca5)


记下端口，没有就创建一个。

### [](#p-1040014-ssh-4)ssh执行一键脚本

登录ssh，执行上面的一键脚本，期间会自动安装`sing-box`，然后让填IP和端口。

成功后，会生成一个vmess订阅。

## [](#p-1040014-h-5)其他

当前实现方式是用`sing-box`的`FreeBSD`二进制包来绕过包管理器，直接把`sing-box`装到用户目录里了。

`sing-box`支持的协议很多，我试了下`hysteria`和`reality`，但是没成功，提示打包时没有选择包含`quic`和`reality`的tag，不知道是啥原因让`sing-box`打`FreeBSD`包时排除了这两个tag。  
有感兴趣的兄弟可以去尝试下，自己基于`sing-box`源码来build一个带`quic`和`reality`的包试试看，如果能成，那可玩性就又高出一个层级了。

另外，毕竟免费资源，速度一般，辣鸡电信晚高峰速度如下：

![image](https://github.com/user-attachments/assets/03e460b1-7e94-4d46-8ebf-a83df999136b)


用CF拉了一下，快了一丢丢，7万左右，看4k还是没问题的：  

![image](https://github.com/user-attachments/assets/4de544b5-b191-4028-9682-f5f9ce461b23)


配置CDN也简单，在CF里设置下端口转发就行了，就不赘述了。

脚本开源的：[GitHub - RayWangQvQ/sing-box-installer: 基于docker一键安装sing-box服务端，并自动生成vmess、naiveproxy、hysteria2节点 105](https://github.com/RayWangQvQ/sing-box-installer) ，如果发现有可以优化的地方，欢迎大佬们来贡献PR~
参考文章：
https://linux.do/t/topic/134828
https://www.nodeloc.com/d/6279

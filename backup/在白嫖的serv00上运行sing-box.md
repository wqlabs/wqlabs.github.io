今天折腾吃灰serv00
之前就想尝试在serv00上跑sing-box，一直没时间弄，今天试了下，还真给搞成了。
一键脚本开源在G站了，来分享下，顺便混点能量~

省流：
```
mkdir -p ./sing-box && cd ./sing-box
bash <(curl -sSL https://raw.githubusercontent.com/RayWangQvQ/sing-box-installer/main/install-serv00.sh)
```
![image](https://github.com/user-attachments/assets/619df31c-c46e-4dfe-9fae-b07a9360fee8)
![image](https://github.com/user-attachments/assets/dbe69e33-52c0-4d58-95db-3e84d14b7765)

## 1. 教程
需要先从serv00里收集如下信息：

### 1.1. IP
![image](https://github.com/user-attachments/assets/f814a285-b323-447a-af40-5a7d873820e2)
![image](https://github.com/user-attachments/assets/bb2289c0-6738-4794-945b-bfb17f7dc835)

任选一个，记住IP。 

### 1.2. 端口
![image](https://github.com/user-attachments/assets/092148e6-def2-43ab-a065-2c39b6416c1e)

记下端口，没有就创建一个。

### 1.3. ssh执行一键脚本
登录ssh，执行上面的一键脚本，期间会自动安装sing-box，然后让填IP和端口。

成功后，会生成一个vmess订阅。

## 2. 其他
### 2.1. 实现方式
当前实现方式是用sing-box的FreeBSD二进制包来绕过包管理器，直接把sing-box装到用户目录里了。

### 2.2. 关于协议（hysteria和reality）
sing-box支持的协议很多，我试了下hysteria和reality，但是没成功，提示打包时没有选择包含quic和reality的tag，不知道是啥原因让sing-box打FreeBSD包时排除了这两个tag。
有感兴趣的兄弟可以去尝试下，自己基于sing-box源码来build一个带quic和reality的包试试看，如果能成，那可玩性就又高出一个层级了。

### 2.3. 关于速度
毕竟免费资源，速度一般，辣鸡电信晚高峰速度如下：：
![image](https://github.com/user-attachments/assets/0d2c12f4-f308-4329-8f28-84b393df4b0c)

用CF拉了一下，快了一丢丢，7万左右，看4k还是没问题的：
![image](https://github.com/user-attachments/assets/14af807d-ccb3-45c9-8efb-ec089d2499fd)


配置CDN也简单，在CF里设置下端口转发就行了，就不赘述了。

脚本开源的，如果发现有可以优化的地方，欢迎大佬们来贡献PR~

更新：
reality搞定了，果然跟FreeBDS没关系，是sing-box官方build没有带这些tag，自己build一个就行了。
那hysteria应该也是没问题的。


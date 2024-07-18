零.延迟
低情商:卡 高情商:犹如国际级服务器hypixel般的体验 勉强能玩吧
![image](https://github.com/user-attachments/assets/0e7f5ddf-6bcf-45e2-ae41-12013c71a46e)


网站倒是还算流畅的
![image](https://github.com/user-attachments/assets/81fd3381-b5aa-4af5-9e73-255d26c0b3c6)
## 一.前戏
### 1.设置端口
面板左侧 Port reservation→+Add port (如图)

![image](https://github.com/user-attachments/assets/6df7e222-0983-442e-b4e2-e3cc8dd06e24)

一共可以创建三个,这里记作端口A B C,后面会用到

### 2.打开允许自己的软件
Additional services 选项卡中找到 Run your own applications 项目，将其设置为 Enabled 即可。如果不开启这一项，自己的用户目录下的所有文件都无法添加可执行权限。
**如果你是在ssh之后才设置的这个选项,记得要重新ssh链接一遍,不然依然无法添加权限** 

### 3.安装pm2
在 SSH 连接 serv00 之后，直接使用一键脚本安装 pm2+全局调用
```
bash <(curl -s https://raw.githubusercontent.com/k0baya/alist_repl/main/serv00/install-pm2.sh) && source ~/.bashrc
```
目前有bug,每次重新ssh不会自动读取.bashrc,所以每次ssh链接都要重新
```
source ~./bashrc
```
当然你也可以路径调用
```
~/.npm-global/bin/pm2
```
## 二.好戏开场了
### 1.安装frp
建议手动下载frp_版本号_freebsd_amd64.tar.gz后进去panel左侧的File manager后上传,使用wget可能会更新不及时
```
wget https://github.com/fatedier/frp/releases/download/v0.56.0/frp_0.56.0_freebsd_amd64.tar.gz #截止2024/3/30版本为0.56.0
```
解压并重命名并赋予权限
```
tar -zxvf frp_0.56.0_freebsd_amd64.tar.gz && mv frp_0.56.0_freebsd_amd64 frp && chmod 777 frp
```
接着在你的本地客户机上下载对应系统版本安装包解压备用

2.编辑服务端配置文件
这边依然建议在本地写好后上传(才不是因为我不会使用freebsd里的在线编辑呢)
新建一个文本文档,把下面写入后保存为frps.toml
```
bindPort = A
vhostHTTPPort = B #如果你不需要http(s)穿透可以只写上面那行
auth.token = "123456" #可选 链接密钥,为string类型,建议加上以防别人链接
```
然后上传至serv00的那个frp文件夹中(记得先把原来的frps.toml删掉)
just like this

![image](https://github.com/user-attachments/assets/1345af59-5d49-458a-9fd1-bfd09af44b33)

### 3.编辑客户端配置文件
这次要改名为frpc.toml
```
serverAddr = "114.514.1919.810" #这串端口下面再细说
serverPort = A
auth.token = "123456" #你刚才在frps.toml中设置的密钥

#tcp/udp穿透实例
[[proxies]] #这里理论上可以改,但是改了就连接失败,建议别动
name = "abcde" #这里可以随便写
type = "tcp" #或者改成udp
localIP = "127.0.0.1" #本地地址
localPort = 25565 #本地要穿出去的端口
remotePort = C #如果你要udp,开放C端口时记得选择udp

#http(s)实例
[[proxies]]
name = "web"  
type = "http" 
localIP = "127.0.0.1"
localPort = 8080 #本地网站的端口
customDomains = ["example.serv00.net"] #这个域名下面细说

#你也可以同时穿透多个网站
[[proxies]]
name = "web2"
type = "http"
localPort = 8080 #不写localIP默认为127.0.0.1
customDomains = ["www.yourdomain2.com"] #与上面不同的域名
```
先说"serverAddr",这个端口在panel点击左侧的SSL,然后点WWW websites,下面的两个ip任选其一
![image](https://github.com/user-attachments/assets/efdce182-2466-4ed1-9b03-842c7299f41b)

"customDomains"部分,panel左侧点击WWW Websites,然后点击Add new website,然后像我这样写
![image](https://github.com/user-attachments/assets/84b4bed4-4f53-4683-8009-033b320bfd8e)

然后放到一个文件夹内
![image](https://github.com/user-attachments/assets/2c7d94fe-9c00-4b9f-9883-b324789a385d)


### 3.5绑定自己的域名
①用argo隧道(不会)
②手动绑定
先在你的域名的dns记录里A解析到serverAddr中填的那个ip,然后在panel面板刚才创建域名中Domain写A解析的你自己的域名,其他不变点添加
![image](https://github.com/user-attachments/assets/04aa7417-46a3-4e7b-80ab-efd61e9da5c3)

然后在SSL→WWW websites→serverAddr中填的ip的那个manage→serverAddr
Type选Certificate file的话下面就上传cf的证书,Certificate上传.pem Key上传.key,下面域名选择你自己的那个域名.没有证书就在Type选择Generate Let's Encrypt certificate(但是我会报错)(找到报错原因了,这里申请证书cf小黄云要先关闭)
![image](https://github.com/user-attachments/assets/b5588670-41c6-40fb-b576-b72b030a6583)

![image](https://github.com/user-attachments/assets/e05fbeb3-67ec-427f-a7d1-292d2d19d7dd)

然后在上面的frpc.toml中的customDomains把域名改成你自己A解析的那个域名这样你就可以访问了.
4.测试
先在ssh中开启frpc(先cd到frp目录)
```
./frps -c ./frps.toml
```
然后在你的客户端中启动frpc(依然先cd到frp目录)
```
./frpc -c ./frpc.toml #其他系统使用效果相同的命令,比如win:frpc -c frpc.toml
```
如果成功效果如图
frps
![image](https://github.com/user-attachments/assets/ac56fff7-143e-4194-9fea-f8aa6892d479)

frpc
![image](https://github.com/user-attachments/assets/822e1103-8a5e-4e88-a662-ff1a860f7578)

退出就ctrl+c就行

三.完结散花
1.开机自启
还记得之前装的pm2吗
先在ssh退出frps
然后使用PM2监控
```
pm2 start -x ./frp/frps -n frp -- -c ./frp/frps.toml
```
在Panel中找到Cron jobs选项卡，使用Add cron job功能添加任务，Specify time选择After reboot，即为重启后运行。Form type选择Advanced，Command写：
```
/home/你的用户名/.npm-global/bin/pm2 resurrect
```
然后在ssh保存pm2任务快照
```
pm2 save
```
## 2.定时ssh
### 方法①青龙面板(可能有时连不上,建议ssh链接时间调短一点)
添加Linux依赖 sshpass .添加定时任务 其他随意
命令
```
sshpass -p '密码' ssh -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null -tt 用户名@地址 "exit"
```
定时规则 1 1 1 * * .这样每月一号自动ssh

### 方法②自交
进入一个你喜欢的路径(根目录就行,方便就好)新建一个脚本(把用户名 密码改成自己的)
```
cat > auto_renew.sh << EOF
#!/bin/bash

sshpass -p '密码' ssh -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null -tt 用户名@地址 "exit" &
EOF
```
添加权限
```
chmod +x auto-renew.sh
```
再去 Panel 中找到 Cron jobs 选项卡，使用 Add cron job 功能添加任务，Specify time 选择 Monthly，Form type 选择 Advanced。Command 写 auto_renew.sh 脚本文件的绝对路径，如
```
/home/username/auto_renew.sh >/dev/null 2>&1
```
即可。
文章引用至大佬 ：https://www.huluohu.com/posts/429/
> 今天要介绍的是一款追书神器：`Reader`，绝对是网文爱好者的福音，它可以使用很多网友分享的书源、并自动订阅更新。除此之外还支持导入TXT、EPUB、UMD等格式的书籍、支持漫画音频、支持Kindle阅读等等，是一款超级强大的书源/书仓管理器。

## 安装和运行Reader

Reader目前最新版本是`v3.2.6`，在Github上有5.6k的Star，支持Windows、Mac和Docker（Web）方式部署。不过目前开发者对开源版本做了一些限制，比如最多只能支持50个注册用户、代码只开源到v2.x并退出闭源版本等等，可能也是怕被滥用引火烧身或者有商业化打算吧。

笔者为了能够支持iOS阅读，本文以Docker为例，介绍如何安装和运行Reader的Web版本。

### 准备工作

+   创建应用目录，例如在/share/Container下创建文件夹`reader`
+   在`Reader`下创建2个子文件夹，分别为：`logs`、`storage`

## 安装Reader

**第一步、** 在/share/Container/reader文件夹下创建文件`docker-compose.yml`，

**第二步、** 并将下面内容复制粘贴到`docker-compose.yml`中，保存：

```yml
version: "3.8"
services:
  reader:
    image: hectorqin/reader:openj9-latest
    container_name: reader
    restart: unless-stopped
    network_mode: bridge
    environment:
      - PUID=1000
      - PGID=100
      - TZ=Asia/Shanghai
      - SPRING_PROFILES_ACTIVE=prod
      - READER_APP_USERLIMIT=50 #用户上限,默认50
      - READER_APP_USERBOOKLIMIT=200 #用户书籍上限,默认200
      - READER_APP_CACHECHAPTERCONTENT=true #开启缓存章节内容 V2.0
      # 如果启用远程webview，需要取消注释下面的 remote-webview 服务
      # - READER_APP_REMOTEWEBVIEWAPI=http://remote-webview:8050 #开启远程webview
      # 下面都是多用户模式配置
      - READER_APP_SECURE=true #开启登录鉴权，开启后将支持多用户模式
      - READER_APP_SECUREKEY=adminpwd  #管理员密码  建议修改
      - READER_APP_INVITECODE=registercode #注册邀请码 建议修改,如不需要可注释或删除
    ports:
      - 5009:8080 #4396端口映射可自行修改
    volumes:
      - /share/Container/reader/logs:/logs #log映射目录 /home/reader/logs 映射目录可自行修改
      - /share/Container/reader/storage:/storage #数据映射目录 /home/reader/storage 映射目录可自行修改
   
  # remote-webview:
  #   image: hectorqin/remote-webview
  #   container_name: remote-webview #容器名 可自行修改
  #   restart: unless-stopped
  #   network_mode: bridge
  #   ports:
  #     - 8050:8050
```

> 参数说明

| 参数 | 说明 |
| --- | --- |
| \-p 8080 | http协议访问WebUI的端口，宿主机的端口可以修改成你自己喜欢的 |
| \-e PUID=1000 | 设置PUID的值，请改成自己的 |
| \-e PGID=100 | 设置PGID的值，请改成自己的 |
| \-e READER\_APP\_SECUREKEY=adminpwd | 管理员账号的密码，建议修改成其他的 |
| \-e READER\_APP\_INVITECODE=registercode | 注册账号的要求码，建议修改成其他的 |
| \-e TZ=Asia/Shanghai | 设置时区 |
| \-v /logs | 配置日志文件的保存位置，宿主机的位置可以修改成你自己喜欢的 |
| \-v /storage | 配置数据文件的保存位置，宿主机的位置可以修改成你自己喜欢的 |

> **特别说明：** 如果要开启远程webview功能（针对webview类型的书源），可以将上面的`remote-webview:`节点的注释(#)删掉，然后将 `- READER_APP_REMOTEWEBVIEWAPI`的注释也删掉，并设置好`remote-webview`的IP和端口。

**第三步、** 在NAS的SSH中，切换到reader文件夹下，执行下面命令启动：


```shell
docker-compose up -d
```

**第四步、** 等待应用启动完成后，打开WebUI

> 在浏览器中输入NAS的IP+端口，例如：192.168.31.91:5009；如果使用Kindle阅读，可使用`http://ip:端口/simple-web`（需购买授权！！！），

![image](https://github.com/user-attachments/assets/29c06c08-fa01-4297-bcf9-14fd982f197f)


![image](https://github.com/user-attachments/assets/975890ce-eec0-4742-8e8f-344ff8bbc225)


## 注册用户

首次打开页面后，会弹出登录界面，直接在页面上点击`注册`。  
![image](https://github.com/user-attachments/assets/845b3a64-147f-4bbc-beda-401863bae338)


输入用户名和密码，输入我们在上面设置的邀请码，点击`确定`，就创建一个用户了。  
![image](https://github.com/user-attachments/assets/c58aade4-b821-4153-b99b-e06ed30b64df)


## 导入书源

如果想追更各大网文网站的小说，首先得导入书源才行，导入以后就可以直接搜索你想看的小说/漫画等网文了。

左侧菜单`书源管理`中，点击`导入书源`，导入你的书源文件，至于书源文件怎么找，某度应该可以找找，在这里笔者不方便多写。  
![image](https://github.com/user-attachments/assets/19139c9b-a2ca-4aa8-9df0-be7c9d0e430f)


![image](https://github.com/user-attachments/assets/90abf65f-febc-44aa-a84e-41aacd624379)


## 搜索并订阅书籍

书源导入玩出，就可以搜索内容了，需要特别说明下，能不能搜到你想看的小说，还是要看你的书源质量如何。

在左上角搜索框中输入你要查找的内容名称，等待后台搜索。如果最终啥都没有，说明你的书源需要继续加强。  
![image](https://github.com/user-attachments/assets/430f4373-61d2-4710-9f85-96a0b0db7825)


选择你想阅读的数据，点击`加入书架`，这本书就加到你的书架中了，如果书籍有更新，reader也会自动帮你下载到系统中，打开reader就能看！  
![image](https://github.com/user-attachments/assets/c8f7adbf-caad-45aa-a322-3b9e897a51b0)

添加到书架上的时候，你也可以修改数据的作者、书名和分组。  
![image](https://github.com/user-attachments/assets/7f503ef1-7f3c-4ac6-9b1d-e78215a42259)


## 导入本地书籍

除了直接搜索网文，reader也支持直接导入本地书籍，支持TXT、EPUB、UMD、PDF等格式的书籍。

左侧菜单`书架设置`中，点击`导入书籍`，选择你自己电脑上的书籍导入即可，然后你在其他终端使用reader也可以阅读。  
![image](https://github.com/user-attachments/assets/1a4e9c0c-dd2c-474b-93f1-73b7266b48c6)


## 总结

除了以上主要配置外，reader还支持其他的一些功能，例如清理失效书源、书签管理、书架管理等等。如果你想将reader作为主力阅读器，还是得亲自上手试试才知道，笔者抛转引起，其他大佬们完善指正。

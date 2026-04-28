域名的基本概念

众所周知，域名的作用是将复杂的IP地址转化为易于记忆的字符串。以我自己的域名www.tech-shrimp.com为例，被两个点划分成了三个部分。其中，最右边的.com是顶级域名，顶级域名通常由国家或机构持有，普通用户是无法直接注册的。中间这部分英文名是Apex Domain，在各种资料与教程中，这部分有时候被称为一级域名，有时候被称为二级域名。为了避免歧义，在我视频中统一称之为主域名。普通用户通常购买的就是这个主域名。主域名的左边就是子域名，一个主域名可以免费扩展出很多个子域名。

免费域名的限制

目前有不少服务商提供免费子域名注册，视频的后面会演示如何获取免费域名。但俗话说，免费的就是最贵的。免费域名使用时经常受到各种限制。因此，我更推荐直接购买一个主域名，这样可以更加自由地使用和管理。

如何购买一个域名

我一般使用Namesilo网站

www.namesilo.com 

购买一个便宜域名。在这里输入一个你想要的域名，比如这里我还是输入tech-shrimp，技术爬爬虾，点击搜索。
![image](https://github.com/wqlabs/wqlabs.github.io/assets/39255755/4181b256-89b3-45c6-8519-9ebaa7392ead)


这里就给出了一些对应域名的报价，上面这个是第一年的价格，然后下面这个renew是后面续费的价格。

![image](https://github.com/wqlabs/wqlabs.github.io/assets/39255755/398f7831-7834-4261-8d3b-2b4346d04dce)

还有一种更便宜的域名，这里输入任意六位数字，比如输入我们家猫的生日，然后点击search。这种纯数字的xyz域名，第一年跟续费都只需要1美元。如果担心后续续费涨价，也可以提前续费。

![image](https://github.com/wqlabs/wqlabs.github.io/assets/39255755/512c9db6-144f-4fa0-a07d-3e3c619b1371)



这里我选择这个点top的，它比较便宜，这里我就点击加入购物车，然后这里点check out。没有账号就在这里注册一个，注册成功这里自动生成了一个假地址，我就直接用这个默认了。然后我继续点击付款，这里最方便的就选择支付宝，右下角选择接受点击支付。本期视频成本13.67人民币。

域名解析与DNS服务

有了域名，我们还需要DNS。DNS是一种域名转换为IP地址的服务，当用户在浏览器输入一个网址时，浏览器会向DNS服务器发送请求以获取该网址对应的IP地址。DNS服务商我基本上都是用Cloudflare，因为它速度快，而且有一大堆的免费服务。我们看一下如何将域名托管到Cloudflare。

将域名托管到Cloudflare

我们先登录Cloudflare，

www.cloudflare.com

右上角点击添加站点，这里就输刚才买的域名tech-shrimp.top，然后点击继续。
![image](https://github.com/wqlabs/wqlabs.github.io/assets/39255755/684849af-73ae-4574-8e7b-ca71a37bad7b)


这里有一些付费的，我们都不要，直接找下面这个免费的，点击继续。
![image](https://github.com/wqlabs/wqlabs.github.io/assets/39255755/c09c58e7-5774-4e6c-a21c-64df2c1eacb9)


到这一步，什么都不用管，直接点击下一步。这一步是重点，更改名称服务器往下找，找到这两个名称服务器。我们需要去刚才买域名的网站更改一下。
![image](https://github.com/wqlabs/wqlabs.github.io/assets/39255755/7226baf5-4db4-477c-89df-da52357b4e48)


这里回到刚才的Namesilo，点击domain manager，然后进入这个域名，这里有一个name server。就把这里改一下，把原来的这三条全部删掉，然后填上刚才网站给我分配的这两个。点击保存。
![image](https://github.com/wqlabs/wqlabs.github.io/assets/39255755/c6b001e8-1c1a-48ca-8cfa-4c0601ba327d)


好，我们再回到Cloudflare，点击立即检查，然后点击继续。这里可以把自动重写https勾上，这些都保持默认，然后直接点击开始。我们回到网站的主页，等个几分钟，看到这里打上一个对勾，就可以开始直接使用了。

使用Cloudflare做DNS

爬爬虾之前有两期视频都介绍过使用Cloudflare做DNS。一期是将自己的域名代理到GitHub Pages上做个人博客使用，还有一期是使用自己的域名做DDNS，从而达成外网访问家庭服务器的内网。如果感兴趣的话，大家可以找来那两期视频看一下。

国内外域名购买与备案

说到这里，我想讨论一下关于从国内或者国外购买域名还有域名备案的问题。如果想要搭建网站，并且要保证网站在国内被访问到，那就需要使用国内的域名服务商加国内的云服务器，并且做好备案，保证网站的全产品链路都使用国内厂商，这样最保险。如果不做网站，只是做个普通的API接口，或者类似前几期视频我使用的DDNS，给家庭宽带做远程桌面，做SMB文件共享等等，那大可不必备案，也无所谓国内或者国外的域名服务商，哪里域名便宜去哪里买就可以。

如何获取免费域名

下面我们来看如何获取免费域名。我对比了很多网站，最好用的还是这个CloudNS。这个网站申请域名不需要人工审核，基本上秒过，而且我今天测试的它可以托管到Cloudflare。我马上来演示一下。

我们先进入这个网站

www. cloudns.net，

然后这里点击登记，注册一个账号。进入以后，我们在这里点击创建区域，点击免费。
![image](https://github.com/wqlabs/wqlabs.github.io/assets/39255755/cb5ba7b9-23ef-41fb-988e-cad143ae3fe1)


这里域名我还是填tech-shrimp，下面这两种是可以托管Cloudflare的，那我们就选择这个be，然后点击创建。好，这就创建成功了。我把它托管到Cloudflare上，先把这4个NS删掉，

![image](https://github.com/wqlabs/wqlabs.github.io/assets/39255755/1b4b6d8f-0514-445e-be6b-5d2ae4841491)

然后进入Cloudflare，还是添加站点，填我刚才那个域名，点击继续，还是把这两个NS服务放到这里。

![image](https://github.com/wqlabs/wqlabs.github.io/assets/39255755/e856576b-6bab-43d7-b6d8-ebe81f1bcb61)
![image](https://github.com/wqlabs/wqlabs.github.io/assets/39255755/85ac319c-aecb-4d86-af5b-846dcd8c8a85)


点击添加记录，这里类型就选择NS name server指向到，填Cloudflare给我分配的两个地址，先是这个，然后这个，保存。这里打上了对勾，那就代表托管成功了。

免费域名的注意事项

不过使用这个CloudNS的免费域名还有几个注意事项。首先是每一个前缀，我们都需要给它加一个NS服务器指向到Cloudflare的NS server。比如这个www的前缀，我就添了两条记录，然后这个blog的前缀我也添了两条记录。

还有第二个注意事项，我们进入这个域名，点击左侧的SSL TSL，点击边缘证书，把这个证书展开，这里有两条证书，我们必须把它填写到记录里面。

![image](https://github.com/wqlabs/wqlabs.github.io/assets/39255755/e5927a17-60af-42dc-8066-465ea1756866)

这里新添加一条记录，就按照这个格式写，然后下面指向到的这个字符串，就是从边缘证书这里拷贝过来的。需要把这些配置好才算配置成功。

![image](https://github.com/wqlabs/wqlabs.github.io/assets/39255755/72e4f7a4-77ba-4c7c-aa2b-e813a4ec1a87)



这里我还是按照上次Github Pages的视频，把这个域名通过Cloudflare代理到了一个Github Page，就是这个www.tech-shrimp.cloudns.be，可以看到它可以正常访问。不过像这种免费域名还是有很多缺点的。首先我在这里测了一下，只有这个www.tech-shrimp这个域名解析的算是比较好。可以看到这种不带前缀的解析的都非常差，除了澳洲，其他地方都没有解析好。

![image](https://github.com/wqlabs/wqlabs.github.io/assets/39255755/7b328d1a-a186-4e20-9d4a-b1022763f1ff)

还有这个blog.tech-shrimp.cloudns.be的解析也不好，好多地方也没解析成功。我还试了一下ddns go，这里我保存一下，可以看到这个提示，这里ddns go也没有配置成功。所以总的来说，这种免费域名还是有很多问题的。
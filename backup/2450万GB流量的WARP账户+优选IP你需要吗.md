<article class="joe_detail__article animated fadeIn center-img    line-numbers ">
    <div id="post-inner">
      

<p>科学上网是指通过一些技术手段，绕过网络审查和限制，访问一些被屏蔽或者无法正常访问的网站和服务。科学上网的方法有很多，比如VPN，SSR，V2Ray，Trojan等等。但是这些方法都需要自己搭建或者购买服务器，而且可能会被封锁或者干扰，导致无法正常使用。</p>
<p>本文将介绍一种利用replit+telegarm机器人来搭建一个WireGuard节点的方法，该方法不需要购买服务器，只需要一个Telegram账号和一个Replit账号，就可以在Replit平台上生成WARP的WireGuard节点配置文件，然后在电脑或者手机上使用WireGuard客户端连接，就可以实现科学上网。</p>
<p>WARP是Cloudflare提供的一种基于WireGuard协议的网络加速和安全服务，它可以将你的流量通过Cloudflare的网络传输，提高你的网络速度和安全性。WARP有免费版和付费版（WARP+），免费版每月有10GB的流量限制，付费版则没有限制，而且速度更快。WARP提供了官方的客户端，但是官方的客户端不支持自定义节点。所以，我们需要使用第三方的脚本来生成WARP的WireGuard节点配置文件，然后使用WireGuard客户端来连接。</p>
<p>Replit是一个在线的代码平台，它可以让你在浏览器上编写和运行各种编程语言的代码，而且提供了免费的云端服务器和数据库。Replit可以用来运行一些脚本，可以帮助我们生成WARP的WireGuard节点配置文件。</p>
<p>Telegarm是一个在国外非常流行的聊天工具，可以帮助我们获取WARP+的密钥，以及激活WARP+的流量。</p>
<h2 id="步骤">步骤</h2><h3 id="1. 准备工作">1. 准备工作</h3>
<p>首先，你需要注册一个Telegram账号和一个Replit账号，如果你已经有了，可以跳过这一步。</p>
<p>你可以通过以下的链接来注册Telegram账号和Replit账号：</p>
<ul>
<li><a href="https://telegram.org/" target="_blank" rel="noopener noreferrer nofollow">Telegram</a></li>
<li><a href="https://replit.com/" target="_blank" rel="noopener noreferrer nofollow">Replit</a></li>
</ul>
<p>下载WireGuard上网工具</p>
<ul>
<li><a href="https://zfile.ilue.pp.ua/s/t20mrr" target="_blank" rel="noopener noreferrer nofollow">WireGuard</a></li>
</ul>
<h3 id="2. 获取WARP+的密钥">2. 获取WARP+的密钥</h3>
<p>接下来，你需要获取WARP+的密钥，如果你不想使用WARP+，可以跳过这一步。</p>
<p>WARP+是WARP的付费版，它可以提供更快的速度和更多的流量，但是它需要一个密钥来激活。我们可以通过telegarm机器人来获取WARP+的密钥，每个密钥可以获取24598562GB的流量。</p>
<p>你可以通过以下的步骤来获取WARP+的密钥：</p>
<ul>
<li>打开Telegram，搜索@Warp+ bot，或者点击<a href="https://t.me/generatewarpplusbot" target="_blank" rel="noopener noreferrer nofollow">这里</a>。</li>
<li>输入 <code>/start</code> 命令。</li>
<li>再输 <code>/generate</code> 命令，这时机器人会让我们做一下数学题。</li>
<li>然后，输入命令，将答案发给机器人。<code>/generate 答案</code> 。</li>
<li>最后，机器人就就会给我们串激活码。</li>
</ul>
<p><span style="display: block;" data-fancybox="Joe" href="https://picsur.ilue.pp.ua/i/15f92069-5f52-4f09-abe0-5f1940b8a269.webp"><img src="https://picsur.ilue.pp.ua/i/15f92069-5f52-4f09-abe0-5f1940b8a269.webp" alt=""></span></p>
<h3 id="3. 生成WARP的WireGuard节点配置文件">3. 生成WARP的WireGuard节点配置文件</h3>
<p>接下来，你需要生成WireGuard节点配置文件，这个配置文件包含了WARP的账户信息，以及WARP的对端IP和密钥，你可以通过这个配置文件来连接WARP的服务。</p>
<p>你可以通过以下的步骤来生成WARP的WireGuard节点配置文件：</p>
<ul>
<li>打开Replit，登录你的账号，或者点击<a href="https://replit.com/" target="_blank" rel="noopener noreferrer nofollow">这里</a>。</li>
<li>搜索甬哥的WARP-Wireguard-Register项目，点击Fork，或者复制这个链接：<a href="https://replit.com/@ygkkkk/WARP-Wireguard-Register?v=1#README.md" target="_blank" rel="noopener noreferrer nofollow">https://replit.com/@ygkkkk/WARP-Wireguard-Register?v=1#README.md</a></li>
</ul>
<p><span style="display: block;" data-fancybox="Joe" href="https://picsur.ilue.pp.ua/i/a084d387-2532-49b1-b4b9-a1a93875f189.webp"><img src="https://picsur.ilue.pp.ua/i/a084d387-2532-49b1-b4b9-a1a93875f189.webp" alt=""></span></p>
<p><span style="display: block;" data-fancybox="Joe" href="https://picsur.ilue.pp.ua/i/482079c3-3ac4-485f-b9be-52066e526f57.webp"><img src="https://picsur.ilue.pp.ua/i/482079c3-3ac4-485f-b9be-52066e526f57.webp" alt=""></span></p>
<p><span style="display: block;" data-fancybox="Joe" href="https://picsur.ilue.pp.ua/i/6f01286b-5d1f-44e7-9cfc-cd226cab4aa1.webp"><img src="https://picsur.ilue.pp.ua/i/6f01286b-5d1f-44e7-9cfc-cd226cab4aa1.webp" alt=""></span></p>
<p><span style="display: block;" data-fancybox="Joe" href="https://picsur.ilue.pp.ua/i/fb28e780-180e-4f3c-aefa-07d75f571059.webp"><img src="https://picsur.ilue.pp.ua/i/fb28e780-180e-4f3c-aefa-07d75f571059.webp" alt=""></span></p>
<ul>
<li>回到首页，进入刚刚Fork的项目，点击Run，然后等待一会儿，你会看到一个类似于这样的界面：</li>
</ul>
<p><span style="display: block;" data-fancybox="Joe" href="https://picsur.ilue.pp.ua/i/a2af4ca9-7fa2-4663-8a2c-25201c85c182.webp"><img src="https://picsur.ilue.pp.ua/i/a2af4ca9-7fa2-4663-8a2c-25201c85c182.webp" alt=""></span></p>
<p><span style="display: block;" data-fancybox="Joe" href="https://picsur.ilue.pp.ua/i/d7188cde-e4ce-421c-be86-5c9775ab6fc4.webp"><img src="https://picsur.ilue.pp.ua/i/d7188cde-e4ce-421c-be86-5c9775ab6fc4.webp" alt=""></span></p>
<div class="code-toolbar"><pre class="c_title c_hr c_macdot c_hover_tools c_copy language-scss line-numbers" tabindex="0"><code class="hljs language-scss">1.选择 warp-go  注册warp配置 <span class="token punctuation">(</span>支持所有账户升级，显示reserved值，推荐<span class="token punctuation">)</span> 
2.选择 wgcf     注册warp配置 <span class="token punctuation">(</span>支持普通账户、+账户<span class="token punctuation">)</span>    
3.选择 warp api 注册warp配置 <span class="token punctuation">(</span>支持普通账户，显示reserved值<span class="token punctuation">)</span>
0.退出
请选择<span class="token punctuation">:</span>
<span aria-hidden="true" class="line-numbers-rows"><span></span><span></span><span></span><span></span><span></span></span></code><span class="copy-button"><i class="joe-font joe-icon-copy" title="复制代码"></i></span></pre><div class="toolbar"><div class="toolbar-item"><span data-rel="Sass (Scss)"></span></div><div class="toolbar-item"><button class="copy-to-clipboard-button" type="button" data-copy-state="copy" data-rel="复制"></button></div></div></div>
<ul>
<li>输入1，然后按下Enter，你会看到一个类似于这样的界面：</li>
</ul>
<div class="code-toolbar"><pre class="c_title c_hr c_macdot c_hover_tools c_copy language-go line-numbers" tabindex="0"><code class="hljs language-go"><span class="token number">1</span><span class="token punctuation">.</span>warp<span class="token operator">-</span><span class="token keyword">go</span>普通账户
<span class="token number">2</span><span class="token punctuation">.</span>warp<span class="token operator">-</span><span class="token keyword">go</span><span class="token operator">+</span>账户
<span class="token number">3</span><span class="token punctuation">.</span>warp<span class="token operator">-</span><span class="token keyword">go</span><span class="token operator">+</span>teams团队账户
<span class="token number">0.</span>退出
请选择<span class="token punctuation">:</span> 
<span aria-hidden="true" class="line-numbers-rows"><span></span><span></span><span></span><span></span><span></span></span></code><span class="copy-button"><i class="joe-font joe-icon-copy" title="复制代码"></i></span></pre><div class="toolbar"><div class="toolbar-item"><span data-rel="Go"></span></div><div class="toolbar-item"><button class="copy-to-clipboard-button" type="button" data-copy-state="copy" data-rel="复制"></button></div></div></div>
<ul>
<li>
<p>输入你想要的账户类型，如果你想要使用WARP+，你需要输入2，然后输入你之前获取的WARP+密钥，如果你想要使用Teams，你需要输入3，然后输入你的Teams账户的域名，如果你想要使用免费版，你可以输入1，或者直接按下Enter。</p>
</li>
<li>
<p>这里我就选择2，等待一会儿，你会看到一个类似于这样的界面：</p>
</li>
</ul>
<div class="code-toolbar"><pre class="c_title c_hr c_macdot c_hover_tools c_copy language-sql line-numbers" tabindex="0"><code class="hljs language-sql">下载warp<span class="token operator">-</span>go注册程序
<span class="token comment">########################################################################################### 100.0%</span>
  <span class="token operator">%</span> Total    <span class="token operator">%</span> Received <span class="token operator">%</span> Xferd  Average Speed   <span class="token keyword">Time</span>    <span class="token keyword">Time</span>     <span class="token keyword">Time</span>  <span class="token keyword">Current</span>
                                 Dload  Upload   Total   Spent    <span class="token keyword">Left</span>  Speed
<span class="token number">100</span>   <span class="token number">401</span>  <span class="token number">100</span>   <span class="token number">401</span>    <span class="token number">0</span>     <span class="token number">0</span>    <span class="token number">169</span>      <span class="token number">0</span>  <span class="token number">0</span>:<span class="token number">00</span>:<span class="token number">02</span>  <span class="token number">0</span>:<span class="token number">00</span>:<span class="token number">02</span> <span class="token comment">--:--:--   169</span>
请复制手机WARP客户端WARP<span class="token operator">+</span>状态下的按键许可证秘钥 或 网络分享的秘钥（<span class="token number">26</span>个字符），随意输入有机率获得<span class="token number">1</span>G流量WARP<span class="token operator">+</span>账户
请输入升级WARP<span class="token operator">+</span>密钥：
<span aria-hidden="true" class="line-numbers-rows"><span></span><span></span><span></span><span></span><span></span><span></span><span></span></span></code><span class="copy-button"><i class="joe-font joe-icon-copy" title="复制代码"></i></span></pre><div class="toolbar"><div class="toolbar-item"><span data-rel="SQL"></span></div><div class="toolbar-item"><button class="copy-to-clipboard-button" type="button" data-copy-state="copy" data-rel="复制"></button></div></div></div>
<ul>
<li>这里要我们输入WARP+密钥，我们就输入刚刚再Telegram里获取到的密钥。</li>
</ul>
<p><span style="display: block;" data-fancybox="Joe" href="https://picsur.ilue.pp.ua/i/ea0ce103-3900-4860-afaa-d0ad94b025bf.webp"><img src="https://picsur.ilue.pp.ua/i/ea0ce103-3900-4860-afaa-d0ad94b025bf.webp" alt=""></span></p>
<ul>
<li>等待片刻，Warp+账户就申请成功了，WireGuard配置文件和二维码也生成好了。</li>
</ul>
<p><span style="display: block;" data-fancybox="Joe" href="https://picsur.ilue.pp.ua/i/cc37fd74-c4f4-4a25-8421-eb23a2361e4b.webp"><img src="https://picsur.ilue.pp.ua/i/cc37fd74-c4f4-4a25-8421-eb23a2361e4b.webp" alt=""></span></p>
<h3 id="4.连接WARP的服务">4.连接WARP的服务</h3>
<p>使用WireGuard客户端来连接WARP的服务，WireGuard是一种基于UDP的简单，快速，安全的VPN协议，它支持多平台，多设备，多语言，以及端到端加密。WireGuard提供了官方的客户端，你可以通过导入WARP的WireGuard节点配置文件来连接WARP的服务。</p>
<p>你可以通过以下的步骤来连接WARP的服务：</p>
<ul>
<li>下载并安装WireGuard客户端，你可以通过以下的链接来下载WireGuard客户端：
<ul>
<li>[<a href="https://zfile.ilue.pp.ua/s/t20mrr" target="_blank" rel="noopener noreferrer nofollow">Windows</a>]</li>
<li>[<a href="https://itunes.apple.com/us/app/wireguard/id1451685025?ls=1&amp;mt=12" target="_blank" rel="noopener noreferrer nofollow">MacOS</a>]</li>
<li>[<a href="https://zfile.ilue.pp.ua/s/z4gks6" target="_blank" rel="noopener noreferrer nofollow">Android</a>]</li>
<li>[<a href="https://itunes.apple.com/us/app/wireguard/id1441195209?ls=1&amp;mt=8" target="_blank" rel="noopener noreferrer nofollow">iOS</a>]</li>
</ul>
</li>
<li>打开WireGuard客户端，点击添加隧道，然后选择从文件导入，或者直接粘贴刚刚创建的WireGuard节点配置文件的内容。</li>
</ul>
<p><span style="display: block;" data-fancybox="Joe" href="https://picsur.ilue.pp.ua/i/6f18a0e2-0411-46a8-89a8-3ee63d175d6b.webp"><img src="https://picsur.ilue.pp.ua/i/6f18a0e2-0411-46a8-89a8-3ee63d175d6b.webp" alt=""></span></p>
<p><span style="display: block;" data-fancybox="Joe" href="https://picsur.ilue.pp.ua/i/2c2e667a-e061-4c7d-908c-f2d76f4e3e0b.webp"><img src="https://picsur.ilue.pp.ua/i/2c2e667a-e061-4c7d-908c-f2d76f4e3e0b.webp" alt=""></span></p>
<p><span style="display: block;" data-fancybox="Joe" href="https://picsur.ilue.pp.ua/i/55b50086-f2c3-4ca7-8fda-f076f494deb1.webp"><img src="https://picsur.ilue.pp.ua/i/55b50086-f2c3-4ca7-8fda-f076f494deb1.webp" alt=""></span></p>
<ul>
<li>点击连接，你就可以连接WARP的服务了。如果你想要断开连接，点击断开。</li>
</ul>
<p><span style="display: block;" data-fancybox="Joe" href="https://picsur.ilue.pp.ua/i/f84d5881-8eb6-49c7-83fb-2a8063c4a863.webp"><img src="https://picsur.ilue.pp.ua/i/f84d5881-8eb6-49c7-83fb-2a8063c4a863.webp" alt=""></span></p>
<h3 id="5. 优选WARP的对端IP">5. 优选WARP的对端IP</h3>
<p>接下来，你可以优选WARP的对端IP，以提高你的科学上网的速度和稳定性，如果你不想优选，可以跳过这一步。</p>
<p>WARP的对端IP是指WARP的服务器的IP地址，不同的对端IP可能会有不同的延迟和速度，所以我们可以通过测试每个对端IP的性能，来选择最优的对端IP。</p>
<p>你可以通过以下的步骤来优选WARP的对端IP：</p>
<ul>
<li>下载Warp优选IP工具。<a href="https://zfile.ilue.pp.ua/s/uvxvej" target="_blank" rel="noopener noreferrer nofollow">点击下载</a></li>
<li>解压之后运行第一个 <code>bat</code> 文件。</li>
</ul>
<p><span style="display: block;" data-fancybox="Joe" href="https://picsur.ilue.pp.ua/i/120228ed-a416-4aaa-8b34-ebe6ce6d2e24.webp"><img src="https://picsur.ilue.pp.ua/i/120228ed-a416-4aaa-8b34-ebe6ce6d2e24.webp" alt=""></span></p>
<ul>
<li>可以选择ipv4或者ipv6，我这里就选择优选ipv4对端IP。</li>
</ul>
<p><span style="display: block;" data-fancybox="Joe" href="https://picsur.ilue.pp.ua/i/75292926-0932-437f-976d-8c0954614b69.webp"><img src="https://picsur.ilue.pp.ua/i/75292926-0932-437f-976d-8c0954614b69.webp" alt=""></span></p>
<ul>
<li>回车之后，你会看到这样的界面，我们等待运行结束</li>
</ul>
<p><span style="display: block;" data-fancybox="Joe" href="https://picsur.ilue.pp.ua/i/bd86362b-9556-4b87-968e-37a354767726.webp"><img src="https://picsur.ilue.pp.ua/i/bd86362b-9556-4b87-968e-37a354767726.webp" alt=""></span></p>
<ul>
<li>然后，我们回到工具的目录，看到脚本会自动生成一个文档，双击它。</li>
</ul>
<p><span style="display: block;" data-fancybox="Joe" href="https://picsur.ilue.pp.ua/i/80a288f8-463a-41e8-a644-a5c6cea43382.webp"><img src="https://picsur.ilue.pp.ua/i/80a288f8-463a-41e8-a644-a5c6cea43382.webp" alt=""></span></p>
<ul>
<li>文档里会记录针对你目前网络环境最优的对端IP，并从上到下排序。</li>
</ul>
<p><span style="display: block;" data-fancybox="Joe" href="https://picsur.ilue.pp.ua/i/a3841ad3-0a2a-4d3f-aa59-f0fdf5af5cc2.webp"><img src="https://picsur.ilue.pp.ua/i/a3841ad3-0a2a-4d3f-aa59-f0fdf5af5cc2.webp" alt=""></span></p>
<ul>
<li>复制第一条IP（也就是最优的），替换掉原WireGuard配置文件的对端IP</li>
</ul>
<p><span style="display: block;" data-fancybox="Joe" href="https://picsur.ilue.pp.ua/i/41d070d0-0457-46dd-8660-0b567c510f34.webp"><img src="https://picsur.ilue.pp.ua/i/41d070d0-0457-46dd-8660-0b567c510f34.webp" alt=""></span></p>
<p><span style="display: block;" data-fancybox="Joe" href="https://picsur.ilue.pp.ua/i/2e2090dc-2662-457a-afbe-6b3a22d09600.webp"><img src="https://picsur.ilue.pp.ua/i/2e2090dc-2662-457a-afbe-6b3a22d09600.webp" alt=""></span></p>
<h2 id="测试">测试</h2>
<p>测一下速，针对我目前使用的网络环境，下行速度:<code>90.14Mbps</code> 下行速度:<code>55.73Mbps</code> 也差不多能跑满</p>
<p>测速地址：https://www.speedtest.net/</p>
<p><span style="display: block;" data-fancybox="Joe" href="https://picsur.ilue.pp.ua/i/5f944354-0d60-4482-a6a4-252416773e78.webp"><img src="https://picsur.ilue.pp.ua/i/5f944354-0d60-4482-a6a4-252416773e78.webp" alt=""></span></p>
<p>YouTube 4K视频</p>
<p><span style="display: block;" data-fancybox="Joe" href="https://picsur.ilue.pp.ua/i/45df581e-b458-4417-9f4d-7d9763652341.webp"><img src="https://picsur.ilue.pp.ua/i/45df581e-b458-4417-9f4d-7d9763652341.webp" alt=""></span></p>
<p>可以看到，本地时间 <code>22:52</code> 分也能达到 <code>82000Kbps</code> 的播放速度，但这只是针对我使用的网络环境。测速只和你使用的网络有关系，我这里有 <code>82000</code> 的播放速度，你的测试结果可能会更高，也有可能会更低。</p>
<h2 id="结语">结语</h2>
<p>恭喜你，你已经成功的搭建了一个近乎无限流量的WireGuard节点，你可以享受WARP提供的网络加速和安全服务了。🎉</p>
<p>如果你觉得这篇教程对你有帮助，你可以点赞，收藏，或者分享给你的朋友，让更多的人知道这个方法。如果你有任何问题，意见，或者建议，你可以在评论区留言，或者联系我，我会尽力回复你。</p>
<p>感谢你的阅读，祝你科学上网愉快！😊</p>
<p>本篇文章脚本由<a href="https://github.com/yonggekkk" target="_blank" rel="noopener noreferrer nofollow">甬哥侃侃侃ygkkk</a>提供</p>
<p>[更多相关教程]</p>
<p><a href="https://blog.ilue.pp.ua/archives/zi-ji-dong-shou-da-jian-yi-ge-yong-jiu-mian-fei-de-ke-xue-shang-wang-jie-dian" target="_blank" rel="noopener noreferrer nofollow">自己动手搭建一个永久免费的科学上网节点</a></p>
<p><a href="https://blog.ilue.pp.ua/archives/ru-he-you-xuan-fan-dai-ip" target="_blank" rel="noopener noreferrer nofollow">如何优选反代IP</a></p>
<p><a href="https://blog.ilue.pp.ua/archives/ke-xue-shang-wang-cloudflare-worker-you-xuan-ip-clashding-yue-lian-jie" target="_blank" rel="noopener noreferrer nofollow">【科学上网】Cloudflare+worker+优选IP+clash订阅链接</a></p>
<p><a href="https://blog.ilue.pp.ua/archives/ke-xue-shang-wang-chromegoke-xue-shang-wang-shen-qi" target="_blank" rel="noopener noreferrer nofollow">【科学上网】ChromeGO科学上网神器</a></p>

      
      
    </div>
    
  </article>
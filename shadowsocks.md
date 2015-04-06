科学上网利器-----shadowsocks

生在我朝，掌握科学上网几乎是一名思进取、爱折腾、重网瘾的穷程序员的必备技能。于是乎，寻找一款省时省力关键还能省钱的科学上网工具是我毕生追求的目标之一。

[GoAgent](https://github.com/goagent/goagent)，它完全免费，配置过程繁琐，早期GoAgent用起来还算省心，随着时间推移，用的人多了，稳定性也随之下降，常常影响到工作效率，随之转到[曲径](http://getqujing.com/)。曲径是一款收费工具，配置简单，服务稳定，50元/月的费用断断续续用了差不多两个季度，最后因无力支付其高昂的费用选择了放弃，不过这是高富帅的不二选择。古云：“世上无难事，就怕爱折腾”。
[Shadowsocks](https://github.com/shadowsocks/shadowsocks)华丽出场。

Shadowsocks的运行原理是通过客户端以指定的密码、加密方式和端口连接服务器，成功连接到服务器后，客户端在用户的电脑上构建一个本地socks5代理。使用时将流量分到本地socks5代理，客户端将自动加密并转发流量到服务器，服务器以同样的加密方式将流量回传给客户端，以此达到科学上网的目的。了解其本原理后，我们就可以着手搭建一个基于Shadowsocks的科学上网环境。

首先，你得有一台云主机，这里推荐使用[DigitalOcean](https://www.digitalocean.com/?refcode=af4cff8f42bc)，它对开发者来说特别友好，拥有独立IP，SSD硬盘，最便宜的云主机只需5$，折合软妹币三十多，这样的价格应该可以秒杀国内各大厂的IAAS，用有一台SSD云主机后从此你不仅可以用来科学上网，还可以在上面搭建个人博客，开发应用程序，简它直就是开发者的福音，你只需一张信用卡或者一个paypal帐号即可开始使用（两者都没的，或许我能帮你一下，如果我有空的话），注册时如果从链接[https://www.digitalocean.com/?refcode=af4cff8f42bc](https://www.digitalocean.com/?refcode=af4cff8f42bc)进入可以让我获得5$的优惠，当然你也可以不填，我们依然可以继续做朋友。

####服务端安装配置

假设现在你已经拥有一台正在运行的云主机了，接下来就是安装软件及配置。首先是服务端安装，不同系统安装方式不尽一样，Windows的安装方法可参考[Install Shadowsocks Server on Windows](https://github.com/shadowsocks/shadowsocks/wiki/Install-Shadowsocks-Server-on-Windows) 下面是Linux/OSX的安装方式：  

Debian / Ubuntu ：  
	 
	 apt-get install python-pip
	 pip install shadowsocks

CentOS：  
	
	yum install python-setuptools && easy_install pip
	pip install shadowsocks

 

接下来就是服务端Shadowsocks的配置，创建/etc/shadowsocks.json文件，并填入内容：  
	
	{
	    "server":"0.0.0.0",
	    "server_port":8388,
	    "local_address": "127.0.0.1",
	    "local_port":1080,
	    "password":"123456",
	    "timeout":300,
	    "method":"aes-256-cfb",
	    "fast_open": false,
	    "workers": 1
	}
	
配置没有问题就可以启动/停止：  
	
	ssserver -c /etc/shadowsocks.json -d start
	ssserver -c /etc/shadowsocks.json -d stop
	~
####客户端安装配置
Shadowsocks客户端几乎支持所有主流平台，具体可以参看[这里](http://shadowsocks.org/en/download/clients.html)，选择相应平台的客户端下载安装，如果无法下载，可以到[百度网盘下载](http://pan.baidu.com/s/1gdepDJH)，安装成功后，填上服务端的参数，如图：![参数](http://blog-resource.qiniudn.com/shadowsocks.png)

下载安装Chrome的浏览器插件[Proxy SwitchySharp](https://chrome.google.com/webstore/detail/proxy-switchysharp/dpplabbmogkhghncfbfdeeokoefdjegm?hl=zh-CN)（[百度网盘下载](http://pan.baidu.com/s/1eQ4GcWa)），打开Chrome，输入chrome://extensions，把下载的extension_1_10_4.crx文件拖进去即可安装），安装成功后Chrome右上方看到Proxy SwitchySharp的图标，点击选项，新建情景模式如下图设置保存；  
![switchy](http://blog-resource.qiniudn.com/switchyproxy2.jpg)    
最后切换到showdsocks：  
![x](http://upload-images.jianshu.io/upload_images/29832-d5c270c7fb0f7e7e.png)  

最后来访问测试一下：[http://twitter.com](http://twitter.com)，如果在安装配置过程中遇到问题，欢迎骚扰[我](http://weibo.com/527355345)。
# 自建hysteria服务器教程

Hysteria 是一个功能丰富的，专为恶劣网络环境进行优化的网络工具（双边加速），比如卫星网络、拥挤的公共 Wi-Fi、在中国连接国外服务器等。 基于修改版的 QUIC 协议。由go编写的非常优秀的“轻量”代理程序，它很好的解决了在搭建科学上网服务器时的痛点——线路一般、高峰时期慢。虽然是走的udp但是提供obfs，暂时不会被运营商针对性的QoS(不开obfs也不会被QoS)。下图为原开发项目提供的不同协议的速度对比：

![](https://camo.githubusercontent.com/e30d7a192564f01e8468c7278c30b06af8802d87929789a38c9ad2227d77ca0a/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f48794e6574776f726b2f68797374657269612f646f63732f62656e63682f62656e63682e706e67)

**自建hysteria教程很简单，整个教程分三步** ：

第一步：购买VPS服务器

第二步：一键部署VPS服务器

***

**第一步：购买VPS服务器**

VPS服务器需要选择国外的，首选国际知名的vultr，速度不错、稳定且性价比高，按小时计费，能够随时开通和删除服务器，新服务器即是新ip。

vultr注册地址： [https://www.vultr.com/?ref=7048874](https://www.vultr.com/?ref=7048874) （vps最低2.5美元/月，vultr全球32个服务器位置可选，包括洛杉矶、韩国、新加坡、日本、德国、荷兰等。支持支付宝和paypal付款。）

[![](https://camo.githubusercontent.com/3213dae59599fd2e671de317c336a4b150b707c9099910ac552fa45bc244a7e5/68747470733a2f2f7777772e76756c74722e636f6d2f6d656469612f62616e6e6572732f62616e6e65725f3732387839302e706e67)](https://www.vultr.com/?ref=7048874)

虽然是英文界面，但是现在的浏览器都有网页翻译功能，鼠标点击右键，选择网页翻译即可翻译成中文。

注册并邮件激活账号，充值后即可购买服务器。充值方式是支付宝或paypal，使用paypal有银行卡（包括信用卡）即可。paypal注册地址： [https://www.paypal.com](https://www.paypal.com/) （paypal是国际知名的第三方支付服务商，注册一下账号，绑定银行卡即可购买国外商品）

***

**注意：2.5美元套餐只提供ipv6 ip，一般的电脑用不了，所以建议选择3.5美元及以上的套餐。**

vultr实际上是折算成小时来计费的，比如服务器是5美元1个月，那么每小时收费为5/30/24=0.0069美元 会自动从账号中扣费，只要保证账号有钱即可。如果你部署的服务器实测后速度不理想，你可以把它删掉（destroy），重新换个地区的服务器来部署，方便且实用。因为新的服务器就是新的ip，所以当ip被墙时这个方法很有用。当ip被墙时，为了保证新开的服务器ip和原先的ip不一样，先开新服务器，开好后再删除旧服务器即可。在账号的Account——Make a payment选项里可以看到账户余额。

**账号充值如图** ：

![](https://camo.githubusercontent.com/3d848aae5644db37aafc0934cbf3f191f45ee339738d66c8d0a0b6712cc4cd2a/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f416c76696e393939392f706163322f736f6674696d61672f76302e6a7067)

依次点击Account——Make a payment——Alipay(支付宝)

**vultr改版了，最新开通服务器步骤如图** ：

![](https://camo.githubusercontent.com/1589e8dd32d0a10192bc120a7ba221a982fb82fe8725d813eddaa6a8173a7efc/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f416c76696e393939392f706163322f736f6674696d61672f76312e6a7067)

点击网页右上角的Deploy图标

![](https://camo.githubusercontent.com/1cb46fe7931df154eaaffd98f6b44e0a83f2004275cb7aab45cc7400f853e2b9/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f416c76696e393939392f706163322f736f6674696d61672f76322e6a7067)

在下拉菜单中，点击Deploy New Server

![](https://camo.githubusercontent.com/a2e5fd01238afa3910f20d08aeb55405d8efe4f925f27fddce8c76ccf1eb2a36/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f416c76696e393939392f706163322f736f6674696d61672f76332e6a7067)

服务器类型选择Cloud Compute-Shared CPU

![](https://camo.githubusercontent.com/bc3dc2e18a3e7947a44b42f0e024009aa7bde8739c8b6d97d322a32c2507d759/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f416c76696e393939392f706163322f736f6674696d61672f76342e6a7067)

选择服务器位置。不同的服务器位置速度会有所不同，有的服务器的最低价格会不同，一般纽约等位置的价格最低，有3.5美元/月的，可根据自己的需求来选择。推荐洛杉矶服务器，延迟较低且比较稳定。

![](https://camo.githubusercontent.com/200ffdd0b49b1f85987d2e686d6debae43d145140ca9cb78583f5bd278009751/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f416c76696e393939392f706163322f736f6674696d61672f64656269616e3131303930382e706e67)

点击图中的系统名字，会弹出具体系统版本，推荐Debian系统

![](https://camo.githubusercontent.com/9d880600e5cdac13bd18413b9b4610cb3bbc02236f12ae605e7ec087b3aa502a/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f416c76696e393939392f706163322f736f6674696d61672f76362e6a7067)

选择服务器套餐。根据自己的需求来选择，如果服务器位置定了，套餐不影响速度，影响流量和配置，一般用的人数少，选择低配置就够了。便宜的套餐，点击Regular Cloud Compute，选择第一个套餐，提示升级选择No Thanks。

![](https://camo.githubusercontent.com/d26936f5a978dc4048295780ed1ae8b5eb9dffdc98a027ff2dde1ffe0842b62a/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f416c76696e393939392f706163322f736f6674696d61672f76372e6a7067)

关闭自动备份Auto Backups，这个是收费的。点击它，在右侧的I understand the risk前面选择勾，然后点击Disable Auto Backups即可关闭自动备份。

![](https://camo.githubusercontent.com/d977c40f63eab081cfe69ff43fac94311c31f743df15806d485f2d33abe4a761/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f416c76696e393939392f706163322f736f6674696d61672f76382e6a7067)

最后点击“Deploy Now”开始部署，等6\~10分钟就差不多了。

**完成购买后，找到系统的密码记下来，部署服务器时需要用到。vps系统的密码获取方法如下图：**

![](https://camo.githubusercontent.com/e8ddeda92f89d3d0ace97eaaef69429c540edd43d92c18fc695179923e0c6eb7/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f416c76696e393939392f706163322f736f6674696d61672f76392e6a7067)

点击Products——Compute就可以看到购买的服务器列表

![](https://camo.githubusercontent.com/c12004100feb5f52f6f272d3da29f0d37441b152dfd667c05ebc777d61628032/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f416c76696e393939392f706163322f736f6674696d61672f7631302e6a7067)

![](https://camo.githubusercontent.com/66e87041789a489bf9987fbf8997de8aa4a472be8fcc3087f9160788c60a06af/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f416c76696e393939392f706163322f736f6674696d61672f7631312e6a7067)

在服务器的最右边，点击三个点，再点击Server Details就可以看到该服务器的详细信息。

![](https://camo.githubusercontent.com/e19b4193ee4486c89b11d03f3892ffeff6403e0938f2ec9c46790b7100813621/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f416c76696e393939392f706163322f736f6674696d61672f7631322e6a7067)

服务器ip和系统密码可以看到并能复制。

**删掉服务器步骤如下图** ：

删除服务器时，先开新的服务器后再删除旧服务器，这样可以保证新服务器的ip与旧ip不同。

![](https://camo.githubusercontent.com/f7110267ac256ee5fe8d4e23ef94f134016ccc522a4d8d79e7084f223ab7713c/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f416c76696e393939392f5041432f73732f6465322e504e47)

![](https://camo.githubusercontent.com/fa3bb15bee5d5b38f894d925519d8d1689be182833283c49c328a723dd4cec8c/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f416c76696e393939392f5041432f73732f6465352e706e67)

***

**第二步：部署VPS服务器**

购买服务器后，需要部署一下。因为你买的是虚拟东西，而且又远在国外，我们需要一个叫Xshell的软件来远程部署。Xshell windows版下载地址：

xshell5:

[国外云盘1下载](https://d2.freessr2.xyz/Xshell_setup_wm.exe) [国外云盘2下载](https://d.dtku35.xyz/Xshell_setup_wm.exe)

**注意：如果使用xshell5的过程中提示“找不到匹配的host key算法”，可以下载更高的版本来解决，比如xshell7，可在xshell中文官方网站下载** ： [https://www.xshell.com/zh/free-for-home-school](https://www.xshell.com/zh/free-for-home-school)

如果你是Mac苹果电脑操作系统，更简单，无需下载xshell，系统可以直接连接VPS。直接打开Terminal终端，输入：ssh root@43.45.43.21（将45.45.43.21换成你的IP），之后输入你的密码就可以登录了（输入密码的时候屏幕上不会有显示）

![](https://camo.githubusercontent.com/b3c6fc9c37c0870d981bffdd0b275d7a5c8276076f229f37fc288e808405f9be/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f416c76696e393939392f706163322f4d61632e706e67)

如果不能用Mac自带的终端连接的话，直接网上搜“Mac连接SSH的软件”，有很多，然后通过软件来连接vps服务器就行，具体操作方式参考windows xshell。Mac成功连接vps后剩下的操作和windows一样。

***

部署教程：

下载windows xshell软件并安装后，打开软件

![](https://camo.githubusercontent.com/77195649ee2253d0c839214c5b66a839497650b4817e7062702bb8a665916440/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f416c76696e393939392f5041432f787368656c6c31312e706e67)

选择文件，新建

![](https://camo.githubusercontent.com/2186cff801aa6fa6bd0e3e88c83ce3fd7195176608c49035d44f0735013b5b70/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f416c76696e393939392f5041432f787368656c6c31322e706e67)

随便取个名字，然后把你的服务器ip填上

![](https://camo.githubusercontent.com/23624c056968922ccf72b57da930dbd8d564b4cfe04d5203c541836a7e16f116/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f416c76696e393939392f5041432f787368656c6c31332e706e67)

连接国外ip即服务器时，软件会先后提醒你输入用户名和密码，用户名默认都是root，密码是你购买的服务器系统的密码。

**如果xshell连不上服务器，没有弹出让你输入用户名和密码的输入框，表明你开到的ip是一个被墙的ip，遇到这种情况，重新开新的服务器，直到能用xshell连上为止，耐心点哦！如果同一个地区开了多台服务器还是不行的话，可以换其它地区。**

![](https://camo.githubusercontent.com/cbc8b7cfbc99b70b357f2b1c6a3773b743be660b651e8a20bbd8e480a5f1070a/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f416c76696e393939392f5041432f787368656c6c31342e706e67)

![](https://camo.githubusercontent.com/61ed54fd8905a905e7435997ee22553ecb8ee9d026e38af4646c45e0a6c460c4/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f416c76696e393939392f5041432f73732f787368656c6c322e706e67)

连接成功后，会出现如上图所示，之后就可以复制粘贴代码部署了。

注意：以下是安装hysteria 1脚本，教程的末尾是安装hysteria 2脚本。图文教程是安装hysteria 1。hysteria 1和2不兼容，安装hysteria 1后请使用hysteria 1相关的客户端。

***

**hysteria 1一键部署管理脚本：**

```
bash <(curl -fsSL https://git.io/hysteria.sh)
```

***

> 如果输入安装命令后提示curl: command not found，那是因为服务器系统没有自带curl命令，安装一下curl。

> CentOS系统安装curl命令：yum install -y curl

> Debian/Ubuntu系统安装curl命令：apt-get install -y curl

> 安装完成后，输入hihy可进入管理页面。脚本来自 [emptysuns/Hi\_Hysteria](https://github.com/emptysuns/Hi_Hysteria) 。

***

复制上面的 **脚本代码** 到VPS服务器里，复制代码用鼠标右键的复制，然后在vps里面右键粘贴进去，因为ctrl+c和ctrl+v无效。接着按回车键，脚本会自动安装，以后只需要运行这个快捷命令就可以出现下图的界面进行设置，快捷管理命令为：hihy

![](https://camo.githubusercontent.com/7848e6a61e27ca75a65b36d1d4b47631a0c4d2d7aeefe6479e345e7f32cfa643/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f416c76696e393939392f706163322f76756c74722f6879312e706e67)

如上图出现管理界面后， **输入数字1来安装** 。

![](https://camo.githubusercontent.com/88c4734ca36d6524e2c7233633c83bdae93e60059f9932b785aff4eb77b2abef/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f416c76696e393939392f706163322f76756c74722f6879322e706e67)

没有域名就选择数字3

![](https://camo.githubusercontent.com/4cb3fd8fc1aa0fee54555fbffead60f1fe5cdf987c0c94d1e90404b90ef0827f/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f416c76696e393939392f706163322f736f6674696d61672f68793030312e706e67)

自签证书可以输入bing.com

![](https://camo.githubusercontent.com/ed78bc502930649b26eba8130c4f47a82cc99d6099061d43bdef6943388d98f2/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f416c76696e393939392f706163322f736f6674696d61672f68793030322e706e67)

选择数字1，正确

![](https://camo.githubusercontent.com/3e596da06fa2d6e7a9a08d1cd1968c713da8dcc68f629f7ff5665fdbbede754b/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f416c76696e393939392f706163322f736f6674696d61672f68793030332e706e67)

选择数字1，udp类型

![](https://camo.githubusercontent.com/e608a8165f073a9c9ded0d6712f0197a35b84997e90b442ed9a23c1a8c6201f0/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f416c76696e393939392f706163322f736f6674696d61672f68793030342d322e706e67)

端口可以回车随机

关于是否启用端口跳跃/多端口模式，一般选择2，跳过。如果封锁严重的时候可以选择1，启用。如果启用端口跳跃/多端口模式，需要按照提示输入开始端口和结束端口。

![](https://camo.githubusercontent.com/7c0b41390a94b8098beff2c1be35e6490b6b8abfa1f1ce823aa22c03dea069d3/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f416c76696e393939392f706163322f736f6674696d61672f68793030352e706e67)

延迟、上传速度、下载速度、密码都可以用默认的配置，也可以自己修改，默认就回车

关于验证方式，一般选择1，auth\_str(默认)

![](https://camo.githubusercontent.com/b5efa53d7856d98cc6ff5fb75036206b46c852a4217c99b041c7511f50ce309e/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f416c76696e393939392f706163322f736f6674696d61672f68793030362e706e67)

关于客户端名称，默认就回车

接下来会等待几分钟，成功后会出现“安装完成，请查看下方配置详细信息”。如果失败会有相应的提示，一般解决方法就是卸载脚本后重新安装。

![](https://camo.githubusercontent.com/5a97f4d8d9079556699c1869cddbcc16c16d0a8eb7a74d4d54262824c1b7271f/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f416c76696e393939392f706163322f736f6674696d61672f68793030372e706e67)

带大括号的就是整个配置信息，需要复制下来，用鼠标右键有复制。在电脑上新建一个 **config.json** 的文件，把配置信息粘帖进去。需要 **注意** 的是： **有两行必须删除** ，不然会无法启动hysteria客户端。这两行信息是：

"acl": "acl/routes.acl",

"mmdb": "acl/Country.mmdb",

**连带标点符号一起删除。**

有了配置文件，接下来就是下载hysteria客户端。

***

【hysteria 1客户端下载及使用方法】

hysteria 1官方客户端下载地址：

根据电脑系统进行下载，电脑windows 32位系统就下载 [hysteria-windows-386.exe](https://github.com/HyNetwork/hysteria/releases/download/v1.3.5/hysteria-windows-386.exe) 64位系统可以用 [hysteria-windows-386.exe](https://github.com/HyNetwork/hysteria/releases/download/v1.3.5/hysteria-windows-386.exe) 或者 [hysteria-windows-amd64.exe](https://github.com/HyNetwork/hysteria/releases/download/v1.3.5/hysteria-windows-amd64.exe)

hysteria客户端下载好后，将config.json配置文件放在同一级目录就能启动了。

![](https://camo.githubusercontent.com/b685de73765557041c30900c329429da429d3cd95fd38626a03feee43f122164/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f416c76696e393939392f706163322f76756c74722f6879382e706e67)

启动hysteria，浏览器代理设置成和配置文件一样就行，配置文件包含http和socks5代理，http代理默认的是127.0.0.1和10809，socks5代理默认的是127.0.0.1和10808，端口号可以修改，浏览器二选一，端口号和配置文件一致。

如果按照默认来设置浏览器，可以设置成http127.0.0.1和10809 或者socks5 127.0.0.1和10808

![](https://camo.githubusercontent.com/fe7f3710e8e3dc8ab7ceb94b8ae45d034e5a453f355697410b31529703d66254/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f416c76696e393939392f706163322f76756c74722f687931302e706e67)

启动客户端后，出现connected和running字样表示启动成功。如果没有启动成功，请检查配置信息是否设置正确以及与服务器一致。

谷歌浏览器chrome可配合switchyomega插件来使用，下载插件： [switchyomega](https://github.com/atrandys/trojan/releases/download/1.0.0/SwitchyOmega_Chromium.crx)

安装插件，打开chrome，打开扩展程序，将下载的插件拖动到扩展程序页面，添加到扩展。 ![20181116000534](https://user-images.githubusercontent.com/12132898/70548725-0461d000-1bae-11ea-9d1e-4577e36ac46e.png)

完成添加，会跳转到switchyomega页面，点跳过教程，然后点击proxy，如图填写，最后点击应用选项。 ![20181116001438](https://user-images.githubusercontent.com/12132898/70548727-04fa6680-1bae-11ea-99da-568af4fd6f5f.png)

（注意：如果按照默认配置来设置，图片中的1080端口需要改为10808）

***

**常见问题及解决方法** ：

**1、搭建的账号之前能用，突然不能用了，怎么解决？**

A：如果ip不能ping通，xshell不能直接连接vps服务器，说明ip被墙了，需要换ip。vultr开通和删除服务器非常方便，新服务器即新ip，为了保证开通的新服务器ip和旧ip不一样，先开新服务器出现ip后再删旧服务器。其它大多数vps服务商换ip都要额为收费。

B: 如果ip正常，那么多半是端口号被封了，此时需要换端口号，可以重新搭建。

2、需要安装bbr加速吗？

bbr加速是tcp加速，而hysteria是Quic(udp)协议。所以不用再部署bbr加速，当然自己想部署也可以，部署bbr加速可参考其它教程。

3、如何安装hysteria 2？

Hysteria 2 继承了 Hysteria 1.x 的几乎所有功能，同时引入了各种新的修复和增强。但值得注意的是，由于协议和代码经过了重大更改，Hysteria 2 与 Hysteria 1.x 完全不兼容。 用户必须在客户端和服务器上使用一致的版本。安装Hysteria 2后客户端请使用2.0及以上版本。

***

**hysteria 2一键部署管理脚本：**

```
wget -N --no-check-certificate https://raw.githubusercontent.com/flame1ce/hysteria2-install/main/hysteria2-install-main/hy2/hysteria.sh && bash hysteria.sh
```

***

> 如果输入安装命令后提示wget: command not found，那是因为服务器系统没有自带wget命令，安装一下wget。

> CentOS系统安装curl命令：yum install -y wget

> Debian/Ubuntu系统安装curl命令：apt-get install -y wget

![](https://camo.githubusercontent.com/c87dfec6782e89244a21dd3fe81f81227c5bac1746d86e77c15996fbbdf0c337/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f416c76696e393939392f706163322f736f6674696d61672f6879322d3030312e6a7067)

输入安装脚本后，选择数字1安装程序。

![](https://camo.githubusercontent.com/1b440c9b77e644a52e4825ead76fd7abb715ec996a2b4ca6a648200e5c11baf0/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f416c76696e393939392f706163322f736f6674696d61672f6879322d3030322e6a7067)

协议证书申请方式选择1。

![](https://camo.githubusercontent.com/ba8bfb3b6ef33321bd57ec915fa37e740887ee75ff015c5b2aa8c1d54a68a667/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f416c76696e393939392f706163322f736f6674696d61672f6879322d3030332e6a7067)

端口可以自己填写想要的，也可以回车随机。

![](https://camo.githubusercontent.com/dd16476ba1d44a5233087d6cbea925d0db04826d17f3ec44690947cd722ba9c2/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f416c76696e393939392f706163322f736f6674696d61672f6879322d3030342e6a7067)

端口模式一般选择1，单端口模式。如果封锁严重的时候可以选择2，启用端口跳跃/多端口模式。如果启用端口跳跃，需要按照提示输入开始端口和结束端口。

![](https://camo.githubusercontent.com/338bd531225c50f4a5dc6c6d6cfe94328b3bf4bffb2350ab80e523ffcee26710/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f416c76696e393939392f706163322f736f6674696d61672f6879322d3030352e6a7067)

端口可以自己填写想要的，也可以回车随机。

伪装网站地址回车。

![](https://camo.githubusercontent.com/61994119f21e66dee851109d3ff0ac940f379d6b759c21f4ca7a57b316f33120/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f416c76696e393939392f706163322f736f6674696d61672f6879322d3030362e6a7067)

最后出现这一步就成功了。

![](https://camo.githubusercontent.com/9a6ac1fa82fa9eea855bd0e543fe8e75500363a8f1d0fbfb2969083b68f59b5a/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f416c76696e393939392f706163322f736f6674696d61672f6879322d3030372e6a7067)

这一部分就是客户端配置信息，可以复制下来。新建名字为config.json文件，将客户端配置信息复制进去并保存。

hysteria 2的v2.2.3版本下载： [https://github.com/apernet/hysteria/releases/download/app%2Fv2.2.3/hysteria-windows-386.exe](https://github.com/apernet/hysteria/releases/download/app%2Fv2.2.3/hysteria-windows-386.exe)

hysteria 2更新地址： [https://github.com/apernet/hysteria/releases](https://github.com/apernet/hysteria/releases)

将下载后的hysteria-windows-386.exe文件和config.json文件放在同一目录，双击运行ysteria-windows-386.exe就可以启动了。需要注意的是，脚本搭建后默认的代理端口是5678，那么浏览器代理端口也要填写socks5 127.0.0.1 5678, 当然你也可以在客户端配置信息文件修改5678端口。

![](https://camo.githubusercontent.com/0267a391ed771c15f0e60520123c3467504e62e848ef62cba849986c4ad1062f/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f416c76696e393939392f706163322f736f6674696d61672f6879322d3030382e6a7067)

***

有问题可以发邮件至海外邮箱 [rebeccalane27@gmail.com](https://github.com/Alvin9999/new-pac/wiki/)

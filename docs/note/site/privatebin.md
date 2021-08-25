![](https://privatebin.info/img/logo.png)

## 一.介绍

很多人应该都用过PasteBin(有Ubuntu PasteBin和一个就叫PasteBin的)，作为一个用于临时分享文本(当然也有很多人拿来分享代码啥的)的网站，在有些时候还是挺方便的，比如你要在论坛上发帖或者要发推啥的，然后有一段代码要贴，但是因为太长了不方便直接放，那么这个时候你就可以用到这些服务。理论上和短链接是差不多是思路(缩短内容)，只是它不是一个重定向而是直接存放你原始的内容。

好了，不说了，介绍下我们今天的主角，[PrivateBin](http://www.senra.me/tag/privatebin/)。PirvateBin是一个开源的极简风格的在线PasteBin程序，可以从Private看出其特性，那就是所有数据均是加密的，而且是在浏览器端加密，服务器对于保存的数据是无法知晓的，因而具有比较好的保密性。这个源码最早是一个ZeroBin(已经停止开发)的fork，在它的基础上PrivateBin增加了许多的功能与特性，目前已经是一个相当成熟的程序了。

在安装前，我们可以先去官网一睹为快——>[传送门](https://privatebin.net/)

![img](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/2cy/f0069d78d2ff3da095be4adeb6780c60.jpeg)

看上去还是相当棒的，而且能够加密以及阅后即焚的特性也是比较有用的，此外，自带的代码高亮，能够渲染Markdown以及需要在配置文件中开启的图片上传也是非常实用的功能。

![img](http://ucdn.senra.me/2018/04/15235524323099.jpg)

这个能对分享的内容进行讨论的功能也是蛮有意思的(~~才怪~~)

## 二.安装

好了，看完之后大概也有一个总体的印象了，那我们开始日常的安装流程吧
还是和往常一样，先来确认下环境要求

> \1. PHP版本 >= 5.4
>
> \2. 为保证加密的安全和随机性，需要满足以下条件之一:
>
> PHP版本 >= 7(自带openssl扩展)
> Libsodium和它的PHP扩展(php_libsodium)
> open_basedir配置了能够有权限访问/dev/urandom(用于生成随机数据)
> mcrypt扩展(PHP7用openssl取代了这个)
> com_dotnet扩展
>
> PS. Mcrypt需要有权限访问/dev/urandom(这意味着如果启用了open_basedir，就必须配置包含这个路径)
>
> \3. GD扩展(php_gd用于图像处理)
>
> \4. 一部分磁盘空间(默认存储数据直接用文件系统)或者一个被PDO支持的数据库(可选)
>
> \5. 有权限在安装目录以及在index.php中定义的PATH所指代的路径(额外指定路径以便提高安全性)创建文件和文件夹
>
> \6. 一个支持javascript的浏览器(加解密依赖JS，所以这是必须的)

安装的话比较简单，因为甚至可以不需要数据库，不过优化还是需要注意挺多的，后面我会提到，创建vhost我就不说了

```shell
#进入网站vhost根目录
cd /path/to/vhost/root
#下载程序并解压
wget -O PrivateBin-v1.1.1.tar.gz https://github.com/PrivateBin/PrivateBin/archive/1.1.1.tar.gz
tar xzf PrivateBin-v1.1.1.tar.gz
#将二级目录内的程序移动到网站根目录
mv PrivateBin-1.1.1/* .
mv PrivateBin-1.1.1/.htaccess.disabled .
#清理文件
rm -rf PrivateBin-1.1.1 PrivateBin-v1.1.1.tar.gz
rm -rf CHANGELOG.md INSTALL.md README.md LICENSE.md CREDITS.md
#创建程序需要的目录
mkdir data tmp
#创建配置文件
cp cfg/conf.sample.php cfg/conf.php
#修改所所有者
chown -R www:www *
```

这时候其实已经能用了，但是我们也可以做些安全方面的优化，也可以对配置做些修改

## 三.配置以及优化

\1. 修改路径

这个是把你的PHP文件以及存储目录啥的全部移到网站目录外，然后在index.php中指定目录的位置，从而提高安全性，防止某些注入漏洞和文件上传提权

```shell
#进入网站vhost根目录
cd /path/to/vhost/root
#在网站根目录的父目录创建文件夹(请确保这个路径是无法被直接访问到的)
mkdir ../privatebin
#将数据目录和PHP程序目录移动到这个目录中
mv cfg data lib tpl vendor ../privatebin/
#修改所有者，确保能被Web服务器和PHP有权限读写，另外如果开了open_basedir请配置包含此目录
chown -R www:www ../privatebin
#修改PrivateBin的index.php文件
vi index.php
#在define含有PATH那行改成类似如下的
define('PATH', '../privatebin/');
```

\2. 使用HTTPS(这就不说了)

\3. 正确的文件(夹)权限

这个的话跑一下命令就OK(自己确认路径)

```shell
#设置权限(这儿的网站路径如果你做了上面的修改路径请自己注意了)
find 网站路径 -type f -exec chmod 0640 {} \;
find 网站路径 -type d -exec chmod 0550 {} \;
find data目录路径 -type f -exec chmod 0640 {} \;
find data目录路径 -type d -exec chmod 0750 {} \;
#修改所有者
chown -R www:www 网站路径
chown -R www:www data目录路径
```

\4. 修改配置

**请参考下方的配置文件翻译**

\5. 使用robots.txt与.htaccess

默认程序包含了robots.txt，而如果网站是Apache的话请将自带的.htaccess.disabled改名为.htaccess来启用，这个是屏蔽了一些爬虫和程序的网页预览功能啥的

\6. 使用数据库代替默认的文件存储

**这部分参考配置文件翻译**

## **四.配置文件翻译**

```shell
;<?php http_response_code(403); /*
; PrivateBin 配置文件
;
; 每个选项的解释可以参考 https://github.com/PrivateBin/PrivateBin/wiki/Configuration.
; 本配置由Senra翻译
 
[main]
; (可选) 设置一个用于在网站上显示的项目名(网站名)
; name = "PrivateBin"
 
; 启用或禁用讨论功能(针对Paste内容留言讨论)，默认为true
discussion = true
 
; 预选讨论功能(是否在创建新的Paste时默认勾选开启讨论)，默认为false
opendiscussion = false
 
; 启用或禁用密码功能，默认为true
password = true
 
; 启用或禁用文件上传功能，默认false
fileupload = false
 
; (是否在创建新的Paste时默认勾选阅后即焚)，默认为false
burnafterreadingselected = false
 
; 当启用了阅后即焚的Paste被第一次访问后马上进行删除，而不是等待一次成功的解密
; 按照说明，PrivateBin默认在你浏览器成功解密后才会使用js来做一个回调以便删除Paste，这个功能将无视你是否成功解密，直接进行删除
instantburnafterreading = false
 
; 预选的默认显示模式(在创建新的Paste时默认选择的显示\渲染格式)，默认为"plaintext"(纯文本)
; 请确保这个值存在于[formatter_options]中
defaultformatter = "plaintext"
 
; (可选) 设置一种代码高亮的主题，可以在 css/prettify/ 目录中查看
; syntaxhighlightingtheme = "sons-of-obsidian"
 
; 每个Paste或者评论留言的大小限制，单位为bytes，默认是2Mb
sizelimit = 2097152
 
; 使用的模板，默认是"bootstrap" (tpl/bootstrap.php)
template = "bootstrap"
 
; (可选) 显示的提示
; notice = "Note: This is a test service: Data may be deleted anytime. Kittens will die if you abuse this service."
 
; 默认情况下PrivateBin会根据用户的浏览器设置来猜测用户使用的语言，启用该选项将使得用户能够在菜单中选择语言
; 语言的选择记录会以session cookie的形式存储在你的浏览器中，保存到你的浏览器关闭之前
languageselection = false
 
; 设置默认语言，默认为English
; 如果这个选项被设置了且上一个语言选择功能被关闭，则这将成为唯一的语言
; languagedefault = "en"
 
; (可选) 链接缩短程序的地址(API)，通过配置这个能在创建新的Paste时同时创建短链以方便使用
; 需要注意的是请选择可靠的或者是自建的短链，因为这会使得短链提供者能够获取你带有加密密钥的完整链接
; urlshortener = "https://shortener.example.com/api?link="
 
; (可选) 是用户能够一键生成一个用于分享Paste链接的二维码
; 这个会对你创建Paste以及浏览Paste的页面同时生效
; qrcode = true
 
; (可选) 使用基于IP的评论头像来区分一条评论是否是来自于一个使用了相同的用户名的不同用户是一个比较差劲的机制。
; 因为这种情况下如果服务器的salt泄露，可以通过为IP生成彩虹版的方式来碰撞获得所有非匿名的评论者的IP
; 这个选项可以被设置为 none / vizhash / identicon(默认)
; icon = none
 
; Content Security Policy(CSP)这个HTTP头允许网站限制什么内容可以在它的页面加载(用于防止插入恶意内容)
; 如果你修改模板来添加第三方域名的自定义脚本(比如追踪脚本或者使用了某些抗D服务)，你可能需要修改这个。
; 可以参考 https://content-security-policy.com/ 来配置
; 注意: 如果你使用bootstrap主题，你可以去除sandbox限制中的allow-popups
; cspheader = "default-src 'none'; manifest-src 'self'; connect-src *; form-action 'none'; script-src 'self'; style-src 'self'; font-src 'self'; img-src 'self' data:; referrer no-referrer; sandbox allow-same-origin allow-scripts allow-forms allow-popups"
 
; 和PrivateBin Alpha 0.19保持兼容，会导致降低一定的安全性
; 如果启用这项，将使用base64.js的1.7版本，而不是2.1.9版本，并且在HMAC中将使用sha1而不是sha256(用于生成删除Paste的token)
zerobincompatibility = false
 
[expire]
; 预选的过期时间(创建新的Paste时默认选择的过期时间)，请确保这个值存在于[expire_options]中
default = "1week"
 
; (可选) 克隆按钮可以在过期的Pastes中关闭，但是请注意这只是隐藏了按钮，复制和粘贴还是可能的
; clone = false
 
[expire_options]
; 为每个过期的时间段设置具体的秒数，0代表永不过期
5min = 300
10min = 600
1hour = 3600
1day = 86400
1week = 604800
; 这个一个月只有30天，所以不算准确
1month = 2592000
1year = 31536000
never = 0
 
[formatter_options]
; 设置可选的格式(用于渲染和显示)，它们的顺序和标签
plaintext = "Plain Text"
syntaxhighlighting = "Source Code"
markdown = "Markdown"
 
[traffic]
; 同一个IP的访问频率限制，单位为秒，设为0代表禁用
limit = 10
 
; (可选) 如果你的网站运行在一个反代或者负载均衡之后，设置包含用户IP的HTTP头可以将用户正确的IP传递给程序
; header = "X_FORWARDED_FOR"
 
; 存储访问频率限制的目录
dir = PATH "data"
 
[purge]
; 清除过期Paste的最小时间间隔，清除只会在创建Paste的时候触发，设为0代表每次创建都进行清除
limit = 300
 
; 清除过期Paste一次最多删除的Paste数量，设为0代表禁用清除。如果网站使用人数较多建议把这个值设置的稍微大点
batchsize = 10
 
; 存储清除频率限制的目录
dir = PATH "data"
 
[model]
; 加载的模型类(指定了把数据存哪)，以及存储用的目录
; 默认的模型"Filesystem"(文件系统)将所有数据都直接存储在文件中
class = Filesystem
[model_options]
dir = PATH "data"
 
;[model]
; 使用MySQL存储的配置示例
;class = Database
;[model_options]
;dsn = "mysql:host=localhost;dbname=privatebin;charset=UTF8"
;tbl = "privatebin_" ; table prefix
;usr = "privatebin"
;pwd = "Z3r0P4ss"
;opt[12] = true ; PDO::ATTR_PERSISTENT
 
;[model]
; 使用SQLite存储的配置示例
;class = Database
;[model_options]
;dsn = "sqlite:" PATH "data/db.sq3"
;usr = null
;pwd = null
;opt[12] = true ; PDO::ATTR_PERSISTENT
```

## 五.注意事项

\1. 配合Cloudflare等CDN使用

- 请关闭Email Obfuscation功能(邮箱混淆，防止爬虫抓取)
- 请关闭Rocket Loader功能(加速静态资源加载)
- 请取消勾选Auto Minify中的Javascript(压缩代码)

PS.如果网站在二级目录不想对根目录的其他网站关闭这些功能可以配置Page Rule

\2. 在开启流量节省的安卓chrome等浏览器上使用

- 请配置HTTPS或者关闭流量节省模式(会导致JS被压缩缓存然后功能失效)

\3. 网站服务器开启了Selinux

- 请配置Selinux规则，参考——>[传送门](https://github.com/PrivateBin/PrivateBin/wiki/Installation-on-Red-Hat-with-SELinux)

\4. 网站服务器安装了Naxsi

- 请配置Naxsi白名单，参考——>[传送门](https://github.com/PrivateBin/PrivateBin/wiki/Installation-on-Red-Hat-with-SELinux)(页面最下方)
- 也可以针对程序的域名关闭WAF

我全部配完后测试了下上传图片的功能，图片是直接由js从后端抓取到浏览器的，直接是blob类型，所以这样的话如果上传的文件较大网络又不是很好的情况下可能容易出问题，还是请注意下

![image-20210824173439783](https://cdn.jsdelivr.net/gh/love2wind/cloudimg/2cy/79daf3aacf1c447c8c9f49bb5887e7a7.png)

[PrivateBin——搭建你的在线私密剪贴板(开源版PasteBin)](http://www.senra.me/deploy-your-private-online-clipboard-using-privatebin/)


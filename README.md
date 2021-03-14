# Fastadmin Shopro 从零部署，搭建过程

## 介绍
主要是记录一下部署流程，以便后续需要重新部署的时候快速部署不用踩坑，如果部署中有新坑可咨询作者QQ3104710541，记录常见问题我会第一时间进行修改补充

## 环境
* Linux CentOS 7.2
* 宝塔面板
* php 7.2
* nginx 1.18
* mysql 5.7
* redis 5.0
* supervisor

## 安装

### 宝塔面板
打开`宝塔`官方网站，选择安装 `linux` 版

![图片.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c6f4e9d4e39f49f6a9d12e956f30e3c2~tplv-k3u1fbpfcp-watermark.image)

![图片.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a2ca4906f5094813aa4e65dfc7093c47~tplv-k3u1fbpfcp-watermark.image)

### 部署站点

##### 1. 创建站点
![图片.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c5b049e30a8840868beb087c90e2183c~tplv-k3u1fbpfcp-watermark.image)

##### 2. 设置站点
* 解析域名，并指向服务器 ip
* 设置 ssl 证书 请务必配置
* 设置伪静态和跨域, [点此](https://doc.fastadmin.net/shopro/228.html#toc-7)

##### 3. fastadmin安装
* 将`fastadmin`完整包`zip`上传到站点目录
* 解压
* 删除`zip`包

![图片.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/51d5c4faf2334d318fac877247da41e0~tplv-k3u1fbpfcp-watermark.image)


##### 4. 配置站点运行目录

![图片.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/706d9a1c5f0342c7b702655d95756a38~tplv-k3u1fbpfcp-watermark.image)


##### 5. 开始安装`fastadmin`

> 访问 `http://{域名}/install.php`, 设置好数据库账号密码, 管理员账号密码


##### 6. 配置站点`ssl`证书

![图片.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/427477789f784018be89385c6cc7e9ad~tplv-k3u1fbpfcp-watermark.image)


### 7. 安装`shopro`插件

> 开发环境下打开`debug`随时定位问题


![图片.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/78301ac4d5864156be941d3370d25d71~tplv-k3u1fbpfcp-watermark.image)


##### 1. 进入后台管理-插件管理-安装shopro

![图片.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/64b2dbf078c74cf1b60e3001e543259c~tplv-k3u1fbpfcp-watermark.image)


##### 2. 安装新版PHP微信扩展包
```
$ composer remove overtrue/wechat
$ composer require "overtrue/wechat:^4.2" -vvv
$ composer update
```

##### 3. 商城配置
根据官方文档配置，[点此](https://doc.fastadmin.net/shopro/229.html)

### 前端部署

##### 1. 安装`HbuilderX`

##### 2. 下载前端代码包到本地


![图片.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/524c0cd7821f473a8f343ce7b737f5c6~tplv-k3u1fbpfcp-watermark.image)

##### 3. 在 `HbuilderX` 打开

![图片.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/825b50c59ac64f2cb5f5f710f61ac58e~tplv-k3u1fbpfcp-watermark.image)

##### 4. 点击顶部菜单运行->运行到浏览器-> chrome 【H5 运行为例】

![图片.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/950d1e308f624f7f8753101446a03190~tplv-k3u1fbpfcp-watermark.image)

> 此问题是未安装前端依赖包

使用 `HbuilderX` 终端（或者任意熟悉的终端，需要进入前端代码目录）， 执行 `npm install`

![图片.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f4c121ec05d1427cac3b79cad6f9ce38~tplv-k3u1fbpfcp-watermark.image)

执行 `npm install` ,结果如下即为成功：

![图片.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/8f699f52ab5f4acfa367cdfe21a0b2b6~tplv-k3u1fbpfcp-watermark.image)


##### 5. 再次运行到浏览器

> 又报错了


![图片.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/56d9a08c84e943699d03a3ba08273f92~tplv-k3u1fbpfcp-watermark.image)


根据提示找到对应的插件，进行安装 工具 -> 插件安装

![图片.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/7aaeb0258e8d48a4ac561a087795da3e~tplv-k3u1fbpfcp-watermark.image)

再次运行

![图片.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b78d435ba5064333b8f271462dc44f61~tplv-k3u1fbpfcp-watermark.image)

##### 6. 修改配置文件`env.js`, 替换域名

![图片.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a0c02d00ed9d4d09a4cd1d53ff0a22b6~tplv-k3u1fbpfcp-watermark.image)

至此，如果上面`伪静态`，`跨域`，`SSL` 配置没有问题，就能看到正常的商城页面了


### 分享海报设置-H5

> 生成海报前, 设置 后台 -> 商城配置 -> 商城信息 -> 分享


![图片.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/43f229e9117d4909adfd491500fe77b2~tplv-k3u1fbpfcp-watermark.image)

![图片.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/bbafaad544134414931b459ae566bc87~tplv-k3u1fbpfcp-watermark.image)


![图片.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/febb1229544a40cfa1daed67d58eefc0~tplv-k3u1fbpfcp-watermark.image)

### 分享海报设置-小程序

> 生成海报请先确保小程序发布过至少一版，否则服务端会报 /pages/index/index 页面路径无效 41030invalid page hint: [zEDCRb0gE-Nr333a]

1. 配置小程序 `appid`

![图片.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ac19658c8a2d44fcbc084ceea4bf295b~tplv-k3u1fbpfcp-watermark.image)

2. 下载小程序开发工具

> 小程序开发工具 -> 设置 -> 安全设置 -> 安全 -> 服务端口 -> 开启

![图片.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/49106de477994dbd8431489e44915b78~tplv-k3u1fbpfcp-watermark.image)


![图片.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f59a7f7d12d64555944e9c9f2d909222~tplv-k3u1fbpfcp-watermark.image)

> 保证商城配置正确：商城配置 -> 平台配置 -> 小程序配置


![图片.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c805384d034341288d4372f00e5890c5~tplv-k3u1fbpfcp-watermark.image)


到这里还没有完，当使用手机预览的时候发现海报无法生成，甚至连首页也出不来（开发工具能出来是因为开发工具有个选项 不校验域名合法性 ），这是因为，后端的域名和海报图片地址都需要添加到小程序允许的服务器域名中

> 小程序后台 -> 开发 -> 开发设置 -> 服务器域名

```
api 域名    // 后端 api 接口域名，请部署 `https`
api.7wpp.com      // 后台默认的海报背景的域名
wx.qlogo.cn         // 微信授权登录的头像地址
shopro-1253949872.image.myqcloud.com      // 商城演示商品图片地址
```



### redis队列

> 提高系统性能，活动可靠性，系统引入了 队列 和 redis 缓存

##### 1. 下单试试

> 此报错为未安装 队列插件，队列 和 redis 配置文档已经很详细了，请移步按照文档进行配置，[点此](https://doc.fastadmin.net/shopro/239.html)

![图片.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d7f4c152ef4c4e49b39c16d21846d585~tplv-k3u1fbpfcp-watermark.image)

##### 配好队列，加上余额，使用余额付款，一切正常的话，就能看到订单支付成功啦！！！


### 上线

> 前提已经走过上面开发过程，env appid 等已经正常设置

#### 1. H5

前端请单独部署，不要和后端接口使用一个站点，[点此](https://ask.fastadmin.net/question/20393.html)


![图片.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/28703edbea93482bb03f32c2f5232992~tplv-k3u1fbpfcp-watermark.image)


![图片.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/3b94cfd2493548588f032fcdb0132cb0~tplv-k3u1fbpfcp-watermark.image)

> SSL，请参考上面后端的进行设置 请务必配置


打包前端

![图片.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a57ed888db1743aa980740a9c76f5c49~tplv-k3u1fbpfcp-watermark.image)


![图片.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/3347f356a35d41f480403d8b8a4b265a~tplv-k3u1fbpfcp-watermark.image)


![图片.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/8bf4f813ca3e41db9b966b52bb810461~tplv-k3u1fbpfcp-watermark.image)


将两个文件上传到宝塔前端站点根目录


![图片.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/8e577ac5438f4891b1d7f2f57c8d9185~tplv-k3u1fbpfcp-watermark.image)

访问前端网址，至此 H5 前端部署完成


### 小程序端

> 注意不要运行模式下的代码提交小程序审核, 点击 发行 -> 小程序 -> 微信


![图片.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/4a9b506418254b8285aca005e43612a0~tplv-k3u1fbpfcp-watermark.image)


![图片.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/88480326a06b4508be6fa659068855a9~tplv-k3u1fbpfcp-watermark.image)


![图片.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/dc507a6188164d80a22e1d8f9de8cdc6~tplv-k3u1fbpfcp-watermark.image)



## 常见问题

### 1. 部分用户接口出现 EventDispatcher not found


![图片.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ede89e4adbf442eca0e28d5007e428ba~tplv-k3u1fbpfcp-watermark.image)

这是 php 和 overtrue/wechat 某个版本才会出现的问题，导致 symfony/event-dispatcher 扩展包被移除

解决办法：
```
$ composer require symfony/event-dispatcher:^4.3 -vvv
```

### 2. 新添加订单，支付页提示订单不存在

请检查队列配置文件 application/extra/queue.php 的 connector 配置是否是 redis【推荐】 或者 database，如果不是（Sync）, [点此](https://doc.fastadmin.net/shopro/239.html)

### 3. 拼团开团支付成功，跳转我的拼团不显示
* 因为支付成功之后采用异步队列进行执行，可能会存在短暂延迟
    * 首先稍微等待一下，60秒之内，刷新我的拼团页面，看是否能显示出来
    * 如果长时间还是未出来，确定队列监听是否正常，配置在[这里](https://doc.fastadmin.net/shopro/239.html)
    
    
### 4. 微信公众号登录提示 redirect_uri 域名与后台配置不一致

![图片.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b3ea3bce650a40a884c4360e0674a1b6~tplv-k3u1fbpfcp-watermark.image)

请在微信公众号后台 开发-> 接口权限 -> 网页服务 ->网页授权 设置网页授权回调域名为后台 api 的域名，别忘了配置 ip 白名单

### 5. 权限不足 Permission denied

![图片.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e2e795e287064ecdaf46969d1751ada1~tplv-k3u1fbpfcp-watermark.image)

首先检查 supervisor 守护进程执行用户是否是和 php-fpm 执行用户一直，宝塔是 www，如果不一致请修改为 www

![图片.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/02a22f4b192f40a99c90f63a17204fff~tplv-k3u1fbpfcp-watermark.image)

修改整个后端目录所属用户为 www


![图片.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/4e2a910eddc34ffbb2e323796d063257~tplv-k3u1fbpfcp-watermark.image)

### 6. 短信验证码无法发送
* 请安装阿里云短信插件
* 在阿里云申请短信模板
* 在现有默认模板基础再增加 mobilelogin 的短信模板

![图片.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/0553ec3c34b84b988256ffdc1a11d42e~tplv-k3u1fbpfcp-watermark.image)

### 7. 个人中心等级图标不显示

> 参考[点此](https://doc.fastadmin.net/shopro/230.html)

![图片.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/2af412ededc54177966f7b9bde6f712b~tplv-k3u1fbpfcp-watermark.image)


### 8. 部分接口请求报错

cURL error 60: SSL certificate problem: unable to get local issuer certificate (see https://curl.haxx.se/libcurl/c/libcurl-errors.html)

可能错误原因:
* 第一在本地部署的测试环境
* 第二未配置域名SSL 证书

```
下载 cacert.pem 证书
https://curl.haxx.se/ca/cacert.pem

编辑当前系统php 配置文件 php.ini

[curl]
; A default value for the CURLOPT_CAINFO option. This is required to be an
; absolute path.
curl.cainfo = 刚才下载的 cacert 的放置的绝对地址/cacert.pem

重启 php-fpm，重启 nginx
```

### 如果安装中有问题可以咨询一下作者QQ3104710541,我会第一时间进行修改补充

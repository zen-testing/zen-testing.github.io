---
title: 'Snapd设置代理'
date: 2022-09-26 18:51:33
tags: [Proxy]
published: true
hideInList: false
feature: https://s1.ax1x.com/2022/09/04/vofoRO.jpg
isTop: false
---

>Snap,全称SnapCraft,是一个全新的应用软件环境.在Snap中,软件被封装在类似于Docker的容器中,即开即用,可随时获取,这一切由其后台服务snapd提供支持.Ubuntu从18.04开始,就引入它作为系统的一部分,而其他的Linux发行版(如Deepin)也可以通过软件管理工具进行安装(如sudo apt install snapd).

>SnapCraft将软件包分发在自己的服务器上.然而,因为众所周知的原因,访问位于海外的Snap服务器异常缓慢,不加代理的情况下,下载速度会持续降到十几KB每秒.这使得我们不得不想办法通过代理服务器进行加速.

>一般地,Linux上的一些应用程序会通过读取环境变量http_proxy和https_proxy来应用代理服务器设置,典型的有Chrome.然而,Snap比较特别,它不会从环境变量中上述环境变量中读取代理服务器设置,因此直接使用export http_proxy=[代理服务器地址]或export https_proxy=[代理服务器地址]是不起作用的.

那么,有何正确的方法?

# 更改`/etc/environment`

`/etc/environment`是一个Shell脚本,snapd会读取它,应用其中指定的配置信息.因此,设置代理服务器的正确目标,实际上就是这里

```shell
$ sudo vim /etc/environment

http_proxy=http://[服务器地址]:[端口号]
https_proxy=http://[服务器地址]:[端口号]

$ sudo systemctl restart snapd
```

# 覆盖snapd的现有设置

```shell
$ sudo systemctl edit snapd.service

[Service]
Environment=http_proxy=http://proxy:port
Environment=https_proxy=http://proxy:port

$ sudo systemctl daemon-reload
$ sudo systemctl restart snapd.service
```

# 注意事项

一般的本地代理都不支持HTTPS,所以https_proxy的值也只能是http地址,否则会出现如下错误
```shell
cannot install "conjure-up": Post https://api.snapcraft.io/v2/snaps/refresh: proxyconnect tcp: EOF
```
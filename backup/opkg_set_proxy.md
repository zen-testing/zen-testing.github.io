---
title: 'openWrt设置代理'
date: 2023-01-14 23:04:58
tags: [Proxy]
published: true
hideInList: false
feature: 
isTop: false
---
![世界触手可及](https://raw.githubusercontent.com/zhangyiming748/AVIF-Repository/master/%E5%B0%81%E9%9D%A2%E5%9B%BE/%E4%B8%96%E7%95%8C%E8%A7%A6%E6%89%8B%E5%8F%AF%E5%8F%8A.avif)
<!-- more -->
假设本机IP为`192.168.1.10`代理的端口为`7890`
确认本机与openwrt路由器在同一局域网下
```shell
echo "option http_proxy http://192.168.0.192:7890" >> /etc/opkg.conf
```
然后更新软件包列表
`opkg update`
安装相应的软件
`opkg install xxx`
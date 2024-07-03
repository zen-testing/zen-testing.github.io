---
title: 'homebrew设置代理'
date: 2022-09-26 17:04:33
tags: [Proxy]
published: true
hideInList: false
feature: 
isTop: false
---
brew用curl下载,所以给curl挂上代理即可
在`~/.curlrc`文件中输入代理地址
```shell
socks5 = "127.0.0.1:1089"
```
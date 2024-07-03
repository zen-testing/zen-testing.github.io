---
title: 'go get 设置临时代理'
date: 2022-11-08 13:20:53
tags: [Proxy,Golang]
published: true
hideInList: false
feature: 
isTop: false
---
![世界触手可及](https://s1.ax1x.com/2022/09/04/vofoRO.jpg)

<!-- more -->

# 临时命令

```shell
$ http_proxy=http://127.0.0.1:1081/ https_proxy=http://127.0.0.1:1081/ no_proxy=localhost,127.0.0.0/8,::1 go get xxx
```

# 设置别名

```shell
$ alias goproxy='http_proxy=http://127.0.0.1:1081/ https_proxy=http://127.0.0.1:1081/ no_proxy=localhost,127.0.0.0/8,::1 go'
```

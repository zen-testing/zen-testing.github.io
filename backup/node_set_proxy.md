---
title: 'Node.js设置代理'
date: 2022-09-26 19:01:16
tags: [Proxy]
published: true
hideInList: false
feature: https://s1.ax1x.com/2022/09/04/vofoRO.jpg
isTop: false
---

```shell
export NODE_MIRROR=https://mirrors.tuna.tsinghua.edu.cn/nodejs-release/
```

或

```shell
$ npm config set proxy http://proxy.company.com:8080
$ npm config set https-proxy http://proxy.company.com:8080
```
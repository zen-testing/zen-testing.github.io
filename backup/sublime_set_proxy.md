---
title: 'Sublime设置ss代理'
date: 2022-09-26 18:55:22
tags: [Proxy]
published: true
hideInList: false
feature: https://s1.ax1x.com/2022/09/04/vofoRO.jpg
isTop: false
---
Sublime设置http/https代理
Preference -> Package Setting -> Package Control -> Setting-User添加以下设置
```
"http_proxy": "socks5://127.0.0.1:1080",
"https_proxy": "socks5://127.0.0.1:1080",
```
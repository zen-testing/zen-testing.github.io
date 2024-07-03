---
title: 'Git设置代理'
date: 2022-09-26 16:44:07
tags: [Proxy]
published: true
hideInList: false
feature: 
isTop: false
---

# http
git config --global http.proxy "http://127.0.0.1:8889"
git config --global https.proxy "http://127.0.0.1:8889"
# socks5
git config --global http.proxy "socks5://127.0.0.1:1080"
git config --global https.proxy "socks5://127.0.0.1:1080"
# 取消设置
git config --global --unset http.proxy
git config --global --unset https.proxy
# git vim ~/.ssh/config
```
# 必须是 github.com
Host github.com
HostName github.com
User git
# 走 HTTP 代理
# ProxyCommand socat - PROXY:127.0.0.1:%h:%p,proxyport=8889
# 走 socks5 代理(如 Shadowsocks)
# ProxyCommand nc -v -x 127.0.0.1:1089 %h %p
```

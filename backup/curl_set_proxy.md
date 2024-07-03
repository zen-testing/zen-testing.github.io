---
title: 'curl设置代理'
date: 2022-11-02 23:10:10
tags: [Proxy]
published: true
hideInList: false
feature: 
isTop: false
---
![世界触手可及](https://s1.ax1x.com/2022/09/04/vofoRO.jpg)
<!-- more -->

# 使用参数
```shell
curl -x socks5://127.0.0.1:1024 http://www.google.com # -x 参数等同于 --proxy
```
# 设置配置文件

```shell
# 修改curl配置文件
vim ~/.curlrc
# 写入
socks5 = "127.0.0.1:1024"

# 如果临时不需要代理使用以下参数
curl --noproxy "*" http://www.google.com
```

# 设置linux全局代理配置

```shell
# 修改shell配置文件 ~/.bashrc ~/.zshrc等
export http_proxy=socks5://127.0.0.1:1024
export https_proxy=$http_proxy

# 设置setproxy和unsetproxy 可以快捷的开关
# 需要时先输入命令 setproxy
# 不需要时输入命令 unsetproxy
alias setproxy="export http_proxy=socks5://127.0.0.1:1024; export https_proxy=$http_proxy; echo 'HTTP Proxy on';"
alias unsetproxy="unset http_proxy; unset https_proxy; echo 'HTTP Proxy off';"
```
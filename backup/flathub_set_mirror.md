---
title: 'flathub更换国内源'
date: 2023-01-03 20:01:56
tags: [Proxy]
published: true
hideInList: false
feature: 
isTop: false
---
# 上海交通大学镜像
Flathub 镜像是 flathub.org 的智能缓存。当您请求镜像中的资源时， 如果文件没有被镜像服务器缓存，我们会将您重定向回原站，并在后台进行缓存。 目前镜像服务器上已经预先缓存了所有 Flathub 软件的分支。

使用方法
```shell
$ sudo flatpak remote-modify flathub --url=https://mirror.sjtu.edu.cn/flathub
```
如果出现错误可尝试
```shell
$ wget https://mirror.sjtu.edu.cn/flathub/flathub.gpg
$ sudo flatpak remote-modify --gpg-import=flathub.gpg flathub
```

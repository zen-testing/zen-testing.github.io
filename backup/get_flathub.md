---
title: '安装flathub并更换国内源'
date: 2022-09-26 17:14:51
tags: [Linux]
published: true
hideInList: false
feature: 
isTop: false
---
```shell
$ sudo apt-get install flatpak

$ flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
$ flatpak remote-modify flathub --url=https://mirror.sjtu.edu.cn/flathub

# 或者
$ flatpak remote-add --if-not-exists sjtu  https://mirror.sjtu.edu.cn/flathub/flathub.flatpakrepo
```
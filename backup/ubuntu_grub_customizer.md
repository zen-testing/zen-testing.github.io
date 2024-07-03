---
title: 'Ubuntu22.04安装Grub-Customizer'
date: 2022-09-26 19:23:49
tags: [Linux,Ubuntu]
published: true
hideInList: false
feature: 
isTop: false
---

目前 Grub-Customizer 没有进入 Ubuntu 的主仓库,可以通过添加 PPA 安装

<!-- more -->

```shell
$ sudo add-apt-repository ppa:trebelnik-stefina/grub-customizer
$ sudo apt update
$ sudo apt install grub-customizer
```
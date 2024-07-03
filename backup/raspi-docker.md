---
title: '树莓派4安装docker'
date: 2022-09-26 18:20:51
tags: [Raspberry]
published: true
hideInList: false
feature: 
isTop: false
---
性感荷官,在线教你安装docker

<!-- more -->

## Docker在线安装

```shell
#官方脚本:会自动检测当前的系统和版本后,安装docker,只需要在联网情况下,耐心等待
sudo curl -fsSL https://get.docker.com | sh

#或者这样安装
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo apt-get update

#查找可用版本
apt-cache madison docker-ce

#安装最新版本
sudo apt-get install docker-ce

#安装指定版本
sudo apt install docker-ce=5:19.03.1~3-0~raspbian-buster

#查看docker版本
docker version

#查看docker信息
docker info
```

## 配置Docker开机自启动服务

```shell
#启动Docker
systemctl start docker

#查看docker启动状态
systemctl status docker

#查看启动中的容器
docker ps

#设置开机自启动
systemctl enable docker.service

#查看docker开机启动状态 enabled:开启, disabled:关闭
systemctl is-enabled docker.service
```
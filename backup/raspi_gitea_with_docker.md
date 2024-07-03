---
title: '树莓派4安装Gitea(Docker实现)'
date: 2022-09-26 18:24:07
tags: [Raspberry,Docker,Gitea]
published: true
hideInList: false
feature: 
isTop: false
---
性感荷官,在线教你在docker上部署gitea

<!-- more -->
# 准备
新建`docker-compose.yml`文件内容如下
```yml
version: "3"

networks:
  gitea:
    external: false

services:
  server:
    image: gitea/gitea:1.18.1
    container_name: gitea
    environment:
      - USER_UID=1000
      - USER_GID=1000
    restart: always
    networks:
      - gitea
    volumes:
      - ./gitea:/data
      - /etc/timezone:/etc/timezone:ro
      - /etc/localtime:/etc/localtime:ro
    ports:
      - "3000:3000"
      - "222:22"
```
# 安装
```shell
$ sudo curl -L "https://github.com/docker/compose/releases/download/v2.2.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
https://github.com/docker/compose/releases
```
其中`v2.2.2`可以更换成最后一个发行版
[代码仓库](https://github.com/docker/compose/releases)
运行
```shell
# 运行
$ sudo docker-compose up -d
```
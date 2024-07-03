---
title: 'docker image 设置代理'
date: 2022-09-26 16:09:53
tags: [Proxy]
published: true
hideInList: false
feature: 
isTop: false
---

```shell
$ sudo mkdir -p /etc/systemd/system/docker.service.d
$ sudo nano /etc/systemd/system/docker.service.d/http-proxy.conf
```
文件内容

```shell
[Service]
Environment="HTTP_PROXY=http://USER:PASSWD@SERVER:PORT/"
Environment="HTTPS_PROXY=http://USER:PASSWD@SERVER:PORT/"
```

保存后重启服务

```shell
$ sudo systemctl daemon-reload
$ sudo systemctl restart docker
```
或者更换为国内源
```shell
"experimental": true,
"debug": true,
"registry-mirrors": ["https://registry.docker-cn.com","https://docker.mirrors.ustc.edu.cn","https://docker.mirrors.ustc.edu.cn"]
```

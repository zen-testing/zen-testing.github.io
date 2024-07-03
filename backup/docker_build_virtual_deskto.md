---
title: 'docker搭建虚拟桌面'
date: 2024-03-01 22:09:44
tags: [Docker]
published: true
hideInList: false
feature: 
isTop: false
---
![](https://imgse.com/i/pFCmkH1)

```shell
version: '3.5'

services:
    ubuntu-xfce-vnc:
        container_name: xfce
        image: imlala/ubuntu-xfce-vnc-novnc:latest
        shm_size: "1gb"
        ports:
            - 5900:5900
            - 6080:6080
        environment: 
            - VNC_PASSWD=imlala
            - GEOMETRY=1280x720
            - DEPTH=24
        volumes: 
            - ./Downloads:/root/Downloads
            - ./Documents:/root/Documents
            - ./Pictures:/root/Pictures
            - ./Videos:/root/Videos
            - ./Music:/root/Music
        restart: unless-stopped
```
```bash
docker run --name xfce -d --shm-size 1gb -p 5900:5900 -p 6080:6080 -e VNC_PASSWD=imlala -e GEOMETRY=1280x720 
```
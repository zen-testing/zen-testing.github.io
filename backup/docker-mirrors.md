---
title: '时至今日还可以用的docker镜像源'
date: 2023-11-07 09:24:59
tags: [Docker]
published: true
hideInList: false
feature: 
isTop: false
---
```json
# /etc/docker/daemon.json
{
    "builder": {
        "gc": {
            "defaultKeepStorage": "20GB",
            "enabled": true
        }
    },
    "experimental": false,
    "registry-mirrors": [
        "https://mirror.baidubce.com"
    ]
}
```
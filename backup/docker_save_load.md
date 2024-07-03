---
title: 'docker save load'
date: 2024-04-03 23:06:49
tags: [Docker]
published: true
hideInList: false
feature: 
isTop: false
---
```bash
docker save -o my_image.tar my_image:latest
docker save REPOSITORY | xz > REPOSITORY.tar.xz
```
 
 ```bash
 docker load -i my_image.tar
xz -d -k < REPOSITORY.tar.xz | docker load
```
---
title: '5分钟学会用Docker常用命令'
date: 2023-11-23 17:20:46
tags: [五分钟已经很棒了]
published: true
hideInList: false
feature: 
isTop: false
---
```bash
# 展示版本号
docker -v
docker version
# 查找镜像
docker search hello-world
# 拉取镜像
docker pull hello-world
# 查看本地镜像
docker images
# 删除本地镜像
docker rmi hello-world
# 导出已经下载的镜像
docker save <image id> > hello.tar
docker save <R:T> > hello.tar
# 导入已经下载的镜像
docker load < hello.tar
# 查看全部容器
docker ps -a
# 进入容器
docker -it <name> #!/bin/sh
# 查看容器标准输出
docker logs <name> --tail 20 -f
# 复制文件到容器
docker cp file container:dir
docker cp container:dir file
-a 带权限

```

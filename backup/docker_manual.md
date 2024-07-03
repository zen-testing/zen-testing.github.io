---
title: 'docker从入门到删库跑路'
date: 2024-04-30 23:23:46
tags: [Docker,收费教程]
published: true
hideInList: false
feature: 
isTop: false
---
# 1.docker 概念介绍

## 为什么使用docker
使用docker，可以帮助我们快速在一台全新的机器上部署我们的应用。
### 没有使用docker之前
如果需要部署一个web项目，则需要在目标机器上面安装redis，mysql，rabbitmq,memcahe等组件，而且安装过程并不会很顺利，因为不是缺这个库就是缺那个依赖，所以部署一个应用是非常麻烦的；而且如果你需要再部署一套新的环境，又得重新做这些操作...这让开发和运维就会一直抱怨。
### 使用docker后
需要什么环境，只需要做出一份镜像，然后这个镜像里面会包含你所需要的环境，如果需要重新部署一套，则只用基于这个镜像，启动容器，然后把自己的项目丢进去，就可以了，不需要经历以前那种重复且无聊的工作。
## 镜像
镜像类似于咱们装操作系统使用的镜像，就像win10.iso、win8.iso、win7.iso...
这些镜像都是只读的，但是我们可以基于这些镜像制作出新的镜像。
## 容器
容器就相当于我们使用的操作系统，我们根据指定的镜像，然后安装了对应的操作系统，也就是我们的容器
## 仓库
仓库是用来集中存放镜像的地方，可以比作咱们的Maven仓库，这里会对所有镜像进行统一的管理
## 一图搞懂关系
[![pkFOgG8.png](https://s21.ax1x.com/2024/05/01/pkFOgG8.png)](https://imgse.com/i/pkFOgG8)
[![pkFOcPf.png](https://s21.ax1x.com/2024/05/01/pkFOcPf.png)](https://imgse.com/i/pkFOcPf)

# 2.docker 安装及配置
**以下内容(第二节)都当做放屁好了,安装就乖乖使用官方的方法,别把时间浪费在这里**
## 环境
操作系统：Ubuntu20
## 安装docker
### 更新apt仓库
```
apt-get update
```
### 安装docker
```
apt install -y docker.io
```
### 验证docker是否安装成功
```
docker version
```
[![pkFOIZn.md.png](https://s21.ax1x.com/2024/05/01/pkFOIZn.md.png)](https://imgse.com/i/pkFOIZn)
## 安装docker-compose（可选）
### 安装docker-compose
```
apt install -y docker-compose
```
### 验证是否安装成功
```
docker-compose version
```
[![pkFO4qs.md.png](https://s21.ax1x.com/2024/05/01/pkFO4qs.md.png)](https://imgse.com/i/pkFO4qs)
## 配置镜像加速
### 编辑配置文件
```
vim /etc/docker/daemon.json


{
"registry-mirrors": [
"https://docker.mirrors.ustc.edu.cn",
"https://hub-mirror.c.163.com/"]
}
```
### 重启docker服务
```
systemctl reload docker
systemctl restart docker
```
### 查看docker 镜像仓库地址是否更新
```
docker info
```
[![pkFOoaq.md.png](https://s21.ax1x.com/2024/05/01/pkFOoaq.md.png)](https://imgse.com/i/pkFOoaq)

# 3.docker 镜像操作

## 拉取镜像
### 命令
```
docker pull 镜像名称:Tag
```
### 样例
```
docker pull ubuntu
docker run ubuntu /bin/echo "Hello world,My name is "
```
## 查看镜像信息
### 列出所有镜像
####  命令
```
docker images
```
[![pkFObGT.md.png](https://s21.ax1x.com/2024/05/01/pkFObGT.md.png)](https://imgse.com/i/pkFObGT)
#### 字段解释

- REPOSITORY：来自于哪个仓库
- TAG：镜像的标签信息，类似于Maven的打tag
- IMAGE ID：代表镜像的唯一标识，如果两个镜像id相同，则有可能他们指向同一个镜像，只是标签不同
- CREATED：镜像最后的更新时间
- SIZE：镜像大小
#### 子命令
```
# 列出所有镜像，包括临时文件	
docker images -a
# 列出镜像摘要
docker images --digests=true
# 查看更多子命令
man docker-images
```
### 打标签
#### 命令
```
docker tag 镜像名称:tag 自定义的标签
```
#### 样例
```
docker tag ubuntu:latest myubuntu:1.0.0
```
### 查看详细信息
```
docker inspect ubuntu:latest
```
## 搜索镜像
```
docker search ubuntu
```
### 搜索官方镜像
```
docker search --filter=is-official=true ubuntu
```
### 搜索start>4的镜像
```
docker search --filter=stars=4 ubuntu
```
## 清除/删除 镜像
### 按标签删除
```
docker rmi ubuntu:latest
```
### 按镜像ID删除
```
docker images
docker rmi ba6acccedd29
```
### 清理镜像
```
docker image prune
```
## 创建镜像
### 基于已有容器创建
```
docker commit -m '提交日志' -a '作者信息' 容器ID 自定义的镜像名称
```
#### 样例
```
# 进入容器
docker run -it ubuntu:latest /bin/bash
# 创建新文件 并追加内容
echo 'test commit' > lglbc.txt
exit
# 下载
# 创建镜像
docker commit -m '第一次提交' -a '乐哥聊编程' 6918e5c0e454 lglbc:1.0.0
```
### 基于本地模版导入
```
docker [image] i mport [OPTIONS] filelURLl -[REPOSITORY
[:TAG] ]
```
#### 样例
```
# 下载ubuntu模版
wget https://download.openvz.org/template/precreated/contrib/ubuntu-6.06-i386-minimal.tar.gz
# 导入镜像
cat ubuntu-6.06-i386-minimal.tar.gz | docker import - ubuntu:6.06
```
### 基于docker file创建
```
FROM ubuntu:latest
LABEL version='1.0.0' maintainer= 'docker user lglbc@https://gitee.com/lglbc'
RUN echo 'test docker file' > docker.txt
```
```
docker build . -t lglbc:dockerfile
docker exec -it lglbc:dockerfile /bin/bash
cat docker.txt
```
## 导入/导出镜像
### 导出
```
docker save -o ubuntu.latest.tar ubuntu:latest
```
### 导入
```
docker load -i[<] ubuntu.latest.tar
```

# 4.docker 容器操作

## 创建容器
### 新建容器
```
docker create -it 镜像名称
```
### 启动容器
```
docker start 容器ID
```
### 新建并启动容器
```
docker run [-it] 镜像名称
```
### 后台运行
```
docker run -d 镜像名称
```
### 查看容器控制台日志
```
docker logs [-f] 容器id
```
## 停止容器
### 暂停容器
```
docker pause 容器id
```
### 终止容器
```
docker stop 容器id
```
## 进入容器
### attach
```
docker attach 容器ID
# 多个窗口attach 同一个容器，所有窗口同步显示
```
### exec
```
docker exec -it 容器ID /bin/bash
```
## 删除容器
```
docker rm 删除不在运行的容器
docker rm -f 容器ID（发送一个sigkill信号给容器，后强行删除）
```
## 查看容器
```
# 查看容器信息
docker inspect 容器ID
# 查看容器内进程
docker top 容器ID
# 查看统计信息
docker stats 容器ID

```
## 高级命令
### 复制本地文件到容器
```
docker cp 本地目录 容器ID:/容器目录
```
### 查看容器内数据的变更
```
docker diff 容器ID
```
### 查看端口映射
```
docker port 容器ID	
```
### 更新配置
```
docker update --restart=always/no 容器ID
```

## 5.搭建私有仓库

## 安装私有仓库
```
docker run -d -p 5000:5000 registry:2
```
## 打标签
```
docker tag 镜像名称:标签 仓库地址:仓库端口/镜像名称[:标签]
```
## 推送镜像到仓库
```
docker push 仓库地址:仓库端口/镜像名称[:标签]
```
## 查看仓库包含的镜像
```
curl http://仓库地址:仓库端口/v2/_catalog
```
## 从私有仓库拉取镜像
```
docker pull 仓库地址:仓库端口/镜像名称[:标签]
```
## 从其他机器拉取
### 修改配置，允许http响应
在客户端机器执行
```
vim /etc/docker/daemon.json

{
"insecure-registries": ["192.168.64.3:5000"]
}

systemctl daemon-reload && systemctl restart docker
```
### 拉取镜像
```
docker pull 192.168.64.3:5000/test
```
# 6.docker数据持久化

## 为什么要做持久化
因为在每个容器在运行过程中的数据，默认都会存储在容器内部，如果将容器删除，重新跑一个新的容器，数据就会丢失，如果是一些无关紧要的日志类数据丢失，那倒无所谓，如果是一些产生的业务数据，那么我就务必需要保存这些数据。

## 怎么去做持久话呢？
其实很简单 ，只需要一个命令即可
### 命令
```
docker run -d  -v 本机绝对路径:容器内部路径 镜像名称
```
### 示例
```
docker run -d --name nginx -v /root/app/html:/usr/share/nginx/html -p 80:80 nginx
```
# 7.端口映射及容器互联

默认情况下，容器是不能被外部或其他容器访问的。
那么我们应该怎么配置能够实现容器能够被外部访问呢？
## 端口映射
### 随机端口映射
```
docker run -d -P
```
### 映射指定端口
```
docker run -d -p 5000:5000
```
### 映射到指定地址端口
```
docker run -d -p 127.0.0.1:5000:5000
```
### 映射到指定地址的任意端口
```
docker run -d -p 127.0.0.1::5000
```
### 查看端口配置
```
docker port 容器ID
```
## 容器互联
### 自定义容器名称
```
docker run -d -P --name
```
### 容器互联
```
docker run -d -P --name web --link 容器名称[:内部别名] 
```

# 8.使用DockerFile创建镜像

## 常用指令
### ARG
#### 用途
申明创建镜像过程中使用的变量
#### 用法
ARG tag=latest
### FROM
#### 用途
指定基础镜像，写在第一行
#### 用法
FROM nginx:latest
### LABEL
#### 用途
给镜像元数据添加标签
#### 用法
LABEL author=lglbc
### EXPOSE
#### 用途
申明需要需要的端口，但是不会做端口映射
#### 用法
EXPOSE 80 443
### ENV
#### 用途
指定环境变量，在后续容器中也会存在
#### 用法
ENV key=value key1=value1
### ENTRYPOINT
#### 用途
设置镜像的默认入口命令，容器启动时，首先会去执行这个命令
#### 用法
ENTRYPOINT  ["ls" "-l"]
### WORKDIR
#### 用途
配置工作目录
#### 用法
WORKDIR /a
### ONBUILD
#### 用途
build镜像时，优先执行的指令，只会在子镜像中执行
#### 用法
ONBUILD 任意dockerfile 指令
## 操作指令
### RUN
#### 用途
运行指定命令
### 用法
RUN ls -l
### CMD
#### 用途
CMD 指令用来指定启动容器时默认执行的命令 。与run不同之处在于这个只能出现一次，如果出现多次，则只有最后一条生效
#### 用法
CMD java -jar app.jar
### ADD
#### 用途
添加内容到镜像
#### 用法
ADD ./*.jar /app/
### COPY
#### 用途
复制内容到镜像，如果是本地目录推荐使用COPY
#### 用法
COPY ./*.jar /app/
## 实战案例
```bash
FROM nginx:latest
ARG version=1
LABEL author="乐哥聊编程"
EXPOSE 80 443
ENV profile dev
#ENTRYPOINT echo 'nginx start success...'
WORKDIR /usr/share/nginx/html
ONBUILD RUN apt-get update
ONBUILD RUN apt install -y tree
RUN echo 'dockerfile build success ...'
RUN rm -rf /usr/share/nginx/html/*
ADD ./html/index.html /usr/share/nginx/html/
```

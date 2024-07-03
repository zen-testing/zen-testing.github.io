---
title: '部署局域网音视频服务器'
date: 2024-03-01 21:51:49
tags: [Docker]
published: true
hideInList: false
feature: 
isTop: false
---
**在Windows上使用WSL2的docker设置文件夹映射 一定要确保文件夹本身可以通过bash访问**

<!-- more -->

docker-compose.yml

```shell
version: '3.9'
name: nas
services:
    navidrome:
        image: 'deluan/navidrome:latest'
        environment:
            - ND_LOGLEVEL=debug
        ports:
            - '4533:4533'
        volumes:
            - '/f/data/navidrome:/data'
            - '/f/alist/music/audio:/music'
        deploy:
            resources:
                limits:
                    memory: 8192M
                    cpus: '4'
        restart: unless-stopped
        container_name: navidrome
    alist:
        image: 'xhofe/alist:latest'
        container_name: alist
        environment:
            - UMASK=022
            - PGID=0
            - PUID=0
        ports:
            - '2147:5244'
        volumes:
            - '/f/data/alist:/opt/alist/data'
            - '/f/alist:/share'
            - '/f/Telegram:/Telegram'
        deploy:
            resources:
                limits:
                    memory: 8192M
                    cpus: '4'
        restart: unless-stopped
    nginx:
        image: 'nginx:latest'
        ports:
            - '80:80'
        volumes:
            - '/f/alist:/usr/share/nginx/html/download'
            - '/f/data/nginx/nginx.conf:/etc/nginx/nginx.conf'
        container_name: nginx
        deploy:
            resources:
                limits:
                    memory: 8192M
                    cpus: '4'
        restart: unless-stopped
    qbittorrent:
        image: lscr.io/linuxserver/qbittorrent:latest
        container_name: qbittorrent
        deploy:
            resources:
                limits:
                    memory: 8192M
                    cpus: '4'
        environment:
          - PUID=1000
          - PGID=1000
          - TZ=Asia/Shanghai
          - WEBUI_PORT=8080
          - TORRENTING_PORT=6881
        volumes:
          - '/f/data/qbittorrent:/config'
          - '/f/alist/qbittorrent:/downloads'
        ports:
          - 8080:8080
          - 6881:6881
          - 6881:6881/udp
        restart: unless-stopped
    sshd:
        container_name: sshd
        build:
            context: .
            dockerfile: alpineWithSSH
        ports:
            - 8022:22
        volumes:
            - '/f/alist:/alist'
    leanote:
        ports:
            - 9800:9000
        environment:
            - TZ=Asia/Shanghai
        restart: always
        volumes:
            - /f/data/leanote/db:/data/db
            - /f/data/leanote/conf/:/data/leanote/conf
            - /f/data/leanote/files:/data/leanote/files
            - /f/data/leanote/upload:/data/leanote/public/upload
        deploy:
            resources:
                limits:
                    memory: 50M
        oom_kill_disable: true
        # memswap_limit: true
        container_name: leanote
        image: axboy/leanote
    halo:
        stdin_open: true
        tty: true
        container_name: halo
        ports:
            - 8090:8090
        volumes:
            - /f/data/halo:/root
        image: halohub/halo:2.13.1
```
# alpineWithSSH

```shell
# 使用alpine3.19作为基础镜像
FROM alpine:3.19
# 使用sed替换apk源为清华大学镜像源
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors4.tuna.tsinghua.edu.cn/g' /etc/apk/repositories
# 安装openssh服务
RUN apk add --no-cache openssh ffmpeg build-base python3 py3-pip nano openrc
RUN echo "PermitRootLogin yes" >> /etc/ssh/ssh_config
RUN pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
RUN pip install -U yt-dlp --break-system-packages
RUN echo "root:123456" | chpasswd
RUN sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config	
# 创建ssh密钥对
RUN ssh-keygen -A
# 暴露ssh服务端口
EXPOSE 22
# 启动ssh服务
CMD ["/usr/sbin/sshd", "-D"]
```
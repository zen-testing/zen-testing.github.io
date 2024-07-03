---
title: '编译安装支持vvc(h266)的ffmpeg6.0'
date: 2023-04-07 22:18:40
tags: [ffmpeg]
published: true
hideInList: false
feature: 
isTop: false
---
为了尽可能地统一使用方法,方便后期维护,这里使用了docker容器ubuntu:jammy安装
<!-- more -->

**vvc编解码器目前不支持任何ARM架构设备,不要挣扎**

# Dockerfile

```bash
FROM ubuntu:jammy
ENV TIME_ZONE Asia/Shanghai
RUN sed -i 's/archive.ubuntu.com/mirrors.tuna.tsinghua.edu.cn/g' /etc/apt/sources.list
RUN sed -i 's/security.ubuntu.com/mirrors.tuna.tsinghua.edu.cn/g' /etc/apt/sources.list
RUN apt update -y
RUN DEBIAN_FRONTEND=noninteractive apt install -y vim nano less ca-certificates sudo man-db git wget curl openssh-server language-pack-zh-hans net-tools apt-utils iproute2 dialog libfdk-aac-dev libmp3lame-dev libtheora-dev libvorbis-dev yasm libx264-dev libxvidcore-dev libaom-dev libass-dev libopencv-dev build-essential libavformat-dev libssl-dev libopenh264-dev libopenjp2-7-dev librsvg2-dev libsvtav1enc-dev libtesseract-dev libtwolame-dev libvpx-dev libwebp-dev libx265-dev make cmake tzdata locales gcc g++ libsdl2*dev file xz-utils openssh-server vim nano less ca-certificates dialog locales tzdata iproute2 language-pack-zh-hans* sudo fonts-droid-fallback ttf-wqy-zenhei ttf-wqy-microhei fonts-arphic-ukai fonts-arphic-uming
RUN DEBIAN_FRONTEND=noninteractive apt full-upgrade -y
RUN locale-gen zh_CN.utf8
RUN echo "export LC_ALL=zh_CN.UTF-8">> /etc/profile
RUN yes | unminimize
RUN echo "PermitRootLogin yes" >> /etc/ssh/sshd_config
RUN service ssh start
RUN git clone https://github.com/fraunhoferhhi/vvdec /root/vvdec
RUN git clone https://github.com/fraunhoferhhi/vvenc /root/vvenc
RUN git clone https://git.ffmpeg.org/ffmpeg.git /root/ffmpeg
```

# 根据dockerfile创建基础镜像

```bash
docker build -t ubuntu:ffmpeg -f .\Dockerfile .
```

# 根据镜像创建容器

```bash
docker run --name=vvc -p 8022:22 -v /Users/zen/container:/mnt --privileged --restart=on-failure:5 -idt ubuntu:ffmpeg /bin/bash
```

# 进入容器

```bash
docker exec -it vvc bash
```

# 编译安装vvc解码器

```bash
cd /root/vvdec
cmake -S . -B build/release-shared -DCMAKE_INSTALL_PREFIX=/usr/local -DCMAKE_BUILD_TYPE=Release -DVVDEC_INSTALL_VVDECAPP=true -DBUILD_SHARED_LIBS=1
cmake --build build/release-shared -j
cmake --build build/release-shared --target install
# 如果编译出错使用以下命令清理 效果相当于 make clean
rm -rf build bin lib install
```

# 编译安装vvc编码器

```bash
cd /root/vvenc
cmake -S . -B build/release-shared -DCMAKE_INSTALL_PREFIX=/usr/local -DCMAKE_BUILD_TYPE=Release -DBUILD_SHARED_LIBS=1
cmake --build build/release-shared -j
cmake --build build/release-shared --target install
# 如果编译出错使用以下命令清理 效果相当于 make clean
rm -rf build bin lib install
```

# 改装ffmpeg

```bash
# 进入下载好的ffmpeg文件夹
cd /root/ffmpeg
# 切换到6.x的分支上
git checkout release/6.0 # 切换
git branch -vv # 确认
# 下载补丁
wget -O Add-support-for-H266-VVC.patch https://patchwork.ffmpeg.org/series/8365/mbox/
# 应用补丁
git apply ./Add-support-for-H266-VVC.patch --exclude=libavcodec/version.h
```

# 编译安装ffmpeg

```bash
# 进入ffmpeg目录
./configure  --prefix=/opt/ffmpeg \
--enable-pthreads \
--enable-pic \
--arch=amd64 \
--enable-libvvdec \
--enable-libvvenc \
--enable-shared \
--enable-libaom \
--enable-gpl \
--enable-nonfree \
--enable-postproc \
--enable-avfilter \
--enable-pthreads \
--enable-libx264 \
--enable-libx265 \
--enable-libwebp \
--enable-libvpx \
--enable-ffplay
# 如果没有红字报错就继续
make -j8 # 可以改成你电脑全部的核心数,加快编译过程
make install
```

# 添加lib到系统能找到的位置

```bash
# 以下命令需要使用root用户
echo "/opt/ffmpeg/lib" >> /etc/ld.so.conf.d/ffmpeg6.conf
ldconfig
```

# 添加ffmpeg到系统环境变量

编辑 `vim /etc/profile`

```bash
echo "FFMPEG_HOME=/opt/ffmpeg" >> /etc/profile
echo 'export PATH=$PATH:$FFMPEG_HOME/bin' >> /etc/profile
```

使变量生效 `source /etc/profile`

# 后记

尝试在8G内存的电脑上编译vvdec直接爆内存了

于是尝试在其他电脑编译后移植过来

唯一要注意的是

需要把 `/usr/local/lib/libvvdec.so` 和 `/usr/local/lib/libvvenc.so` 同时复制过来
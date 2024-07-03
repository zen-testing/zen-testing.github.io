---
title: '编译安装支持vvc的ffmpeg6,更优雅的方法'
date: 2023-06-06 20:21:42
tags: [ffmpeg,Docker]
published: true
hideInList: false
feature: 
isTop: false
---
为了尽可能地统一使用方法,方便后期维护,这里使用了docker容器alpine:3.18安装

**vvc编解码器目前不支持任何ARM架构设备,不要挣扎**

----

# dockerfile

```ini
# 基础镜像
FROM alpine:3.18
# 备份原始安装源
RUN cp /etc/apk/repositories /etc/apk/repositories.bak
# 修改为国内源
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.alyun.com/g' /etc/apk/repositories
# 安装基础软件
RUN apk add zsh vim nano less git wget curl ca-certificates ttf-dejavu fontconfig iproute2 dialog make cmake alpine-sdk gcc nasm yasm aom-dev libvpx-dev libwebp-dev x264-dev x265-dev dav1d-dev xvidcore-dev fdk-aac-dev
# 准备软件
RUN git clone https://github.com/fraunhoferhhi/vvdec /root/vvdec
RUN git clone https://github.com/fraunhoferhhi/vvenc /root/vvenc
RUN git clone https://git.ffmpeg.org/ffmpeg.git /root/ffmpeg
RUN git clone https://github.com/ultravideo/kvazaar.git /root/kvazaar
```

# 根据dockerfile创建基础镜像

```bash
docker build -t alpine:ffmpeg -f ./Dockerfile .
```

# 根据镜像创建容器

```bash
docker run --name=vvc -p 8022:22 -v /Users/zen/container:/mnt --privileged --restart=on-failure:5 -idt alpine:ffmpeg ash

```

# 进入容器

```bash
docker exec -it vvc ash
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

# 编译安装开源HEVC编解码器

```bash
cd /root/kvazaar
./configure --prefix=/usr/local
make
make install
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
./configure  --prefix=/usr/local \
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
--enable-libfdk-aac \
--enable-libkvazaar \
--enable-libdav1d \
--enable-libxvid \
--enable-libopencore-amrnb \
--enable-libopencore-amrwb \
--enable-version3 \
--enable-ffplay
# 如果没有红字报错就继续
make -j8 # 可以改成你电脑全部的核心数,加快编译过程
make install
```

# 重新读取lib库文件

```bash
ldconfig
```

# 总结

整体看来,基础镜像选择alpine是比Ubuntu更小巧\更优雅的方案
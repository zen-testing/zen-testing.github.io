---
title: '编译安装ffmpeg'
date: 2023-02-27 10:17:51
tags: [ffmpeg]
published: true
hideInList: false
feature: 
isTop: false
---
**由于编译安装的不确定性,这里使用容器测试**
`docker run --name=ffmpeg -p 2222:22 -v /Users/zen/container:/mnt --privileged -it ubuntu /bin/bash`

1. 先安装需要的软件
```bash
$ apt install libfdk-aac-dev \
libmp3lame-dev \
libtheora-dev \
libvorbis-dev \
yasm \
libx264-dev \
libxvidcore-dev \
libaom-dev \
libass-dev \
libopencv-dev \
build-essential \
libavformat-dev \
libssl-dev \
libopenh264-dev \
libopenjp2-7-dev \
librsvg2-dev \
libsvtav1enc-dev \
libtesseract-dev \
libtwolame-dev \
libvpx-dev \
libwebp-dev \
libx265-dev \
make
```

2. 设定配置文件
```bash
./configure --prefix=/opt/ffmpeg \
--enable-shared \
--enable-libfdk-aac \
--enable-libaom \
--enable-gpl \
--enable-nonfree \
--enable-postproc \
--enable-avfilter \
--enable-pthreads \
--enable-libmp3lame \
--enable-libtheora \
--enable-libvorbis \
--enable-libx264 \
--enable-libxvid \
--enable-libx265 \
--enable-libwebp \
--enable-libvpx \
--enable-libass \
--enable-libmp3lame \
--enable-libopenh264 \
--enable-libopenjpeg \
--enable-librsvg \
--enable-libsvtav1 \
--enable-libtesseract \
--enable-libtwolame 
```

3. 编译安装
```bash
# 需要切换到root用户
make -j8 # 时间长
make install
```
4. 将ffmpeg的库文件加入系统

```bash
$ sudo -i
$ echo "/opt/ffmpeg/lib" >> /etc/ld.so.conf
$ ldconfig
```
5. 将ffmpeg程序目录加入环境变量
```bash
$ echo "export PATH=$PATH:/opt/ffmpeg/bin" >> ~/.profile
$ source ~/.profile
```
6. 测试
```bash
$ ffmpeg -i 心中的日月.mp3 -c:a libfdk_aac -profile:a aac_he -b:a 96k 心中的日月.aac
```
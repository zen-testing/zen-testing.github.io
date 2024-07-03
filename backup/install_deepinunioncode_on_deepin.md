---
title: '在deepin上安装DeepinUnionCode'
date: 2023-11-07 10:54:57
tags: [Deepin]
published: true
hideInList: false
feature: 
isTop: false
---
![效果图](https://z1.ax1x.com/2023/11/04/piQSH3Q.png)

# 0x00 安装系统

微软商店下载[deepin WSL](https://apps.microsoft.com/detail/9P6HT7L0QGRH?hl=zh-cn&gl=CN) 安装过程这里不赘述

# 0x01 添加源

deepin v23对应Debian 11 所以添加bullseye的源

```bash
# 需要使用root用户执行
echo -e 'deb https://mirrors4.tuna.tsinghua.edu.cn/debian/ bullseye main contrib non-free\ndeb https://mirrors4.tuna.tsinghua.edu.cn/debian/ bullseye-updates main contrib non-free\ndeb https://mirrors4.tuna.tsinghua.edu.cn/debian/ bullseye-backports main contrib non-free\ndeb https://mirrors4.tuna.tsinghua.edu.cn/debian-security bullseye-security main contrib non-free\n' >> /etc/apt/sources.list.d/bullseye.list
```

# 0x02 处理缺失的密钥

添加后执行更新命令`sudo apt update`会提示没有密钥

```bash
# 其中16位的密钥是根据你自己的报错信息修改
# 加入了代理是因为这算是个"不存在的网站" 如果你对当前的网络环境有信心 可以去掉
sudo apt-key adv --keyserver-options http-proxy=http://192.168.1.20:8889/ --keyserver keyserver.ubuntu.com --recv-keys 605C66F00D6C9793
sudo apt-key adv --keyserver-options http-proxy=http://192.168.1.20:8889/ --keyserver keyserver.ubuntu.com --recv-keys 6ED0E7B82643E131
sudo apt-key adv --keyserver-options http-proxy=http://192.168.1.20:8889/ --keyserver keyserver.ubuntu.com --recv-keys 54404762BBB6E853
sudo apt update
```

# 0x03 安装全部依赖项

```bash
# 如果程序更新后依赖改变 以 ./debian/control为准
sudo apt install \
debhelper \
cmake \
qt5-qmake \
qtbase5-dev \
qttools5-dev \
qttools5-dev-tools \
lxqt-build-tools \
libssl-dev \
llvm \
llvm-dev \
libclang-dev \
libutf8proc-dev \
libmicrohttpd-dev \
libjsoncpp-dev \
libargtable2-dev \
libhiredis-dev \
catch \
libzstd-dev \
libjson-c-dev \
libelf-dev \
libcapstone-dev \
libunwind-dev \
libelfin-dev \
libdbus-1-dev \
libxi-dev \
qtscript5-dev \
libqt5scripttools5 \
clang \
doxygen \
qtbase5-dev \
qtdeclarative5-dev \
qtscript5-dev \
qttools5-dev \
libqt5svg5-dev \
libqt5opengl5-dev \
libqt5sql5-mysql \
libqt5sql5-sqlite \
libqt5quick5-dev \
libqt5websockets5-dev \
qtcreator
```

# 0x04 确保已经安装所有依赖库

```bash
git clone https://gitee.com/deepin-community/deepin-unioncode.git
cd deepin-unioncode
sudo apt build-dep ./
```

# 0x05 构建

```bash
# 如果你对自己的电脑有信心 也可以使用全部线程构建
cmake -B build -DCMAKE_INSTALL_PREFIX=/usr -DCMAKE_BUILD_TYPE=Release
cmake --build build
```

# 0x06 安装

```bash
sudo cmake --build build --target install
```

# 0x07 运行

```bash
deepin-unioncode
```
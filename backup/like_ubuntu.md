---
title: '为啥这么像?一定是我的错觉'
date: 2022-09-26 17:20:23
tags: [Linux,openKylin]
published: true
hideInList: false
feature: 
isTop: false
---

在鸭子类型中,关注点在于对象的行为,能做什么;而不是关注对象所属的类型.例如,在不使用鸭子类型的语言中,我们可以编写一个函数,它接受一个类型为"鸭子"的对象,并调用它的"走"和"叫"方法.在使用鸭子类型的语言中,这样的一个函数可以接受一个任意类型的对象,并调用它的"走"和"叫"方法.如果这些需要被调用的方法不存在,那么将引发一个运行时错误.任何拥有这样的正确的"走"和"叫"方法的对象都可被函数接受的这种行为引出了以上表述,这种决定类型的方式因此得名

<!-- more -->

<iframe width="560" height="315" src="https://player.bilibili.com/player.html?bvid=BV1rG4y1e7WJ&page=1" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/rqPShZlEULg" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

以下是文字说明
----

# 0x01
正常下载安装openKylin

```shell
wget https://mirror.lzu.edu.cn/openkylin-cdimage/yangtze/openKylin-0.7-x86_64.iso
wget https://mirror.lzu.edu.cn/openkylin-cdimage/yangtze/openKylin-0.7.5-x86_64.iso
```

## tips

先安装openssh-server

然后就可以顺利地复制粘贴以下代码了

# 0x02 备份原始文件

```shell
sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak
```

# 0x03 清空源文件

```shell
sudo echo -n > /etc/apt/sources.list
```

# 0x04 用你喜欢的编辑器写入文件内容

```shell
deb http://software.openkylin.top/openkylin/yangtze default all
deb http://mirrors.163.com/openkylin/ yangtze main cross pty
deb http://mirrors.163.com/openkylin/ yangtze-security main cross pty
deb http://mirrors.163.com/openkylin/ yangtze-updates main cross pty
deb http://mirrors.163.com/openkylin/ yangtze-proposed main cross pty
deb http://mirrors.163.com/openkylin/ yangtze-backports main cross pty

deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-security main restricted universe multiverse

# 预发布软件源,不建议启用
# deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse
```

# 0x05 更新一次

```shell
sudo apt-get update
```

此时不出意外应该会报公钥错误

```shell
由于没有公钥,无法验证下列签名: NO_PUBKEY 3B4FE6ACC0B21F32 NO_PUBKEY 871920D1991BC93C
```

# 0x06 添加缺失的公钥

```shell
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 3B4FE6ACC0B21F32
```

再更新一次

```shell
sudo apt-get update
```

此时就不会出现任何错误

# 0x07 安装缺失的软件

一些很基础的软件竟然在openkylin的官方源中找不到

比如 `less` `top` `nano` `neofetch` `tail` 等

添加ubuntu源之后就可以正常安装了

![效果图](https://s1.ax1x.com/2022/09/04/voWe7q.png)
<center>效果图</center>

![更新后](https://s1.ax1x.com/2022/09/04/voWnA0.png)
<center>更新后</center>

![安装Gnome后](https://s1.ax1x.com/2022/09/04/voWKhT.png)
<center>安装Gnome后</center>

**<center>这还说不是100%复制粘贴ubuntu系统谁信啊</center>**

# 0x08 卸载ukui

```shell
sudo apt-get purge \
libqt5-ukui-style1 \
libukui-common0 \
libukui-log4qt-dev \
libukui-log4qt1 \
libukui-search0 \
qml-module-org-ukui-qqc2desktopstyle \
qml-module-org-ukui-stylehelper  \
qt5-gesture-extensions:amd64 \
qt5-styles-ukui \
qt5-ukui-platformtheme \
ukui-biometric-manager \
ukui-bluetooth \
ukui-clock \
ukui-control-center \
ukui-desktop-environment-core \
ukui-globaltheme-common \
ukui-globaltheme-heyin \
ukui-globaltheme-light-seeking \
ukui-greeter \
ukui-input-gather \
ukui-media \
ukui-media-common \
ukui-menu \
ukui-notification-daemon \
ukui-panel \
ukui-polkit \
ukui-power-manager \
ukui-screensaver \
ukui-search \
ukui-search-systemdbus \
ukui-session-manager \
ukui-session-wayland \
ukui-settings-daemon \
ukui-settings-daemon-common \
ukui-sidebar ukui-system-monitor \
ukui-touch-settings-plugin \
ukui-window-switch \
time-shutdown \
kmre \
peony-common \
kylin-user-guide-common \
peony-vfs-kylin-kmre \
peony-set-wallpaper \
kwin-common \
kwin-data \
kwin-wayland \
kwin-wayland-backend-drm \
kwin-wayland-backend-wayland \
kylin-kmre-window \
kylin-app-cgroupd \
kylin-burner \
kylin-installer \
kylin-ipmsg \
kylin-kmre-daemon \
kylin-kmre-display-control \
kylin-kmre-image-data-x64 \
kylin-kmre-image-update-x64 \
kylin-kmre-manager \
kylin-kmre-modules-dkms \
kylin-scanner \
kylin-software-center \
kylin-software-properties \
kylin-system-updater \
kylin-tablet-desktop-general \
kylin-update-notify \
kylin-weather \
openkylin-default-settings \
openkylin-fonts \
openkylin-gtk-theme \
openkylin-icons-theme \
openkylin-initiate-theme \
openkylin-sounds-theme \
openkylin-theme \
openkylin-theme-configure \
openkylin-wallpapers \
openkylin-wallpapers-yangtze
# 如果不需要lightdm也可以卸载,反正已经有gdm3了
```

# 0x09 彩蛋

更换了ubuntu 22.04 LTS 的源

好家伙

1141个更新

![更换为Jammy](https://s1.ax1x.com/2022/09/04/voWuNV.png)
<center>更换为Jammy</center>

# Plan B

如果有人担心这样改动之后会出现问题

也可以直接在`/etc/apt/sources.list.d`下单独新建ubuntu的源,比如`focal.list`

文件内容如下
```shell
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-security main restricted universe multiverse
# 预发布软件源,不建议启用
# deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse
```

同样的效果

# 0x0A 使用ubuntukylin源

`focal.list`的内容改成
```shell
deb http://mirrors.aliyun.com/ubuntu/ focal main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ focal-backports main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ focal-security main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ focal-updates main restricted universe multiverse
```

# 0x0B 更新一次

```shell
sudo apt-get update
```

此时不出意外应该会报公钥错误

```shell
由于没有公钥,无法验证下列签名: NO_PUBKEY 3B4FE6ACC0B21F32 NO_PUBKEY 871920D1991BC93C
```

# 0x0C 添加缺失的公钥

```shell
sudo apt-key adv --recv-keys --keyserver keyserver.Ubuntu.com 9C949F2093F565FF
```

再更新一次

```shell
sudo apt-get update
```

此时就不会出现任何错误

# 0x0D 摆烂之王

这是我见过最不要脸的企业

本来想使用ubuntukylin的源

没想到从20.04开始

优麒麟就已经不维护自己的源了

暗度陈仓,换成了ubuntu原版的安装源(阿里镜像源)

连装都不想装了

就是在赌政府采购的决策层领导没有懂电脑的

摆烂已经做到了极致

# 惊喜

原来这已经不是麒麟第一次干这事了

银河麒麟桌面版早就玩过了

只不过当时忘了删掉密钥环再发布罢了

至少到 桌面版V10SP1HWE之前

都是这么干的

直接添加ubuntu jammy源

你猜怎么着?

![银河麒麟添加jammy](https://s1.ax1x.com/2022/10/11/xtqbdg.png)

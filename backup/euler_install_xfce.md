---
title: 'openEuler安装xfce桌面(official)'
date: 2022-09-26 18:14:16
tags: [openEuler,Linux,xfce]
published: true
hideInList: false
feature: 
isTop: false
---

# 0x01 [下载](https://openeuler.org/zh/download/)

openEuler ISO镜像并安装系统,更新软件源(需要配置Everything源,以及EPOL源,下面命令是在最小化安装系统的情况下安装XFCE)

```
sudo dnf update
```

# 0x02 安装字库
```
sudo dnf install dejavu-fonts liberation-fonts gnu-*-fonts google-*-fonts
```

# 0x03 安装Xorg
```
sudo dnf install xorg-*
```

# 0x04 安装XFCE及组件
```
sudo dnf install xfwm4 xfdesktop xfce4-* xfce4-*-plugin network-manager-applet *fonts
```

# 0x05 安装登录管理器
```
sudo dnf install lightdm lightdm-gtk
```

# 0x06 设置默认桌面为XFCE
通过root权限用户设置
```
echo 'user-session=xfce' >> /etc/lightdm/lightdm.conf.d/60-lightdm-gtk-greeter.conf
```

# 0x07 使用登录管理器登录XFCE
```
sudo systemctl start lightdm
```
登录管理器启动后,在右上角左侧选择"xfce-session"
输入用户名\密码登录

# 0x08 设置开机自启动图形界面
```
sudo systemctl enable lightdm
sudo systemctl set-default graphical.target
```
如果默认安装了gdm,建议停用gdm
```
systemctl disable gdm
```
重启验证
```
sudo reboot
```

# 0x09 FAQ

Q:为什么lightdm登录界面背景是黑色的?
A:登录界面是黑色的是因为lghtdm-gtk默认配置文件/etc/lightdm/lightdm-gtk-greeter.conf中没有设置background.
可以在该配置文件最后的[greeter]段中设置 background=/usr/share/backgrounds/xfce/xfce-blue.jpg
然后systemctl restart lightdm 就可以看到背景了.图片权限为644,尽量使用png格式

# 0x0A 效果图

[![vRq58O.png](https://s1.ax1x.com/2022/08/27/vRq58O.png)](https://imgse.com/i/vRq58O)

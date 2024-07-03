---
title: '为uos更换轻量级桌面'
date: 2022-09-26 15:52:43
tags: [UOS,Linux]
published: true
hideInList: false
feature: 
isTop: false
---

>众所周知,deepin在整个系统中最占用资源的就是桌面环境,如果你也希望把系统资源放在你手头的工作上而不是花里胡哨的桌面特效那就继续往下看,换一更轻量级的桌面环境和登陆管理器


# 安装xfce
```shell
$ sudo apt-get install xfce4 xfce4-goodies
```
# 选择xfce
重启后登陆界面的右下角会多出一个按钮(右下角第一个)
![四个按钮](https://s1.ax1x.com/2022/08/05/vmDNjA.png)
<center>点击后选择xfce</center>

![选择xfce](https://s1.ax1x.com/2022/08/05/vmDanI.png)
<center>回到输入密码的界面正常登陆</center>

![登陆到xfce](https://s1.ax1x.com/2022/08/05/vmDtcd.png)
<center>登陆到xfce</center>

# 安装slim
```shell
$ sudo apt-get install slim
```
# 切换到slim
```shell
$ sudo dpkg-reconfigure slim
```
![选择slim](https://s1.ax1x.com/2022/08/05/vmrkDI.png)
<center>通过方向键选择`slim`回车确认</center>

# 卸载lightdm
```shell
$ sudo apt-get purge lightdm
```
# 重启
![dm](https://s1.ax1x.com/2022/08/05/vmrnPS.png)
<center>如果登陆后发现还是之前的界面,可以通过F1切换,直到下方显示`xfce session`</center>

# 卸载dde
```shell
$ sudo apt-get remove \
  dde-desktop \
  dde-launcher \
  deepin-aiservice \
  deepin-activation-alert
```

![](https://s1.ax1x.com/2022/08/05/vmrbi8.png)
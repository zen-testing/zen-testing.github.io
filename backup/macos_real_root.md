---
title: 'macOS开启真正的root用户'
date: 2022-09-26 17:30:28
tags: [macOS]
published: true
hideInList: false
feature: 
isTop: false
---
[这是原文地址](https://www.xiebruce.top/809.html/comment-page-1#comment-289)
之所以要盗过来,就是怕这个博文哪天消失了,留个备份,因为这确实是我需要的功能

<!-- more -->

右键`访达`选择`前往文件夹`或者`shift+command+G`

输入`/System/Library/CoreServices/Applications`
![1](https://img.xiebruce.top/2019/01/26/3d58bab278d09bab1fd8e910600c1699.png)

找到`目录实用工具`并打开
![2](https://img.xiebruce.top/2019/01/26/ae23e53657cf74d121dde5d9dc6d834b.png)

点击左下角的锁,并打开

![3](https://img.xiebruce.top/2019/01/26/1c6349f22caaff534c70c93fbb4f74a5.jpg)

点击顶部菜单栏的`编辑` `启用root用户`

![4](https://img.xiebruce.top/2019/01/26/6a1f5a338e436671bb55fe1f28efa47e.jpg)

给root用户设置密码,设置成功后root用户开启
![5](https://img.xiebruce.top/2019/01/26/e73ed3fcf7358fc1006f9392cd22ddd0.jpg)

开启之后就能在用户登录界面的其他用户里选择root登陆了

终端环境默认root权限

在管理员用户下的`sudo su` `sudo -i` `sudo -s`并不是真正的root,即使能做的已经很多了

类比正版Windows系统的administrator账户

----

没有需求的人尽量别开
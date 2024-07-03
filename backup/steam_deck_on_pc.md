---
title: '在amd64电脑上体验steam deck系统'
date: 2023-01-01 19:23:11
tags: [Steam]
published: true
hideInList: false
feature: 
isTop: false
---
目前这个系统理论上对AMD的支持会比Nvidia更好,支持xbox手柄
<!-- more -->
<iframe width="100%" height="550" src="https://www.youtube.com/embed/jmNqayVakAs" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

如果视频无法显示,点击[这里](https://player.bilibili.com/player.html?aid=819643071&bvid=BV1ZG4y1j79b&cid=948443776&page=1)查看

# 0x01 准备工具
[写入启动盘的软件](https://www.balena.io/etcher/)
P.S. 如果你无法下载这个软件,也可以通过最原始的命令制作启动盘
```shell
# 假设要写入的ISO文件名为SteamOS.iso U盘设备名为sdb
sudo dd if=SteamOS.iso of=/dev/sdb bs=4M status=progress oflag=sync
```
[系统镜像](https://drive.google.com/file/d/1tAJQbqrg8t6hzymeynNIXp-pAzqLbYb3/view)
P.S. 如果你无法下载镜像或者想随时获取最新版镜像,也可以在arch下运行如下命令构建最新的ISO
```shell
pacman -Sy archiso
git clone https://github.com/bhaiest/holoiso/
mv holoiso/mkarchiso-holoiso /usr/bin
chmod +x /usr/bin/mkarchiso-holoiso
sudo mkarchiso-holoiso -v holoiso
```
# 0x02 开始安装
插入启动盘,~~选择第四项`SteamOS install medium (linux holoiso extra compability x86_64 uefi copy to ram)~~

**双击安装图标**

~~进入tty之后如果需要连接Wi-Fi,可以执行以下命令~~
```shell
 $ iwctl # 配置网络
 $ device list # 列出所有可用的无线网卡 假设这里的网卡叫做 wlan0
 $ station wlan0 get-networks # 列出所有可用Wi-Fi 假设你的Wi-Fi名称叫做 103
 $ station wlan0 connect 103 # 连接Wi-Fi 回车后会询问密码 输入Wi-Fi密码即可
 $ quit # 退出网络配置工具
 ```

 **执行安装命令**

 ```shell
 $ holoinstall # 开始系统安装进程 会询问你简单安装还是完整安装
 $ 2 # 这里选择完整安装
 # 如果你的电脑现在有多于一块硬盘 会询问你系统安装到哪里(sda或者nvme0n1)具体的设备名会有提示
 # 然后会询问你是否擦出这个驱动器 输入y确定
 # 安装过程中如果有其他提示 如果你看不懂直接默认选项就行 再说这些都看不懂玩什么steam deck?
 # 安装完成后输入reboot重启电脑 这时可以移除U盘了
 ```

 **按照提示安装即可**

# 效果图

![1](https://s1.ax1x.com/2023/01/02/pSPcvgP.jpg)
![2](https://s1.ax1x.com/2023/01/02/pSPcj3t.jpg)
![3](https://s1.ax1x.com/2023/01/02/pSPcxjf.jpg)
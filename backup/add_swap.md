---
title: '添加swap分区(文件)'
date: 2022-09-26 15:13:25
tags: [Linux]
published: true
hideInList: false
feature: 
isTop: false
---

# 0x01 检查是否有Swap空间

![free -h](https://s1.ax1x.com/2022/09/01/v51hE8.png)
<center>`free -h`</center>

# 0x02 创建swap分区

创建2G的swap,可以根据你的服务器配置来调整大小,一般情况下,Swap空间不需要很大

```shell
$ sudo dd if=/dev/zero of=/mnt/swap bs=1M count=2048  
```

# 0x03 设置交换分区文件

```shell
$ sudo mkswap /mnt/swap
```

# 0x04 启动swap

```shell
$ sudo swapon /mnt/swap
```

# 0x05 设置开机启用 swap 分区

```shell
$ sudo vim /etc/fstab
#
/mnt/swap swap swap defaults 0 0
#
```

# 0x06 检查是否有Swap空间

![free -h](https://s1.ax1x.com/2022/09/01/v51hE8.png)
<center>`free -h`</center>

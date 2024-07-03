---
title: 'openKylin使用snap商店安装软件'
date: 2022-09-26 18:15:57
tags: [openKylin,Linux]
published: true
hideInList: false
feature: 
isTop: false
---

# 0x01 安装snap

```shell
$ sudo apt-get install snapd
```

<iframe width="560" height="315" src="https://player.bilibili.com/player.html?aid=687617237&bvid=BV1XU4y1B7zm&cid=819695217&page=1" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

# 0x02 设置服务开机自启

```shell
$ sudo systemctl start snapd
$ sudo systemctl enable snapd
```

# 0x03 安装第一个软件

这里唯一的难点就是需要登陆商店[官网](https://snapcraft.io/store)获取软件的正式名称(安装命令)

1. 搜索框里输入你要安装的软件![查找软件](https://s1.ax1x.com/2022/08/31/v4ljPJ.png)

2. 点击右侧`install`下方会显示安装命令,复制到你的终端执行即可安装![安装软件](https://s1.ax1x.com/2022/08/31/v4lx2R.png)

```shell
# 比如 我要安装 sublime text
$ sudo snap install sublime-text --classic
```

<iframe width="560" height="315" src="player.bilibili.com/player.html?aid=472558914&bvid=BV1cT411c7xX&cid=819697259&page=1" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

# 0x04 tips

第一次安装软件的时候才会下载商店核心包,会慢一些,以后没有大版本更新的情况下不会重新下载,就会快很多了
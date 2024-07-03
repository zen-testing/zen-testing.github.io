---
title: '常规安装双系统的方法'
date: 2022-10-10 11:36:28
tags: [双系统]
published: true
hideInList: false
feature: 
isTop: false
---

这里只演示一种最常见的安装双系统方法 - 单硬盘安装双系统

<!-- more -->

<iframe width="100%" height="550" src="https://www.youtube.com/embed/cL3nhIo_1Z4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

如果视频无法显示,点击[这里](http://player.bilibili.com/player.html?aid=558984376&bvid=BV1Fe4y1S7bt&cid=857529247&page=1)查看

# 文字说明

首先正常安装WINDOWS

进入安装前,一定要保证你安装的这个系统是在gpt分区表的硬盘上

当然,如果你会什么高级解决办法,你也没必要看这篇教程了

如果你并不确定你现在的磁盘是否为gpt分区表

安装过程中直接再重新设置一次

如果接下来你要安装到另一个Linux系统,是uos这种强制需要300M以上的efi分区,这里也顺便手动创建一个efi分区

插入Linux的安装盘,启动后选择手动安装

找到刚才压缩出来的空间创建分区

格式为 `ext4`,挂载点是`/`,容量一般都会自动最大值,如果不是,手动拉到最大

然后开始进入安装

安装后会提示你拔出U盘,虽然uefi不需要这个过程,但你还是拔掉吧

重启后就能看到双系统选单了

安装结束

虽然整个过程没有一点技术含量

完全是看屏幕上提示什么跟着做就完了

奈何还是有人不看教程不敢下手

# 高级玩法 先安装Linux

1. 正常安装Linux系统,在划分/分区的时候留出空间给Windows,或者在用全部容量安装后通过Gparted的LiveCD压缩出给Windows的空间
2. 找一个正经并且功能齐全的PE把Windows安装镜像中的install.wim或者install.esd释放到这个留出来的空间
3. 重启进入linux系统更新GRUB
    ```shell
    $ sudo update-grub
    ```
再次重启就可以看到两个系统的选择菜单了

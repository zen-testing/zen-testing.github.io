---
title: 'UOS通过命令打开开发者模式'
date: 2022-09-26 19:28:38
tags: [UOS]
published: true
hideInList: false
feature: 
isTop: false
---

>开发者模式类似于window 的管理员权限,可以对系统文件进行任意操作,具体体现在 具有root权限 和 可执行sudo命令操作;
如果不打开开发者模式,不能使用sudo 权限,同时也不能安装离线安装包.
设计开发者模式的初衷是一些普通用户用不到那么高级别权限,为了防止普通用户对系统数据的误操作,所以设计了开发者模式.
这么做到底是好还是不好,这里不予置评

程序员只谈技术,毕竟曾经有一位哲人说过,技术是无罪的
# 测试环境
+ 未激活的uniontechos-desktop-20-professional-1043-amd64系统
>选择用专业版系统做示范是因为专业版限制最严格,专业版能用的方法,其他版本都能用
+ 作为live CD的uniontechos-desktop-20-professional-1043-amd64.iso

![安装完成](https://s1.ax1x.com/2022/09/04/vTF8Yt.png)

![正常安装系统](https://s1.ax1x.com/2022/09/04/vTFdmQ.png)


# 使用安装介质进入live cd模式

1. 用你的系统盘(U盘)启动电脑,这里以UOS自带系统盘为例
2. 开机时在选择菜单时按下`e`或者`Tab`
![删除前](https://s1.ax1x.com/2022/09/04/vTFN6S.png)
3. 在下方代码中删掉`livecd-installer`后,`CTRL+X`或`Enter`启动live cd模式
![删除后](https://s1.ax1x.com/2022/09/04/vTFwwj.png)

# 挂载系统分区

`lsblk`看一下系统分区的名称,比如`sda2`

挂载这个分区

```shell
$ sudo mount /dev/sda2 /mnt
$ sudo chroot /mnt
```

![挂载硬盘](https://s1.ax1x.com/2022/09/04/vTFUOg.png)
并`chroot`到这里

![chroot](https://s1.ax1x.com/2022/09/04/vTFtl8.png)

# 编辑开发者文件

```shell
# 确保文件夹存在
mkdir /var/lib/deepin/developer-mode
cd /var/lib/deepin/developer-mode
# 关闭不可修改模式
chattr -i enabled
# 开启开发者
echo -n 1 > enabled
# 锁定文件不可更改删除
chattr +i enabled
# 退出chroot
exit
# 重启电脑,重启的时候需要拔掉系统盘
reboot
```
![回锁文件](https://s1.ax1x.com/2022/09/04/vTF0Ts.png)

# 验证

虽然没有显示开启
![虽然没有显示开启](https://s1.ax1x.com/2022/09/04/vTFDkn.png)

但实际上已经开启
![但实际上已经开启](https://s1.ax1x.com/2022/09/04/vTFGfP.png)

可以正常通过apt更新软件
![可以正常通过apt更新软件](https://s1.ax1x.com/2022/09/04/vTFYSf.png)
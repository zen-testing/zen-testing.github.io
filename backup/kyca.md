---
title: '关于 [麒麟操作系统桌面工程师KYCA(桌面)模拟题]的疑问'
date: 2024-04-02 16:56:21
tags: [openKylin]
published: true
hideInList: false
feature: https://s21.ax1x.com/2024/04/02/pFHmXE8.png
isTop: false
---

[原题地址](https://inst.kylinos.cn/#/index/autoTestDetail/11697535105015795663557)

```
2.安装银河麒麟桌面操作系统进行磁盘分区时
A在安装操作系统时只给硬盘划分了扩展分区和逻辑分区处理
B在安装银河麒麟桌面操作系统时可以不划分主分区
C在安装银河麒麟桌面操作系统时必须划分主分区
D在安装银河麒麟桌面操作系统时可以只划分逻辑分区
```
正确答案选C
**但是** 如果我MBR硬盘已经有三个主分区加一个扩展分区的情况下 只要保证/boot设置为活动分区即可 不需要重新划分主分区

```
12.按下哪个键能终止当前运行的命令？
A Ctrl+C
B Ctrl+F
C Ctrl+B
D Ctrl+D
```
正确答案选A
**但是** 众所周知`Ctrl+C`对应`SIGINT`信号`Ctrl+D`对应`SIGTTOU`信号

```
20.以下关于分区描述错误的是？
A swap分区推荐大小为内存的2倍
B 若希望使用系统的备份恢复功能，则需要创建/backup分区
C /boot分区无需过大，一般设置为50M左右即可
D 根分区/大小必须不小于10G
```
正确答案选C
**但是** swap分区的必要性、应该多大、是否应该由更灵活的swap file替代性我在另一篇文章已经讲过这里不再赘述; 先说C选项,设置一种场景:MBR硬盘4个主分区全盘安装,电脑使用legacy方式启动,已知一个内核加上冗余空间约为100~250M,给boot50M限制是不是太过自信了?;D选项,如果我把根目录下`dev`、`home`、`media`、`opt`、`root`、`sbin`、`sys`、`usr`、`bin`、`etc`、`lib`、`mnt`、`proc`、`run`、`srv`、`tmp`、`var`、`boot`分别挂载到同一个服务的18块物理硬盘上,那/所在分区不就是走个形式吗?

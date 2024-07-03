---
title: 'WSL相关命令'
date: 2022-09-26 21:09:36
tags: [Windows]
published: true
hideInList: false
feature: 
isTop: false
---
# wsl 命令

### 查看帮助

`wsl -h`

### 设置默认版本,选择linux默认运行在 wsl1 还是 wsl2

`wsl --set-default-version 2`

### 设置 某个linux发行版运行版本,需要先安装好 linux 后才可以转换

`wsl --set-version <distro> 2`

示例:

`wsl --set-version ubuntu 1`

### ubuntu 版本转换

`wsl --set-version ubuntu 2`

### 查看安装的 linux

`wsl --list --verbose`
或
`wsl -l -v`

### 停止所用运行Linux

`wsl --shutdown`

### 启动虚拟机

直接输入系统名称如`Ubuntu` `kali`等直接进入
或使用wsl命令,例如:
`wsl -d ubuntu`

### 终止所有运行的linux

`wsl --shutdown`

### 终止指定的linux

`wsl --terminate <distro>`
或
`wsl -t <distro>`

### 查看linux列表

`wsl -l`

### 关闭ubutnu ,关闭没有任何显示

`wsl -t Ubuntu`
# 将ubuntu导出

导出类似,docker的导出,方便移动等

### 导出到d盘:

```
wsl --export Ubuntu D:/ubuntu.tar
//很快就会完成,本次实例 tar大小 1.15G,进行压缩 ,大小为 414M
```

### 导入

```
wsl --import Ubuntu D:/ubuntu_dir  D:/ubuntu.tar
/*
–import :导入
ubuntu: 导入名称,可自定义
D:/ubuntu_dir : 导入到那个目录,导入成功,有 ext4.vhdx 文件
D:/ubuntu.tar: 源文件
*/
```
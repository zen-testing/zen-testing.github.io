---
title: 'UOS一键安装方式重新设置系统分区容量'
date: 2022-09-26 19:31:54
tags: [UOS]
published: true
hideInList: false
feature: 
isTop: false
---

进入第一个安装界面后

Ctrl+Alt+F2进入tty2
```shell
sudo nano /etc/deepin-installer.conf
```
`Ctrl+-` 输入74 跳到`partition_full_disk_large_root_part_range=15:15`行末

改15:15 为你需要的大小 比如 30:30

`Ctrl+-` 输入95 跳到`partition_root_space_required=15`行末

改15 为你需要的大小 比如30

Ctrl+x 输入y回车保存 再Ctrl+Alt+F1切回安装界面 一路下一步即可
---
title: '关机提示acpi错误解决办法'
date: 2022-12-05 21:44:44
tags: [Linux]
published: true
hideInList: false
feature: 
isTop: false
---
刚开始装上系统时候，Ubuntu是能够正常关机的，出现此类问题的原因有很多种，可能是装了某些软件，也可能更新了新的Linux内核等等，造成ACPI（Advanced Configuration and Power Interface）出现问题，现附上解决方法
<!-- more -->

在终端输入以下命令
```shell
$ sudo gedit /etc/default/grub
```
找到这一行：`GRUB_CMDLINE_LINUX_DEFAULT=”quiet splash” `
改成：`GRUB_CMDLINE_LINUX_DEFAULT=”quiet splash acpi=force pci=nomsi” 
`
保存退出。

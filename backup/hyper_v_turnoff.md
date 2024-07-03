---
title: 'HyperV的历史遗留问题'
date: 2022-09-26 17:12:18
tags: [Windows]
published: true
hideInList: false
feature: 
isTop: false
---

已经卸载了hyperV仍然提示VM与hyperV不兼容?

天天模拟器,提示VT模式没有开启?

虽然BIOS里面已经设置过了但还会提示怎么办?

百度搜不到的正确答案这里有!

----

## 前提条件

已经正确在控制面板->程序和功能里关闭了hyperV全部功能和Windows sandBox功能
这里的问题在于有些人自作聪明在系统里禁用了hyperV创建的网卡或者提升了hyperV相关文件的权限使得user权限的用户无法访问,导致相关功能不能被正常关闭,那就不用继续往下看了

## 解决方法

进入正题

卸载 hyper-v 后需要关闭hyper-v启动类型.具体步骤如下

1. 以管理员身份运行命令提示符

2. 执行命令 `bcdedit /set hypervisorlaunchtype off`

3. 重启,运行vm即可

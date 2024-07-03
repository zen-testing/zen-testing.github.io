---
title: '为什么不建议直接修改sudoer文件?'
date: 2023-04-08 13:54:25
tags: [Linux]
published: true
hideInList: false
feature: 
isTop: false
---
编辑`/etc/sudoers`文件
第一行会显示`This file MUST be edited with the 'visudo' command as root.`

查询stack overflow后总结有两类原因

1. `visudo`在编辑保存后可以检查文件语法错误,如果出现错误文件不会被更新,防止文件编辑错误后sudo权限错误,导致没有任何用户能再次编辑`sudoer`文件
2. 编辑文件时加锁,防止多个进程同时编辑`sudoer`文件,导致文件错乱
---
title: 'OpenWrt设置samba密码'
date: 2023-01-16 20:54:52
tags: [openWrt,Samba]
published: true
hideInList: false
feature: 
isTop: false
---
1. 编辑Luci模板，注释掉`invalid users = root`行
2. 添加用户
    ```shell
    $ smbpasswd -a root
    ```
3. 在Luci中勾选用户

|共享名|目录|允许用户|只读|可浏览|允许匿名用户|创建权限掩码|目录权限掩码|
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|share|/mnt/sda1/share|root|否|是|是|0775|0775|
---
title: '设置默认选择的DE'
date: 2022-09-26 21:30:28
tags: [Linux]
published: true
hideInList: false
feature: 
isTop: false
---
# Plan A
```shell
$ sudo update-alternatives --config x-session-manager
```

# Plan B

```shell
 $ sudo vim /var/lib/AccountsService/users/$USER

[User]
Language=zh_CN
Session=
FormatsLocale=zh_CN.UTF-8
Icon=/home/zen/.face
SystemAccount=false
# 改为
[User]
Language=zh_CN
Session=xfce
FormatsLocale=zh_CN.UTF-8
Icon=/home/zen/.face
SystemAccount=false
```
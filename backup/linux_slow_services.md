---
title: 'linux开关机卡在服务项临时解决办法'
date: 2023-09-29 19:25:54
tags: [Linux]
published: true
hideInList: false
feature: 
isTop: false
---
临时解决方案有用，但是经过测试，是修改两个文件，而不是一个
```bash
sudo vim /etc/systemd/system.conf
sudo vim /etc/systemd/user.conf
 ```
把
```bash
#DefaultTimeoutStartSec=90s
#DefaultTimeoutStopSec=90s
```
修改为
```bash
DefaultTimeoutStartSec=10s
DefaultTimeoutStopSec=10s
```

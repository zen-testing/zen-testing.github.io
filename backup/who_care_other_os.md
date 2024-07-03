---
title: '解决新版本update-grub不鸟其他系统的问题'
date: 2023-11-07 09:33:03
tags: [Linux]
published: true
hideInList: false
feature: 
isTop: false
---
```bash
sudo update-grub
```
执行后会警告不加入其他系统

# 解决办法

```bash
echo 'GRUB_DISABLE_OS_PROBER=false' >> /etc/default/grub
```
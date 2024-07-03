---
title: 'WSL挂载移动硬盘U盘'
date: 2023-08-18 13:59:38
tags: [WSL,Windows]
published: true
hideInList: false
feature: 
isTop: false
---
假设你的移动硬盘在windows下显示为 `G:\`

1. 新建文件夹g

```bash
sudo mkdir /mnt/g
```

2. 挂载盘符g

```bash
sudo mount -t drvfs G: /mnt/g
```

3. 大功告成.进入`/mnt/g`即可

4. 弹出移动硬盘,这样才能在windows下正常弹出,否则是会一直占用的.

```bash
sudo umount /mnt/g  
```
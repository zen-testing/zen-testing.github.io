---
title: 'wsl挂载移动硬盘和u盘'
date: 2023-07-21 17:46:43
tags: [Windows]
published: true
hideInList: false
feature: 
isTop: false
---
WSL比起linux挂载硬盘简单一些。而且windows本身自己的硬盘位ntfs格式，所以移动硬盘感觉挂载要比单纯的linu下ntfs挂载更加稳定一些。个人感觉而已....无法验证。

假设你的移动硬盘在windows下显示为 G:\\

1. 新建文件夹

```powershell
sudo mkdir /mnt/g
```

2. 挂载盘符

```powershell
sudo mount -t drvfs G: /mnt/g
```

3. 大功告成

进入/mnt/g即可与windows下一摸一样。

4. 弹出移动硬盘，这样才能在windows下正常弹出，否则是会一直占用的。

```powershell
sudo umount /mnt/g  
```
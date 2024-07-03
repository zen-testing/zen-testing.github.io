---
title: 'Linux 的 挂载命令如何添加所有用户的读写执行权限'
date: 2023-05-24 20:43:05
tags: [Linux]
published: true
hideInList: false
feature: 
isTop: false
---
在Linux中,可以

## 使用`mount`命令的`-o`选项来指定挂载选项

要给所有用户添加读写执行权限,可以使用以下选项

`-o umask=000` 
`umask`值指定新建文件或目录的权限掩码.`umask=000`表示创建文件或目录时不修改权限,直接保留指定的值.
所以,如果指定`-o umask=000`,则在挂载时为所有用户赋予最高权限777.
例如,挂载一个USB盘:

```bash
mount -o umask=000 /dev/sdb1 /mnt/usb 
``` 

## -o permissions:

直接指定挂载点的权限,如:

```bash
mount -o permissions=777 /dev/sdb1 /mnt/usb
```

---
title: '在Linux中挂载ISO'
date: 2023-05-24 20:44:34
tags: [Linux]
published: true
hideInList: false
feature: 
isTop: false
---
挂载ISO文件步骤

1. 创建挂载点目录

```bash
mkdir /mnt/iso
```

2. 挂载ISO文件

```bash 
mount -o loop /path/to/filename.iso /mnt/iso

# /path/to/filename.iso:ISO文件的路径
# /mnt/iso:挂载点目录
# -o loop:指定以loop设备挂载
```

3. 访问ISO文件内容

可以在/mnt/iso目录下访问ISO文件中的内容

4. 卸载ISO文件

```bash
umount /mnt/iso
# 完成ISO文件访问后记得要卸载,否则可能导致进程占用ISO文件而无法删除.
```

5. 举个例子

```bash
mkdir /mnt/centos7
mount -o loop /home/user/CentOS-7-x86_64-DVD.iso  /mnt/centos7

ls /mnt/centos7
# 可以看到CentOS安装镜像的内容

umount /mnt/centos7
```

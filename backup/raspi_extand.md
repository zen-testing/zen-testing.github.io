---
title: '树莓派扩展根分区'
date: 2023-08-18 13:14:50
tags: [Raspberry]
published: true
hideInList: false
feature: 
isTop: false
---
# 树莓派扩展 root 根分区

使用了封装好的镜像后发现root分区只有3GB,为了避免出现未来不够用的情况,我准备把root分区扩展到最大容量.

**操作不会影响分区数据,但记得重要数据需要备份!**

1. 使用fdisk进入磁盘分区工具

```bash
sudo fdisk /dev/mmcblk0
```

2. 查看现有分区

输入`p` 正常情况应该有两个分区第一个是`boot` 第二个是系统所在分区
看起来会是这种形式

|Devices| Boot |Start|End|Sectors|Size|Id|Type|
|:---:|:----:|:---:|:---:|:---:|:---:|:---:|:---:|
|/dev/mmcblk0p1|      |8192|532480|523289|256M|c|W95 FAT32 (LBA)|
|/dev/mmcblk0p2|      |540672|31291391|30750720|14.7G|83|Linux|

3. 删除第二块分区

输入`d`后输入`2`

4. 建立新分区

输入`n`后输入`p`

分区编号输入`2`

起始块输入之前记录的起始块数`540672`

结束块直接使用默认的最大值(直接回车)

提示移除分区签名选择`N`

5. 保存更改

输入`p`检查新分区

确认无误后输入`w`保存

6. 重启树莓派

```bash
sudo reboot
```

7. 可选操作

```bash
# 重启后使用 resize2fs修复新分区
sudo resize2fs /dev/mmcblk0p2
```

8. 查看成果

```bash
df -h
```
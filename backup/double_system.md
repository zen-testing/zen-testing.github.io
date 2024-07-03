---
title: '双系统安装方案-硬盘规划'
date: 2022-09-26 16:18:23
tags: [双系统]
published: true
hideInList: false
feature: 
isTop: false
---

安装Linux+Windows双系统常用的硬盘规划方案

### 单硬盘

|分区|格式|备注|
|:---:|:---:|:---:|
|esp|fat32|windows的efi分区|
|msr|ntfs|windows的msr分区|
|windows|ntfs|windows的系统盘|
|recovery|ntfs|windows的恢复分区(可选)|
|oem|ntfs|品牌笔记本的特定功能分区(可选)|
|sda6|efi|linux的efi分区|
|sda7|ext4|linux的/分区|

### 双硬盘

|分区|格式|备注|
|:---:|:---:|:---:|
|esp|fat32|windows的efi分区|
|msr|ntfs|windows的msr分区|
|windows|ntfs|windows的系统盘|
|recovery|ntfs|windows的恢复分区(可选)|
|oem|ntfs|品牌笔记本的特定功能分区(可选)|
|sdb1|efi|linux的efi分区|
|sdb2|ext4|linux的/分区|

都2022年了,不会有人还在坚守legacy吧? 不会吧?
![不会吧](https://i11.hoopchina.com.cn/hupuapp/bbs/0/thread_0_20210603135107_93554.jpg)

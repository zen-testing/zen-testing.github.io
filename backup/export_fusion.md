---
title: '解决Fusion个人版虚拟机导出问题'
date: 2022-12-19 21:55:06
tags: [vmware]
published: true
hideInList: false
feature: 
isTop: false
---
虽然Fusion个人版免费,但是也缺少了导出虚拟机功能,这里提供了一种使用命令的方法

<!-- more -->

```shell
cd /Applications/VMware\ Fusion.app/Contents/Library/VMware\ OVF\ Tool/

./ovftool  <PATH TO SOURCE VM's .vmx file>   <PATH TO OUTPUT ova file>

# example
./ovftool --acceptAllEulas ~/Documents/Virtual\ Machines.localized/CentOS\ 6.5.vmwarevm/CentOS\ 6.5.vmx      /tmp/CentOS6.5.ova
```

也可以导出vmware workstation可识别的虚拟机文件
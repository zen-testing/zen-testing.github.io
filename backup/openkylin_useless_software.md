---
title: '可以精简掉的软件，尤其是在单板计算机的系统中不要有这些东西'
date: 2023-11-23 17:05:36
tags: [openKylin]
published: true
hideInList: false
feature: 
isTop: false
---
```bash
#!/bin/bash
# 虚拟键盘
sudo apt remove kylin-virtual-keyboard
# 语音助手
sudo apt remove kylin-asrassistant
# 工具箱
sudo apt remove youker-assistant
# 平板桌面
sudo apt remove ukui-tablet-desktop
# mate 文本编辑器(kate编辑器替代)
sudo apt remove pluma
# kylin影音(ffplay替代)
sudo apt remove kylin-video
# kylin启动盘创建工具(dd命令替代)
sudo apt remove kylin-usb-creator
# kylin平板桌面
sudo apt remove kylin-tablet-desktop-general
# kylin扫描
sudo apt remove kylin-scanner
# kylin录音机
sudo apt remove kylin-recorder
# kylin打印
sudo apt remove kylin-printer
# kylin看图
sudo apt remove kylin-photo-viewer
# kylin音乐
sudo apt remove kylin-music
# 高仿Micorsoft VS Code(sublime text替代)
sudo apt remove kylin-code
# kylin计算器
sudo apt remove kylin-calculator
# kylin刻录
sudo apt remove kylin-burner
# WPS(libreoffice替代)
sudo apt remove wps-office
# kylin用户手册
sudo apt remove kylin-user-guide
# 安装器(apt命令替代)
sudo apt remove kylin-installer
# kylin备份(dd命令替代)
sudo apt remove yhkylin-backup-tools
# kylin便笺
sudo apt remove ukui-notebook
# kylin多端协同
sudo apt remove kylin-connectivity
# kylin传书(局域网传文件)(scp命令替代)
sudo apt remove kylin-ipmsg
# kylin管家
sudo apt remove kylin-os-manager
# 生物特征管理工具(不允许单独卸载)
sudo apt remove ukui-biometric-manager
# kylin天气(curl wttr.in?lang=zh替代)
sudo apt remove kylin-weather
# kylin闹钟
sudo apt remove ukui-clock
```
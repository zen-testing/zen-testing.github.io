---
title: '卸载UOS默认安装但是不必要的软件和服务'
date: 2022-09-26 18:30:33
tags: [UOS]
published: true
hideInList: false
feature: 
isTop: false
---

# 软件

建议使用`sudo apt-get purge`命令卸载

|软件名|包名|
|:---:|:---:|
|相册|deepin-album|
|桌面智能助手|deepin-aiassistant|
|手机助手|deepin-mobile-assistant|
|启动盘制作工具|deepin-boot-maker|
|画板|deepin-draw|
|音乐|deepin-music|
|影院|deepin-movie|
|电脑管家|deepin-pc-butler<br>deepin-pc-butler-daemon|
|服务与支持|uos-service-support|
|日历|dde-calendar|
|语音记事本|deepin-voice-note|
|计算器|deepin-calculator|
|下载器|org.deepin.downloader|
|文档查看器|deepin-reader|
|看图|deepin-image-viewer|
|远程协助|uos-remote-assistance|
|安全中心|deepin-defender<br>deepin-defender-vdbup|
|五子棋|com.deepin.gomoku|
|连连看|com.deepin.lianliankan|
|联系人|deepin-contacts<br>org.deepin.contacts|
|邮箱|deepin-mail|
|打印管理|dde-printer|
|地理定位服务|geoclue-2.0|
|扫描管理器|org.deepin.scanner|
|帮助手册|deepin-manual|
|归档管理器|deepin-compressor|
|浏览器|org.deepin.browser<br>uos-browser-plugin|
|Gnome浏览器|yelp<br>yelp-xsl|
|日志收集工具|deepin-log-viewer|
|全局搜索|dde-grand-search|
|A/B备份还原后端服务|deepin-ab-recovery|
|相机|deepin-camera|
|Android 虚拟机|UEngine<br>uengine-android-image<br>uengine-modules-dkms|
|安装器|deepin-deb-installer|
|U粉俱乐部|deepin-ucare-club|
|怀疑用来强制安装程序|deepin-pre-package|
|应用商店|deepin-app-store|
|plymouth-theme-deepin-logo|开机笑脸动画|
|deepin-icon-theme|图标主题|
|blur-effect|模糊效果|
|openbox|windowsmanager|

# 服务

用不到的服务使用`systemctl`命令停止并禁用

|服务|服务名|
|:---:|:---:|
|通用打印服务|cups|
|笔记本模式|laptop-mode|
|开机声音|deepin-login-sound|
|关机声音|deepin-shutdown-sound|
|建立文件索引|deepin-anything-tool<br>deepin-anything-monitor|
|网络唤醒|deepin-wakeonlan|

# 水印
`/usr/share/deepin/dde-desktop-watermask.json`

# 脚本

保存以下内容命名为removeUOS.sh
```shell
#!/usr/bin/env bash

echo 相册
sudo apt-get purge -y deepin-album
echo 桌面智能助手
sudo apt-get purge -y deepin-aiassistant
echo 手机助手
sudo apt-get purge -y deepin-mobile-assistant
echo 启动盘制作工具
sudo apt-get purge -y deepin-boot-maker
echo 画板
sudo apt-get purge -y deepin-draw
echo 音乐
sudo apt-get purge -y deepin-music
echo 影院
sudo apt-get purge -y deepin-movie
echo 五子棋
sudo apt-get purge -y com.deepin.gomoku
echo 连连看
sudo apt-get purge -y com.deepin.lianliankan
echo 电脑管家
sudo apt-get purge -y deepin-pc-butler
sudo apt-get purge -y deepin-pc-butler-daemon
echo 服务与支持
sudo apt-get purge -y uos-service-support
echo 日历
sudo apt-get purge -y dde-calendar
echo 语音记事本
sudo apt-get purge -y deepin-voice-note
echo 计算器
sudo apt-get purge -y deepin-calculator
echo 下载器
sudo apt-get purge -y org.deepin.downloader
echo 文档查看器
sudo apt-get purge -y deepin-reader
echo 看图
sudo apt-get purge -y deepin-image-viewer
echo 远程协助
sudo apt-get purge -y uos-remote-assistance
echo 安全中心
sudo apt-get purge -y deepin-defender
sudo apt-get purge -y deepin-defender-vdbup
echo 联系人
# echo sudo rm -rf /usr/share/bizBin
sudo apt-get purge -y deepin-contacts
sudo apt-get purge -y org.deepin.contacts
echo 邮箱
sudo apt-get purge -y deepin-mail
echo 打印机管理
sudo apt-get purge -y dde-printer
echo 地理定位服务
sudo apt-get purge -y geoclue-2.0
echo 扫描管理器
sudo apt-get purge -y org.deepin.scanner
echo 帮助手册
sudo apt-get purge -y deepin-manual
echo 归档管理器
sudo apt-get purge -y deepin-compressor
echo 浏览器
sudo apt-get purge -y org.deepin.browser
sudo apt-get purge -y uos-browser-plugin
echo Gnome浏览器
sudo apt-get purge -y yelp
sudo apt-get purge -y yelp-xsl
echo 日志收集工具
sudo apt-get purge -y deepin-log-viewer
echo 全局搜索
sudo apt-get purge -y dde-grand-search
echo A/B 备份还原后端服务
sudo apt-get purge -y deepin-ab-recovery
echo 相机
sudo apt-get purge -y deepin-camera
echo Android 虚拟机
sudo apt-get purge -y UEngine
sudo apt-get purge -y uengine-android-image
sudo apt-get purge -y uengine-modules-dkms
echo 安装器
sudo apt-get purge -y deepin-deb-installer
echo U粉俱乐部
sudo apt-get purge -y deepin-ucare-club
echo 怀疑用来强制安装程序
sudo apt-get purge -y deepin-pre-package
echo 应用商店
sudo apt-get purge -y deepin-app-store
echo 停止并禁止自启动通用打印服务
sudo systemctl stop cups
sudo systemctl disable cups
echo 停止并禁止自启动笔记本模式
sudo systemctl stop laptop-mode
sudo systemctl disable laptop-mode
echo 停止并禁止自启动开机声音
sudo systemctl stop deepin-login-sound
sudo systemctl disable deepin-login-sound
echo 停止并禁止自启动关机声音
sudo systemctl stop deepin-shutdown-sound
sudo systemctl disable deepin-shutdown-sound
echo 停止并禁止自启动建立文件索引
sudo systemctl stop deepin-anything-tool
sudo systemctl disable deepin-anything-tool
sudo systemctl stop deepin-anything-monitor
sudo systemctl disable deepin-anything-monitor
echo 停止并禁止自启动网络唤醒
sudo systemctl stop deepin-wakeonlan
sudo systemctl disable deepin-wakeonlan
echo 打完收工
sudo apt-get update && sudo apt-get -y upgrade && sudo apt-get -y dist-upgrade && sudo apt-get -y autoremove
```



# 添加运行权限
`$ chmod a+x ./removeUOS.sh`
# 运行
`$ sudo ./removeUOS.sh`
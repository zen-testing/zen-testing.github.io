---
title: 'linux启动器文件详解'
date: 2022-09-26 17:23:32
tags: [Linux]
published: true
hideInList: false
feature: 
isTop: false
---

```shell
[Desktop Entry]
Name=firefox
Name[zh_CN]=火狐浏览器
Comment=火狐浏览器
Exec=/home/jimmy/Soft/firefox/firefox
Icon=/home/jimmy/Soft/firefox/browser/icons/mozicon128.png
Terminal=false
Type=Application
Categories=Application;
Encoding=UTF-8
StartupNotify=true
NoDisplay=true
Hidden=true
```

|关键词|意义|
|:----:|:---:|
|[Desktop Entry]|文件头|
|Encoding|编码|
|Name|应用名称|
|Name[xx]|不同语言的应用名称|
|Comment|描述|
|Exec|执行的命令|
|Icon|图标路径|
|Terminal|是否使用终端|
|Type|启动器类型|
|Categories|应用的类型(内容相关)|
|NoDisplay|在启动台中显示|
|Hidden|在dash中隐藏这个图标|

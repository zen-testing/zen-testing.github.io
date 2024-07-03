---
title: 'Windows家庭版开启HyperV功能'
date: 2022-09-26 21:06:32
tags: [Windows]
published: true
hideInList: false
feature: 
isTop: false
---
<iframe width="100
%" height="100%" src="https://player.bilibili.com/player.html?aid=762946237&bvid=BV1m64y1h7c9&cid=407703383&page=1" scrolling="no" border="0" frameborder="no" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" framespacing="0" allowfullscreen="true"> </iframe>

# 使用记事本编辑文件enableHyperV.bat并保存为ANSI编码
```
pushd "%~dp0"
dir /b %SystemRoot%\servicing\Packages\*Hyper-V*.mum >hyper-v.txt
for /f %%i in ('findstr /i . hyper-v.txt 2^>nul') do dism /online /norestart /add-package:"%SystemRoot%\servicing\Packages\%%i"
del hyper-v.txt
Dism /online /enable-feature /featurename:Microsoft-Hyper-V-All /LimitAccess /ALL

```
# 以管理员身份运行

# 尽量重启一次再使用
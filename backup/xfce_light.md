---
title: 'xfce桌面调节屏幕背光亮度'
date: 2022-09-26 21:31:15
tags: [Linux,xfce]
published: true
hideInList: false
feature: 
isTop: false
---
# 相关目录

```shell
/sys/class/backlight/xxx/brightness
```

比如我这里是

```shell
/sys/class/backlight/amdgpu_bl0/brightness
```

可调节范围

`0~255`

可直接使用重定向修改文件内容

`echo 50 > /sys/class/backlight/amdgpu_bl0/brightness`
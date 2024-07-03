---
title: '桌面管理器slim相关配置'
date: 2022-09-26 21:27:24
tags: [Linux]
published: true
hideInList: false
feature: 
isTop: false
---
slim的主题文件在`/usr/share/slim/themes/default/`

slim的配置文件在`/etc/slim.conf`

# slim的主题文件

```shell
# text04 theme for SLiM
# by Johannes Winkelmann

# Messages (ie: shutdown)
msg_color               #FFFFFF
msg_font                Verdana:size=18:bold:dpi=75
msg_x                   50%
msg_y                   40%
msg_shadow_color #702342
msg_shadow_xoffset 1
msg_shadow_yoffset 1

# valid values: stretch, tile
background_style        stretch
background_color        #eedddd

# Input controls
input_panel_x           10%
input_panel_y           60%
input_name_x            394
input_name_y            181
input_font          	Verdana:size=12:dpi=75
input_color             #000000

# Username / password request
username_font          	Verdana:size=14:bold:dpi=75
username_color        	#f9f9f9
username_x              280
username_y              183
password_x              50%
password_y              183
username_shadow_color   #702342
username_shadow_xoffset 1
username_shadow_yoffset 1

username_msg            Username:
password_msg            Password:

# session messages eg: pressing F1: 切换de时显示的文字
session_x 50%
session_y 95%
session_font DejaVu Sans:bold:size=12:dpi=96
session_color #ffffff
#session_shadow_xoffset 1
#session_shadow_yoffset 1
#session_shadow_color #000000

## panel 输入面板在屏幕中的位置
# Horizonatal and vertical position for the panel.
input_panel_x 10%
input_panel_y 40%
```

# 快速预览主题的改动

```shell
slim -p /usr/share/slim/themes/default/
```

# 效果图

![](https://i.imgur.com/r0sDs1Z.jpg)

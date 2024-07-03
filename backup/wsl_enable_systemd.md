---
title: 'WSL开启原生systemd'
date: 2022-10-23 12:11:42
tags: [WSL]
published: true
hideInList: false
feature: 
isTop: false
---
wsl2版本不低于0.67

<!-- more -->

# 查看版本：

`wsl --version`

# 如果已经安装的版本太低，可以升级一下：

`wsl --update`

# 进入子系统

`wsl -d <子系统名称>`

# 进入子系统之后，修改wsl子系统配置

```shell
vim /etc/wsl.conf

#添加以下内容
[boot]
systemd=true

exit 退出子系统，关闭子系统

wsl --shutdown <子系统名称>
```
# 重新进入子系统
```shell
#查看是否正常启动，如果返回init则失败，如果返回systemd则成功
ps --no-headers -o comm 1
```

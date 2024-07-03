---
title: '允许使用root用户登录ssh'
date: 2022-09-26 15:16:19
tags: [ssh,Linux]
published: true
hideInList: false
feature: 
isTop: false
---

近期在本地的虚拟机VMware上安装了Ubuntu 21.04.3 LTS,由于系统是无界面的,所有操作都需要通过Linux命令进行操作.后来不想直接在服务器上操作,想通过PowerShell去访问Linux系统.却发现根本连接不上.后来查资料,原来需要在Ubuntu上安装SSH协议软件,因为Ubuntu默认是不安装SSH服务的.安装了SSH服务后发现其他用户可以通过Xshell远程访问了,root用户访问会报密码被拒绝的错误,上网查资料,发现Ubuntu默认是不开启root远程登录的,需要设置一下.

# 检查是否开启SSH服务
```shell
ps -e|grep ssh
//查看SSH服务是否开启,或者通过命令:service sshd status 可以查看某个服务的状态.
```

# 安装SSH服务
```shell
apt-get install ssh
```
# 启动SSH服务
```shell
sudo /etc/init.d/ssh start
```
# 修改SSH配置文件
```shell
sudo vim /etc/ssh/sshd_config
```
找到`PermitRootLogin without-password`
修改为`PermitRootLogin yes`
# 重启SSH服务
`service ssh restart`

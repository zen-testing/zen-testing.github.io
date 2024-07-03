---
title: 'ssh三步解决免密登录'
date: 2022-09-26 19:11:29
tags: [ssh]
published: true
hideInList: false
feature: 
isTop: false
---

# 1.客户端生成公私钥

```shell
$ ssh-keygen -t rsa -C "zhangyiming748@gmail.com"
```

# 2.上传公钥到服务器

### 方式一 通过`ssh-copy-id`命令设置

>最后一个参数是我们要免密钥登录的服务器 ip 地址.

```shell
$ ssh-copy-id -i ~/.ssh/id_rsa.pub pi@192.168.1.5
```

### 方式二 通过`scp`直接将该文件远程复制过去

>使用这种方式需要注意,如果你之前已经配置了其它服务器上的密钥,这是使用这种方法,就会覆盖掉你原来的密钥,这时候是不建议使用这种方式的,如果你是先将该文件复制到服务器上的一个目录下,然后在使用追加的方式,将密钥追加到 authorized_keys 也是完全 OK 的.如果你只有两台服务器也是可以直接复制到文件.

```shell
scp -p ~/.ssh/id_rsa.pub root@:/root/.ssh/authorized_keys
```

### 方式三 通过手工复制

>将本地 id_rsa.pub 文件的内容拷贝至远程服务器的 ~/.ssh/authorized_keys 文件中也完全可以的.先使用 cat 命令查看当前的公钥,然后复制,在到目标服务器上去粘贴.

```shell
echo <cat ~/.ssh/id_rsa.pub> >> ~/.ssh/authorized_keys
```
# 3.测试免密登录

客户端通过ssh连接远程服务器,就可以免密登录了.
```shell
ssh pi@192.168.1.5
```
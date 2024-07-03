---
title: '(Debian/Ubuntu)mysql8.x 设置或更改root密码'
date: 2022-10-25 10:51:24
tags: [Linux,MySql]
published: true
hideInList: false
feature: 
isTop: false
---
本来也不想写这类的教程，因为这都是运维该干的事儿，我不了解也不想了解。没想到有一个人发现他在openKylin上安装自带的Mysql，并不能更改root用户的密码，然后不知道怎么想的，直接给了一个结论说通过apt安装的数据库，本来就不能更改root密码，然后就写了一个所谓的教程，教你怎么在openKylin系统上添加别的已经很完善的系统的源，然后安装数据库。我就很费解这个事，不会和不能是两回事，不能因为你不会就告诉大家这个东西不能。

<!-- more -->

<iframe width="100%" height="550" src="https://www.youtube.com/embed/nF8zUpICKDk" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

如果视频无法显示,点击[这里](http://player.bilibili.com/player.html?aid=304378272&bvid=BV18P411A7n6&cid=871477088&page=1)查看
# 0x01

通过`/etc/mysql/debian.cnf`文件查看初始用户名和密码

```shell
host     = localhost
user     = debian-sys-maint
password = QOjIKKtExpD5cXRK
socket   = /var/run/mysqld/mysqld.sock
```

# 0x02

进入对应的数据库

```sql
show databases;
use mysql;
```

# 0x03

设置新密码

```sql
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '你的密码';  
```

# 0x04

重启服务或重启电脑

```shell
$ sudo systemctl restart mysql
```

# 0x05

使用新密码登陆

```shell
mysql -u root -p
```

# 分析

我觉得这个人很有可能是在国内的CSDN等粪坑上找到一些7.0版本之前的教程。 因为之前版本原有字段在更新后有了一些改变，在他每一次尝试输入代码更改数据库表的时候一定会报错，所以我认为他有可能是觉得因为一直在报错，但写的完全是按照网上的教程来的，所以这个数据改不了。
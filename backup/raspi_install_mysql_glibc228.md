---
title: '树莓派安装mysql-glibc2.28'
date: 2023-06-15 23:33:15
tags: [Raspberry,MySql]
published: true
hideInList: false
feature: 
isTop: false
---
# 解压

```bash
tar xvf mysql-8.0.33-linux-glibc2.28-aarch64.tar.gz -C /opt
```

# 重命名

```bash
mv mysql-8.0.33-linux-glibc2.28-aarch64 mysql8
```

# 创建数据存放文件夹

```bash
mkdir /opt/mysql8/data
```

# 创建用户组以及用户

```bash
groupadd mysql
useradd -g mysql mysql
id mysql
```

# 授权用户

```bash
chown -R mysql.mysql /opt/mysql8
```

# mysql初始化

```bash
./mysqld --user=mysql --basedir=/opt/mysql8 --datadir=/opt/mysql8/data/ --initialize
```

# 记住初始密码

```bash
2023-06-15T14:57:01.077372Z 0 [System] [MY-013169] [Server] /opt/mysql8/bin/mysqld (mysqld 8.0.33) initializing of server in progress as process 7933
2023-06-15T14:57:01.119821Z 1 [System] [MY-013576] [InnoDB] InnoDB initialization has started.
2023-06-15T14:57:06.984302Z 1 [System] [MY-013577] [InnoDB] InnoDB initialization has ended.
2023-06-15T14:57:13.289470Z 6 [Note] [MY-010454] [Server] A temporary password is generated for root@localhost: <Q1ZlruFqsfy
```

# 编辑配置文件

```bash
vim /etc/my.cnf
[mysqld]
#default_authentication_plugin=mysql_native_password
bind-address=0.0.0.0
port=3306
user=mysql
basedir=/usr/local/mysql8
datadir=/usr/local/mysql8/data
socket=/tmp/mysql.sock
#character config
character_set_server=utf8mb4
symbolic-links=0
lower_case_table_names=0
max_connections=1024
```

# 添加mysqld服务

```bash
cp -a ./support-files/mysql.server /etc/init.d/mysql
chmod +x /etc/init.d/mysql
vim /etc/init.d/mysql
# 其中basedir和datadir修改为对应目录
```

# 设置环境变量

```bash
echo 'export PATH=$PATH:/opt/mysql8/bin' >> /etc/profile
source /etc/profile
```

# 重启电脑后开启服务

```bash
sudo systemctl reboot
sudo systemctl start mysql
sudo systemctl enable mysql
```

# 修改root密码

```bash
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '123456';
```

# 创建远程用户

```bash
CREATE USER 'zen'@'%' IDENTIFIED BY '123456';
```

# 赋予新用户所有权限

```bash
GRANT ALL PRIVILEGES ON *.* TO 'zen'@'%' WITH GRANT OPTION;
```

# 刷新权限表

```bash
FLUSH PRIVILEGES;
```
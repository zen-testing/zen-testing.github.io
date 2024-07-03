---
title: '5分钟物理恢复MySQL数据'
date: 2023-11-23 17:19:22
tags: [五分钟已经很棒了]
published: true
hideInList: false
feature: 
isTop: false
---
```bash
docker run --name src -p 3306:3306 -v /Users/zen/container/src:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 -d mysql:8.2
```

```sql
-- 源机器上创建用户
CREATE USER 'zen'@'%' IDENTIFIED BY 'Qwert1234%';
GRANT ALL PRIVILEGES ON *.* TO 'zen'@'%' WITH GRANT OPTION;
```

```sql
-- 源机器上创建表
CREATE TABLE `mydb`.`class`  (
  `id` int NOT NULL,
  `name` varchar(255) NULL,
  `age` int NULL,
  `sex` bool NULL,
  PRIMARY KEY (`id`)
);
```

```bash
# 欧洲卡车模拟2
cp -Ra src dst
# 确认文件权限 如果改变 改回来
chown -R mysql:mysql dst
```


```bash
docker run --name dst -p 2147:3306 -v /Users/zen/container/dst:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 -d mysql:8.2
```

查看之前的表
```sql
DESCRIBE class;
```

```bash
+-------+--------------+------+-----+---------+-------+
| Field | Type         | Null | Key | Default | Extra |
+-------+--------------+------+-----+---------+-------+
| id    | int          | NO   | PRI | NULL    |       |
| name  | varchar(255) | YES  |     | NULL    |       |
| age   | int          | YES  |     | NULL    |       |
| sex   | tinyint(1)   | YES  |     | NULL    |       |
+-------+--------------+------+-----+---------+-------+
4 rows in set (0.00 sec)
```

查看之前的权限

```sql
select user,host from user ;
```

```bash
+------------------+-----------+
| user             | host      |
+------------------+-----------+
| root             | %         |
| zen              | %         |
| mysql.infoschema | localhost |
| mysql.session    | localhost |
| mysql.sys        | localhost |
| root             | localhost |
+------------------+-----------+
6 rows in set (0.00 sec)
```
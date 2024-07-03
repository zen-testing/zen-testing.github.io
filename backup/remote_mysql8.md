---
title: 'MySql8.x允许外部访问'
date: 2022-10-25 19:43:53
tags: [Linux,MySql]
published: true
hideInList: false
feature: 
isTop: false
---
# 0x01

登陆后使用`mysql`库

```sql
use mysql
```

# 0x02

更新域属性

```sql
update user set host='%' where user ='root';
```

# 0x03

应用当前表到内存

```sql
FLUSH PRIVILEGES;
```

# 0x04

执行授权语句

```sql
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%'WITH GRANT OPTION;
```
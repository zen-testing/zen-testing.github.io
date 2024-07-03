---
title: 'os.Mkdir/os.MkdirAll区别'
date: 2022-09-26 16:59:15
tags: [Golang]
published: true
hideInList: false
feature: 
isTop: false
---
# Mkdir 用于创建单个目录

```
err:=os.Mkdir("./dir1",os.ModePerm)
if err!=nil{
   fmt.Println(err)
}
```

# MkdirAll 用于创建文件夹路径
```
err=os.MkdirAll("./dir1/dir2",os.ModePerm)
if err!=nil{
   fmt.Println(err)
   }
err为nil
//成功创建dir1/dir2文件路径
```

---
title: '使用exec.Command执行带管道的命令'
date: 2023-11-07 11:31:35
tags: [Golang]
published: true
hideInList: false
feature: 
isTop: false
---
使用 sh -c ""命令
`exec.Command("bash", "-c", "ps aux|grep go")`
这是推荐的做法。
如果输出不是很多，推荐使用github.com/go-cmd/cmd库来执行系统命令，如：
```golang
import "github.com/go-cmd/cmd"

c := cmd.NewCmd("bash", "-c", "ps aux|grep go")
<-c.Start()
fmt.Println(c.Status().Stdout)
```
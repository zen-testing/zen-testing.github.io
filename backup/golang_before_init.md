---
title: 'golang 中在init之前运行的函数'
date: 2023-11-23 17:30:09
tags: [Golang]
published: true
hideInList: false
feature: 
isTop: false
---
```golang
package main

import "fmt"

var a = 8
// b 会最先运行
var b = func() int {
	fmt.Println("b")
	return 0
}()

func init() {
	fmt.Println("init")
}

func main() {
	fmt.Println("main")
}

func hello() {
	fmt.Println("hello")
}
```

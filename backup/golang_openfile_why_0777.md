---
title: 'golang openfile 权限 0777'
date: 2023-11-23 17:33:20
tags: [Golang]
published: true
hideInList: false
feature: 
isTop: false
---
```golang
func of() {
	os.OpenFile("name", os.O_APPEND|os.O_CREATE|os.O_RDWR, 0777)
	// 其中 0 代表八进制数字的前缀标记
	num := 10 + 010 + 0xf
	fmt.Println(num)
}
```
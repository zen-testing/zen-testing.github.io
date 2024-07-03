---
title: 'golang interface 的类型断言'
date: 2023-11-07 11:15:21
tags: [Golang]
published: true
hideInList: false
feature: 
isTop: false
---
```golang
func main() {
	var data interface{} = "ehoo"
	if res, ok := data.(int); ok {
		fmt.Printf("int res:%d\n", res)
	} else if res, ok := data.(bool); ok {
		fmt.Printf("bool res:%b\n", res)
	} else {
		fmt.Printf("other res:%v\n", res) // 断言类型的零值,结果:false
	}
}
```
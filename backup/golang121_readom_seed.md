---
title: 'Golang1.21废弃的方法--random.seed'
date: 2023-09-29 19:30:48
tags: [Golang]
published: true
hideInList: false
feature: 
isTop: false
---
![seed方法已经被废弃](https://z1.ax1x.com/2023/09/29/pPqP1eA.png)
新的方式如下
```golang
func RandomWithSeed() {
	rand.Seed(time.Now().Unix())
	a := rand.Intn(2000)
	seed := rand.New(rand.NewSource(time.Now().Unix()))
	b := seed.Intn(2000)
	if a == b {
		slog.Info("生成的随机数", slog.Int("a", a), slog.Int("b", b))
	} else {
		slog.Info("不相等")
	}
}
```

但是经过测试,两者等效,虽然被废弃但是功能相同
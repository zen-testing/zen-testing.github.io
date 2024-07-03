---
title: '面试的时候为什么非要问一些一线工作人员根本不可能有时间死记硬背的问题'
date: 2024-03-19 14:36:19
tags: [Golang]
published: true
hideInList: false
feature: 
isTop: true
---
### golang从是什么时候开始测试slog日志包？什么版本之后归入标准库？

Golang 从 Go 1.17 版本开始在 `golang.org/x/exp/slog` 下提供 slog 包的测试版本，并在 Go 1.21 版本正式将其纳入标准库，导入路径为 log/slog。
slog 包 是 Go 官方团队设计并开发的结构化日志包，旨在提供一种更易用、更高效的日志记录方式。
slog 包的测试版本 在 Go 1.17 版本中首次提供，主要用于收集社区反馈并进行完善。在测试阶段，slog 包的 API 和功能可能发生变化。
slog 包 在 Go 1.21 版本中正式纳入标准库，这意味着其 API 和功能已经稳定，可以用于生产环境。
以下是 slog 包的测试版本和正式版本之间的主要区别：
• 测试版本 的 API 和功能可能发生变化。
• 正式版本 的 API 和功能已经稳定。
• 测试版本 不在 Go 标准库中，需要通过 `go mod download` 命令下载。
• 正式版本 在 Go 标准库中，可以直接使用。
如果您想要使用 slog 包，建议使用 Go 1.21 或更高版本。
以下是一些关于 slog 包的学习资源：
• Go 官方文档: [移除了无效网址]
• Tony Bai: [slog正式版来了：Go日志记录新选择！](https://tonybai.com/2023/09/01/slog-a-new-choice-for-logging-in-go)

### golang什么时候开始弃用ioutil包？

Golang 从 Go 1.16 版本开始弃用 ioutil 包。
原因：
• ioutil 包中的许多函数功能已被其他包取代，例如 io 包和 os 包。
• ioutil 包中的函数命名不规范，不易理解。
• ioutil 包缺乏类型安全性，容易导致错误。
建议：
• 优先使用 io 包和 os 包中的函数来替代 ioutil 包中的函数。
• 如果需要使用 ioutil 包中的函数，请谨慎使用，并注意类型安全性。
以下是 ioutil 包中一些常用函数的替代方案：
函数	替代方案
```golang
ReadFile	io.ReadFile
WriteFile	os.WriteFile
TempFile	ioutil.TempFile
ReadDir	ioutil.ReadDir
```
如果您正在使用 ioutil 包，建议您尽快将其迁移到其他包。

### golang的切片扩容策略从哪一个版本开始发生了改变
Golang 的切片扩容策略在 Go 1.18 版本发生了改变。
Go 1.18 之前的版本：
• 当切片容量小于 1024 时，扩容后容量为原来的 2 倍。
• 当切片容量大于或等于 1024 时，扩容后容量为原来的 1.25 倍。
Go 1.18 版本之后的版本：
• 当新切片需要的容量大于两倍扩容的容量，则直接按照新切片需要的容量扩容。
• 当原切片容量小于阈值（threshold）时，新切片容量变成原来的 2 倍。
• 当原切片容量大于或等于阈值时，进入循环，每次容量增加（旧容量 + 3 * 阈值） / 4。
阈值 的值根据系统架构而异，在 32 位系统上为 1024，在 64 位系统上为 4096。
以下是 Go 1.18 之前和之后切片扩容策略的示例：
Go 1.18 之前
```Go
s := make([]int, 0, 10)
// 添加 11 个元素fori := 0; i < 11; i++ {
    s = append(s, i)
}
// 切片容量扩容为 20fmt.Println(cap(s)) // 20
```
Go 1.18 之后

```Go
s := make([]int, 0, 10)
// 添加 11 个元素fori := 0; i < 11; i++ {
    s = append(s, i)
}
// 切片容量扩容为 16fmt.Println(cap(s)) // 16
```
Go 1.18 版本对切片扩容策略的改变主要有以下几个优点：
• 减少了内存浪费。
• 提高了内存分配效率。
• 降低了 GC 压力。
如果您正在使用 Go 1.18 或更高版本，建议您了解新的切片扩容策略，以便更好地使用切片。

### golang 什么时候废弃了rand.Seed方法

Golang 在 Go 1.20 版本废弃了 rand.Seed(time.Now().Unix()) 方法，原因如下：
1. 安全性问题
• 使用时间戳作为随机种子，在高并发场景下可能导致种子重复，进而导致随机数生成不随机。
• 使用纳秒时间戳可以提高随机性，但仍然存在重复的可能性。
2. 可预测性问题
• 使用时间戳作为随机种子，可以预测随机数生成序列，降低安全性。
3. 更优的选择
• Go 提供了 crypto/rand 包，可以生成更安全、更随机的随机数。
建议：
• 使用 crypto/rand 包生成随机数，例如：
```Go
reader := rand.Reader{}
n, err := reader.Read(b)
iferr != nil{
    panic(err)
}
```
• 如果需要使用 rand 包，可以使用 rand.NewSource() 函数生成新的随机数源，例如：
```Go
source := rand.NewSource(time.Now().UnixNano())
r := rand.New(source)
n := r.Intn(100)
```
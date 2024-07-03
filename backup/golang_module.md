---
title: 'GO Module相关知识点'
date: 2022-09-26 16:46:30
tags: [Golang]
published: true
hideInList: false
feature: 
isTop: false
---

# 介绍
## go mod是什么
go mod 是Golang 1.11 版本引入的官方包(package)依赖管理工具,用于解决之前没有地方记录依赖包具体版本的问题,方便依赖包的管理.
之前Golang 主要依靠vendor和GOPATH来管理依赖库,vendor相对主流,但现在官方更提倡go mod.
## go mod初始化及使用
官方包1.11(及其以上版本将会自动支持gomod)默认GO111MODULE=auto(auto是指如果在gopath下不启用mod)
Golang 提供一个环境变量 GO111MODULE 来设置是否使用mod,它有3个可选值,分别是off, on, auto(默认值),具体含义如下:
1. off: GOPATH mode,查找vendor和GOPATH目录
2. on:module-aware mode,使用 go module,忽略GOPATH目录
3. auto:如果当前目录不在$GOPATH 并且 当前目录(或者父目录)下有go.mod文件,则使用 GO111MODULE, 否则仍旧使用 GOPATH mode.

修改 GO111MODULE 的值的语句是:`set GO111MODULE=on `
在使用模块的时候, GOPATH 是无意义的,不过它还是会把下载的依赖储存在 GOPATH/src/mod 中,也会把 go install 的结果放在 GOPATH/bin(如果 GOBIN 不存在的话)
```
	• go mod download 下载模块到本地缓存,缓存路径是 $GOPATH/pkg/mod/cache
	• go mod edit 是提供了命令版编辑 go.mod 的功能,例如 go mod edit -fmt go.mod 会格式化 go.mod
	• go mod graph 把模块之间的依赖图显示出来
	• go mod init 初始化模块(例如把原本dep管理的依赖关系转换过来)
	• go mod tidy 增加缺失的包,移除没用的包
	• go mod vendor 把依赖拷贝到 vendor/ 目录下
	• go mod verify 确认依赖关系
	• go mod why 解释为什么需要包和模块
```
注意有几个坑的地方:
```
	• go mod 命令在 $GOPATH 里默认是执行不了的,因为 GO111MODULE 的默认值是 auto.默认在$GOPATH 里是不会执行, 如果一定要强制执行,就设置环境变量为 on.
	• go mod init 在没有接module名字的时候是执行不了的,会报错 go: cannot determine module path for source directory.可以这样执行:
	$ go mod init github.com/jiajunhuang/hello
```

# 命令
## 指定module的根目录并生成go.mod文件
`go mod init example.com/hello`
## 下载并添加依赖到go.mod文件中
`go build, go test`
## 查看module下的所有依赖
`go list -m all`
## 更新稳定版依赖
`go get rsc.io/sampler`
## 更新为指定版本依赖
```
go list -m -versions rsc.io/sampler
$rsc.io/sampler v1.0.0 v1.2.0 v1.2.1 v1.3.0 v1.3.1 v1.99.99
go get rsc.io/sampler@v1.3.1
```
## 清理无用的依赖
`go mod tidy`
## 将依赖复制到项目路径的vendor文件夹中
`go mod vendor`
## 忽略cache里的包,只使用vendor目录里的依赖进行编译
`go build -mod=vendor`
## 校验依赖并查看是否有修改
`go mod verify`



# 例子

go mod初始化:在$GOPATH外建一个文件夹,把个人代码放进去,我的测试代码路径:https://github.com/kevinhao8/go-mod-example.
首先main入口代码所在文件夹创建mod
创建语句  go mod init [module name]
比如我的测试代码 redisTest.go,创建语句就是  go mod init redisTest,成功创建时返回  go: creating new go.mod: module redisTest
此时文件夹下出现 go.mod文件,打开发现只有2行如下,并没有记录依赖库.
module redisTest
go 1.12
此时需要输入go test语句,根据需要的依赖自动生成require,也就是依赖包,此时go.mod多了如下内容(红字是我写的注释,文件里面没有)
```
require (
       github.com/gin-contrib/sse v0.0.0-20190301062529-5545eab6dad3 // indirect(有indirect注释的代表间接依赖,没有的代表直接依赖)
       github.com/gin-gonic/gin v1.3.0  
       github.com/golang/protobuf v1.3.1 // indirect
       github.com/mattn/go-isatty v0.0.7 // indirect
       github.com/ugorji/go/codec v0.0.0-20190316192920-e2bddce071ad // indirect(这里是版本号+时间戳+hash)
       gopkg.in/go-playground/validator.v8 v8.18.2 // indirect
       gopkg.in/yaml.v2 v2.2.2 // indirect
 )
 ```

```
require (
       dbredis v0.0.0
       github.com/gin-contrib/sse v0.0.0-20190301062529-5545eab6dad3 // indirect
       github.com/gin-gonic/gin v1.3.0
       github.com/golang/protobuf v1.3.1 // indirect
       github.com/mattn/go-isatty v0.0.7 // indirect
       github.com/ugorji/go/codec v0.0.0-20190316192920-e2bddce071ad // indirect
       gopkg.in/go-playground/validator.v8 v8.18.2 // indirect
       gopkg.in/yaml.v2 v2.2.2 // indirect
 )
 ```

----
# gopath 与go mod的区别
1. 环境变量GOPATH不再用于解析imports包路径,即原有的GOPATH/src/下的包,通过import是找不到了.
2. Go Module功能开启后,下载的包将存放与$GOPATH/pkg/mod路径
3. $GOPATH/bin路径的功能依旧保持

# go get 流程的变化
1. 老的go get取包过程类似:git clone + go install , 开启Go Module功能后go get就只有 git clone 或者 download过程了.	2. 新老实现还有一个不同是,两者存包的位置不同.前者,存放在$GOPATH/src目录下;后者,存放在$GOPATH/pkg/mod目录下.
3. 老的go get取完主包后,会对其repo下的submodule进行循环拉取.新的go get不再支持submodule子模块拉取.


# 依赖包的变化
1. 三方远程包:
2. 检查远程仓库最新的tag版本,有就取得该版本
3. 远程仓库没有tag版本时,直接获取master分支的HEAD版本
4. 如果在go.mod文件中指定了具体版本,go get直接获取该指定版本
5. go.mod中除了可以指定具体版本号以外,还支持分支名
6. 通过replace()进行替换




参考:
[1](https://blog.csdn.net/Lazybones_3/article/details/89355133)
[2](https://blog.csdn.net/kevinh531/article/details/88691870)
[3](https://jiajunhuang.com/articles/2018_09_03-go_module.md.html)
[4](https://blog.csdn.net/qq_33296108/article/details/88184060)

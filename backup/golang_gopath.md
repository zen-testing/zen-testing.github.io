---
title: 'GOPATH 不能访问Golang.org解决办法'
date: 2022-09-26 17:00:55
tags: [Golang]
published: true
hideInList: false
feature: 
isTop: false
---
例子:
`git clone git@github.com:golang/net.git $GOPATH/src/golang.org/x/net`
说明:
原命令`go get golang.org/x/net`
无法实现
使用GitHub镜像安装


# 实例
## 报错信息:
安装gin:
`go get -u github.com/gin-gonic/gin `
报错:
`package gopkg.in/yaml.v2: unrecognized import path "gopkg.in/yaml.v2" (https fetch: Get https://gopkg.in/yaml.v2?go-get=1: net/http: TLS handshake timeout)`
## 解决方案:
尝试多种方法均无效
所以直接Git镜像手动安装
`cd $GOPATH`
`mkdir gopkg.in`
`cd gopkg.in/`
`git clone https://github.com/go-yaml/yaml.git`
`mv yaml/ yaml.v2`
`cd yaml.v2/`
`go install`

## 报错信息:
` unrecognized import path XXX`
## 解决方案:
1. 手动加入被墙的包(原始包),一定要记住版本号,实在不知道的话,就试试v0.0.0;

`$ go mod edit -require=golang.org/x/net@v0.0.0`
2. 用github上的镜像地址替换

`$ go mod edit -replace=golang.org/x/crypto@v0.0.0=github.com/golang/crypto@latest`

`$ go mod edit -replace=golang.org/x/sys@v0.0.0=github.com/golang/sys@latest`

## 报错信息:                                      
```
vendor/github.com/gin-gonic/gin/binding/default_validator.go:11:2: cannot find package "gopkg.in/go-playground/validator.v8" in any of:
	/Users/jackyue/go/src/github.com/locutus666/mygin/vendor/gopkg.in/go-playground/validator.v8 (vendor tree)
	/usr/local/go/src/gopkg.in/go-playground/validator.v8 (from $GOROOT)
	/Users/jackyue/go/src/gopkg.in/go-playground/validator.v8 (from $GOPATH)
vendor/github.com/gin-gonic/gin/render/yaml.go:10:2: cannot find package "gopkg.in/yaml.v2" in any of:
	/Users/jackyue/go/src/github.com/locutus666/mygin/vendor/gopkg.in/yaml.v2 (vendor tree)
	/usr/local/go/src/gopkg.in/yaml.v2 (from $GOROOT)
	/Users/jackyue/go/src/gopkg.in/yaml.v2 (from $GOPATH)
    ```
## 解决方案:
在mygin工程目录下的vendor文件夹中,go并没有找到gin框架所依赖的第三方包,我们只能单独想办法下载.
翻看vendor/vendor.json,我们可以知道在github下载到依赖.

比如,gopkg.in/go-playground/validator.v8 这个包,实际对应的就是 github.com/go-playground/validator 的v8分支,那么只要 git clone -b v8 https://github.com/go-playground/validator.git 就可以拉下来.重命名后,在mygin工程目录下的vendor文件夹中,按照 gopkg.in/go-playground/validator.v8 路径,放置第三方包.

gopkg.in/yaml.v2 依赖包也可以以类似方式处理.
----
git clone https://github.com/golang/tools.git $GOPATH/src/golang.org/x/tools
git clone https://github.com/golang/genproto.git $GOPATH/src/google.golang.org/genproto
git clone https://github.com/grpc/grpc-go.git $GOPATH/src/google.golang.org/grpc
git clone https://github.com/golang/net.git $GOPATH/src/golang.org/x/net
git clone https://github.com/golang/text.git $GOPATH/src/golang.org/x/text
git clone https://github.com/golang/sys.git $GOPATH/src/golang.org/x/sys
git clone https://github.com/golang/xerrors.git $GOPATH/src/golang.org/x/xerrors
git clone https://github.com/golang/mod.git $GOPATH/src/golang.org/x/mod


git clone https://github.com/golang/crypto.git $GOPATH/src/golang.org/x/crypto
go get -u github.com/golang/protobuf/{proto,protoc-gen-go}
go get -u github.com/hashicorp/consul/api
git clone https://github.com/google/go-genproto.git $GOPATH/src/google.golang.org/genproto
cd $GOPATH/src/
go install google.golang.org/grpc


实例
mkdir $GOPATH/go.etcd.io
cd go.etcd.io
git clone https://github.com/etcd-io/bbolt.git $GOPATH/src/go.etcd.io/bbolt
mkdir $GOPATH/synder
git clone https://github.com/syndtr/goleveldb.git $GOPATH/src/github.com/syndtr/goleveldb
mkdir $GOPATH/shirou
git clone https://github.com/shirou/gopsutil.git $GOPATH/src/github.com/shirou/

git clone https://github.com/golang/snappy.git $GOPATH/src/google.golang.org/snappy

git clone https://github.com/golang/snappy.git $GOPATH/src/github.com/golang/snappy

//go install  

git clone https://github.com/go-vgo/gt.git $GOPATH/src/github.com/go-vgo/gt

git clone https://github.com/pelletier/go-toml.git $GOPATH/src/github.com/pelletier/go-toml

git clone https://github.com/go-ego/murmur.git $GOPATH/src/github.com/go-ego/murmur

git clone https://github.com/go-ego/gse.git $GOPATH/src/github.com/go-ego/gse

git clone https://github.com/go-ego/gpy.git $GOPATH/src/github.com/go-ego/gpy

git clone https://github.com/dgraph-io/badger.git $GOPATH/src/github.com/dgraph-io/badger

git clone https://github.com/dgryski/go-farm.git $GOPATH/src/github.com/dgryski/go-farm

git clone https://github.com/dgraph-io/ristretto.git $GOPATH/src/github.com/dgraph-io/ristretto

git clone https://github.com/cespare/xxhash.git $GOPATH/src/github.com/cespare/xxhash

git clone https://github.com/DataDog/zstd.git $GOPATH/src/github.com/DataDog/zstd

git clone https://github.com/go-ego/cedar.git $GOPATH/src/github.com/go-ego/cedar

---
title: 'Golang代码规范'
date: 2022-09-26 15:58:52
tags: [Golang]
published: true
hideInList: false
feature: 
isTop: false
---

# 前言

本规范旨在提供一个切实的共识,在代码开发的过程中实现最佳实践和设计模式.这些规范可以帮助我们编写出优雅简洁代码,也便于团队易懂易维护

指导原则:

* 简单性(最高目标)
* 可读性(可维护性)
* 生产力(协作高效性)

# 大纲

* 分层处理,明确各层职责.
* 单元测试,保障代码质量.
* 先处理错误,避免嵌套.
* 用空行来分解函数.


# 代码示例

## 分层处理,明确各层职责

* Resource(Router) 资源路由层,负责 Http 请求,遵循 RESTful API 接口设计标准及规范.

* Controller 控制层,负责接收并响应客户端的输入与输出,包括对输入参数的过滤\转换\校验,对输出数据结构的维护,并调用 Logic 实现业务逻辑处理.

* Logic 业务逻辑层,负责具体业务逻辑的实现以及封装,原则上只有 Controller 和 Logic 层调用.

* Service 服务层,负责基础服务的封装,原则上只有 Logic 层会调用,但特殊情况除外,如日志服务.

* Model 数据访问层,负责所有的数据访问接口,原则上只有 Logic 层会调用.


## 单元测试,保障代码质量

原则上每个函数都应该有单元测试覆盖,首先,测试用例可以保证代码的质量,保证代码的正确性,方便代码进行回归测试;其次,通过测试用例展示业务代码的正确使用方式.

```
func TestAddVideo(t *testing.T) {
    articleParams := &articlePrototype.ArticleParams{
        Kind:      articleModels.KindVideo,
        Title:     "xxxxx!",
        Content:   "xxxxxx",
        VideoPath: "dev/wh/video/uid_13/video_1620649085116.mp4",
        Cover:     "dev/wh/image/uid_13/image_1620648670144.jpeg",
        StudentId: 29
    }

    articleId, err := AddVideo(articleParams)
    if err != nil {
        t.Error(err)
        return
    }

    articleDetail, err := articleModels.GetArticleDetailById(articleId)
    if err != nil {
        t.Error(err)
        return
    }

    if !reflect.DeepEqual(articleParams.Title, articleDetail.Title) {
        t.Errorf("Expected %v got %v", articleParams.Title, articleDetail.Title)
    }

    if !reflect.DeepEqual(articleParams.Content, articleDetail.Content) {
        t.Errorf("Expected %v got %v", articleParams.Content, articleDetail.Content)
    }
}

```

## 先处理错误,避免嵌套

非最佳实践示例:

```
// 查询操作人员信息
if rsp, err := new(mysql_model.SysUser).GetUserInfo(data.Int("op_id")); err == nil {
	userTempt := rsp.Map("data")
	if realname := userTempt.String("realname"); realname != "" {
		data["op_name"] = realname
	} else {
		data["op_name"] = userTempt.String("username")
	}
} else {
	data["op_name"] = ""
}
```

最佳实践示例:

```
func (g *Gopher) WriteTo(w io.Writer) (size int64, err error) {
    err = binary.Write(w, binary.LittleEndian, int32(len(g.Name)))
    if err != nil {
        return
    }
    size += 4
    n, err := w.Write([]byte(g.Name))
    size += int64(n)
    if err != nil {
        return
    }
    .....
    return
}
```

通过上面两个示例代码对比,先处理错误,可减少嵌套,使代码简洁,可读性强.

## 用空行来分解函数

```
type Person struct {
    Name string
    Age  int
}

// AverageAge returns the average age of people.
func AverageAge(people []Person) int {
    if len(people) == 0 {
        return 0
    }

    var count, sum int
    for _, p := range people {
        sum += p.Age
        count += 1
    }

    return sum / count
}

```

如上所示,与使用段落分解文档的方式一样用空行来分解函数. 在 AverageAge 中,按顺序共有三个操作.
* 第一个是前提条件,检查 people 是否为空;
* 第二个是 sum 和 count 的累积;
* 最后是平均值的计算.

# 参考文献
[Go 最佳实践: 编写可维护 Go 代码](https://learnku.com/go/wikis/38430)

[高效的 Go 编程 Effective Go ](https://learnku.com/docs/effective-go/2020)

[Uber 开源的<Go 语言编码规范>](https://learnku.com/go/wikis/38426)

[Go Code Review Comments](https://github.com/golang/go/wiki/CodeReviewComments)

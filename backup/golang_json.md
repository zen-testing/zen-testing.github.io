---
title: 'Golang解析JSON'
date: 2022-09-26 16:56:36
tags: [Golang]
published: true
hideInList: false
feature: 
isTop: false
---
## 解析简单JSON

如:
```golang
{
    "name": "Standard",
    "fruit": [
        "Apple",
        "Banana",
        "Orange"
    ],
    "id": 999,
    "created": "2018-04-09T23:00:00Z"
}
```
那么:
```golang
type FruitBasket struct {
    Name    string    `json:"name"`
    Fruit   []string  `json:"fruit"`
    Id      int64     `json:"id"`
    Created time.Time `json:"created"`
}
```
完整代码如下
```golang
package main

import (
    "fmt"
    "encoding/json"
    "time"

)

func main() {
    type FruitBasket struct {
        Name    string    `json:"name"`
        Fruit   []string  `json:"fruit"`
        Id      int64     `json:"id"`
        Created time.Time `json:"created"`
    }

    jsonData := []byte(`
    {
        "name": "Standard",
        "fruit": [
             "Apple",
            "Banana",
            "Orange"
        ],
        "id": 999,
        "created": "2018-04-09T23:00:00Z"
    }`)

    var basket FruitBasket
    err := json.Unmarshal(jsonData, &basket)
    if err != nil {
         fmt.Println(err)
    }
    fmt.Println(basket.Name, basket.Fruit, basket.Id)
    fmt.Println(basket.Created)
}
```
**由于`json.UnMarshal()`方法接收的是字节切片,所以首先需要把JSON字符串转换成字节切片`c := []byte(s)`**

## 解析内嵌对象的JSON

把上面的`fruit`键对应的值如果改成字典变成`"fruit" : {"name":"Apple", "priceTag":"$1"}`

如:
```golang
jsonData := []byte(`
    {
        "name": "Standard",
        "fruit" : {"name": "Apple", "priceTag": "$1"},
        "def": 999,
        "created": "2018-04-09T23:00:00Z"
    }`)
```

解析类型应该变成
```golang
type Fruit struct {
    Name string `json":name"`
    PriceTag string `json:"priceTag"`
}

type FruitBasket struct {
    Name    string    `json:"name"`
    Fruit   Fruit     `json:"fruit"`
    Id      int64     `json:"id"`
    Created time.Time `json:"created"`
}
```

## 解析内嵌对象数组的JSON(Embed Array of Object)

如果上面JSON数据里的Fruit值现在变成了

```golang
"fruit" : [
    {
        "name": "Apple",
      "priceTag": "$1"
    },
    {
        "name": "Pear",
        "priceTag": "$1.5"
    }
]
```
这种情况也简单把存放解析后数据的类型其声明做如下更改,把`Fruit`字段类型换为`[]Fruit`即可
```golang
type Fruit struct {
    Name string `json:"name"`
    PriceTag string `json:"priceTag"`
}

type FruitBasket struct {
    Name    string    `json:"name"`
    Fruit   []Fruit   `json:"fruit"`
    Id      int64     `json:"id"`
    Created time.Time `json:"created"`
}
```

## 解析具有动态Key的对象(Parse a JSON object with dynamic key)

下面再做一下复杂的变通,如果把上面的对象数组变为Key为水果ID的对象(object of object)比如

```golang
"Fruit" : {
	"1": {
		"Name": "Apple",
		"PriceTag": "$1"
	},
	"2": {
		"Name": "Pear",
		"PriceTag": "$1.5"
	}
}
```
每个Key的名字在声明结构体的时候是不知道值的,这样该怎么声明呢,答案是把Fruit字段的类型声明为一个key为string类型值为Fruit类型的map
```golang
type Fruit struct {
    Name string `json:"Name"`
    PriceTag string `json:"PriceTag"`
}

type FruitBasket struct {
    Name    string
    Fruit   map[string]Fruit
    Id      int64 `json:"ref"`// 声明对应的json key
    Created time.Time
}
```
示例代码
```golang
package main

import (
	"fmt"
	"encoding/json"
	"time"

)

func main() {
    type Fruit struct {
        Name string `json:"Name"`
        PriceTag string `json:"PriceTag"`
    }

    type FruitBasket struct {
        Name    string
        Fruit   map[string]Fruit
        Id      int64 `json:"ref"`// 声明对应的json key
        Created time.Time

    }    
    jsonData := []byte(`
    {
        "Name": "Standard",
        "Fruit" : {
	    "1": {
		"Name": "Apple",
		"PriceTag": "$1"
	    },
	    "2": {
		"Name": "Pear",
		"PriceTag": "$1.5"
	    }
        },
        "ref": 999,
        "Created": "2018-04-09T23:00:00Z"
    }`)

    var basket FruitBasket
    err := json.Unmarshal(jsonData, &basket)
    if err != nil {
         fmt.Println(err)
    }
    for _, item := range basket.Fruit {
	fmt.Println(item.Name, item.PriceTag)
    }
}
```
虽然将JSON数据存储到空接口类型的值中可以用来解析任意结构的JSON数据,但是在实际应用中发现还是有不可控的地方,比如将数字字符串的值转换成了float类型的值,所以经常会在运行时报类型断言的错误,所以在JSON结构确定的情况下还是优先使用结构体类型声明,将JSON数据到结构体中的方式来解析JSON.

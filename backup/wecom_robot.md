---
title: '企业微信机器人使用文档'
date: 2023-05-24 20:50:56
tags: [tencent]
published: true
hideInList: false
feature: 
isTop: false
---
# 发送文本消息

curl请求方式

```bash
curl 'https://qyapi.weixin.qq.com/cgi-bin/webhook/send?key=<key>' \
   -H 'Content-Type: application/json' \
   -d '
   {
    	"msgtype": "text",
    	"text": {
        	"content": "hello world",
        	"mentioned_list":["wangqing","@all"],
			"mentioned_mobile_list":["13800001111","@all"]
    	}
   }'
```

+ 其中`mentioned_list`和`mentioned_mobile_list`是可选参数
+ `mentioned_list`需要输入`userid`或`@all`
+ 在企业微信管理员没有开启用户查询`userid`的情况下普通用户不能使用这种方式
+ `mentioned_mobile_list`通过输入用户绑定的手机号实现@,无需输入国际区号(如`+86``00852`)

<center><img center src="https://s1.ax1x.com/2023/04/11/ppOC8r4.png"></center>
<center>效果图</center>

# 发送图片消息

```bash
curl 'https://qyapi.weixin.qq.com/cgi-bin/webhook/send?key=<key>' \
-H 'Content-Type: application/json' \
   -d '
   {
    "msgtype": "image",
    "image": {
        "base64": "DATA",
		"md5": "MD5"
		}
	}'
```

+ `MD5`是图片编码前的md5值 如`md5sum *.png`  `a1f66a6368857c9c78d688931a50a5c0`
+ `DATA`是图片内容的base64编码`base64 *.png > base64.txt` 
+ 本地或网站上编码base64都会自动加上`\n`简单的解决方法就是使用office word替换功能替换换行符`^p`
+ **base64中包含换行符就会报错**
+ 图片不能超过2MB,png/jpg格式
<center><img center src="https://s1.ax1x.com/2023/04/11/ppOkeyT.png"></center>
<center><img center src="https://s1.ax1x.com/2023/04/11/ppOkmOU.png"></center>
<center>效果图</center>

# makedown消息

```bash
curl 'https://qyapi.weixin.qq.com/cgi-bin/webhook/send?key=<key>' \
-H 'Content-Type: application/json' \
   -d '
   {
    "msgtype": "markdown",
    "markdown": {
        "content": "实时新增用户反馈<font color=\"warning\">132例</font>，请相关同事注意。\n
         >类型:<font color=\"comment\">用户反馈</font>
         >普通用户反馈:<font color=\"comment\">117例</font>
         >VIP用户反馈:<font color=\"comment\">15例</font>"
    }
}	'
```

+ 支持标题、引用、链接、图片、单行代码、多行代码块、绿(info)灰(comment)红(warning)三种颜色的html标签,特殊字符需要使用转义字符表示

<center><img center src="https://s1.ax1x.com/2023/04/11/ppOARv6.jpg"></center>
<center><img center src="https://s1.ax1x.com/2023/04/11/ppOAHPA.png"></center>
<center>效果图</center>

# 图文消息

```bash
curl 'https://qyapi.weixin.qq.com/cgi-bin/webhook/send?key=<key>' \
-H 'Content-Type: application/json' \
   -d '
   {
    "msgtype": "news",
    "news": {
       "articles" : [
           {
               "title" : "中秋节礼品无法领取",
               "description" : "今年中秋节公司没有豪礼相送",
               "url" : "zhangyiming748.github.io",
               "picurl" : "https://s1.ax1x.com/2022/09/04/vofIJK.jpg"
           }
        ]
    }
}'
```

<center><img center src="https://s1.ax1x.com/2023/04/11/ppOEGqO.png"></center>
<center><img center src="https://s1.ax1x.com/2023/04/11/ppOEtde.png"></center>
<center>效果图</center>

# 上传文件

```bash
curl -F "media=@<file>" 'https://qyapi.weixin.qq.com/cgi-bin/webhook/upload_media?key=<key>&type=file' \
-H 'Content-Type: multipart/form-data' \
```
会返回文件的`media_id`通过它来找到文件
+ 文件大小在5B~20M之间
+ 这一步只是把文件上传到腾讯的服务器,需要后续步骤把文件发到群组,文件唯一标识`media_id`这里记为`31d3eAxvNvRWRtXfuQCjDmmCaI6WoBYqkyjwHSXhtk__tG4o_igjEq2X9qpTGrSXr`

<center><img center src="https://s1.ax1x.com/2023/04/11/ppOVa0U.png"></center>
<center>效果图</center>

# 发送文件

```bash
curl 'https://qyapi.weixin.qq.com/cgi-bin/webhook/send?key=<key>' \
-H 'Content-Type: application/json' \
   -d '
   {
    "msgtype": "file",
    "file": {
 		"media_id": "31d3eAxvNvRWRtXfuQCjDmmCaI6WoBYqkyjwHSXhtk__tG4o_igjEq2X9qpTGrSXr"
    }
}'
```

+ 文件过期时间宣称三天
<center><img center src="https://s1.ax1x.com/2023/04/11/ppOVqnf.png"></center>
<center><img center src="https://s1.ax1x.com/2023/04/11/ppOVLB8.png"></center>
<center>效果图</center>

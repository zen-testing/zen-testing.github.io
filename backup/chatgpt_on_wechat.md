---
title: '微信接入chatGPT(docker)实现'
date: 2023-02-16 15:00:46
tags: [ChatGPT,Docker]
published: true
hideInList: false
feature: 
isTop: false
---
1. 创建一个容器

```shell
$ docker run --name=openai --cpus=2 --memory=5120M -p 2222:22 -v /Users/zen/container:/mnt --privileged -it alpine /bin/sh
```

2. 更换软件源为清华镜像

```shell
$ sed -i 's/dl-cdn.alpinelinux.org/mirrors.tuna.tsinghua.edu.cn/g' /etc/apk/repositories
$ sed -i 's/https/http/g' /etc/apk/repositories
```

3. 安装必要软件

```shell
$ apk update && apk upgrade && apk add git vim less python3 py3-pip
```

4. 新建普通用户

```shell
$ adduser {user-name} # 根据提示输入两次这个用户的密码
```

5. 切换到普通用户

```shell
$ su zen # 假设我刚才创建的用户是 zen
```

6. 把源码克隆到家目录

```shell
$ cd ~
$ git clone https://github.com/zhayujie/chatgpt-on-wechat
```

7. 修改文件

```shell
$ cd chatgpt-on-wechat/
$ pip3 install itchat-uos==1.5.0.dev0
$ pip3 install --upgrade openai -i https://pypi.tuna.tsinghua.edu.cn/simple/
$ cp config-template.json config.json
$ vim config.json # 如果你不擅长使用vim也可以用nano
```

8. 修改配置文件

```json
# config.json文件内容示例
{ 
  "open_ai_api_key": "YOUR API KEY",                          // 填入上面创建的 OpenAI API KEY
  "single_chat_prefix": ["bot", "@bot"],                     // 私聊时文本需要包含该前缀才能触发机器人回复
  "single_chat_reply_prefix": "[bot] ",                      // 私聊时自动回复的前缀，用于区分真人
  "group_chat_prefix": ["@bot"],                             // 群聊时包含该前缀则会触发机器人回复
  "group_name_white_list": ["ChatGPT测试群", "ChatGPT测试群2"],// 开启自动回复的群名称列表
  "image_create_prefix": ["画", "看", "找"],                  // 开启图片回复的前缀
  "conversation_max_tokens": 1000,                           // 支持上下文记忆的最多字符数
  "character_desc": "你是ChatGPT, 一个由OpenAI训练的大型语言模型, 你旨在回答并解决人们的任何问题，并且可以使用多种语言与人交流。"  // 人格描述
}
```

你需要改的只有第一项`YOUR API KEY`

改成你自己的

最终应该像这样

![config.json](https://s1.ax1x.com/2023/02/16/pSHwwRA.png)

9. 运行

	1. 本地运行
        ```shell
            $ touch nohup.out
            $ python3 app.py
        ```
	2. 服务器部署
        ```shell
            touch nohup.out
            nohup python3 app.py & tail -f nohup.out          # 在后台运行程序并通过日志输出二维码
        ```

10. FAQ

Q:Log in time out, reloading QR code. 二维码一直刷新,手机来不及登录
A:`pip3 show itchat-uos`找到这个包的安装位置比如`/home/zen/.local/lib/python3.10/site-packages`,所以文件绝对路径是`/home/zen/.local/lib/python3.10/site-packages/itchat/components/login.py`,修改`login.py` 中的 `login`函数,在`while not isLoggedIn`循环前加上一个`sleep(15)`,代码在第59行![](https://user-images.githubusercontent.com/26161723/208597034-76720c20-8eb3-4537-9604-b46f5f255f47.png)

# 参考文献

https://www.buxiaoyao.com/chatgpt-wechat/
---
title: 'gitcode告诉我们github并不"安全",还是自建私有代码托管服务吧'
date: 2024-07-02 08:59:45
tags: [Gitea,Docker]
published: true
hideInList: false
feature: 
isTop: false
---
华为和CSDN联合开发了一个gitcode
爬取了国内外绝大部分人的github仓库
甚至为这些作者创建了一个他们自己都不知道,但是属于他们的用户账户
CSDN做这种事不稀奇 毕竟人家就是靠抄袭起家的
华为这个浓眉大眼的也叛变革命了,还是挺不可思议的
难道是CSDN给的太多了?

# 设置并运行gitea

```yml
version: "3"
services:
  server:
    image: gitea/gitea:@version@
    container_name: gitea
    environment:
      - USER_UID=1000
      - USER_GID=1000
    restart: always
    networks:
      - gitea
    volumes:
      - ./gitea:/data
      - /etc/timezone:/etc/timezone:ro
      - /etc/localtime:/etc/localtime:ro
    ports:
      - "3000:3000"
      - "222:22"
```
进入浏览器地址栏输入`http://127.0.0.1:3000`
进入配置页面输入自己的设置
确认后即可进入gitea自己的主页
[![pk6jwtJ.png](https://s21.ax1x.com/2024/06/29/pk6jwtJ.png)](https://imgse.com/i/pk6jwtJ)

# 配置gitea action

浏览器输入url`http://127.0.0.1/admin/actions/runners`
[![pk6jDpR.png](https://s21.ax1x.com/2024/06/29/pk6jDpR.png)](https://imgse.com/i/pk6jDpR)
选择右上角`创建Runner`
记住这个token
从[这里](https://gitea.com/gitea/act_runner/releases]下载适合你物理电脑架构的act-runner二进制文件

```bash
chmod +x act_runner
./act_runner --version
./act_runner generate-config
# 运行后会交互提示你输入ip地址
# 输入你物理记载局域网内的地址而不是localhost,如http://192.168.1.6:3000
# 回车后要求你输入token,直接复制过来就行
```

然后编辑`docker-compose.yml`文件

```yml
version: "3.8"
services:
  runner:
    image: gitea/act_runner:nightly
    environment:
      CONFIG_FILE: /config.yaml
      GITEA_INSTANCE_URL: <和上面地址保持一致>
      GITEA_RUNNER_REGISTRATION_TOKEN: <和上面token保持一致>
    volumes:
      - ./config.yaml:/config.yaml # 确保config文件存在 如果不在同级目录 用绝对路径
      - ./data:/data
      - /var/run/docker.sock:/var/run/docker.sock
```

# 就可以使用自动构建的功能了
[![pk6j59A.png](https://s21.ax1x.com/2024/06/29/pk6j59A.png)](https://imgse.com/i/pk6j59A)

# 为什么github的action功能在中国通常被成为CI / CD ?

GitHub 的 Actions 功能在中国通常被称为 "CI/CD"，其中 "CI" 指的是持续集成（Continuous Integration），"CD" 指的是持续部署（Continuous Deployment）。这种称呼主要是因为 GitHub Actions 提供了持续集成和持续部署的功能，使开发者能够自动化构建、测试和部署他们的代码。因此，在中国，人们更倾向于将 GitHub Actions 简称为 "CI/CD"，以表示其集成了持续集成和持续部署的功能。这种简称也更符合行业标准和术语，更容易被开发者理解和使用。

**今天就是天王老子来了 我也要叫它自动构建**

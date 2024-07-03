---
title: '树莓派4安装Gitlab'
date: 2022-09-26 18:26:58
tags: [Raspberry,Gitlab]
published: true
hideInList: false
feature: 
isTop: false
---
gitee已经变质了

<!-- more -->

# 下载命令
[下载地址](https://packages.gitlab.com/gitlab/gitlab-ce/packages/debian/bullseye/gitlab-ce_14.10.3-ce.0_arm64.deb)

```
wget --content-disposition https://packages.gitlab.com/gitlab/gitlab-ce/packages/debian/bullseye/gitlab-ce_14.10.3-ce.0_arm64.deb/download.deb
```
## 安装命令
```
sudo dpkg -i gitlab-ce_14.10.3-ce.0_arm64.deb
```

## 修改配置文件
`vim /etc/gitlab/gitlab.rb`
```shell
external_url 'http://192.168.10.123:80'
# 改成本机端口
......
gitlab_rails['time_zone'] = 'Asia/Shanghai'
# 电子邮件可以不设置 反正是本地代码托管
gitlab_rails['gitlab_email_from'] = 'xxxxxx@163.com'
......
gitlab_rails['smtp_enable'] = true
gitlab_rails['smtp_address'] = "smtp.163.com"
gitlab_rails['smtp_port'] = 25
gitlab_rails['smtp_user_name'] = "xxxxxx@163.com"
gitlab_rails['smtp_password'] = "111111" # 客户端授权密码
gitlab_rails['smtp_domain'] = "163.com"
gitlab_rails['smtp_authentication'] = "login"
gitlab_rails['smtp_enable_starttls_auto'] = true
......
user["git_user_email"] = "xxxxxx@163.com"
```shell
修改后重新配置
```shell
sudo gitlab-ctl reconfigure
```
查看状态
```shell
sudo gitlab-ctl status
```
## 初始密码
```shell
/etc/gitlab/initial_root_password
# 会在第一次执行sudo gitlab-ctl reconfigure后生成 24小时后自动删除
```


|常用命令|说明|
|:---:|:---:|
|sudo gitlab-ctl reconfigure|重新加载配置,每次修改/etc/gitlab/gitlab.rb文件之后执行|
|sudo gitlab-ctl status|查看 GitLab 状态|
|sudo gitlab-ctl start|启动 GitLab|
|sudo gitlab-ctl stop|停止 GitLab|
|sudo gitlab-ctl restart|重启 GitLab|
|sudo gitlab-ctl tail|查看所有日志|
|sudo gitlab-ctl tail nginx/gitlab_acces.log|查看 nginx 访问日志|
|sudo gitlab-ctl tail postgresql|查看 postgresql 日志|


## 效果图

![效果图](https://raw.githubusercontent.com/zhangyiming748/zhangyiming748.github.io/master/img/Gitlab/Gitlab.webp)\
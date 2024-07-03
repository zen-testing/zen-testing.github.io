---
title: '修改密码规则'
date: 2022-09-26 15:50:01
tags: [Linux]
published: true
hideInList: false
feature: 
isTop: false
---
自定义规则集在 `/etc/security/pwquality.conf`

```shell
# Configuration for systemwide password quality limits
# 系统范围密码质量限制的配置
# Defaults:
# 默认
#
# Number of characters in the new password that must not be present in the
# old password.
# 新密码中不能出现在旧密码中的字符数
# difok = 0
#
# Minimum acceptable size for the new password (plus one if
# credits are not disabled which is the default). (See pam_cracklib manual.)
# 新密码的最小可接受大小(如果未禁用默认值,则加一). (参见 pam_cracklib 手册.)
# 人话:最小密码长度
minlen = 2
#
# The maximum credit for having digits in the new password. If less than 0
# it is the minimum number of digits in the new password.
# 新密码中包含数字的最大信用.如果小于 0,则为新密码中的最小位数.
# 人话:最大密码长度
# dcredit = 0
#
# The maximum credit for having uppercase characters in the new password.
# If less than 0 it is the minimum number of uppercase characters in the new
# password.
# 新密码中包含大写字符的最大信用.如果小于 0,则为新密码中大写字符的最小数量.
# 人话:大写字母最大长度
# ucredit = 0
#
# The maximum credit for having lowercase characters in the new password.
# If less than 0 it is the minimum number of lowercase characters in the new
# password.
# 新密码中包含小写字符的最大信用.如果小于 0,则为新密码中小写字符的最小数量.
# 人话:小写字母最大长度
lcredit = 0
#
# The maximum credit for having other characters in the new password.
# If less than 0 it is the minimum number of other characters in the new
# password.
# 新密码中包含特殊字符的最大信用.如果小于 0,则为新密码中特殊字符的最小数量.
# 人话:特殊字符最大长度
ocredit = 0
#
# The minimum number of required classes of characters for the new
# password (digits, uppercase, lowercase, others).
# 新密码所需的最少字符类别数
minclass = 1
#
# The maximum number of allowed consecutive same characters in the new password.
# The check is disabled if the value is 0.
# 新密码中允许的最大连续相同字符数,0=禁用
maxrepeat = 0
#
# The maximum number of allowed consecutive characters of the same class in the
# new password.
# The check is disabled if the value is 0.
# 新密码中允许的同一类的最大连续字符数,0=禁用
# maxclassrepeat = 0
#
# Whether to check for the words from the passwd entry GECOS string of the user.
# The check is enabled if the value is not 0.
# 是否从用户的 passwd 条目 GECOS 字符串中检查单词.如果值不为 0,则启用检查.
# gecoscheck = 0
#
# Whether to check for the words from the cracklib dictionary.
# The check is enabled if the value is not 0.
# 是否检查cracklib字典中的单词.如果值不为 0,则启用检查.
# dictcheck = 0
#
# Whether to check if it contains the user name in some form.
# The check is enabled if the value is not 0.
# 是否检查它是否包含某种形式的用户名.如果值不为 0,则启用检查.
# usercheck = 0
#
# Whether the check is enforced by the PAM module and possibly other
# applications.
# The new password is rejected if it fails the check and the value is not 0.
# 检查是否由 PAM 模块和可能的其他应用程序强制执行.如果新密码未通过检查且值不为 0,则新密码将被拒绝.
# enforcing = 1
#
# Path to the cracklib dictionaries. Default is to use the cracklib default.
# cracklib 字典的路径.默认是使用cracklib 默认值.
# dictpath =
#
# Prompt user at most N times before returning with error. The default is 1.
# 在返回错误之前最多提示用户 N 次.默认值为 1.
retry = 3
#
# Enforces pwquality checks on the root user password.
# Enabled if the option is present.
# 对 root 用户密码强制执行 pwquality 检查.如果存在该选项,则启用.
# enforce_for_root
#
# Skip testing the password quality for users that are not present in the
# /etc/passwd file.
# Enabled if the option is present.
# 跳过测试 /etc/passwd 文件中不存在的用户的密码质量.如果存在该选项,则启用.
# local_users_only
#
# Whether to check the new password is a palindrome or not
# Enabled if the option is present
# 检查新密码是否为回文如果存在该选项,则启用
# palindrome
#
# Whether to check the new password is simliar with old one
# Check include only case changes and rotated
# Disabled if the option is present
# 是否检查新密码与旧密码类似 检查仅包括大小写更改和轮换 如果该选项存在,则禁用
# no_similar_check
```

# /etc/login.defs

```shell
PASS_MAX_DAYS 99999 #密码的最大有效期, 99999:永久有期
PASS_MIN_DAYS 0 #是否可修改密码,0可修改,非0多少天后可修改
PASS_MIN_LEN 5 #密码最小长度,使用pam_cracklib module,该参数不再有效
PASS_WARN_AGE 7 #密码失效前多少天在用户登录时通知用户修改密码
```
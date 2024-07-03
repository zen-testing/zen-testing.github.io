---
title: 'Windows 设置环境变量'
date: 2022-09-26 18:47:16
tags: [Windows]
published: true
hideInList: false
feature: 
isTop: false
---
## 这个方法适用于以下的场景

你电脑对面的女神希望你帮他设置他电脑的环境变量,而你又不想在她面前表现出你是在一边查怎么设置一边设置的

----

功能
1. 要验证刚刚的用户环境变量有没有创建成功
    1. PowerShell命令`$env:变量名`
    2. 示例`$env:JAVA_HOME`
    3. CMD命令`echo %刚刚创建的变量名%`
    4. 示例`echo %JAVA_HOME%`

2. 创建用户变量
    1. PowerShell命令`[Environment]::SetEnvironmentVariable("要创建的用户环境变量的变量名", "要创建的用户环境变量的变量值" ,"User")`
    2. 示例`[Environment]::SetEnvironmentVariable("JAVA_HOME","C:\Program Files\Java\jdk1.8.0_201","User")`
    3. CMD命令`setx 要创建的用户环境变量的变量名 "要创建的用户环境变量的变量值"`
    4. 示例`setx JAVA_HOME "C:\Program Files\Java\jdk1.8.0_201"`

3. 创建系统变量
    1. PowerShell命令`[Environment]::SetEnvironmentVariable("要创建的系统环境变量的变量名", "要创建的系统环境变量的变量值" ,"Machine")`
    2. 示例`[Environment]::SetEnvironmentVariable("JAVA_HOME","C:\Program Files\Java\jdk1.8.0_201","Machine")`
    3. CMD命令`setx /M 要创建的系统环境变量的变量名"要创建的系统环境变量的变量值"`
    4. 示例`setx /M JAVA_HOME "C:\Program Files\Java\jdk1.8.0_201"`

4. 追加变量
    1. PowerShell命令`$Env:变量名=$Env:变量名+";变量值"`
    2. 示例`$Env:path=$Env:Path+";C:\Go\bin"`
    3. CMD命令`setx 变量名 %变量名%;"新变量值"`
    4. 示例`setx testx %testx%;"C:\Users\zhang\Desktop\PINBALL"`


**实例** 你的女神让你设置JAVA环境变量

```
setx /M JAVA_HOME "C:\Program Files\Java\jdk1.8.0_201"
setx /M PATH %PATH%;"%JAVA_HOME%\bin"
setx /M CLASSSPATH ".;%JAVA_HOME%\lib;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar"
```
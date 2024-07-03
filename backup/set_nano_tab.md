---
title: '设置nano 默认tab长度'
date: 2024-04-17 16:51:55
tags: [nano,Linux,AI]
published: true
hideInList: false
feature: 
isTop: false
---
在nano编辑器中设置默认的tab长度，你需要编辑nano的配置文件。以下是步骤：

1. 打开终端。

2. 输入 `nano ~/.nanorc` 命令，按回车键。这将创建一个名为 `.nanorc` 的文件（如果尚不存在）或打开现有文件。

3. 在文件中添加以下内容来设置tab长度，例如设置为4个空格：

   ```
   set tabsize 4
   ```

   如果你想用制表符（而不是空格）来表示tab，你可以使用：

   ```
   set tabstospaces
   ```

4. 保存并关闭文件。在nano编辑器中，按 `Ctrl + X`，然后按 `Y`，最后按回车键。

5. 重新启动终端或运行 `source ~/.nanorc` 命令以应用更改。

现在，每次使用nano时，都会按照你在 `.nanorc` 文件中设置的值来显示和插入tab。
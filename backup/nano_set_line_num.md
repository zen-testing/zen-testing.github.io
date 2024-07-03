---
title: '设置nano 默认显示行号'
date: 2024-04-17 16:47:27
tags: [nano,AI,Linux]
published: true
hideInList: false
feature: 
isTop: false
---
要在 nano 编辑器中默认显示行号，可以按照以下步骤操作：

1. 打开终端。
2. 输入 `nano ~/.nanorc` 命令，按回车键。这将创建一个名为 `.nanorc` 的文件（如果尚不存在）或打开现有文件。
3. 在文件中添加以下内容：

```shell
set constantshow
set linenumbers
```

4. 保存并关闭文件。在 nano 编辑器中，按 `Ctrl + X`，然后按 `Y`，最后按回车键。
5. 重新启动终端或运行 `source ~/.nanorc` 命令以应用更改。

现在，每次打开 nano 编辑器时，都会默认显示行号。
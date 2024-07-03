---
title: '设置vim 默认tab长度'
date: 2024-04-17 16:54:17
tags: [vim,AI,Linux]
published: true
hideInList: false
feature: 
isTop: false
---
要在 Vim 编辑器中设置默认的 tab 长度，你需要编辑 Vim 的配置文件。以下是步骤：

1. 打开终端。

2. 输入 `vim ~/.vimrc` 命令，按回车键。这将创建一个名为 `.vimrc` 的文件（如果尚不存在）或打开现有文件。

3. 在文件中添加以下内容来设置 tab 长度，例如设置为 4 个空格：

   ```shell
   set tabstop=4
   set shiftwidth=4
   set expandtab
   ```

   - `set tabstop=4` 设置 tab 停止的长度为 4 个空格。
   - `set shiftwidth=4` 设置自动缩进的长度也是 4 个空格。
   - `set expandtab` 设置使用空格而不是制表符进行缩进。

4. 保存并关闭文件。在 Vim 编辑器中，按 `Esc` 键，然后输入 `:wq`，最后按回车键。

5. 重新启动终端或运行 `source ~/.vimrc` 命令以应用更改。

现在，每次使用 Vim 时，都会按照你在 `.vimrc` 文件中设置的值来显示和插入 tab。
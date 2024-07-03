---
title: 'shell实现对指定目录下的所有文件计算大小并生成美观的树状图文本文件'
date: 2024-04-17 17:15:12
tags: [shell,AI,Linux]
published: true
hideInList: false
feature: 
isTop: false
---
你可以使用以下shell脚本来实现这个功能：

```bash
#!/bin/bash

# 指定目录
dir_path="/path/to/your/directory"

# 输出文件
output_file="tree.txt"

# 清空输出文件
> $output_file

# 遍历目录下的所有文件和子目录
function traverse() {
    local path="$1"
    local indent="$2"

    # 获取当前目录下的所有文件和子目录
    for item in "$path"/*; do
        # 如果是目录，则递归遍历
        if [ -d "$item" ]; then
            echo "${indent}├── $(basename "$item")" >> $output_file
            traverse "$item" "    $indent"
        # 如果是文件，则计算大小并输出
        elif [ -f "$item" ]; then
            size=$(du -sh "$item" | cut -f1)
            echo "${indent}├── $(basename "$item") ($size)" >> $output_file
        fi
    done
}

# 从根目录开始遍历
traverse "$dir_path" ""

# 打印生成的树状图文本文件
cat $output_file
```

将上述脚本保存为一个文件，例如`tree.sh`，并将`dir_path`变量设置为你想要查看的目录路径。然后在终端中运行`bash tree.sh`，脚本将会生成一个名为`tree.txt`的文件，其中包含指定目录下所有文件的大小以及树状图。
---
title: 'shell实现读取当前目录下指定扩展名的全部文件 并在循环里打印分开的文件名和扩展名'
date: 2024-05-01 13:23:53
tags: [shell,AI]
published: true
hideInList: false
feature: 
isTop: false
---
```shell
#!/bin/bash


# 指定要查找的扩展名
extension="mkv"

# 遍历当前目录下的所有文件
for file in *; do
    # 检查文件是否具有指定的扩展名
    if [[ $file == *.$extension ]]; then
        # 提取文件名和扩展名
        filename=$(basename "$file")
        basename_without_ext="${filename%.*}"
        ext="${filename##*.}"
        aftername=${basename_without_ext}.ogg
        # 打印分开的文件名和扩展名
        echo "文件名： $basename_without_ext"
        echo "扩展名： $ext"
        ffmpeg -i "${filename}" -map 0:a:0 -c:a libvorbis "${aftername}"
        echo "旧文件名: ${filename} 新文件名: ${aftername}" 
        echo ""
    fi
done
# ffmpeg -i "18Merry Christmas Mr Lawrence坂田龙一.mkv" -map 0:a:0 -c:a libvorbis "Merry Christmas Mr Lawrence坂田龙一.ogg"
```
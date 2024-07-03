---
title: 'FFmpeg 的 -strict'
date: 2024-03-05 15:49:52
tags: [ffmpeg]
published: true
hideInList: false
feature: 
isTop: false
---
FFmpeg 的 `-strict` 选项用于**设置MPEG4视觉编码的兼容性**。

FFmpeg 是一个强大的开源工具，能够处理多种音频和视频格式的录制、转换及流化。在处理 MPEG-4 视频编码时，`-strict` 选项特别重要，因为 MPEG-4 标准存在多个版本，不同版本的编解码器之间可能存在兼容性问题。

具体来说，`-strict` 选项可以有以下几个值：

1. `-strict -2`：这是一个比较宽松的模式，它允许使用一些非标准的编码特性。这在处理一些旧的或者非主流的设备生成的视频文件时可能会有用。
2. `-strict default` 或 `-strict experimental`：这些是更严格的模式，它们要求编码必须符合特定的标准。`default` 模式通常用于确保编码的兼容性，而 `experimental` 模式可能包含一些最新的编码技术，但这些技术可能不被所有的播放器支持。
3. `-strict -1`：这个选项在新版本的 FFmpeg 中不再推荐使用，因为它允许大量的非标准编码特性，可能会导致编码的视频与其他设备的兼容性问题。

综上，在使用 FFmpeg 进行 MPEG-4 编码时，选择合适的 `-strict` 选项可以帮助确保视频文件的兼容性和播放效果。如果不确定应该使用哪个选项，通常建议使用 `-strict default` 以保证最好的兼容性。
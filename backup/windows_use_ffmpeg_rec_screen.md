---
title: 'Windows下如何使用ffmpeg录制屏幕'
date: 2024-04-17 17:18:50
tags: [Windows,ffmpeg]
published: true
hideInList: false
feature: 
isTop: false
---
在Windows下使用ffmpeg录制屏幕，您可以通过以下步骤进行操作：

1. **安装FFmpeg**：您需要下载并安装FFmpeg。您可以从官方网站或者第三方网站下载适合Windows系统的FFmpeg版本，并解压缩。将bin目录添加到系统环境变量中，以便能够在命令行中直接使用ffmpeg命令。
2. **安装dshow软件**：为了能够使用dshow捕获屏幕，您需要安装一个名为Screen Capturer Recorder的软件。这个软件可以帮助您捕捉屏幕内容。您可以从项目的GitHub页面或者SourceForge网站上下载并安装它。
3. **查看可用设备**：安装完Screen Capturer Recorder后，打开命令提示符，输入`ffmpeg -list_devices true -f dshow -i dummy`来查看可用的DirectShow设备列表。这将列出您可以使用的设备名称，包括屏幕捕获设备。
4. **录制屏幕**：确认设备名称后，您可以使用以下命令来录制屏幕：

- `ffmpeg.exe -r 24 -f gdigrab -s 1920x1080 -i desktop -vcodec libx264 -y a.mp4`

其中，“设备名称”需要替换为您在第3步中找到的设备名称，output.mp4是您希望保存的视频文件名。这条命令将会以X264编码器和AAC音频编码器录制屏幕，生成的视频质量较高，文件大小也相对较大。

5. **结束录制**：当您想要结束录制时，可以直接关闭命令提示符窗口，或者在命令提示符中按Ctrl+C键。

请注意，录制屏幕可能会占用较多的系统资源，因此在录制过程中尽量避免进行其他资源密集型操作，以保证录制过程的流畅性。此外，确保您有合适的硬件配置来支持屏幕录制，特别是如果您打算录制高分辨率或长时间的视频内容。
---
title: 'FFMpeg常用命令'
date: 2022-09-26 16:23:32
tags: [ffmpeg]
published: true
hideInList: false
feature: 
isTop: false
---
#  有一个1.mp3音频文件 一个和它对应的1.srt字幕文件 如何利用ffmpeg 制作为纯黑背景 只有白色字幕和声音的mp4视频文件

您可以使用以下命令来利用ffmpeg制作一个只有白色字幕和声音的mp4视频
```shell
ffmpeg -i 1.mp3 -f lavfi -i color=c=black:s=1920x1080 -vf "subtitles=1.srt:force_style='Fontcolor=&HFFFFFF'" -c:v libx264 -c:a aac -strict experimental -shortest -r 60 1.mp4
```
# 查看支持的硬件加速

```shell
ffmpeg -hwaccels
```

# 查看支持的编码器

```shell
ffmpeg -encoders
```

# 查看支持的解码器

```shell
ffmpeg -decoders 
```

# 硬件加速举例

```shell
ffmpeg -hwaccel videotoolbox -i xxx.mp4  -vcodec libx265 demo1.mp4
```

# 转换AVIF图片

+ 静止图像

```shell
ffmpeg -i image.png -c:v libaom-av1 -still-picture 1 image.avif
```

+ 动画图像

```shell
ffmpeg -i video.mp4 animated.avif
```

# 修改视频码率

```shell
ffmpeg -i input.mp4  -b:v 10000k  output4.mp4
```

# 压缩视频

```shell
ffmpeg -i input.mp4 -fs 10MB output.com
```

# 遍历指定文件扩展名转换为其他格式

```shell
#!/bin/bash
for file in $(ls ./)
do
    if [ "${file##*.}" = "m3u8" ]; then
        mv ${file} ${file%.*}.c
        ffmpeg -i ${file} ${file%.*}.mp4
    fi
done
```

# 截取分段视频

```shell
ffmpeg -ss 00:00:00 -t 00:09:00 -i "NieR_Automata 同伴的行踪2.mp4" -vcodec copy -acodec copy "NieR_Automata 同伴的行踪2P1.mp4"`

`ffmpeg -ss 00:09:00 -i "NieR_Automata 同伴的行踪2.mp4" -vcodec copy -acodec copy "NieR_Automata 同伴的行踪2P2.mp4"`

# -ss 启始时间 -t 持续时间 无t参数截取到结束 -to 到第几秒
```

# 合成M4S

```shell
ffmpeg -i video.m4s -i audio.m4s -codec copy multi.mp4
```

# 批量转换格式

```shell
for %a in ("*.mp4") do ffmpeg -i "%a" "%~na.gif"
```

# 旋转视频

```shell
ffmpeg -i <inputfile> -vf "transpose=2,transpose=2" <outputfile>
ffmpeg -i 4.avi -vf "transpose=1" 4done.avi
其中transpose取值:
0 = 90CounterCLockwise and Vertical Flip (default)
1 = 90Clockwise
2 = 90CounterClockwise
3 = 90Clockwise and Vertical Flip
```

# 音视频合并

```shell
ffmpeg -i video.mp4 -i audio.wav -c:v copy -c:a aac -strict experimental output.mp4
```

# 抽取音频

```shell
ffmpeg -i 3.mp4 -vn -y -acodec copy 3.m4a
```

# 提取视频

```shell
ffmpeg -i Life.of.Pi.has.subtitles.mkv -vcodec copy –an  videoNoAudioSubtitle.mp4
```

# 替换音频合并

```shell
ffmpeg -i video.mp4 -i audio.wav -c:v copy -c:a aac -strict experimental -map 0:v:0 -map 1:a:0 output.mp4
```

# 提取视频的音频

```shell
ffmpeg -i input.mp4 -vn -y -acodec copy output.m4a
```

# 去除视频音频

```shell
ffmpeg -i input.mp4 -an output.mp4
```

# 嵌入字幕

```shell
ffmpeg -i movie.mkv -i sub.srt -map 0:v -map 0:a -map 1:s -c copy output.mkv
```

# 抽取音频

~~`ffmpeg -i 3.mp4 -vn -y -acodec copy 3.aac`~~

```shell
ffmpeg -i 3.mp4 -vn -y -acodec copy 3.m4a
```

# 拼接AVI视频

```shell
ffmpeg -f concat -safe 0 -i work.txt -c copy /Users/zen/Movies/out.avi
```

其中`work.txt`文件格式类似

```shell
file /Users/zen/Downloads/redisLesson/video/001.avi
file /Users/zen/Downloads/redisLesson/video/002.avi
file /Users/zen/Downloads/redisLesson/video/003.avi
file /Users/zen/Downloads/redisLesson/video/004.avi
file /Users/zen/Downloads/redisLesson/video/005.avi
file /Users/zen/Downloads/redisLesson/video/006.avi
file /Users/zen/Downloads/redisLesson/video/007.avi
file /Users/zen/Downloads/redisLesson/video/008.avi
file /Users/zen/Downloads/redisLesson/video/009.avi
file /Users/zen/Downloads/redisLesson/video/010.avi
```

**并且文件名外只能使用单引号**

# 为视频添加音轨

```shell
ffmpeg -i input_video_with_audio.avi -i new_audio.ac3 -map 0 -map 1 -codec copy output_video.avi
```

# 裁剪视频

```shell
ffmpeg -i 40.mp4 -vf crop=1080:1920:1291:2510 1.40.mp4
# 其中crop=宽:高:x坐标:y坐标
```

# 修改视频帧率

```shell
ffmpeg -i 40.mp4 -r 30 1.40.mp4
```

# 缩放视频尺寸

1. 完全按照给定尺寸拉伸缩放
```shell
ffmpeg -i 1.mp4 -strict -2 -s 640x480 4.mp4
```

2. 等比例缩放
```shell
ffmpeg -i 1.mp4 -strict -2 -vf scale=-1:480 4.mp4
```

#合并m3u8下载的分段视频

```shell
#!/bin/bash
# ffmpeg -i "concat:0.ts|1.ts|2.ts|3.ts|4.ts|5.ts|6.ts|7.ts|8.ts|9.ts" -c copy -bsf:a aac_adtstoasc -movflags +faststart output.mp4
ffmpeg -i "concat:0.ts|1.ts|2.ts|3.ts|4.ts|5.ts|6.ts|7.ts|8.ts|9.ts|10.ts|11.ts|12.ts" -c copy -bsf:a aac_adtstoasc -movflags +faststart output.mp4
```

# 提取视频中的音频重命名并删除原文件

```shell
#!/bin/bash
filename=$(ls *.mp4)
echo $filename
ffmpeg -i $filename -vn -y -acodec copy "name.m4a"
rm $filename
```

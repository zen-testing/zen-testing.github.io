---
title: 'ffmpeg null 参数'
date: 2023-11-07 10:59:06
tags: [ffmpeg]
published: true
hideInList: false
feature: 
isTop: false
---
中文互联网没救了,一个问题国内搜个遍,除了废话占用全文搜索权重的就是没有验证过的错误答案,最后还是原始wiki页面一点一点抠出来的

<!-- more -->

[原文地址](https://trac.ffmpeg.org/wiki/Null)

1.  [Null muxer](https://trac.ffmpeg.org/wiki/Null#Nullmuxer)
    1.  [Decoding & demuxing](https://trac.ffmpeg.org/wiki/Null#Decodingdemuxing)
    2.  [Encoding](https://trac.ffmpeg.org/wiki/Null#Encoding)
    3.  [With a particular muxer](https://trac.ffmpeg.org/wiki/Null#Withaparticularmuxer)
    4.  [`-benchmark` option](https://trac.ffmpeg.org/wiki/Null#a-benchmarkoption)
2.  [Filters](https://trac.ffmpeg.org/wiki/Null#Filters)
    1.  [anull](https://trac.ffmpeg.org/wiki/Null#anull)
    2.  [null](https://trac.ffmpeg.org/wiki/Null#null)
    3.  [anullsrc](https://trac.ffmpeg.org/wiki/Null#anullsrc)
    4.  [nullsrc](https://trac.ffmpeg.org/wiki/Null#nullsrc)
    5.  [anullsink](https://trac.ffmpeg.org/wiki/Null#anullsink)
    6.  [nullsink](https://trac.ffmpeg.org/wiki/Null#nullsink)

在`ffmpeg`中使用`null`的方法有多种
这对于测试和基准测试,创建输入和过滤非常有用

+ 测试解码速度
+ 无需磁盘写入成本即可测试编码速度
+ 测试设备输入速度
+ 创建一个空白视频"画布"用于过滤
+ 制作无声音频
+ 修复电视媒体播放器问题

___

## 空复用器 [¶](https://trac.ffmpeg.org/wiki/Null#Nullmuxer "链接到这一节")

[空复用器](https://ffmpeg.org/ffmpeg-formats.html#null) 不生成任何输出文件. 它主要用于测试或基准测试目的. 空复用器使用包装帧,因此没有复用开销(即它可以接受任何类型的输入编解码器,例如不必是原始视频).
## 解码和分离 [¶](https://trac.ffmpeg.org/wiki/Null#Decodingdemuxing "链接到这一节")

测试解码和分离 (使用空复用器):

```bash
ffmpeg -i input -f null -
```

## 编码 [¶](https://trac.ffmpeg.org/wiki/Null#Encoding "链接到这一节")

它还可用于测试编码,而无需输出文件的开销. 

```bash
# 此示例将映射第一个视频流,使用 libx264 进行编码,然后丢弃输出
ffmpeg -i input -map 0:v:0 -c:v libx264 -f null -
```

## 使用特定的复用器 [¶](https://trac.ffmpeg.org/wiki/Null#Withaparticularmuxer "链接到这一节")

如果您想选择复用器但实际上不输出文件,你可以输出到 `/dev/null`, 或者 `NUL` 在Windows系统

```bash
ffmpeg -y -i input -c:v mpeg4 -f mp4 /dev/null
```

## `-benchmark` 选项 [¶](https://trac.ffmpeg.org/wiki/Null#a-benchmarkoption "链接到这一节")

添加 `-benchmark` 全局选项 将在编码结束时输出基准测试信息,该信息可以为空复用器提供信息. 显示使用的 CPU 时间和最大内存消耗. 并非所有系统都支持最大内存消耗; 如果不支持,通常会显示为 0

```bash
ffmpeg -benchmark -i input output
...
bench: utime=8.483s
bench: maxrss=52736000kB
```

unix/linux 系统用户也可以使用 `time` 命令

```bash
time ffmpeg -i input output
...
real    0m3.365s
user    0m8.533s
sys     0m0.541s
```
___

## 过滤器 [¶](https://trac.ffmpeg.org/wiki/Null#Filters "链接到这一节")

有多种 null 过滤器

## anull [¶](https://trac.ffmpeg.org/wiki/Null#anull "链接到这一节")

[anull](https://ffmpeg.org/ffmpeg-filters.html#anull) 音频过滤器会将音频源原封不动地传递到输出

[null](https://ffmpeg.org/ffmpeg-filters.html#null) 视频过滤器会将视频源原封不动地传递到输出

也可以看看 [如何解决电视媒体播放器问题](https://trac.ffmpeg.org/wiki/HowToFixTvPlaybackIssues)

## 空源文件 [¶](https://trac.ffmpeg.org/wiki/Null#anullsrc "链接到这一节")

[空源文件](https://ffmpeg.org/ffmpeg-filters.html#anullsrc) 音频源过滤器可以创建无声音频 例如,要将无声音频流添加到视频

```bash
ffmpeg -i input.mp4 -f lavfi -i anullsrc -c:v copy -c:a aac -shortest output.mp4
```

空源文件在使用[concat过滤器](https://ffmpeg.org/ffmpeg-filters.html#concat)时特别有用 因为过滤器的所有输入必须具有相同数量的流. 例如`input0`和`input1`具有 48000 Hz 采样率的视频和立体声音频,而`input2`仅具有视频

```bash
ffmpeg -i input0 -i input1 -i input2 -t 1 -f lavfi -i anullsrc=r=48000:cl=stereo -filter_complex \
"[0:v][0:a][1:v][1:a][2:v][3:a]concat=n=3:v=1:a=1[v][a]" \
-map "[v]" -map "[a]" output
```

注意 `-t 1` 输入选项:您不需要将此持续时间值与关联的视频流相匹配. 它只需要更短,因为串联过滤器将用额外的静音来填充剩余的持续时间.

Windows 用户应将上述命令中的结尾'\'替换为'^'

也可以看看 [如何解决电视媒体播放器问题](https://trac.ffmpeg.org/wiki/HowToFixTvPlaybackIssues)

## 空源文件 [¶](https://trac.ffmpeg.org/wiki/Null#nullsrc "链接到这一节")

[空源文件](https://ffmpeg.org/ffmpeg-filters.html#nullsrc)视频源过滤器返回未处理的(即"原始未初始化内存")视频帧. 它可以用作其他过滤器的基础,其中输入被忽略或者您不介意有些随机输入. 使用 [geq](https://ffmpeg.org/ffmpeg-filters.html#geq) 滤波器在亮度平面中生成噪声的示例

```bash
ffmpeg -f lavfi -i nullsrc=s=256x256:d=5 -vf "geq=random(1)*255:128:128" output
```

## 空水槽 [¶](https://trac.ffmpeg.org/wiki/Null#anullsink "链接到这一节")

The [空水槽](https://ffmpeg.org/ffmpeg-filters.html#anullsink) 音频接收器对输入音频完全不执行任何操作.

## 空水槽 [¶](https://trac.ffmpeg.org/wiki/Null#nullsink "链接到这一节")

[空水槽](https://ffmpeg.org/ffmpeg-filters.html#nullsink) 视频接收器绝对不会对输入视频执行任何操作. `ffmpeg` 是"贪婪的",会抓取它能找到的任何流,所以如果你的 [过滤图](https://ffmpeg.org/ffmpeg-filters.html#Filtergraph-syntax) 不"输出"任何内容,它只会 重新编码输入并忽略过滤器. 例子:

```bash
ffmpeg -i input -filter_complex "[0:v]split[a][b];[a]nullsink" -map "[b]" output.mkv
```

在这种情况下,"ffmpeg"输出指定:

```bash
  split:output1 -> Stream #0:0 (libx264)
```

...这意味着分割的第二个输出正在被编码,并且第一个输出已被发送到空水槽
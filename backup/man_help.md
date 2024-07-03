---
title: '5分钟学会查看Linux帮助文档'
date: 2023-11-23 17:16:56
tags: [五分钟已经很棒了]
published: true
hideInList: false
feature: 
isTop: false
---
# 不知道命令是干什么用的
`whatis mediainfo ls`

```bash
mediainfo (1)        - command line utility to display information about audio/video files
ls (1)               - list directory contents
```
# 命令的基础使用方法
`mediainfo --help`
```bash
MediaInfo Command line,
MediaInfoLib - v23.04
Usage: "mediainfo [-Options...] FileName1 [Filename2...]"

Options:
--Help, -h
                    Display this help and exit
--Help-Output
                    Display help for Output= option
--Help-AnOption
                    Display help for "AnOption"
--Version
                    Display MediaInfo version and exit

--Full, -f
                    Full information Display (all internal tags)
--Output=HTML
                    Full information Display with HTML tags
--Output=XML
                    Full information Display with XML tags
--Output=OLDXML
                    Full information Display with XML tags using the older
                    MediaInfo schema
--Output=JSON
                    Full information Display using JSON
--Output=EBUCore
                    Full information Display with EBUCore compliant XML tags
--Output=EBUCore_JSON
                    Full information Display with EBUCore 1.8 compliant JSON
--Output=PBCore
                    Full information Display with PBCore compliant XML tags
--Output=PBCore2
                    Full information Display with PBCore 2.0 compliant XML tags
--AcquisitionDataOutputMode=segmentParameter
                    Display Acquisition Data by segment then parameter (EBUCore
                    and NISO Z39.87 outputs)
--AcquisitionDataOutputMode=parameterSegment
                    Display Acquisition Data by parameter then segment (EBUCore
                    and NISO Z39.87 outputs)
--ExternalMetadata=...
                    Add external metadata to the output (EBUCore output)
--ExternalMetadataConfig=...
                    Output template for external metadata (EBUCore output)
--Info-Parameters
                    Display list of Inform= parameters

--Language=raw
                    Display non-translated unique identifiers (internal text)
--Details=1
                    Display mediatrace info
--inform_version=1
                    Add MediaInfoLib version to the text output
--inform_timestamp=1
                    Add report creation timestamp to the text output
--File_TestContinuousFileNames=0
                    Disable image sequence detection
--LogFile=...
                    Save the output in the specified file
--BOM
                    Byte order mark for UTF-8 output

--Ssl_CertificateFileName=...
                    File name of the SSL certificate.
                    The default format is "PEM" and can be changed
                    with --Ssl_CertificateFormat.
--Ssl_CertificateFormat=...
                    File format of the SSL certificate.
                    Supported formats are "PEM" and "DER"
--Ssl_PrivateKeyFileName=...
                    File name of the SSL private key.
                    The default format is "PEM" and can be changed
                    with --Ssl_PrivateKeyFormat.
                    Note: private key with a password is not supported.
--Ssl_PrivateKeyFormat=...
                    File format of the SSL private key.
                    Supported formats are "PEM" and "DER"
--Ssl_CertificateAuthorityFileName=...
                    File name of the SSL certificate authorities
                    to verify the peer with.
--Ssl_CertificateAuthorityPath=...
                    Path of the SSL certificate authorities
                    to verify the peer with.
--Ssl_CertificateRevocationListFileName=...
                    File name of the SSL certificate revocation list.
                    The format is "PEM"
--Ssl_IgnoreSecurity=...
                    Does not verify the authenticity of the peer's certificate
                    Use it at your own risks
--Ssh_PublicKeyFileName=...
                    File name of the SSH private key.
                    Default is $HOME/.ssh/id_rsa.pub or $HOME/.ssh/id_dsa.pub
                    if the HOME environment variable is set, and just
                    "id_rsa.pub" or "id_dsa.pub" in the current directory
                    if HOME is not set.
                    Note: you need to set both public and private key.
--Ssh_PrivateKeyFileName=...
                    File name of the SSH private key.
                    Default is $HOME/.ssh/id_rsa or $HOME/.ssh/id_dsa
                    if the HOME environment variable is set, and just
                    "id_rsa" or "id_dsa" in the current directory
                    if HOME is not set.
                    Note: you need to set both public and private key.
                    Note: private key with a password is not supported.
--Ssh_KnownHostsFileName=...
                    File name of the known hosts
                    The format is the OpenSSH file format (libssh2)
                    Default is $HOME/.ssh/known_hosts
                    if the HOME environment variable is set, and just
                    "known_hosts" in the current directory
                    if HOME is not set.
--Ssh_IgnoreSecurity
                    Does not verify the authenticity of the peer
                    (you don't need to accept the key with ssh first)
                    Use it at your own risks
```

# 命令的详细手册

`man mediainfo`
```bash
MEDIAINFO(1)                                                          User Commands                                                         MEDIAINFO(1)

NAME
       MediaInfo - command line utility to display information about audio/video files

       MediaInfo-Gui - graphical utility to display information about audio/video files

SYNOPSIS
       mediainfo [-Options...] FileName1 [Filename2...]
       mediainfo --Inform=FMT FileName
       mediainfo-gui [-Options...] FileName1 [Filename2...]
       mediainfo-gui --Inform=FMT FileName

DESCRIPTION
       MediaInfo supplies technical and tag information about a video or audio file

       What information can I get from MediaInfo?

       - General: title, author, director, album, track number, date, duration...
       - Video: codec, aspect, fps, bitrate...
       - Audio: codec, sample rate, channels, language, bitrate...
       - Text: language of subtitle
       - Chapters: number of chapters, list of chapters

       What format does MediaInfo support?

       - Video: MKV, OGM, AVI, DivX, WMV, QuickTime, Real, MPEG-1, MPEG-2, MPEG-4, DVD (VOB)...
       - Video Codecs: DivX, XviD, MSMPEG4, ASP, H.264, AVC...
       - Audio: OGG, MP3, WAV, RA, AC3, DTS, AAC, M4A, AU, AIFF...
       - Subtitles: SRT, SSA, ASS, SAMI...

       What can I do with it?

       - Read many video and audio file formats
       - View information in different formats (text, sheet, tree, HTML...)
       - Customise these viewing formats
       - Export information as text, CSV, HTML...
       - Graphical Interface, Command Line, or library versions available

OPTIONS
       MediaInfo supports the following case-insensitive options:

       --Help, -h
           Display help and exit

       --Help-Inform
           Display help for --Inform option

       --Help-AnOption
           Display help for "AnOption"

       --Version
           Display MediaInfo version and exit

       --Full, -f
           Full information Display (all internal tags)

       --Output=HTML
           Full information Display with HTML tags

       --Output=XML
           Full information Display with XML tags

       --Inform=FMT
           Template defined information display.

           FMT is "[xxx;]Text", where xxx can be any one of General, Video, Audio, Text, Chapter, Image, or Menu. Text can be the template text, or a
           filename in the form of file:///path

           See --Info-Parameters for available parameters in the text. Parameters must be surrounded by "%".

       --Info-Parameters
           Display list of --Inform parameters

       --Language=raw
           Display non-translated unique identifiers (internal text)

       --LogFile=LogFile
           Save the output in LogFile

EXAMPLES
   Display information about a video file
        $ mediainfo foo.mkv

   Display aspect ratio
        $ mediainfo --Inform="Video;%DisplayAspectRatio%" foo.mkv
        $ mediainfo --Inform="Video;file://Video.txt" foo.mkv

       Both forms are equivalent if Video.txt contains:
        %DisplayAspectRatio%

   Display aspect ration and audio format
        $ mediainfo --Inform="file://Text.txt foo.mkv

       If Text.txt contains:

       - "Video;%DisplayAspectRatio%"
           Then the display aspect ratio is printed out.

       - "Audio;%Format%"
           Then the audio format is printed out.

AUTHOR
       This manual page was written by Chow Loong Jin <hyperair@debian.org> for the Debian system (but may be used by others). Permissions is granted to
       copy, distribute, and/or modify this document under the terms of the GNU General Public License, Version 3 or any later version published by the
       Free Software Foundation.

       On Debian systems, the full text of the GNU General Public License, Version 3 can be found in /usr/share/common-licenses/GPL-3.

MediaInfo 0.7.52                                                       2023-05-02                                                           MEDIAINFO(1)
```

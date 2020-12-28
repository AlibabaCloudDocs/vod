# Video seeking

Video seeking allows you to seek to a specified position during the playback of an audio or a video file without compromising the playback quality. This topic describes how to configure video seeking.

## Overview

Video seeking can be used in the playback of on-demand audio or video files. When you seek to a specified position during the playback, the client sends a URL request, for example, `http://www.aliyun.com/test.flv?start=10`, to the server. After the server receives the request, the server seeks to the keyframe at the position that is specified by the start parameter. If no keyframe can be found at the specified position, the server seeks to the last keyframe before the specified position.

Before you configure video seeking, you must enable object chunking. For more information, see [Object chunking](/intl.en-US/User Guide/Domain management/Video-related settings/Configure object chunking.md). If an HTTP request contains the Range field in its header, the origin server returns the HTTP 206 Partial Content status code.

The following table describes the file formats that are supported by video seeking and the sample URLs.

|File format|Metadata|Start parameter|Example|
|:----------|:-------|:--------------|:------|
|MP4|The metadata of video files on the origin server must be contained in the file headers rather than the file tails.|The value of the start parameter indicates a specified position. If no keyframe can be found at the specified position, Alibaba Cloud CDN automatically seeks to the last keyframe before the specified position. The unit of the start parameter is seconds. This parameter supports decimals. For example, if you set the start parameter to 1.01, Alibaba Cloud CDN seeks to the 1.01-second mark.|The request URL `http://domain/video.mp4? start=10` specifies that the video is played from the 10th second.|
|FLV|Video files on the origin server must contain metadata.|The value of the start parameter indicates a specified byte. If no keyframe can be found at the position of the specified byte, Alibaba Cloud CDN automatically seeks to the last keyframe before the specified byte.|The request URL `http:// domain/video.flv? start=10` specifies that the video is played from the last keyframe before the 10th byte.|

1.  Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/).

2.  In the left-side navigation pane, click **Configuration Management**.

3.  Choose **CDN Configuration** \> **Domain Names**.

4.  On the Domain Names page, select the domain name that you want to configure, and click **Configure** in the Actions column.

    ![Click Configure](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2585068061/p180549.png)

5.  Click the **Video Related** tab and turn on **Drag/Drop Playback**.

    ![Video seeking](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5664888061/p181802.png)



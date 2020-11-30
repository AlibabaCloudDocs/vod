# Python上传SDK

通过视频点播上传SDK服务，您可以实现方便、快速的上传媒体文件。本文通过示例为您详细介绍Python上传SDK服务。

## 功能介绍

使用上传SDK服务可实现的主要功能如下：

-   上传各种媒体文件到视频点播：音视频、图片、辅助媒资（如水印、字幕文件）。
-   上传本地媒体文件到视频点播：默认使用分片上传，最大支持48.8 TB的单个文件，暂不支持断点续传。
-   上传网络媒体文件到视频点播：最大支持48.8 TB的单个文件，需先下载到本地临时目录再上传，暂不支持断点续传。
-   上传m3u8视频：提供解析m3u8索引文件得到分片地址列表的接口，也可以自行指定分片文件地址。

除了上述主要功能外，上传SDK服务还可实现以下功能：

-   上传进度条，支持默认进度回调和自定义进度回调。
-   可指定上传脚本部署的ECS区域，如果和视频点播存储区域相同，则自动使用内网上传，上传更快且更省公网流量。
-   可指定视频点播中心（默认为上海）和存储区域，便于海外上传。
-   支持上传时设置元数据（如标题），以及StorageLocation、UserData、转码模板等。

上传SDK服务支持的文件格式请参见[媒体上传文件格式](/intl.zh-CN/开发指南/媒体上传/概述.md)。

## 前提条件

-   已安装Python 2.7或以上版本，安装方法请参见[Python官网](https://www.python.org/)。
-   已安装pip，安装方法请参见[pip官网](https://pip.pypa.io/en/stable/installing)。

## 安装SDK

1.  执行以下命令安装依赖包。

    pip install aliyun-python-sdk-core

    pip install aliyun-python-sdk-vod

    pip install oss2

    **说明：** 如果使用的是 Python 3.x，请将pip install aliyun-python-sdk-core修改为pip install aliyun-python-sdk-core-v3。如果同时安装了不同版本，可使用pip3命令。

2.  下载Python上传SDK及示例代码VodUploadSDK-Python\_1.3.1.zip，更多信息，请参见[SDK下载](/intl.zh-CN/SDK下载/SDK下载.md)。

    **说明：** 此处以SDK1.3.1版本举例说明。其他版本请根据实际情况操作。

3.  解压VodUploadSDK-Python\_1.3.1.zip，将VodUploadSDK-Python\_1.3.1目录下的voduploadsdk复制到本地SDK安装目录中。


## 更新SDK

若发现新的接口或已有接口新的功能在当前SDK没有，可将SDK更新到最新版。

1.  执行以下命令更新依赖包。

    pip install --upgrade aliyun-python-sdk-vod

    pip install --upgrade oss2

2.  下载最新的Python上传SDK覆盖到本地SDK文件。更多信息，请参见[SDK下载](/intl.zh-CN/SDK下载/SDK下载.md)。

    **说明：** 您可以打开voduploadsdk目录下的ChangeLog.txt文件查看当前SDK的版本号和发布日期。


## SDK目录说明

-   voduploadsdk目录
    -   AliyunVodUtils.py
        -   AliyunVodLog：上传SDK的日志类，基于logging实现。
        -   AliyunVodUtils：上传SDK的工具类。
        -   AliyunVodException：上传SDK的异常类，做统一的异常处理，外部捕获此异常即可。
    -   UploadVideoRequest.py

        UploadVideoRequest：上传视频的请求类，字段请参见[获取视频上传地址和凭证](/intl.zh-CN/服务端API/媒体上传/获取视频上传地址和凭证.md)。

    -   UploadImageRequest.py

        UploadImageRequest：上传图片的请求类，字段请参见[获取图片上传地址和凭证](/intl.zh-CN/服务端API/媒体上传/获取图片上传地址和凭证.md)。

    -   UploadAttachedMediaRequest.py

        UploadAttachedMediaRequest：上传辅助媒资的请求类，字段请参见[获取辅助媒资上传地址和凭证](/intl.zh-CN/服务端API/媒体上传/获取辅助媒资上传地址和凭证.md)。

    -   AliyunVodUploader.py：主要介绍AliyunVodUploader类
        -   uploadLocalVideo：上传本地视频的接口。
        -   uploadWebVideo：上传网络视频的接口。
        -   uploadLocalM3u8：上传本地m3u8视频。
        -   uploadWebM3u8：上传网络m3u8视频。
        -   uploadImage：上传本地或网络图片文件。
        -   uploadAttachedMedia：上传本地或网络辅助媒资文件。
        -   parseWebM3u8：解析网络m3u8文件的分片信息。
        -   parseLocalM3u8：解析本地m3u8文件的分片信息。
        -   setApiRegion：设置VoD的接入地址。默认为cn-shanghai（上海），海外支持ap-southeast-1（新加坡）等区域。详情请参见[点播中心和访问域名](/intl.zh-CN/开发指南/点播中心和访问域名.md)。
        -   setMultipartUpload：设置分片上传的阈值、分片大小。
        -   uploadProgressCallback：上传进度回调函数，可重写。
        -   setEnableCrc：上传时是否启用CRC校验，默认开启。
    -   ChangeLog.txt 版本发布记录，首行即为当前SDK的版本号和发布日期。
-   samples目录
    -   uploadVideo.py：上传视频的示例代码。
    -   uploadImage.py：上传图片的示例代码。

## 使用示例

以上传本地视频和网络视频为例，如下所示：

```
# -*- coding: UTF-8 -*-
from voduploadsdk.AliyunVodUtils import *
from voduploadsdk.AliyunVodUploader import AliyunVodUploader
from voduploadsdk.UploadVideoRequest import UploadVideoRequest 

# 测试上传本地视频
def testUploadLocalVideo(accessKeyId, accessKeySecret, filePath, storageLocation=None):
    try:
        uploader = AliyunVodUploader(accessKeyId, accessKeySecret)
        uploadVideoRequest = UploadVideoRequest(filePath, 'test upload local video')
        # 可以设置视频封面，如果是本地或网络图片可使用UploadImageRequest上传图片到视频点播，获取到ImageURL
        #uploadVideoRequest.setCoverURL('https://sample.com/sample.jpg')  
        #uploadVideoRequest.setTags('tag1,tag2')
        if storageLocation:
            uploadVideoRequest.setStorageLocation(storageLocation)
        videoId = uploader.uploadLocalVideo(uploadVideoRequest)
        print("file: %s, videoId: %s" % (uploadVideoRequest.filePath, videoId))
        
    except AliyunVodException as e:
        print(e)
 
# 测试上传网络视频
def testUploadWebVideo(accessKeyId, accessKeySecret, fileUrl, storageLocation=None):
    try:
        uploader = AliyunVodUploader(accessKeyId, accessKeySecret)
        uploadVideoRequest = UploadVideoRequest(fileUrl, 'test upload web video')
        uploadVideoRequest.setTags('tag1,tag2')
        if storageLocation:
            uploadVideoRequest.setStorageLocation(storageLocation)
        videoId = uploader.uploadWebVideo(uploadVideoRequest)
        print("file: %s, videoId: %s" % (uploadVideoRequest.filePath, videoId))
        
    except AliyunVodException as e:
        print(e)

####  执行测试代码   ####   
accessKeyId = '<AccessKeyId>'
accessKeySecret = '<AccessKeySecret>'

localFilePath = '/opt/video/sample.mp4'
testUploadLocalVideo(accessKeyId, accessKeySecret, localFilePath)

fileUrl = 'http://sample.oss.aliyuncs.com/video/sample.mp4'
#testUploadWebVideo(accessKeyId, accessKeySecret, fileUrl)
```

更多示例代码请参见samples目录中其它示例文件。


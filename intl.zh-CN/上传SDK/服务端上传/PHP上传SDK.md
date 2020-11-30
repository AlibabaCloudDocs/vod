# PHP上传SDK

通过视频点播上传SDK服务，您可以实现方便、快速的上传媒体文件。本文通过示例为您详细介绍PHP上传SDK服务。

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

-   已安装PHP 5.3或以上版本，关于如何安装，请参见[PHP官网](http://cn.php.net/downloads.php)。
-   已安装并启用相应扩展：php-mbstring、php\_curl。

## 安装SDK

1.  下载PHP上传SDK及示例代码VodUploadSDK-PHP\_1.0.2.zip，请参见[服务端上传SDK](/intl.zh-CN/SDK下载/SDK下载.md)。

    **说明：** 此处以SDK1.0.2版本举例说明。其他版本请根据实际情况操作。

2.  解压VodUploadSDK-PHP\_1.0.2.zip，将VodUploadSDK-PHP\_1.0.2目录下的voduploadsdk复制到您的项目中。


## 更新SDK

若发现新的接口或已有接口新的功能在当前SDK没有，请下载最新的PHP上传SDK覆盖到本地SDK文件。更多信息，请参见[服务端上传SDK](/intl.zh-CN/SDK下载/SDK下载.md)。

**说明：** 您可以打开voduploadsdk目录下的ChangeLog.txt文件查看当前SDK的版本号和发布日期。

## SDK目录说明

|目录|说明|
|--|--|
|/VodUploadSDK-PHP\_1.0.2.zip解压目录/VodUploadSDK-PHP\_1.0.2/voduploadsdk/uploader|-   UploadVideoRequest.php

UploadVideoRequest：上传视频的请求类，字段请参见[获取视频上传地址和凭证](/intl.zh-CN/服务端API/媒体上传/获取视频上传地址和凭证.md)。

-   UploadImageRequest.php

UploadImageRequest：上传图片的请求类，字段请参见[获取图片上传地址和凭证](/intl.zh-CN/服务端API/媒体上传/获取图片上传地址和凭证.md)。

-   UploadAttachedMediaRequest.php

UploadAttachedMediaRequest：上传辅助媒资的请求类，字段请参见[获取辅助媒资上传地址和凭证](/intl.zh-CN/服务端API/媒体上传/获取辅助媒资上传地址和凭证.md)。

-   AliyunVodUploader.php：主要介绍AliyunVodUploader类
    -   \_\_construct：构造函数：可设置上传的AccessKey以及视频点播中心和访问域名。请参见[AccessKey](/intl.zh-CN/开发指南/账号和授权/创建RAM用户并授权.md)和[点播中心和访问域名](/intl.zh-CN/开发指南/点播中心和访问域名.md)。
    -   uploadLocalVideo：上传本地视频的接口。
    -   uploadWebVideo：上传网络视频的接口。
    -   uploadLocalImage：上传本地图片。
    -   uploadWebImage：上传网络图片。
    -   uploadLocalAttachedMedia：上传本地辅助媒资文件。
    -   uploadWebAttachedMedia：上传网络辅助媒资文件。
    -   uploadLocalM3u8：上传本地m3u8视频。
    -   uploadWebM3u8：上传网络m3u8视频。
    -   parseM3u8File：解析m3u8索引文件得到分片地址列表。
    -   setEcsRegionId：设置上传脚本部署的ECS区域（如果有），如果与视频点播存储同一区域会自动启用内网上传。
    -   setEnableSSL：是否启用SSL（网络请求使用HTTPS），默认不启用，以避免相关扩展未安装或配置异常时无法使用。
    -   uploadProgressCallback：上传进度回调函数，可重写。
-   AliyunVodUtils.php
    -   AliyunVodUtils：工具类，提供截取字符串、获取扩展名、获取文件名等静态函数。
    -   AliyunVodLog：实现简单打印的日志类，logSwitch为日志开关。
    -   AliyunVodDownloader：实现下载网络文件。
    -   AliyunVodReportUpload：实现上传进度汇报。
    -   AliyunVodError：定义错误码。 |
|/VodUploadSDK-PHP\_1.0.2.zip解压目录/VodUploadSDK-PHP\_1.0.2/voduploadsdk|-   aliyun-php-sdk-core：上传SDK依赖的基础类，封装了阿里云API签名和HTTP请求等。
-   aliyun-php-sdk-vod：视频点播的服务端接口SDK，封装了视频点播API的请求。
-   aliyun-php-sdk-oss：上传SDK依赖的OSS类，封装了OSS上传等操作。 |
|/VodUploadSDK-PHP\_1.0.2.zip解压目录/VodUploadSDK-PHP\_1.0.2/samples|-   uploadVideo.php：上传视频的示例代码。
-   uploadImage.php：上传图片的示例代码。
-   uploadAttachedMedia.php：上传辅助媒资的示例代码。 |

## 使用示例

以上传本地视频和网络视频为例，相关API请参见[获取视频上传地址和凭证](/intl.zh-CN/服务端API/媒体上传/获取视频上传地址和凭证.md)。

```
<?php
/**
 * Created by Aliyun ApsaraVideo VOD.
 */
require_once dirname(__DIR__) . DIRECTORY_SEPARATOR . 'voduploadsdk' . DIRECTORY_SEPARATOR . 'Autoloader.php';
date_default_timezone_set('PRC');
//测试上传本地视频
function testUploadLocalVideo($accessKeyId, $accessKeySecret, $filePath)
{
    try {
        $uploader = new AliyunVodUploader($accessKeyId, $accessKeySecret);
        $uploadVideoRequest = new UploadVideoRequest($filePath, 'testUploadLocalVideo via PHP-SDK');
        //$uploadVideoRequest->setCateId(1);
        //$uploadVideoRequest->setCoverURL("http://xxxx.jpg");
        //$uploadVideoRequest->setTags('test1,test2');
        //$uploadVideoRequest->setStorageLocation('outin-xx.oss-cn-beijing.aliyuncs.com');
        //$uploadVideoRequest->setTemplateGroupId('6ae347b0140181ad371d197ebe289326');
        $userData = array(
            "MessageCallback"=>array("CallbackURL"=>"https://demo.sample.com/ProcessMessageCallback"),
            "Extend"=>array("localId"=>"xxx", "test"=>"www")
        );
        $uploadVideoRequest->setUserData(json_encode($userData));
        $res = $uploader->uploadLocalVideo($uploadVideoRequest);
        print_r($res);
    } catch (Exception $e) {
        printf("testUploadLocalVideo Failed, ErrorMessage: %s\n Location: %s %s\n Trace: %s\n",
            $e->getMessage(), $e->getFile(), $e->getLine(), $e->getTraceAsString());
    }
}
//测试上传网络视频
function testUploadWebVideo($accessKeyId, $accessKeySecret, $fileURL)
{
    try {
        $uploader = new AliyunVodUploader($accessKeyId, $accessKeySecret);
        $uploadVideoRequest = new UploadVideoRequest($fileURL, 'testUploadWebVideo via PHP-SDK');
        $res = $uploader->uploadWebVideo($uploadVideoRequest);
        print_r($res);
    } catch (Exception $e) {
        printf("testUploadWebVideo Failed, ErrorMessage: %s\n Location: %s %s\n Trace: %s\n",
            $e->getMessage(), $e->getFile(), $e->getLine(), $e->getTraceAsString());
    }
}
//测试上传本地m3u8视频
function testUploadLocalM3u8($accessKeyId, $accessKeySecret, $m3u8FilePath)
{
    try {
        $uploader = new AliyunVodUploader($accessKeyId, $accessKeySecret);
        $uploadVideoRequest = new UploadVideoRequest($m3u8FilePath, 'testUploadLocalM3u8 via PHP-SDK');
        // 调用接口解析m3u8的分片地址列表，如果解析结果不准确，请自行拼接地址列表(默认分片文件和m3u8文件位于同一目录)
        $sliceFiles = $uploader->parseM3u8File($m3u8FilePath);
        //print_r($sliceFiles);
        $res = $uploader->uploadLocalM3u8($uploadVideoRequest, $sliceFiles);
        print_r($res);
    } catch (Exception $e) {
        printf("testUploadLocalM3u8 Failed, ErrorMessage: %s\n Location: %s %s\n Trace: %s\n",
            $e->getMessage(), $e->getFile(), $e->getLine(), $e->getTraceAsString());
    }
}
//测试上传网络m3u8视频
function testUploadWebM3u8($accessKeyId, $accessKeySecret, $m3u8FileUrl)
{
    try {
        $uploader = new AliyunVodUploader($accessKeyId, $accessKeySecret);
        $uploadVideoRequest = new UploadVideoRequest($m3u8FileUrl, 'testUploadWebM3u8 via PHP-SDK');
        //调用接口解析m3u8的分片地址列表，如果解析结果不准确，请自行拼接地址列表(默认分片文件和m3u8文件位于同一目录)
        $sliceFileUrls = $uploader->parseM3u8File($m3u8FileUrl);
        //print_r($sliceFileUrls);
        $res = $uploader->uploadWebM3u8($uploadVideoRequest, $sliceFileUrls);
        print_r($res);
    } catch (Exception $e) {
        printf("testUploadWebM3u8 Failed, ErrorMessage: %s\n Location: %s %s\n Trace: %s\n",
            $e->getMessage(), $e->getFile(), $e->getLine(), $e->getTraceAsString());
    }
}
####  执行测试代码   ####
$accessKeyId = '<AccessKeyId>';
$accessKeySecret = '<AccessKeySecret>';
//$localFilePath = 'C:\test\sample.mp4';
$localFilePath = '/opt/video/sample.mp4';
//testUploadLocalVideo($accessKeyId, $accessKeySecret, $localFilePath);
$webFileURL = 'http://vod-test1.cn-shanghai.aliyuncs.com/b55b904bc612463b812990b7c8cc95c8/daa30814c0c340cf8199926f78aa5c0e-a0bc05ba62c3e95cc672e88b828148c9-ld.mp4?auth_key=1608774986-0-0-c56acd302bea0c331370d8ed686502fe';
testUploadWebVideo($accessKeyId, $accessKeySecret, $webFileURL);
$localM3u8FilePath = '/opt/video/m3u8/sample.m3u8';
//testUploadLocalM3u8($accessKeyId, $accessKeySecret, $localM3u8FilePath);
$webM3u8FileURL = 'http://vod-test1.cn-shanghai.aliyuncs.com/b55b904bc612463b812990b7c8cc95c8/daa30814c0c340cf8199926f78aa5c0e-195a25af366b5edae324c47e99a03f04-ld.m3u8?auth_key=1608775606-0-0-9fb038deaecd009dadd86721c5855629';
//testUploadWebM3u8($accessKeyId, $accessKeySecret, $webM3u8FileURL);
```

更多示例代码请参见samples目录中其它示例文件。


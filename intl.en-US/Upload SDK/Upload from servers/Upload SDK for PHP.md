# Upload SDK for PHP

You can use the upload SDKs of ApsaraVideo VOD to upload media files with efficiency. This topic provides an example to describe how to use the upload SDK for PHP.

## Features

The upload SDK provides the following major features:

-   Allows you to upload various types of media files to ApsaraVideo VOD, including video and audio files, images, and auxiliary media assets such as watermarks and subtitle files.
-   Allows you to upload on-premises media files: By default, multipart upload is used. A single file to upload can be up to 48.8 TB in size. Resumable upload is supported.
-   Allows you to upload online media files to ApsaraVideo VOD: A single file to upload can be up to 48.8 TB in size. Online media files are downloaded to on-premises temporary directories and then uploaded to ApsaraVideo VOD. Resumable upload is not supported.
-   Allows you to upload M3U8 video files: ApsaraVideo VOD provides an operation to parse the M3U8 index files to obtain the lists of part URLs. You can also specify the URLs of part files as needed.

The upload SDK provides the following additional features:

-   Provides an upload progress bar and supports the callbacks for default and custom upload progress.
-   Allows you to specify the region of an Elastic Compute Service \(ECS\) instance on which the upload script is to be deployed. If the region of the ECS instance is the same as the storage region in ApsaraVideo VOD, the specified file is automatically uploaded by using an internal network. This can accelerate the upload speed and save the public network traffic.
-   Allows you to specify the VOD center and storage region to facilitate upload outside China. The default VOD center is in the China \(Shanghai\) region.
-   Allows you to set the metadata, such as the title, storage locations, user data, and transcoding templates for the upload.

For more information about the file formats that are supported by ApsaraVideo VOD, see the "Supported file formats" section of [Overview](/intl.en-US/Developer Guide/Upload Medias/Overview.md).

## Prerequisites

-   PHP 5.3 or later is installed. For more information, visit the [PHP official website](http://cn.php.net/downloads.php).
-   The php-mbstring and php\_curl extensions are installed and enabled.

## Install the SDK

1.  Download the VodUploadSDK-PHP\_1.0.2.zip package, which contains the upload SDK for PHP and sample code. For more information, see [SDK download](/intl.en-US/SDK Downloads/SDK download.md).

    **Note:** In this topic, the SDK V1.0.2 is used as an example. You can use other versions based on your business requirements.

2.  Decompress the VodUploadSDK-PHP\_1.0.2.zip package and copy voduploadsdk in the VodUploadSDK-PHP\_1.0.2 directory to your project.


## Update the SDK

If new operations or new features of existing operations are unavailable in the current SDK, download the latest version of the SDK, extract files, and then save them by replacing existing ones. For more information, see [SDK download](/intl.en-US/SDK Downloads/SDK download.md).

**Note:** You can check the version number and release date of the current SDK in the first line of the ChangeLog.txt file in the voduploadsdk directory.

## Description of directories

|Directory|Description|
|---------|-----------|
|/VodUploadSDK-PHP\_1.0.2.zip decompress directory/VodUploadSDK-PHP\_1.0.2/voduploadsdk/uploader|-   UploadVideoRequest.php

UploadVideoRequest: the request class for uploading videos. For more information about the parameters, see [CreateUploadVideo](/intl.en-US/API Reference/Media upload/CreateUploadVideo.md).

-   UploadImageRequest.php

UploadImageRequest: the request class for uploading images. For more information about the parameters, see [CreateUploadImage](/intl.en-US/API Reference/Media upload/CreateUploadImage.md).

-   UploadAttachedMediaRequest.php

UploadAttachedMediaRequest: the request class for uploading auxiliary media assets. For more information about the parameters, see [CreateUploadAttachedMedia](/intl.en-US/API Reference/Media upload/CreateUploadAttachedMedia.md).

-   AliyunVodUploader.php includes methods of the AliyunVodUploader class.
    -   \_\_construct: a constructor used to set the AccessKey pair and ApsaraVideo VOD endpoint for the upload. For more information, see [Create and grant permissions to a RAM user](/intl.en-US/Developer Guide/Access authorization/Create and grant permissions to a RAM user.md) and [VOD centers and endpoints](/intl.en-US/Developer Guide/VOD centers and endpoints.md).
    -   uploadLocalVideo: a method used to upload on-premises videos.
    -   uploadWebVideo: a method used to upload online videos.
    -   uploadLocalImage: a method used to upload on-premises images.
    -   uploadWebImage: a method used to upload online images.
    -   uploadLocalAttachedMedia: a method used to upload on-premises auxiliary media assets.
    -   uploadWebAttachedMedia: a method used to upload online auxiliary media assets.
    -   uploadLocalM3u8: a method used to upload on-premises M3U8 videos.
    -   uploadWebM3u8: a method used to upload online M3U8 videos.
    -   parseM3u8File: a method used to parse the M3U8 playlist to obtain the URLs of parts.
    -   setEcsRegionId: a method used to specify the region of the ECS instance on which the upload script is to be deployed. If the region of the ECS instance is the same as the storage region in ApsaraVideo VOD, the file is automatically uploaded over the internal network.
    -   setEnableSSL: a method used to specify whether to enable Secure Sockets Layer \(SSL\) for HTTPS requests. By default, SSL is disabled to prevent the failure to use the SDK when related extensions are not installed or a configuration exception occurs.
    -   uploadProgressCallback: a method used to set the callback for upload progress. This method can be overridden.
-   AliyunVodUtils.php
    -   AliyunVodUtils: the utility class. It provides static functions for truncating strings and obtaining extensions and file names.
    -   AliyunVodLog: the log class. It provides a simple logging feature. You can set the logSwitch parameter to determine whether to enable logging.
    -   AliyunVodDownloader: downloads online files.
    -   AliyunVodReportUpload: reports the upload progress.
    -   AliyunVodError: defines the error code. |
|/VodUploadSDK-PHP\_1.0.2.zip decompress directory/VodUploadSDK-PHP\_1.0.2/voduploadsdk|-   aliyun-php-sdk-core: provides the base class on which the upload SDK depends. This package encapsulates Alibaba Cloud API signatures and HTTP requests.
-   aliyun-php-sdk-vod: provides the server SDK of ApsaraVideo VOD. This package encapsulates ApsaraVideo VOD API requests.
-   aliyun-php-sdk-oss: provides the Object Storage Service \(OSS\) class on which the upload SDK depends. This package encapsulates operations such as OSS upload. |
|/VodUploadSDK-PHP\_1.0.2.zip decompress directory/VodUploadSDK-PHP\_1.0.2/samples|-   uploadVideo.php: provides the sample code for uploading videos.
-   uploadImage.php: provides the sample code for uploading images.
-   uploadAttachedMedia.php: provides the sample code for uploading auxiliary media assets. |

## Sample code

The following sample code shows you how to upload an on-premises video and an online video. For more information about the related API operation, see [CreateUploadVideo](/intl.en-US/API Reference/Media upload/CreateUploadVideo.md).

```
<? php
/**
 * Created by Aliyun ApsaraVideo VOD.
 */
require_once dirname(__DIR__) . DIRECTORY_SEPARATOR . 'voduploadsdk' . DIRECTORY_SEPARATOR . 'Autoloader.php';
date_default_timezone_set('PRC');
// Test the upload of an on-premises video.
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
// Tests the upload of an online video.
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
// Test the upload of an on-premises M3U8 video.
function testUploadLocalM3u8($accessKeyId, $accessKeySecret, $m3u8FilePath)
{
    try {
        $uploader = new AliyunVodUploader($accessKeyId, $accessKeySecret);
        $uploadVideoRequest = new UploadVideoRequest($m3u8FilePath, 'testUploadLocalM3u8 via PHP-SDK');
        // Call the method for parsing the M3U8 playlist to obtain the URLs of parts. If the parsing result is invalid, manually assemble the URLs of parts. By default, the part files and M3U8 files are stored in the same directory.
        $sliceFiles = $uploader->parseM3u8File($m3u8FilePath);
        //print_r($sliceFiles);
        $res = $uploader->uploadLocalM3u8($uploadVideoRequest, $sliceFiles);
        print_r($res);
    } catch (Exception $e) {
        printf("testUploadLocalM3u8 Failed, ErrorMessage: %s\n Location: %s %s\n Trace: %s\n",
            $e->getMessage(), $e->getFile(), $e->getLine(), $e->getTraceAsString());
    }
}
// Test the upload of an online M3U8 video.
function testUploadWebM3u8($accessKeyId, $accessKeySecret, $m3u8FileUrl)
{
    try {
        $uploader = new AliyunVodUploader($accessKeyId, $accessKeySecret);
        $uploadVideoRequest = new UploadVideoRequest($m3u8FileUrl, 'testUploadWebM3u8 via PHP-SDK');
        // Call the method for parsing the M3U8 playlist to obtain the URLs of parts. If the parsing result is invalid, manually assemble the URLs of parts. By default, the part files and M3U8 files are stored in the same directory.
        $sliceFileUrls = $uploader->parseM3u8File($m3u8FileUrl);
        //print_r($sliceFileUrls);
        $res = $uploader->uploadWebM3u8($uploadVideoRequest, $sliceFileUrls);
        print_r($res);
    } catch (Exception $e) {
        printf("testUploadWebM3u8 Failed, ErrorMessage: %s\n Location: %s %s\n Trace: %s\n",
            $e->getMessage(), $e->getFile(), $e->getLine(), $e->getTraceAsString());
    }
}
####   Run the test code.   ####
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

For more sample code, see the files in the samples directory.


# Upload from servers

You can upload media files from application servers to OSS buckets allocated by ApsaraVideo VOD. This method is suitable for scenarios where you require automated upload or want to upload a large amount of video files or network media files. To upload network media files, you must download the files to an application server and then upload the files from the application server. This topic describes the features, process, prerequisites, and three methods for uploading files from servers.

## Features

You can upload multiple types of media files including video, audio, and image files from local application servers or over the Internet. The following features are provided:

-   Upload local audio or video files: By default, multipart upload is used. A single file to upload can be up to 48.8 TB in size. Resumable upload is supported.
-   Upload network audio or video files: After you specify the URL of a file, the system automatically downloads the file from the URL and uploads it. A single file to upload can be up to 5 GB in size.
-   Upload local images: After you specify the path of a local file, the system automatically uploads the file.
-   Upload network images: After you specify the URL of a file, the system automatically downloads the file from the URL and uploads it.
-   Upload progress bar: You can configure default and custom progress callbacks.
-   For other upload settings, see [Overview](/intl.en-US/Developer Guide/Upload Medias/Overview.md).

## Process

The following figure shows the process of uploading files from servers.

![Flowchart](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9887301161/p179962.png)

## Prerequisites

-   An Alibaba Cloud account is created on the [Create Your Alibaba Cloud Account](https://account.aliyun.com/register/register.htm?oauth_callback=https://vod.console.aliyun.com/&lang=zh) page, real-name verification is completed, and [ApsaraVideo VOD](https://www.aliyun.com/product/vod) is activated.
-   An AccessKey pair to access ApsaraVideo VOD is obtained. You can create an AccessKey pair for your Alibaba Cloud account on the [AccessKey Management](https://ak-console.aliyun.com/?spm=5176.doc57741.2.8.uLYY2M#/accesskey) page in the Alibaba Cloud Management Console. Alternatively, you can create a RAM user in the [RAM console](https://ram.console.aliyun.com/?spm=5176.doc57741.2.2.fQnI2T#/user/list) and grant the user the permission \(such as `AliyunVODFullAccess`\) to access ApsaraVideo VOD. For more information, see [Create and grant permissions to a RAM user](/intl.en-US/Developer Guide/Access authorization/Create and grant permissions to a RAM user.md).

## Upload methods

To upload media files from application servers, you can deploy upload scripts on the servers, use server upload SDKs or OSS SDKs, or call upload API operations.

## Use server upload SDKs

ApsaraVideo VOD provides server upload SDKs and demos of how to use them. Server upload SDKs encapsulate the logic to obtain upload URLs and credentials so that you do not need to obtain them separately. You need only to specify the AccessKey pair \(`AccessKeyId` and `AccessKeySecret`\) and the file URL to upload a file.

The following SDKs are provided:

-   [Java upload SDK](/intl.en-US/Upload SDK/Upload from servers/Upload SDK for Java.md)
-   [Python upload SDK](/intl.en-US/Upload SDK/Upload from servers/Upload SDK for Python.md)
-   [C/C++ upload SDK](/intl.en-US/Upload SDK/Upload from servers/Upload SDK for C or C++.md)
-   [PHP upload SDK](/intl.en-US/Upload SDK/Upload from servers/Upload SDK for PHP.md)

## Use OSS SDKs

ApsaraVideo VOD does not provide server upload SDKs for all programming languages. If the server upload SDK for a programming language is unavailable, you can use OSS SDKs. You can perform the following steps to upload files by using OSS SDKs:

1.  Access ApsaraVideo VOD and obtain the upload URL and credential. For more information, see [Upload URLs and credentials](/intl.en-US/Developer Guide/Upload Medias/Upload URLs and credentials.md).

    **Note:** Information about the media file and a media ID \(such as a video ID or an Image ID\) are returned in this step. Keep the media ID for subsequent operations such as video playback, management, and AI processing.

2.  Decode the upload URL \(UploadAddress\) and upload credential \(UploadAuth\) in Base64 to obtain the URL and credential for uploading the media file to OSS. For more information, see [Upload URLs and credentials](/intl.en-US/Developer Guide/Upload Medias/Upload URLs and credentials.md).
3.  Use an OSS SDK to upload the media file to the specified bucket. In this case, use the `STS Auth` method and use UploadAddress and UploadAuth for initialization. Do not use your AccessKey pair.

In addition to OSS SDKs for Java, Python, and PHP, the following OSS SDKs are provided:

-   OSS SDK for .NET: [Installation](/intl.en-US/SDK Reference/. NET/Installation.md).
-   OSS SDK for Go: [Installation](/intl.en-US/SDK Reference/Go/Installation.md).
-   OSS SDK for Ruby: [Installation](/intl.en-US/SDK Reference/Ruby/Installation.md).
-   OSS SDK for C: [Installation](/intl.en-US/SDK Reference/C/Installation.md).

For more information about OSS SDKs for major programming languages, see [Introduction](/intl.en-US/SDK Reference/Introduction.md). For more information about how to use OSS SDKs to upload media files, see [Upload videos by using the OSS native SDK](/intl.en-US/Best Practice/Upload videos by using the OSS native SDK.md).

## Call API operations \(not recommended\)

You can use ApsaraVideo VOD and OSS APIs to upload media files by following procedures similar to those used when OSS SDKs are used for uploads. The only difference is that in Step 3, you must use OSS API to complete the upload. For more information, see [Upload OSS objects](/intl.en-US/API Reference/Media upload/Upload OSS objects.md).


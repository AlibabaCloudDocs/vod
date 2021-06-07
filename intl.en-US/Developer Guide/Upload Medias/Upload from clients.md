# Upload from clients

You can upload media files from web pages, PCs, or mobile terminals that run an iOS or Android operating system to OSS buckets allocated by ApsaraVideo VOD. This method is suitable for background operations and scenarios where user generated content \(UGC\) and professionally generated content \(PGC\) are uploaded. This topic describes the process, prerequisites, and authorizations for uploading from clients, as well as the supported features and SDKs.

## Features

Client upload SDKs support the following upload features and settings:

-   Variety of media file types: You can upload multiple types of local media files, including video, audio, and image files.
-   Multiple file upload: You can upload multiple media files at a time. You can add files to or delete files from the file list, cancel or resume the upload, and list or clear the files.
-   Upload control: You can start, stop, pause, or resume the upload.
-   Resumable upload: Resumable upload is completed by upload SDKs. If a video fails to be uploaded due to any exceptions, the upload is resumed from where it is stopped.
-   Network switching: You can switch the network of your mobile terminal between 3G or 4G and Wi-Fi. To avoid wasting data in 3G or 4G networks, you can pause the upload when the network switches to 3G or 4G and resume the upload when the network switches back from 3G or 4G to Wi-Fi. Whether your mobile terminal uses a 3G or 4G network or Wi-Fi is determined by the terminal itself.
-   Additional settings: For information about other upload settings, see [Overview](/intl.en-US/Developer Guide/Upload Medias/Overview.md).

## Process

The following figure shows the process to upload from clients.

![Flowchart](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0857301161/p179942.png)

## Prerequisites

-   An Alibaba Cloud account is created on the [Create Your Alibaba Cloud Account](https://account.aliyun.com/register/register.htm?oauth_callback=https://vod.console.aliyun.com/&lang=zh) page, real-name verification is completed, and [ApsaraVideo VOD](https://www.aliyun.com/product/vod) is activated.
-   An AccessKey pair is obtained to access ApsaraVideo VOD. You can create an AccessKey pair for your Alibaba Cloud account on the [AccessKey Management](https://ak-console.aliyun.com/?spm=5176.doc57741.2.8.uLYY2M#/accesskey) page in the Alibaba Cloud Management Console. Alternatively, you can create a RAM user in the [RAM console](https://ram.console.aliyun.com/?spm=5176.doc57741.2.2.fQnI2T#/user/list) and grant the user the permission \(such as `AliyunVODFullAccess`\) to access ApsaraVideo VOD. For more information, see [Create and grant permissions to a RAM user](/intl.en-US/Developer Guide/Access authorization/Create and grant permissions to a RAM user.md).

## Authorizations

When medial files are uploaded from clients, the files are directly uploaded to OSS buckets allocated by ApsaraVideo VOD without passing through servers. Therefore, the clients must be authenticated. You must deploy the authorization service on the application servers.

Client upload SDKs support the following authorization methods:

-   [Use upload URLs and credentials](/intl.en-US/Upload SDK/Upload from clients/Use upload URLs and credentials to upload media files.md)
-   [Use STS](/intl.en-US/Upload SDK/Upload from clients/Use STS tokens to upload media files.md)

**Note:** **By default, ApsaraVideo VOD uses upload URLs and credentials for uploads.** This method is more advantageous over STS. For a comparison between the two methods, see [Comparison between credentials and STS](/intl.en-US/Developer Guide/Access authorization/Comparison between credentials and STS.md).

## Client upload SDKs

ApsaraVideo VOD provides three client upload SDKs. For more information, see the following topics:

-   Upload SDK for Android: [Upload files](/intl.en-US/Upload SDK/Upload from clients/Upload SDK for Android/Upload a file.md).
-   Upload SDK for iOS: [Upload files](/intl.en-US/Upload SDK/Upload from clients/Upload SDK for iOS/Upload a file.md).
-   Web upload SDK: [Use the upload SDK for JavaScript](/intl.en-US/Upload SDK/Upload from clients/Use the upload SDK for JavaScript.md).


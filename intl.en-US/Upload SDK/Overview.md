# Overview

This topic describes the features of the upload SDK. This topic also describes how to use the upload SDK.

The upload SDK is an important part of ApsaraVideo. It supports interactions between clients and Alibaba Cloud and is used to upload media files to ApsaraVideo VOD for storage. You can use the upload SDK to upload various media files in a fast and convenient manner, including video, audio, image, and subtitle files. ApsaraVideo VOD provides various types of upload SDKs, such as SDKs for servers, web clients, and mobile clients. The upload SDK fully adapts to all mainstream platforms and runtime environments.

## Preparations

-   Service activation
    -   An Alibaba Cloud account is created. Real-name verification is complete for the Alibaba Cloud account. For more information, see [Registration](https://account.aliyun.com/register/register.htm?oauth_callback=https%3A%2F%2Fvod.console.aliyun.com%2F&lang=zh) and [Real-name verification](https://help.aliyun.com/knowledge_list/37170.html).
    -   ApsaraVideo VOD is activated and configured. For more information, see the [ApsaraVideo VOD product page](https://www.aliyun.com/product/vod) and [t1959237.md\#](/intl.en-US/Quick Start/Get started with ApsaraVideo for VOD.md).
-   Account preparation

    An AccessKey pair is created to access ApsaraVideo VOD. For more information, see [Overview](/intl.en-US/Developer Guide/Access authorization/Overview.md).

    -   To upload media files from servers, we recommend that you use the AccessKey pair of a RAM user. You can create a RAM user in the Resource Access Management \(RAM\) console and grant the RAM user the permissions on ApsaraVideo VOD. For example, you can attach the `AliyunVODFullAccess` policy to the RAM user. For more information, see [Create and grant permissions to a RAM user](/intl.en-US/Developer Guide/Access authorization/Create and grant permissions to a RAM user.md).
    -   To upload media files from clients, you must first configure a RAM user. Then, use the AccessKey pair of the RAM user to call an operation for media upload to obtain the upload URL and credential. Deliver the upload URL and credential to the client and start the upload. For more information, see [Upload URLs and credentials](/intl.en-US/Developer Guide/Upload Medias/Upload URLs and credentials.md).
    **Warning:** To protect the AccessKey pair of your Alibaba Cloud account, we recommend that you use the AccessKey pair of a RAM user to perform operations.

-   Development environments

    -   Client upload SDKs allow you to upload media files from web pages, PCs, or mobile terminals that run an iOS or Android operating system.
    -   Server upload SDKs support multiple platforms and runtime environments, such as Linux, Windows, and macOS.
    **Note:** You must install the compiler or interpreter of your development language and configure the environment in advance.


## Upload from clients

When media files are uploaded from clients, the files are uploaded to Object Storage Service \(OSS\) buckets allocated by ApsaraVideo VOD without passing through servers. Therefore, the clients must be authenticated. You must deploy the authorization service on the AppServer. Client upload SDKs support the following authorization methods:

-   Use upload URLs and credentials to upload media files. We recommend that you use a server SDK to obtain upload URLs and credentials.
-   Use Security Token Service \(STS\) to upload media files. For more information, see [Create a role and grant temporary access permissions to the role by using STS](/intl.en-US/Developer Guide/Access authorization/Create a role and grant temporary access permissions to the role by using STS.md).

**Note:** STS requires complicated configurations. We recommend that you use upload URLs and credentials to upload media files. For more information about the differences between the two methods, see [Comparison between credentials and STS](/intl.en-US/Developer Guide/Access authorization/Comparison between credentials and STS.md).

ApsaraVideo VOD provides the following client upload SDKs:

-   [Upload SDK for Android](/intl.en-US/Upload SDK/Client upload/Android upload SDK/Multipart upload.md)
-   [Upload SDK for iOS](/intl.en-US/Upload SDK/Client upload/Upload SDK for iOS/Upload a file.md)
-   [Upload SDK for web](/intl.en-US/Upload SDK/Client upload/JavaScript upload SDK.md)

## Upload from servers

A server upload SDK encapsulates the underlying logic for obtaining and parsing upload URLs and credentials and uploading files to ApsaraVideo VOD for storage. You can upload a file only by deploying the server upload SDK on the AppServer and specifying the AccessKey pair and the path of the file. ApsaraVideo VOD provides the following server upload SDKs:

-   [Upload SDK for Java](/intl.en-US/Upload SDK/Upload from servers/Upload SDK for Java.md)
-   [Upload SDK for Python](/intl.en-US/Upload SDK/Upload from servers/Upload SDK for Python.md)
-   [Upload SDK for PHP](/intl.en-US/Upload SDK/Upload from servers/Upload SDK for PHP.md)
-   [Upload SDK for C or C++](/intl.en-US/Upload SDK/Upload from servers/Upload SDK for C or C++.md)

Upload SDKs for other programming languages, such as .NET, Node.js, and Go, will be available in the future.


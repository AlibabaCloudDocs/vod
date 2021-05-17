# Usage notes

ApsaraVideo VOD provides SDKs for multiple mainstream programming languages. You can use server SDKs to write code and call ApsaraVideo VOD operations.

## Features

-   The SDKs encapsulate the API request and response classes to spare you from the complex calculation of an API signature. For more information, see [Signature](/intl.en-US/API Reference/Calling methods/Signature method.md).
-   The SDKs support all ApsaraVideo VOD operations and provide relevant sample code. For more information, see [List of operations by function](/intl.en-US/API Reference/List of operations by function.md).
-   ApsaraVideo VOD supports SDKs for Java, Python, PHP, .NET, Node.js, C/C++, and Go.

**Note:** If new operations are published, Alibaba Cloud updates the SDKs in a timely manner. If the sample code for a new operation is unavailable, you can call the operation based on the sample code of existing operations.

## Prerequisites

-   Service activation
    -   An Alibaba Cloud account is created. To create an Alibaba Cloud account, visit the [account registration page](https://account.aliyun.com/register/register.htm?spm=a2c4g.11186623.2.27.215d276d3EY5iw&oauth_callback=https%3A%2F%2Fvod.console.aliyun.com%2F&lang=zh). Real-name verification is completed.
    -   ApsaraVideo VOD is activated and configured. For more information, see [ApsaraVideo VOD](https://www.aliyun.com/product/vod?spm=a2c4g.11186623.2.29.215d276d3EY5iw) and [Quick Start](/intl.en-US/Quick Start/Get started with ApsaraVideo VOD.md).
-   Account preparation

    An AccessKey pair is created to access ApsaraVideo VOD. You can access ApsaraVideo VOD by using an Alibaba Cloud account, a Resource Access Management \(RAM\) user, or a Security Token Service \(STS\) token. For more information, see [Accounts and authorization](/intl.en-US/Developer Guide/Access authorization/Overview.md).

    -   By using an Alibaba Cloud account: You can create the AccessKey pair of your Alibaba Cloud account in the [User Management console](https://usercenter.console.aliyun.com/#/manage/ak).

        **Note:** An Alibaba Cloud account has the most permissions. If the AccessKey pair is leaked, damages may occur. We recommend that you do not use an Alibaba Cloud account.

    -   By using a RAM user: You must create a RAM user in the [RAM console](https://ram.console.aliyun.com/?spm=a2c4g.11186623.2.33.215d276dGgGSSY#/user/list) and grant the user the permissions on ApsaraVideo VOD, such as `AliyunVODFullAccess`. For more information, see [Create and grant permissions to a RAM user](/intl.en-US/Developer Guide/Access authorization/Create and grant permissions to a RAM user.md).

        **Note:** To ensure account security, we recommend that you use a RAM user to access ApsaraVideo VOD.

    -   By using an STS token: You can access ApsaraVideo VOD by using an STS token. For more information, see [Create a role and grant temporary access permissions to the role by using STS](/intl.en-US/Developer Guide/Access authorization/Create a role and grant temporary access permissions to the role by using STS.md).

## Development environments

Server SDKs support multiple platforms and runtime environments such as Linux, Windows, and macOS. We recommend that you install the compiler or interpreter of the relevant programming language and set up the environment in advance. For more information about version requirements, see the "Installation" topic of the SDK for each programming language.

**Note:** Windows will be supported by SDK for C/C++ in the future.

## SDK installation

-   Versions

    The latest version of a server SDK is `2.15.11`. For more information about the release notes, see [Release notes of server operation SDKs](/intl.en-US/SDK Downloads/Release notes of server operation SDKs.md). Make sure that the latest version is installed. Otherwise, you may fail to call some API operations.

    -   SDKs for Java, Python, PHP, .NET, and Go use the specific request and response classes for each API operation. You must update the SDKs for new API operations or features.
    -   SDKs for Node.js and C/C++ use general libraries and do not encapsulate the API request and response classes. You do not need to update the SDKs for new API operations but must update general libraries as required.
-   Installation

    In most cases, you must install both the SDK core library and ApsaraVideo VOD library. The following table lists the instructions of the SDKs for various programming languages.

    |Alibaba Cloud SDK|ApsaraVideo VOD SDK|Installation|Initialization|
    |-----------------|-------------------|------------|--------------|
    |[Alibaba Cloud SDK for Java](https://open.aliyun.com/sdk?language=java&product=sdkcore)|[Alibaba Cloud VOD SDK for Java](https://open.aliyun.com/sdk?language=java&product=vod)|[Install SDK for Java](/intl.en-US/Server SDK Reference/SDK for Java/Installation.md)|[Initialize SDK for Java](/intl.en-US/Server SDK Reference/SDK for Java/Initialization.md)|
    |[Alibaba Cloud SDK for Python](https://open.aliyun.com/sdk?language=python&product=sdkcore)|[Alibaba Cloud VOD SDK for Python](https://open.aliyun.com/sdk?language=python&product=vod)|[Install SDK for Python](/intl.en-US/Server SDK Reference/Python SDK/Installation.md)|[Initialize SDK for Python](/intl.en-US/Server SDK Reference/Python SDK/Initialization.md)|
    |[Alibaba Cloud SDK for PHP](https://open.aliyun.com/sdk?language=php&product=sdkcore)|[Alibaba Cloud VOD SDK for PHP](https://open.aliyun.com/sdk?language=php&product=vod)|[Install SDK for PHP](/intl.en-US/Server SDK Reference/PHP SDK/Install the SDK/Installation.md)|[Initialize SDK for PHP](/intl.en-US/Server SDK Reference/PHP SDK/Install the SDK/Initialization.md)|
    |[Alibaba Cloud SDK for .NET](https://open.aliyun.com/sdk?language=php&product=sdkcore)|[Alibaba Cloud VOD SDK for .NET](https://open.aliyun.com/sdk?language=net&product=vod)|[Install SDK for .NET](/intl.en-US/Server SDK Reference/.NET SDK/Installation.md)|[Initialize SDK for .NTE](/intl.en-US/Server SDK Reference/.NET SDK/Initialization.md)|
    |[Alibaba Cloud SDK for Node.js](https://open.aliyun.com/sdk?language=nodejs&product=sdkcore)|[Alibaba Cloud VOD SDK for Node.js](https://open.aliyun.com/sdk?language=nodejs&product=vod)|[Install SDK for Node.js](/intl.en-US/Server SDK Reference/Node.js SDK/Installation.md)|[Initialize SDK for Node.js](/intl.en-US/Server SDK Reference/Node.js SDK/Initialization.md)|
    |[Alibaba Cloud SDK for Go](https://open.aliyun.com/sdk?language=go&product=sdkcore)|[Alibaba Cloud VOD SDK for Go](https://open.aliyun.com/sdk?language=go&product=vod)|[Install SDK for Go](/intl.en-US/Server SDK Reference/Go SDK/Installation.md)|[Initialize SDK for Go](/intl.en-US/Server SDK Reference/Go SDK/Initialization.md)|
    |[Alibaba Cloud SDK for C/C++](https://open.aliyun.com/sdk?language=cpp&product=sdkcore)|[Alibaba Cloud VOD SDK for C/C++](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/101254/cn_zh/1545981303612/aliyun-c-sdk-vod.tar.gz?file=aliyun-c-sdk-vod.tar.gz)|[Install SDK for C/C++](/intl.en-US/Server SDK Reference/C/C++ SDK/Installation.md)|[Initialize SDK for C/C++](/intl.en-US/Server SDK Reference/C/C++ SDK/Initialization.md)|

-   Description

    After you install an SDK, initialize the client of the SDK. For more information, see the description of AccessKey pair-based client initialization in the "Initialization" topic of the SDK for each programming language.


## Endpoints

You can access ApsaraVideo VOD in many regions around the world. For more information, see [VOD centers and endpoints](/intl.en-US/Developer Guide/VOD centers and endpoints.md). You can use a region in the `API region` column of the table to initialize a client. The `API region ID` column of the table indicates the value of RegionId for the required API operation or SDK. For example, enter `cn-shanghai` for the China \(Shanghai\) region and `ap-southeast-1` for the Singapore \(Singapore\) region.

**Note:** An access region is different from a storage region. The former indicates the region where you can call ApsaraVideo VOD operations. The latter indicates a region where you can store media files in Object Storage Service \(OSS\). For example, you can enter cn-shanghai as an access region and cn-beijing as a storage region.

## Limits

By default, ApsaraVideo VOD limits the resource usage and the number of API calls. For more information, see [Limits on usage](/intl.en-US/Introduction/Limits.md). To increase the limits, you can contact after-sales technical support or submit a ticket to contact us. In the meantime, you must describe your scenarios and expected thresholds, such as the number of domain names and the frequency of playback operation calls.

## SDK calls

SDKs for different programming languages provide complete API call examples. For more information, see the related modules, such as media upload and video playback, for the SDK for each programming language.

## Common errors

You can troubleshoot errors occurred during the use of the SDKs based on error codes. For more information, see the following common errors in different programming languages:

-   [Common errors in SDK for Java]()
-   [Common errors in SDK for Python]()
-   [Common errors in SDK for Go]()
-   [Common errors in SDK for .NET]()

Common errors are similar for SDKs in various programming languages. Most troubleshooting solutions are applicable to these programming languages. For example, you can apply the solution that is used to troubleshoot the `InvalidAccessKeyId.NotFound` error in the preceding languages to the same error in SDK for PHP.

## Feedback

If you have any questions while you use the SDKs, you can seek help from [Yunqi Community](https://yq.aliyun.com/tags/type_ask-tagid_23350?spm=a2c4g.11186623.2.71.215d276dR8JY7Z).


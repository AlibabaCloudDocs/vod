# Initialization

This topic describes how to initialize ApsaraVideo VOD SDK for .NET by using an AccessKey pair and how to fix errors that occur during the calls of ApsaraVideo VOD operations.

## Prerequisites

-   An Alibaba Cloud account is created. To create an Alibaba Cloud account, visit the [account registration page](https://account.aliyun.com/register/register.htm?spm=a2c4g.11186623.2.13.2a123bd95a5EuV&oauth_callback=https%3A%2F%2Fvod.console.aliyun.com%2F&lang=zh). [Real-name verification](https://account.console.aliyun.com/v2/?spm=5176.2020520207.103.3.6e0f4c126cK3zB#/authc/types) is completed. [ApsaraVideo VOD](https://www.alibabacloud.com/product/apsaravideo-for-vod?spm=a3c0i.7911826.6791778070.dnavproductmedia3.441914b3psWeWQ) is activated.
-   An AccessKey pair is created to call ApsaraVideo VOD operations. You can create the AccessKey pair of your Alibaba Cloud account in the [User Management console](https://usercenter.console.aliyun.com/#/manage/ak). Alternatively, you can create a RAM user in the [RAM console](https://ram.console.aliyun.com/?spm=a2c4g.11186623.2.17.2a123bd95a5EuV#/user/list) and grant the RAM user the permissions on ApsaraVideo VOD. For more information, see [t1959300.md\#](/intl.en-US/Developer Guide/Access authorization/RAM user access.md).

## Initialize the SDK

Determine the region where you want to call ApsaraVideo VOD operations. For more information about the supported regions, see [Access regions and IDs](/intl.en-US/Developer Guide/VOD centers and access domains.md). For example, if you want to call the operations in the China \(Shanghai\) region, use `cn-shanghai`. In the following example, the [AccessKey pair](/intl.en-US/Developer Guide/Access authorization/RAM user access.md) is used to initialize the SDK. Example:

```
using Aliyun.Acs.Core;
using Aliyun.Acs.Core.Profile;

public static DefaultAcsClient InitVodClient(string accessKeyId, string accessKeySecret)
{
    // The region where you want to call ApsaraVideo VOD operations.
    string regionId = "cn-shanghai";
    IClientProfile profile = DefaultProfile.GetProfile(regionId, accessKeyId, accessKeySecret);
    // DefaultProfile.AddEndpoint(regionId, regionId, "vod", "vod." + regionId + ".aliyuncs.com");
    return new DefaultAcsClient(profile);
}
```

## Usage notes

Even if you call ApsaraVideo VOD operations from a region that is included in supported access regions and IDs, the system may return the error message `SDK.InvalidRegionId, Can not find endpoint to access.` due to SDK compatibility issues. For more information, see [Access regions and IDs](/intl.en-US/Developer Guide/VOD centers and access domains.md). To fix this error, invoke the `AddEndpoint` method that has been commented out in **InitVodClient** in the preceding example. The following figure shows an example.

![Usage notes](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8625479061/p208603.png)


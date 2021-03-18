# Initialization

This topic describes how to initialize ApsaraVideo VOD SDK for Node.js by using an AccessKey pair or a Security Token Service \(STS\) token.

## Prerequisites

-   An Alibaba Cloud account is created. To create an Alibaba Cloud account, visit the [account registration page](https://account.aliyun.com/register/register.htm?spm=a2c4g.11186623.2.13.2a123bd95a5EuV&oauth_callback=https%3A%2F%2Fvod.console.aliyun.com%2F&lang=zh). [Real-name verification](https://account.console.aliyun.com/v2/?spm=5176.2020520207.103.3.6e0f4c126cK3zB#/authc/types) is completed. [ApsaraVideo VOD](https://www.alibabacloud.com/product/apsaravideo-for-vod?spm=a3c0i.7911826.6791778070.dnavproductmedia3.441914b3psWeWQ) is activated.
-   An AccessKey pair is created to call ApsaraVideo VOD operations. You can create the AccessKey pair of your Alibaba Cloud account in the [User Management console](https://usercenter.console.aliyun.com/#/manage/ak). Alternatively, you can create a RAM user in the [RAM console](https://ram.console.aliyun.com/?spm=a2c4g.11186623.2.17.2a123bd95a5EuV#/user/list) and grant the RAM user the permissions on ApsaraVideo VOD. For more information, see [Create and grant permissions to a RAM user](/intl.en-US/Developer Guide/Access authorization/Create and grant permissions to a RAM user.md).

## Initialize the SDK

Determine the region where you want to call ApsaraVideo VOD operations. For more information about the supported regions, see [Access regions and IDs](/intl.en-US/Developer Guide/VOD centers and endpoints.md). For example, if you want to call the operations in the China \(Shanghai\) region, use `cn-shanghai`.

-   Use the [AccessKey pair](/intl.en-US/Developer Guide/Access authorization/Create and grant permissions to a RAM user.md) to initialize the SDK. Example:

    ```
    var RPCClient = require('@alicloud/pop-core').RPCClient;
    
    function initVodClient(accessKeyId, accessKeySecret,) {
        var regionId = 'cn-shanghai';   // The region where you want to call ApsaraVideo VOD operations.
        var client = new RPCClient({
            accessKeyId: accessKeyId,
            accessKeySecret: accessKeySecret,
            endpoint: 'http://vod.' + regionId + '.aliyuncs.com',
            apiVersion: '2017-03-21'
        });
    
        return client;
    }
    ```

-   Use an [STS token](/intl.en-US/Developer Guide/Access authorization/Create a role and grant temporary access permissions to the role by using STS.md) to initialize the SDK. Example:

    ```
    var RPCClient = require('@alicloud/pop-core').RPCClient;
    
    function initVodClient(accessKeyId, accessKeySecret, securityToken) {
        var regionId = 'cn-shanghai';   // The region where you want to call ApsaraVideo VOD operations.
        var client = new RPCClient({
            accessKeyId: accessKeyId,
            accessKeySecret: accessKeySecret,
            securityToken: securityToken,
            endpoint: 'http://vod.' + regionId + '.aliyuncs.com',
            apiVersion: '2017-03-21'
        });
    
        return client;
    }
    ```



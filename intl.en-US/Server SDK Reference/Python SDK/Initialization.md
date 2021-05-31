# Initialization

This topic describes how to initialize ApsaraVideo VOD SDK for Python by using an AccessKey pair or a Security Token Service \(STS\) token.

## Prerequisites

-   An Alibaba Cloud account is created. To create an Alibaba Cloud account, visit the [account registration page](https://account.aliyun.com/register/register.htm?spm=a2c4g.11186623.2.13.2a123bd95a5EuV&oauth_callback=https%3A%2F%2Fvod.console.aliyun.com%2F&lang=zh). Real-name verification is completed. [ApsaraVideo VOD](/intl.en-US/Quick Start/Get started with ApsaraVideo VOD.md) is activated.
-   An AccessKey pair is created to call ApsaraVideo VOD operations. You can create the AccessKey pair of your Alibaba Cloud account in the [Access Key management](https://usercenter.console.aliyun.com/#/manage/ak). Alternatively, you can create a RAM user in the [RAM console](https://ram.console.aliyun.com/?spm=a2c4g.11186623.2.17.2a123bd95a5EuV#/user/list) and grant the RAM user the permissions on ApsaraVideo VOD. For more information, see [Create and grant permissions to a RAM user](/intl.en-US/Developer Guide/Access authorization/Create and grant permissions to a RAM user.md).

## Initialization

Determine the region where you want to call ApsaraVideo VOD operations. For more information about the supported regions, see [Access regions and IDs](/intl.en-US/Developer Guide/VOD centers and endpoints.md). For example, if you want to call the operations in the China \(Shanghai\) region, use `cn-shanghai`.

1.  Use the [AccessKey pair](/intl.en-US/Developer Guide/Access authorization/Create and grant permissions to a RAM user.md) to initialize the SDK. Example:

    ```
    # -*- coding: UTF-8 -*-
    import json
    import traceback
    from aliyunsdkcore.client import AcsClient
    
    def init_vod_client(accessKeyId, accessKeySecret):
        regionId = 'cn-shanghai'   # The region where you want to call ApsaraVideo VOD operations.
        connectTimeout = 3 # Connection timeout in seconds.
        return AcsClient(accessKeyId, accessKeySecret, regionId, auto_retry=True, max_retry_time=3, timeout=connectTimeout)
    ```

2.  Use an [STS token](/intl.en-US/Developer Guide/Access authorization/Create a role and grant temporary access permissions to the role by using STS.md) to initialize the SDK. Example:

    ```
    # -*- coding: UTF-8 -*-
    import json
    import traceback
    from aliyunsdkcore.client import AcsClient
    from aliyunsdkcore.auth.credentials import StsTokenCredential
    
    def init_vod_client(accessKeyId, accessKeySecret, securityToken):
        regionId = 'cn-shanghai'   # The region where you want to call ApsaraVideo VOD operations.
        connectTimeout = 3 # Connection timeout in seconds.
        credential = StsTokenCredential(accessKeyId, accessKeySecret, securityToken)
        return AcsClient(region_id=regionId, auto_retry=True, max_retry_time=3, timeout=connectTimeout, credential=credential)
    ```



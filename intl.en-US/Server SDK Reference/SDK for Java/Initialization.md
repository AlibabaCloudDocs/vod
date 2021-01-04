# Initialization

This topic describes how to initialize ApsaraVideo VOD SDK for Java by using an AccessKey pair or a Security Token Service \(STS\) token.

## Prerequisites

-   An Alibaba Cloud account is created. To create an Alibaba Cloud account, visit the [account registration page](https://account.aliyun.com/register/register.htm?spm=a2c4g.11186623.2.13.2a123bd95a5EuV&oauth_callback=https%3A%2F%2Fvod.console.aliyun.com%2F&lang=zh). [Real-name verification](https://account.console.aliyun.com/v2/?spm=5176.2020520207.103.3.6e0f4c126cK3zB#/authc/types) is completed. [ApsaraVideo VOD](https://www.alibabacloud.com/product/apsaravideo-for-vod?spm=a3c0i.7911826.6791778070.dnavproductmedia3.441914b3psWeWQ) is activated.
-   An AccessKey pair is created to call ApsaraVideo VOD operations. You can create the AccessKey pair of your Alibaba Cloud account in the [User Management console](https://usercenter.console.aliyun.com/#/manage/ak). Alternatively, you can create a RAM user in the [RAM console](https://ram.console.aliyun.com/?spm=a2c4g.11186623.2.17.2a123bd95a5EuV#/user/list) and grant the RAM user the permissions on ApsaraVideo VOD. For more information, see [t1959300.md\#](/intl.en-US/Developer Guide/Access authorization/RAM user access.md).

## Initialize the SDK

Determine the region where you want to call ApsaraVideo VOD operations. For more information about the supported regions, see [Access regions and IDs](/intl.en-US/Developer Guide/VOD centers and access domains.md). For example, if you want to call the operations in the China \(Shanghai\) region, use `cn-shanghai`.

-   Use the [AccessKey pair](/intl.en-US/Developer Guide/Access authorization/RAM user access.md) to initialize the SDK.

    ```
    import com.aliyuncs.profile.DefaultProfile;
    import com.aliyuncs.DefaultAcsClient;
    import com.aliyuncs.exceptions.ClientException;
    
    public static DefaultAcsClient initVodClient(String accessKeyId, String accessKeySecret) throws ClientException {
        String regionId = "cn-shanghai";  // The region where you want to call ApsaraVideo VOD operations.
        DefaultProfile profile = DefaultProfile.getProfile(regionId, accessKeyId, accessKeySecret);
        DefaultAcsClient client = new DefaultAcsClient(profile);
        return client;
    }
    ```

-   Use an [STS token](/intl.en-US/Developer Guide/Access authorization/STS authorization.md) to initialize the SDK.

    ```
    import com.aliyuncs.profile.DefaultProfile;
    import com.aliyuncs.DefaultAcsClient;
    import com.aliyuncs.exceptions.ClientException;
    
    public static DefaultAcsClient initVodClient(String accessKeyId, String accessKeySecret, String securityToken) throws ClientException {
        String regionId = "cn-shanghai";  // The region where you want to call ApsaraVideo VOD operations.
        DefaultProfile profile = DefaultProfile.getProfile(regionId, accessKeyId, accessKeySecret, securityToken);
        DefaultAcsClient client = new DefaultAcsClient(profile);
        return client;
    }
    ```



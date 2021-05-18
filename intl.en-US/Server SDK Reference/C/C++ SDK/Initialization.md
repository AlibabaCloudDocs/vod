# Initialization

This topic provides code examples on how to initialize the SDK for C/C++ by using your AccessKey pair and Security Token Service \(STS\) token.

## Prerequisites

-   An Alibaba Cloud account is created. To create an Alibaba Cloud account, visit the [account registration page](https://account.aliyun.com/register/register.htm?spm=a2c4g.11186623.2.13.2a123bd95a5EuV&oauth_callback=https%3A%2F%2Fvod.console.aliyun.com%2F&lang=zh). Real-name verification is completed. [ApsaraVideo VOD](https://www.alibabacloud.com/product/apsaravideo-for-vod?spm=a3c0i.7911826.6791778070.dnavproductmedia3.441914b3psWeWQ) is activated.
-   An AccessKey pair is created to call ApsaraVideo VOD operations. You can create the AccessKey pair of your Alibaba Cloud account in the [User Management console](https://usercenter.console.aliyun.com/#/manage/ak). Alternatively, you can create a RAM user in the [RAM console](https://ram.console.aliyun.com/?spm=a2c4g.11186623.2.17.2a123bd95a5EuV#/user/list) and grant the RAM user the permissions on ApsaraVideo VOD. For more information, see [Create and grant permissions to a RAM user](/intl.en-US/Developer Guide/Access authorization/Create and grant permissions to a RAM user.md).

## Initialize the SDK

Determine the region where you want to call ApsaraVideo VOD operations. For more information about the supported regions, see [Access regions and IDs](/intl.en-US/Developer Guide/VOD centers and endpoints.md). For example, if you want to call the operations in the China \(Shanghai\) region, use `cn-shanghai`.

1.  Use the [AccessKey pair](/intl.en-US/Developer Guide/Access authorization/Create and grant permissions to a RAM user.md) to initialize the SDK. Example:

    ```
    #include "vod_sdk/openApiUtil.h"
    
    VodCredential initVodClient(std::string accessKeyId, std::string accessKeySecret) {
        VodCredential authInfo;
        authInfo.accessKeyId = accessKeyId;
        authInfo.accessKeySecret = accessKeySecret;
        authInfo.regionId = "cn-shanghai";
        return authInfo;
    }
    ```

2.  Use an [STS token](/intl.en-US/Developer Guide/Access authorization/Create a role and grant temporary access permissions to the role by using STS.md) to initialize the SDK. Example:

    ```
    #include "vod_sdk/openApiUtil.h"
    
    VodCredential initVodClient(std::string accessKeyId, std::string accessKeySecret, std::String securityToken) {
        VodCredential authInfo;
        authInfo.accessKeyId = accessKeyId;
        authInfo.accessKeySecret = accessKeySecret;
        authInfo.securityToken = securityToken;
        authInfo.regionId = "cn-shanghai";
        return authInfo;
    }
    ```


## FAQ

-   The dynamic link library \(DLL\) is not installed in the directory where the DLL is complied or the directory where the DLL is run. What do I do?

    Perform the following operations. Example:

    ```
    Add the directory where the DLL is installed to the /etc/ld.so.conf file.
    Run the ldconfig command.        
    ```

    You must add the following parameters when you compile the DLL:

    ```
    lcurl
    ljsoncpp
    lvod_sdk
    loss_c_sdk
    lapr-1
    laprutil-1
    lmxml
    ```

-   Which input parameters does the getAcsResponse function support?

    The getAcsResponse function is a request function. The following parameters are supported:

    -   vodCredential: For more information, see [Initialize the SDK](#section_14q_iza_ceo).
    -   apiName: The name of the API operation.
    -   args: The parameters.
-   Which function returns a value of the VodApiResponse type?

    The getAcsResponse function returns the value of the VodApiResponse type.

    -   If the request succeeds, the value of httpCode in VodApiResponse is an HTTP status code and the value of result is in the JSON format. You can configure the args parameter to specify the data types of return results.
    -   If the request fails, the value of httpCode in VodApiResponse is -1 and the value of result is an error message.


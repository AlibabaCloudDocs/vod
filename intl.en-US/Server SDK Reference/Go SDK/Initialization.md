# Initialization

This topic describes how to initialize ApsaraVideo VOD SDK for Go by using an AccessKey pair or a Security Token Service \(STS\) token.

## Prerequisites

-   An Alibaba Cloud account is created. To create an Alibaba Cloud account, visit the [account registration page](https://account.aliyun.com/register/register.htm?spm=a2c4g.11186623.2.13.2a123bd95a5EuV&oauth_callback=https%3A%2F%2Fvod.console.aliyun.com%2F&lang=zh). [Real-name verification](https://account.console.aliyun.com/v2/?spm=5176.2020520207.103.3.6e0f4c126cK3zB#/authc/types) is completed. [ApsaraVideo VOD](https://www.alibabacloud.com/product/apsaravideo-for-vod?spm=a3c0i.7911826.6791778070.dnavproductmedia3.441914b3psWeWQ) is activated.
-   An AccessKey pair is created to call ApsaraVideo VOD operations. You can create the AccessKey pair of your Alibaba Cloud account in the [User Management console](https://usercenter.console.aliyun.com/#/manage/ak). Alternatively, you can create a RAM user in the [RAM console](https://ram.console.aliyun.com/?spm=a2c4g.11186623.2.17.2a123bd95a5EuV#/user/list) and grant the RAM user the permissions on ApsaraVideo VOD. For more information, see [Create and grant permissions to a RAM user](/intl.en-US/Developer Guide/Access authorization/Create and grant permissions to a RAM user.md).

## Initialize the SDK

Determine the region where you want to call ApsaraVideo VOD operations. For more information about the supported regions, see [Access regions and IDs](/intl.en-US/Developer Guide/VOD centers and endpoints.md). For example, if you want to call the operations in the China \(Shanghai\) region, use `cn-shanghai`.

-   Use the [AccessKey pair](/intl.en-US/Developer Guide/Access authorization/Create and grant permissions to a RAM user.md) to initialize the SDK. Example:

    ```
    package main
    
    import (
        "github.com/aliyun/alibaba-cloud-sdk-go/sdk"
        "github.com/aliyun/alibaba-cloud-sdk-go/services/vod"
        "github.com/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func InitVodClient(accessKeyId  string, accessKeySecret string) (client *vod.Client, err error) {
    
        // The region where you want to call ApsaraVideo VOD operations.
        regionId := "cn-shanghai"
    
        // Create an object for authentication.
        credential := &credentials.AccessKeyCredential{
            accessKeyId,
            accessKeySecret,
        }
    
        // The custom configuration parameters.
        config := sdk.NewConfig()
        config.AutoRetry = true      // Specifies whether to automatically reconnect to the network if a connection fails.
        config.MaxRetryTime = 3      // The maximum number of retry attempts.
        config.Timeout = 3000000000 // The timeout period of connections, in nanoseconds. The default value is 3000000000, which indicates 3 seconds.
    
        // Create a vodClient instance.
        return vod.NewClientWithOptions(regionId, config, credential)
    }
    ```

-   Use an [STS token](/intl.en-US/Developer Guide/Access authorization/Create a role and grant temporary access permissions to the role by using STS.md) to initialize the SDK. Example:

    ```
    package main
    
    import (
        "github.com/aliyun/alibaba-cloud-sdk-go/sdk"
        "github.com/aliyun/alibaba-cloud-sdk-go/services/vod"
        "github.com/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func InitVodClient(accessKeyId  string, accessKeySecret string, securityToken string) (client *vod.Client, err error) {
    
        // The region where you want to call ApsaraVideo VOD operations.
        regionId := "cn-shanghai"
    
        // Create an object for authentication.
        credential := &credentials.StsTokenCredential{
            accessKeyId,
            accessKeySecret,
            securityToken,
        }
    
        // The configurations of the network connection.
        config := sdk.NewConfig()
        config.AutoRetry = true      // Specifies whether to automatically reconnect to the network if a connection fails.
        config.MaxRetryTime = 3      // The maximum number of retry attempts.
        config.Timeout = 3000000000 // The timeout period of connections, in nanoseconds. The default value is 3000000000, which indicates 3 seconds.
    
        // Create a vodClient instance.
        return vod.NewClientWithOptions(regionId, config, credential)
    }
    ```


## Usage notes

You must call `vod.Create${apiName}Request` to create an API request. `${apiName}` indicates the ApsaraVideo VOD operation that you want to call. For more information about ApsaraVideo VOD operations, see [List of operations by function](/intl.en-US/API Reference/List of operations by function.md).

## Call example

The [GetPlayInfo](/intl.en-US/API Reference/Audio and video playback/GetPlayInfo.md) API operation is used in this example. You can call this operation to query a playback URL. Example:

```
func MyGetPlayInfo(client *vod.Client, videoId string) (response *vod.GetPlayInfoResponse, err error) {
    // Call vod.Create${apiName}Request to create an API request and configure the parameters.
    request := vod.CreateGetPlayInfoRequest()
    request.VideoId = videoId
    request.AcceptFormat = "JSON"

    // Call client.${apiName}(request) to send an API request and handle the exceptions.
    return client.GetPlayInfo(request)
}

func main() {
    client, err := InitVodClient("<AccessKeyId>", "<AccessKeySecret>")
    if err ! = nil {
        // Handle the exceptions.
        panic(err)
    }

    response, err := MyGetPlayInfo(client, "<videoId>")
    if err ! = nil {
        // Handle the exceptions.
        panic(err)
    }

    // fmt.Println(response)
    playList := response.PlayInfoList.PlayInfo
    for _, playInfo := range playList {
        // List the definition and playback URL.
        fmt.Printf("%s: %s\n", playInfo.Definition, playInfo.PlayURL)
    }
}
```

**Note:**

-   For more information, see [Use Alibaba Cloud SDK for Go](https://help.aliyun.com/document_detail/66217.html?spm=a2c4g.11186623.2.27.3c9b25dfToJUtM#concept-mkk-vpj-zdb).
-   The API operations that are encapsulated in ApsaraVideo VOD SDK for Go support concurrent and generic calls.
-   You can download the sample code at [test\_vod.go](https://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/87264/cn_zh/1533550966288/test_vod.go).


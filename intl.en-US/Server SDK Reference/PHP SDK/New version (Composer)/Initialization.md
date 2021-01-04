# Initialization

You can use Composer to install Alibaba Cloud SDK for PHP of the new version. Alibaba Cloud SDK for PHP of the new version is different from that of the old version in terms of installation, initialization, and use. For more information about how to initialize and use Alibaba Cloud SDK for PHP of the new version, see the installation instructions and the following sections.

## Initialize the SDK

Determine the region where you want to call ApsaraVideo VOD operations. For more information about the supported regions, see [Access regions and IDs](/intl.en-US/Developer Guide/VOD centers and access domains.md). For example, if you want to call the operations in the China \(Shanghai\) region, use `cn-shanghai`.

-   Use the [AccessKey pair](/intl.en-US/Developer Guide/Access authorization/RAM user access.md) to initialize the SDK. Example:

    ```
    <? php
    require __DIR__ . '/vendor/autoload.php';
    
    <? php
    require __DIR__ . '/vendor/autoload.php';
    use AlibabaCloud\Client\AlibabaCloud;
    use AlibabaCloud\Client\Exception\ClientException;
    use AlibabaCloud\Client\Exception\ServerException;
    use AlibabaCloud\Vod\Vod;
    
    define(VOD_CLIENT_NAME, 'AliyunVodClientDemo');
    
    function initVodClient($accessKeyId, $accessKeySecret) {
        $regionId = 'cn-shanghai';
        AlibabaCloud::accessKeyClient($accessKeyId, $accessKeySecret)
                    ->regionId($regionId)
                    ->connectTimeout(1)
                    ->timeout(3)
                    ->name(VOD_CLIENT_NAME);
    }
    ```

-   Use an [STS token](/intl.en-US/Developer Guide/Access authorization/STS authorization.md) to initialize the SDK. Example:

    ```
    <? php
    require __DIR__ . '/vendor/autoload.php';
    use AlibabaCloud\Client\AlibabaCloud;
    use AlibabaCloud\Client\Exception\ClientException;
    use AlibabaCloud\Client\Exception\ServerException;
    use AlibabaCloud\Vod\Vod;
    
    define(VOD_CLIENT_NAME, 'AliyunVodClientDemo');
    
    function initVodClient($accessKeyId, $accessKeySecret, $securityToken) {
        $regionId = 'cn-shanghai';
        AlibabaCloud::stsClient($accessKeyId, $accessKeySecret, $securityToken)
            ->regionId($regionId)
            ->connectTimeout(1)
            ->timeout(3)
            ->name(VOD_CLIENT_NAME);
    }
    ```


## Use the SDK

You must call `Vod::v20170321()->${apiName}` to create an API request. `${apiName}` indicates the ApsaraVideo VOD operation that you want to call. The first letter of the operation name must be in lower case. For details about API operations that you can call, see [API overview](/intl.en-US/API Reference/API overview.md).

## Call example

The following code shows how to call the [GetPlayInfo](/intl.en-US/API Reference/Video playback/GetPlayInfo.md) operation. Example:

```
function getPlayInfo($videoId) {
    return Vod::v20170321()->getPlayInfo()->client(VOD_CLIENT_NAME)
              ->withVideoId($videoId)    // Specify the parameters for the API operation.
              ->withAuthTimeout(3600*24)
              ->format('JSON')  // Specify the response format.
              ->request();      // Execute the request.
}

try {
    initVodClient('<AccessKeyId>', '<AccessKeySecret>');
    $playInfo = getPlayInfo('<videoId>');
    print_r($playInfo->PlayInfoList->PlayInfo);
} catch (Exception $e) {
    print $e->getMessage()."\n";
}
```


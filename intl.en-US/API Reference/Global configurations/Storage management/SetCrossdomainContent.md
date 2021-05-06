# SetCrossdomainContent

Updates the cross-domain policy file crossdomain.xml.

**Note:** After you use the cross-domain policy file to update the resources on the origin server, you must refresh the resources that are cached on Alibaba Cloud CDN nodes. You can use the ApsaraVideo VOD console to refresh resources. For more information, see [Refresh and prefetch](~~86098~~). Alternatively, you can call the [RefreshVodObjectCaches](~~69215~~) operation to refresh resources.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=SetCrossdomainContent&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SetCrossdomainContent|The operation that you want to perform. Set the value to **SetCrossdomainContent**. |
|Content|String|Yes|<cross-domain-policy\><allow-access-from domain="\*"/\><allow-http-request-headers-from domain="\*" headers="\*" secure="false"/\></cross-domain-policy\>|The content of the cross-domain policy file. The file must be in the XML format and can contain up to 2,048 characters. |
|StorageLocation|String|Yes|outin-67870fd5b\*\*\*\*1e98a3900163e1c35d5.oss-cn-shanghai.aliyuncs.com|The URL of the Object Storage Service \(OSS\) bucket. |
|ResourceRealOwnerId|String|No|3461111|The ID of the resource owner. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|25818875-5F78-4A13-\*\*\*\*-D7393642CA58|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/?Action=SetCrossdomainContent
&Content=<cross-domain-policy><allow-access-from domain="***"/><allow-http-request-headers-from domain="***" headers="*" secure="false"/></cross-domain-policy>
&StorageLocation=outin-67870fd5b****1e98a3900163e1c35d5.oss-cn-shanghai.aliyuncs.com
&<Common request parameters>
```

Sample success responses

`XML` format

```
<SetCrossdomainContentResponse>
      <RequestId>25818875-5F78-4A13-****-D7393642CA58</RequestId>
</SetCrossdomainContentResponse>
```

`JSON` format

```
{
    "RequestId": "25818875-5F78-4A13-****-D7393642CA58"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/vod).


# DeleteVodTemplate

Deletes a snapshot template.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=DeleteVodTemplate&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteVodTemplate|The operation that you want to perform. Set the value to **DeleteVodTemplate**. |
|VodTemplateId|String|Yes|f5b228fe6930e\*\*\*\*\*d6bf55bd87789|The ID of the snapshot template. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|25818875-5F78-4A\*\*\*\*\*F6-D7393642CA58|The ID of the request. |
|VodTemplateId|String|f5b228fe6930e\*\*\*\*\*d6bf55bd87789|The ID of the snapshot template. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=DeleteVodTemplate
&VodTemplateId=f5b228fe6930e*****d6bf55bd87789
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DeleteVodTemplateResponse>
	  <RequestId>25818875-5F78-4A*****F6-D7393642CA58</RequestId>
	  <VodTemplateId>f5b228fe6930e*****d6bf55bd87789</VodTemplateId>
</DeleteVodTemplateResponse>
```

`JSON` format

```
{
    "RequestId": "25818875-5F78-4A*****F6-D7393642CA58",
    "VodTemplateId":"f5b228fe6930e*****d6bf55bd87789"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/vod).

## SDK examples

We recommend that you use [server SDKs](~~101789~~) to call this operation. You can view the sample code of different languages to call this operation by clicking the following links:

-   [Java](~~61063~~)
-   [Python](~~61054~~)
-   [PHP](~~61069~~)
-   [.NET](~~84750~~)
-   [Node.js](~~101396~~)
-   [Go](~~101411~~)
-   [C/C++](~~101261~~)


# UpdateVodTemplate

Modifies a snapshot template.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=UpdateVodTemplate&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|UpdateVodTemplate|The operation that you want to perform. Set the value to **UpdateVodTemplate**. |
|VodTemplateId|String|Yes|8c75a02e339b\*\*\*\*\*0b0d2c48171a22|The ID of the snapshot template. |
|Name|String|No|test|The name of the template.

 -   The name can be up to 128 bytes in length.
-   The value must be encoded in UTF-8. |
|TemplateConfig|String|No|\{"SnapshotConfig":\{"Count":10,"SpecifiedOffsetTime":0,"Interval":1\}|The configurations of the snapshot template. The value is a JSON-formatted string. For more information about the data structure, see the "SnapshotTemplateConfig" section of the [Media processing parameters](~~98618~~) topic. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|25818875-5F78-4A\*\*\*\*\*F6-D7393642CA58|The ID of the request. |
|VodTemplateId|String|8c75a02e339b\*\*\*\*\*0b0d2c48171a22|The ID of the snapshot template. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=UpdateVodTemplate
&VodTemplateId=8c75a02e339b*****0b0d2c48171a22
&<Common request parameters>
```

Sample success responses

`XML` format

```
<UpdateVodTemplateResponse>
      <RequestId>25818875-5F78-4A*****F6-D7393642CA58</RequestId>
	  <VodTemplateId>8c75a02e339b*****0b0d2c48171a22</VodTemplateId>
</UpdateVodTemplateResponse>
```

`JSON` format

```
{
    "RequestId": "25818875-5F78-4A*****F6-D7393642CA58",
    "VodTemplateId": "8c75a02e339b*****0b0d2c48171a22"
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


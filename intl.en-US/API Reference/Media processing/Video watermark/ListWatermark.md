# ListWatermark

Queries watermarks.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=ListWatermark&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ListWatermark|The operation that you want to perform. Set the value to **ListWatermark**. |
|AppId|String|No|app-\*\*\*\*|The ID of the application. Default value: **app-1000000**. For more information, see [Overview](~~113600~~). |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|25818875-5F78-4A\*\*\*\*\*F6-D7393642CA58|The ID of the request. |
|WatermarkInfos|Array of WatermarkInfo| |The watermarks. |
|AppId|String|app-\*\*\*\*|The ID of the application. |
|CreationTime|String|2018-11-07T09:05:52Z|The time when the watermark was added. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|FileUrl|String|https://outin-3262681cd\*\*\*\*\*89f4b3e7.oss-cn-shanghai.aliyuncs.com/image/cover/8CC8B715E6F8A72EC6B-6-2.png?Expires=1541600583&OSSAccessKeyId=\*\*\*\*&Signature=gmf1eYMoDVg%2BHQCb4UGozB\*\*\*\*|The Object Storage Service \(OSS\) URL or Content Delivery Network \(CDN\) URL of the watermark file. A text watermark does not have a file URL. |
|IsDefault|String|NotDefault|Indicates whether the watermark is the default one. Valid values:

 -   **Default**: The watermark is the default one.
-   **NotDefault**: The watermark is not the default one. |
|Name|String|Text watermark test|The name of the watermark. |
|Type|String|Text|The type of the watermark. Valid values:

 -   **Image**
-   **Text** |
|WatermarkConfig|String|\{"FontColor": "Blue","FontSize": 80,"Content": "Watermark test"\}|The configurations such as the position and effect of the text watermark or image watermark. The value is a JSON-formatted string. For more information about the data structure, see the "WatermarkConfig" section of the [Media processing parameters](~~98618~~) topic. |
|WatermarkId|String|9bcc8bfadb843\*\*\*\*\*109a2671d0df97|The ID of the watermark. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=ListWatermark
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ListWatermarkResponse>
  <RequestId>25818875-5F78-4A*****F6-D7393642CA58</RequestId>
  <WatermarkInfos>
        <IsDefault>NotDefault</IsDefault>
        <FileUrl>https://outin-3262681cd*****89f4b3e7.oss-cn-shanghai.aliyuncs.com/image/cover/8CC8B715E6F8A72EC6B-6-2.png?Expires=1541600583&amp;OSSAccessKeyId=****&amp;Signature=gmf1eYMoDVg%2BHQCb4UGozB****</FileUrl>
        <Type>Text</Type>
        <AppId>app-****</AppId>
        <WatermarkId>9bcc8bfadb843*****109a2671d0df97</WatermarkId>
        <CreationTime>2018-11-07T09:05:52Z</CreationTime>
        <WatermarkConfig>{"FontColor": "Blue","FontSize": 80,"Content": "Watermark test"}</WatermarkConfig>
        <Name>Text watermark test</Name>
  </WatermarkInfos>
</ListWatermarkResponse>
```

`JSON` format

```
{
	"RequestId": "25818875-5F78-4A*****F6-D7393642CA58",
	"WatermarkInfos": [{
		"IsDefault": "NotDefault",
		"FileUrl": "https://outin-3262681cd*****89f4b3e7.oss-cn-shanghai.aliyuncs.com/image/cover/8CC8B715E6F8A72EC6B-6-2.png?Expires=1541600583&OSSAccessKeyId=****&Signature=gmf1eYMoDVg%2BHQCb4UGozB****",
		"Type": "Text",
		"AppId": "app-****",
		"WatermarkId": "9bcc8bfadb843*****109a2671d0df97",
		"CreationTime": "2018-11-07T09:05:52Z",
		"WatermarkConfig": "{\"FontColor\": \"Blue\",\"FontSize\": 80,\"Content\": \"Watermark test\"}",
		"Name": "Text watermark test"
	}]
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


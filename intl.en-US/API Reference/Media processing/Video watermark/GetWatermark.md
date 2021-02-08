# GetWatermark

Queries a single watermark.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=GetWatermark&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GetWatermark|The operation that you want to perform. Set the value to **GetWatermark**. |
|WatermarkId|String|Yes|9bcc8bfadb843f\*\*\*\*\*09a2671d0df97|The ID of the watermark. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|25818875-5F78-4A\*\*\*\*\*F6-D7393642CA58|The ID of the request. |
|WatermarkInfo|Struct| |The information about the watermark. |
|AppId|String|app-\*\*\*\*|The ID of the application. |
|CreationTime|String|2018-11-06T08:03:17Z|The time when the watermark was added. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|FileUrl|String|https://outin-32\*\*\*\*\*f4b3e7.oss-cn-shanghai.aliyuncs.com/image/cover/F85529C8B715E6F8A72EC6B-6-2.png?Expires=1541600583&OSSAccessKeyId=\*\*\*\*&Signature=gmf1eYMoDVg%2BHQCb4UGozBW\*\*\*\*|The Object Storage Service \(OSS\) URL or Content Delivery Network \(CDN\) URL of the watermark file. A text watermark does not have a file URL. |
|IsDefault|String|NotDefault|Indicates whether the watermark is the default one. Valid values:

 -   **Default**: The watermark is the default one.
-   **NotDefault**: The watermark is not the default one. |
|Name|String|Image watermark test|The name of the watermark. |
|Type|String|Text|The type of the watermark. Valid values:

 -   **Image**
-   **Text** |
|WatermarkConfig|String|\{"ReferPos": "BottomRight","Height": "55","Width": "55","Dx": "8","Dy": "8" \}|The configurations such as the position and effect of the text watermark or image watermark. The value is a JSON-formatted string. For more information about the data structure, see the "WatermarkConfig" section of the [Media processing parameters](~~98618~~) topic. |
|WatermarkId|String|505e2e287ea\*\*\*\*\*ecfddd386d384|The ID of the watermark. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=GetWatermark
&WatermarkId=9bcc8bfadb843f*****09a2671d0df97
&<Common request parameters>
```

Sample success responses

`XML` format

```
<GetWatermarkResponse>
  <RequestId>25818875-5F78-4A*****F6-D7393642CA58</RequestId>
  <WatermarkInfo>
        <IsDefault>NotDefault</IsDefault>
        <FileUrl>https://outin-32*****f4b3e7.oss-cn-shanghai.aliyuncs.com/image/cover/F85529C8B715E6F8A72EC6B-6-2.png?Expires=1541600583&amp;OSSAccessKeyId=****&amp;Signature=gmf1eYMoDVg%2BHQCb4UGozBW****</FileUrl>
        <Type>Text</Type>
        <AppId>app-****</AppId>
        <WatermarkId>505e2e287ea*****ecfddd386d384</WatermarkId>
        <CreationTime>2018-11-06T08:03:17Z</CreationTime>
        <WatermarkConfig>{"ReferPos": "BottomRight","Height": "55","Width": "55","Dx": "8","Dy": "8" }</WatermarkConfig>
        <Name>Image watermark test</Name>
  </WatermarkInfo>
</GetWatermarkResponse>
```

`JSON` format

```
{
	"RequestId": "25818875-5F78-4A*****F6-D7393642CA58",
	"WatermarkInfo": {
		"IsDefault": "NotDefault",
		"FileUrl": "https://outin-32*****f4b3e7.oss-cn-shanghai.aliyuncs.com/image/cover/F85529C8B715E6F8A72EC6B-6-2.png?Expires=1541600583&OSSAccessKeyId=****&Signature=gmf1eYMoDVg%2BHQCb4UGozBW****",
		"Type": "Text",
		"AppId": "app-****",
		"WatermarkId": "505e2e287ea*****ecfddd386d384",
		"CreationTime": "2018-11-06T08:03:17Z",
		"WatermarkConfig": "{\"ReferPos\": \"BottomRight\",\"Height\": \"55\",\"Width\": \"55\",\"Dx\": \"8\",\"Dy\": \"8\" }",
		"Name": "Image watermark test"
	}
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/vod).

## Common errors

The following table describes the common errors that this operation can return.

|Error code

|Error message

|HTTP status code

|Description |
|------------|---------------|------------------|-------------|
|NoSuchResource

|The specified resource %s does not exist.

|404

|The error message returned because the user-related resource does not exist. %s indicates the specific resource information. |

## SDK examples

We recommend that you use [server SDKs](~~101789~~) to call this operation. You can view the sample code of different languages to call this operation by clicking the following links:

-   [Java](~~61063~~)
-   [Python](~~61054~~)
-   [PHP](~~61069~~)
-   [.NET](~~84750~~)
-   [Node.js](~~101396~~)
-   [Go](~~101411~~)
-   [C/C++](~~101261~~)


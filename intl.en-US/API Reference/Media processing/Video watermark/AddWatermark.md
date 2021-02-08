# AddWatermark

Adds a watermark.

**Note:** ApsaraVideo VOD supports static image watermarks such as PNG files and dynamic image watermarks such as GIF, APNG, and MOV files.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=AddWatermark&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|AddWatermark|The operation that you want to perform. Set the value to **AddWatermark**. |
|Name|String|Yes|Watermark|The name of the watermark. Only letters and digits are supported.

 -   The name can be up to 128 bytes in length.
-   The value must be encoded in UTF-8. |
|Type|String|Yes|Text|The type of the watermark. Valid values:

 -   **Image**: This is the default value.
-   **Text** |
|WatermarkConfig|String|Yes|\{"Width":"55","Height":"55","Dx":"9","Dy":"9","ReferPos":"BottonLeft","Type":"Image"\}|The configurations such as the position and effect of the text watermark or image watermark. The value is a JSON-formatted string.

 **Note:** The value of this parameter varies with the watermark type. For more information about the data structure, see the "WatermarkConfig" section of the [Media processing parameters](~~98618~~) topic. |
|FileUrl|String|No|http://outin-326268\*\*\*\*\*63e1403e7.oss-cn-shanghai.aliyuncs.com/image/cover/C99345\*\*\*\*\*E7FDEC-6-2.png|The Object Storage Service \(OSS\) URL of the watermark file. You must set this parameter if you add image watermarks. |
|AppId|String|No|app-\*\*\*\*|The ID of the application. Default value: **app-1000000**. For more information, see [Overview](~~113600~~). |

**Note:** For more information about how to upload a watermark file, see [CreateUploadAttachedMedia](~~98467~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|25818875-5F78-4A\*\*\*\*\*F6-D7393642CA58|The ID of the request. |
|WatermarkInfo|Struct| |The information about the watermark. |
|CreationTime|String|2018-11-07T09:05:52Z|The time when the watermark was added. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|FileUrl|String|https://outin-3262\*\*\*\*\*9f4b3e7.oss-cn-shanghai.aliyuncs.com/image/cover/E6C3448CC8B715E6F8A72EC6B-6-2.png?Expires=1541600583&OSSAccessKeyId=\*\*\*\*&Signature=gmf1eYMoDVg%2BHQCb4UGozBW\*\*\*\*|The OSS URL or Content Delivery Network \(CDN\) URL of the watermark file. A text watermark does not have a file URL. |
|IsDefault|String|NotDefault|Indicates whether the watermark is the default one. Valid values:

 -   **Default**: The watermark is the default one.
-   **NotDefault**: The watermark is not the default one. |
|Name|String|Text watermark test|The name of the watermark. |
|Type|String|Text|The type of the watermark. Valid values:

 -   **Image**: This is the default value.
-   **Text** |
|WatermarkConfig|String|\{"FontColor": "Blue","FontSize": 80, "Content": "Watermark test" \}|The configurations such as the position and effect of the text watermark or image watermark. The value is a JSON-formatted string.

 **Note:** The value of this parameter varies with the watermark type. For more information about the data structure, see the "WatermarkConfig" section of the [Media processing parameters](~~98618~~) topic. |
|WatermarkId|String|9bcc8bfadb84\*\*\*\*\*109a2671d0df97|The ID of the watermark. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=AddWatermark
&Name=Watermark
&Type=Text
&WatermarkConfig={"Width":"55","Height":"55","Dx":"9","Dy":"9","ReferPos":"BottonLeft","Type":"Image"}
&<Common request parameters>
```

Sample success responses

`XML` format

```
<AddWatermarkResponse>
  <RequestId>25818875-5F78-4A*****F6-D7393642CA58</RequestId>
  <WatermarkInfo>
        <IsDefault>NotDefault</IsDefault>
        <FileUrl>https://outin-3262*****9f4b3e7.oss-cn-shanghai.aliyuncs.com/image/cover/E6C3448CC8B715E6F8A72EC6B-6-2.png?Expires=1541600583&amp;OSSAccessKeyId=****&amp;Signature=gmf1eYMoDVg%2BHQCb4UGozBW****</FileUrl>
        <Type>Text</Type>
        <WatermarkId>9bcc8bfadb84*****109a2671d0df97</WatermarkId>
        <CreationTime>2018-11-07T09:05:52Z</CreationTime>
        <WatermarkConfig>{"FontColor": "Blue","FontSize": 80, "Content": "Watermark test" }</WatermarkConfig>
        <Name>Text watermark test</Name>
  </WatermarkInfo>
</AddWatermarkResponse>
```

`JSON` format

```
{
	"RequestId": "25818875-5F78-4A*****F6-D7393642CA58",
	"WatermarkInfo": {
		"IsDefault": "NotDefault",
		"FileUrl": "https://outin-3262*****9f4b3e7.oss-cn-shanghai.aliyuncs.com/image/cover/E6C3448CC8B715E6F8A72EC6B-6-2.png?Expires=1541600583&OSSAccessKeyId=****&Signature=gmf1eYMoDVg%2BHQCb4UGozBW****",
		"Type": "Text",
		"WatermarkId": "9bcc8bfadb84*****109a2671d0df97",
		"CreationTime": "2018-11-07T09:05:52Z",
		"WatermarkConfig": "{\"FontColor\": \"Blue\",\"FontSize\": 80, \"Content\": \"Watermark test\" }",
		"Name": "Text watermark test"
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


# UpdateWatermark

Modifies a watermark.

**Note:** You can modify only the name and configurations of a watermark.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=UpdateWatermark&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|UpdateWatermark|The operation that you want to perform. Set the value to **UpdateWatermark**. |
|Name|String|Yes|test|The name of the watermark. Only letters and digits are supported.

 -   The name can be up to 128 bytes in length.
-   The value must be encoded in UTF-8. |
|WatermarkConfig|String|Yes|\{"Width":"55","Height":"55","Dx":"9","Dy":"9","ReferPos":"BottonLeft","Type":"Image"\}|The configurations such as the position and effect of the text watermark or image watermark. The value is a JSON-formatted string.

 **Note:** The value of this parameter varies with the watermark type. For more information about the data structure, see the "WatermarkConfig" section of the [Media processing parameters](~~98618~~) topic. |
|WatermarkId|String|Yes|af2afe4761992c\*\*\*\*\*bd947dae97337|The ID of the watermark. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|25818875-5F78-4A\*\*\*\*\*F6-D7393642CA58|The ID of the request. |
|WatermarkInfo|Struct| |The information about the watermark. |
|CreationTime|String|2018-11-06T08:03:17Z|The time when the watermark was added. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|FileUrl|String|https://outin-32\*\*\*\*9f4b3e7.oss-cn-shanghai.aliyuncs.com/image/cover/E6C3448CC8B715E6F8A72EC6B-6-2.png?Expires=1541600583&OSSAccessKeyId=\*\*\*\*&Signature=gmf1eYMoDVg%2BHQCb4UGozBW\*\*\*\*|The Object Storage Service \(OSS\) URL or Content Delivery Network \(CDN\) URL of the watermark file. A text watermark does not have a file URL. |
|IsDefault|String|NotDefault|Indicates whether the watermark is the default one. Valid values:

 -   **Default**: The watermark is the default one.
-   **NotDefault**: The watermark is not the default one. |
|Name|String|Image watermark test|The name of the watermark. |
|Type|String|Text|The type of the watermark. Valid values:

 -   **Image**: This is the default value.
-   **Text** |
|WatermarkConfig|String|\{"Width":"55","Height":"55","Dx":"9","Dy":"9","ReferPos":"BottonLeft","Type":"Image"\}|The configurations such as the position and effect of the text watermark or image watermark. The value is a JSON-formatted string.

 **Note:** The value of this parameter varies with the watermark type. For more information about the data structure, see the "WatermarkConfig" section of the [Media processing parameters](~~98618~~) topic. |
|WatermarkId|String|505e2e287ea\*\*\*\*\*ecfddd386d384|The ID of the watermark. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=UpdateWatermark
&Name=test
&WatermarkConfig={"Width":"55","Height":"55","Dx":"9","Dy":"9","ReferPos":"BottonLeft","Type":"Image"}
&WatermarkId=af2afe4761992c*****bd947dae97337
&<Common request parameters>
```

Sample success responses

`XML` format

```
<UpdateWatermarkResponse>
  <RequestId>25818875-5F78-4A*****F6-D7393642CA58</RequestId>
  <WatermarkInfo>
        <Name>Image watermark test</Name>
        <CreationTime>2018-11-06T08:03:17Z</CreationTime>
        <WatermarkId>505e2e287ea*****ecfddd386d384</WatermarkId>
        <FileUrl>https://outin-32****9f4b3e7.oss-cn-shanghai.aliyuncs.com/image/cover/E6C3448CC8B715E6F8A72EC6B-6-2.png?Expires=1541600583&amp;OSSAccessKeyId=****&amp;Signature=gmf1eYMoDVg%2BHQCb4UGozBW****</FileUrl>
        <IsDefault>NotDefault</IsDefault>
        <Type>Image</Type>
        <WatermarkConfig>
              <ReferPos>BottomRight</ReferPos>
              <Height>55</Height>
              <Width>55</Width>
              <Dx>8</Dx>
              <Dy>8</Dy>
        </WatermarkConfig>
  </WatermarkInfo>
</UpdateWatermarkResponse>
```

`JSON` format

```
{
 "RequestId": "25818875-5F78-4A*****F6-D7393642CA58",
 "WatermarkInfo":{
    "Name": "Image watermark test",
    "CreationTime": "2018-11-06T08:03:17Z",
    "WatermarkId": "505e2e287ea*****ecfddd386d384",
    "FileUrl": "https://outin-32****9f4b3e7.oss-cn-shanghai.aliyuncs.com/image/cover/E6C3448CC8B715E6F8A72EC6B-6-2.png?Expires=1541600583&OSSAccessKeyId=****&Signature=gmf1eYMoDVg%2BHQCb4UGozBW****",
    "IsDefault": "NotDefault",
    "Type": "Image",
    "WatermarkConfig": {
      "ReferPos": "BottomRight",
      "Height": "55",
      "Width": "55",
      "Dx": "8",
      "Dy": "8"
    }
  }
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


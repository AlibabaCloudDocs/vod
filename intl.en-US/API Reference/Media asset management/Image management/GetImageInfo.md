# GetImageInfo

Queries the basic information about an image based on the image ID. The basic information includes the title, type, creation time, and tags of the image.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=GetImageInfo&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GetImageInfo|The operation that you want to perform. Set the value to **GetImageInfo**. |
|ImageId|String|Yes|3e34733b40b\*\*\*\*\*9a96ccf5c1ff6f69|The ID of the image. |
|AuthTimeout|Long|No|3600|The validity period of the image URL. Unit: seconds.

 **Note:**

-   If the OutputType parameter is set to **cdn**:
    -   The image URL has a validity period only if URL signing is enabled. Otherwise, the image URL is permanently valid.
    -   Minimum value: **1**.
    -   Maximum value: unlimited.
    -   Default value: If you do not set this parameter, the default validity period that is specified in URL signing is used.
-   If the OutputType parameter is set to **oss**:
    -   The image URL has a validity period only if the permissions on the Object Storage Service \(OSS\) bucket are private. Otherwise, the image URL is permanently valid.
    -   Minimum value: **1**.
    -   Maximum value: **2592000** \(30 days\). The maximum value is limited to reduce security risks of the origin.
    -   Default value: If you do not set this parameter, the default value is **3600**. |
|OutputType|String|No|cdn|The type of the image URL. Valid values:

 -   **oss**: OSS URL
-   **cdn** \(default\): Content Delivery Network \(CDN\) URL |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|ImageInfo|Struct| |The information about the image. |
|AppId|String|app-\*\*\*\*|The ID of the application. |
|AuditStatus|String|Normal|The review status of the image. Valid values:

 -   **Normal**: The image is approved.
-   **Blocked**: The image is blocked. |
|CateId|Long|254766071|The ID of the category. |
|CateName|String|Test|The name of the category. |
|CreationTime|String|2018-11-21T02:37:23Z|The time when the image file was created. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|Description|String|Test description|The description of the image. |
|ImageId|String|bbc65bba53f9\*\*\*\*\*ed90de118a7849|The ID of the image. |
|ImageType|String|default|The type of the image. Valid values:

 -   **CoverSnapshot**: thumbnail snapshot.
-   **NormalSnapshot**: normal snapshot.
-   **SpriteSnapshot**: sprite snapshot.
-   **SpriteOriginSnapshot**: sprite source snapshot.
-   **All**: images of all the preceding types. If this parameter is not set to All, you can specify multiple types and separate them with commas \(,\). |
|Mezzanine|Struct| |The information about the image mezzanine file. |
|FileSize|String|8932|The size of the file. Unit: byte. |
|FileURL|String|https://outin-bfefbb\*\*\*\*\*163e1c7426.oss-cn-shanghai.aliyuncs.com/image/default/5E84CD536\*\*\*\*\*D4DAD.png?Expires=1590982353&OSSAccessKeyId=\*\*\*\*\*&Signature=ALPET74o\*\*\*\*\*c%3D|The OSS URL of the image. |
|Height|Integer|200|The height of the image. Unit: pixel. |
|OriginalFileName|String|\*\*\*\*.gif|The name of the uploaded file. |
|Width|Integer|200|The width of the image. Unit: pixel. |
|RegionId|String|cn-shanghai|The region ID. |
|Status|String|Uploading|The status of the image. Valid values:

 -   **Uploading**: The image is being uploaded. This is the initial status.
-   **Normal**: The image is uploaded.
-   **UploadFail**: The image fails to be uploaded. |
|StorageLocation|String|sample.oss-cn-shanghai.aliyuncs.com|The OSS bucket where the image is stored. |
|Tags|String|tag1,tag2,tag3|The tag of the image. Multiple tags are separated by commas \(,\). |
|Title|String|this is a sample|The title of the image. |
|URL|String|http://sample.com/image/default/\*\*\*\*.gif?auth\_key=\*\*\*\*|The URL of the image. If a CDN domain name is specified, a CDN URL is returned. Otherwise, an OSS URL is returned. |
|RequestId|String|AB99D4DF-FAFA-49\*\*\*\*\*DC-9C548C1E261E|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=GetImageInfo
&ImageId=3e34733b40b*****9a96ccf5c1ff6f69
&<Common request parameters>
```

Sample success responses

`XML` format

```
<GetImageInfoResponse>
    <RequestId>AB99D4DF-FAFA-49*****DC-9C548C1E261E</RequestId>
    <ImageInfo>
        <Description>Test description</Description>
        <Mezzanine>
            <OriginalFileName>https://outin-bfefbb*****163e1c7426.oss-cn-shanghai.aliyuncs.com/image/default/5E84CD536*****D4DAD.png?Expires=1590982353&OSSAccessKeyId=*****&Signature=ALPET74o*****c%3D</OriginalFileName>
            <Height>200</Height>
            <Width>200</Width>
            <FileSize>8932</FileSize>
        </Mezzanine>
        <CreationTime>2018-11-21T02:37:23Z</CreationTime>
        <ImageId>bbc65bba53f9*****ed90de118a7849</ImageId>
        <Title>this is a sample</Title>
        <CateId>254766071</CateId>
        <CateName>Test</CateName>
        <StorageLocation>outin-bfefbb*****163e1c7426.oss-cn-shanghai.aliyuncs.com</StorageLocation>
        <Tags>tag1,tag2,tag3</Tags>
        <URL>https://al*****.cn/image/default/5E84CD536*****D4DAD.png?auth_key=159098055*****70a396e834</URL>
        <ImageType>default</ImageType>
    </ImageInfo>
</GetImageInfoResponse>
```

`JSON` format

```
{
    "RequestId": "AB99D4DF-FAFA-49*****DC-9C548C1E261E",
    "ImageInfo": {
        "Description": "Test description",
        "Mezzanine": {
            "OriginalFileName": "https://outin-bfefbb*****163e1c7426.oss-cn-shanghai.aliyuncs.com/image/default/5E84CD536*****D4DAD.png?Expires=1590982353&OSSAccessKeyId=*****&Signature=ALPET74o*****c%3D",
            "Height": 200,
            "Width": 200,
            "FileSize": 8932
        },
        "CreationTime": "2018-11-21T02:37:23Z",
        "ImageId": "bbc65bba53f9*****ed90de118a7849",
        "Title": "this is a sample",
        "CateId": 254766071,
        "CateName": "Test",
        "StorageLocation": "outin-bfefbb*****163e1c7426.oss-cn-shanghai.aliyuncs.com",
        "Tags": "tag1,tag2,tag3",
        "URL": "https://al*****.cn/image/default/5E84CD536*****D4DAD.png?auth_key=159098055*****70a396e834",
        "ImageType": "default"
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

|The specified resource does not exist.

|404

|The error message returned because the image does not exist. |

## SDK examples

We recommend that you use a [server SDK](~~101789~~) to call this operation. For more information about the sample code that is used to call this operation in various languages, see the following topics:

-   [Java](~~61063~~)
-   [Python](~~61054~~)
-   [PHP](~~61069~~)
-   [.NET](~~84750~~)
-   [Node.js](~~101396~~)
-   [Go](~~101411~~)
-   [C/C++](~~101261~~)


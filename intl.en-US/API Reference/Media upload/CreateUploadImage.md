# CreateUploadImage

Obtains a URL and a credential for uploading an image.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=CreateUploadImage&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateUploadImage|The operation that you want to perform. Set the value to **CreateUploadImage**. |
|ImageType|String|Yes|default|The type of the image. Valid values:

 -   **default**
-   **cover**

 **Note:** Only images of the **default** type can be managed in the ApsaraVideo VOD console. |
|Title|String|No|mytitle|The title of the image. Rules:

 -   The title can be up to 128 bytes in length.
-   The value must be encoded in UTF-8. |
|ImageExt|String|No|png|The file name extension of the image. Valid values:

 -   **png**: This is the default value.
-   **jpg**
-   **jpeg**
-   **gif** |
|Tags|String|No|Test|The tag of the image. Rules:

 -   Each tag can be up to 32 bytes in length. A maximum of 16 tags can be specified.
-   Separate multiple tags with commas \(,\).
-   The value must be encoded in UTF-8. |
|StorageLocation|String|No|outin-\*\*\*\*..oss-cn-shanghai.aliyuncs.com|The storage location.

 If this parameter is set to a specific value, the image is uploaded to the specified storage location. Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/?spm=a2c4g.11186623.2.15.6948257eaZ4m54#/vod/settings/censored). In the left-side navigation pane, choose **Configuration Management** \> **Media Management** \> **Storage**. On the Storage page, you can view the storage location. |
|CateId|Long|No|12001111|The ID of the category.

 Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/?spm=a2c4g.11186623.2.15.6948257eaZ4m54#/vod/settings/censored). In the left-side navigation pane, choose **Configuration Management** \> **Media Management** \> **Categories**. On the Categories page, you can view the category IDs or modify categories. |
|UserData|String|No|\{"MessageCallback":\{"CallbackURL":"http://test.test.com"\},"Extend":\{"localId":"xxx","test":"www"\}\}|The custom configurations, including callback configurations and upload acceleration configurations. The value is a JSON string. For more information, see the "UserData" section of the [Request parameters](~~86952~~) topic.

 **Note:**

-   The callback configurations take effect only when you specify the HTTP callback URL and select the specific callback events in the ApsaraVideo VOD console.
-   To use the upload acceleration feature, submit a [ticket](https://ticket-intl.console.aliyun.com/#/ticket/createIndex). For more information, see [Upload instructions](~~55396~~). |
|Description|String|No|Image upload test|The description of the image.

 -   The description can be up to 1,024 bytes in length.
-   The value must be encoded in UTF-8. |
|AppId|String|No|app-\*\*\*\*|The ID of the application. Default value: **app-1000000**. For more information, see [Overview](~~113600~~). |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|FileURL|String|http://aliyun.com/cover/2017-\*\*\*\*\*B-4F4C-9373-003AA06012EA.png|The Object Storage Service \(OSS\) URL of the file. The URL does not contain the information used for authentication. You can set the FileUrl parameter to this URL when you call the [AddWatermark](~~98617~~) operation. |
|ImageId|String|93ab850b4f6f4\*\*\*\*\*6e91d24d81d4|The ID of the image. |
|ImageURL|String|http://aliyun.com/cover/2017-\*\*\*\*\*B-4F4C-9373-003AA06012EA.png|The URL of the image. |
|RequestId|String|25818875-5F78\*\*\*\*\*EF6-D7393642CA58|The ID of the request. |
|UploadAddress|String|eyJTZWN1cm\*\*\*\*\*uIjoiQ0FJU3p3TjF|The upload URL. |
|UploadAuth|String|eyJFbmR\*\*\*\*\*CI6Im|The upload credential. |

**Note:**

-   This operation does not upload images. To upload an image, you must obtain the upload URL and credential, decode the URL and credential by using the [Base64 algorithm](~~55397~~), and then use OSS SDKs to upload the image to a specified bucket. This process is the same as that of uploading a video.
-   You can call the [CreateUploadAttachedMedia](~~98467~~) operation to upload image watermarks.
-   If the image upload credential expires after 3,000 seconds, you can call the CreateUploadImage operation again to obtain a new upload URL and a new upload credential.
-   If you enable the URL signing feature of ApsaraVideo VOD, you may be unable to access the returned URL of the image by using a browser and the HTTP status code 403 may be returned. You can disable the [URL signing](~~86090~~) feature or [generate an authentication signature](~~57007~~).
-   For more information, see [Upload URLs and credentials](~~55397~~).

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=CreateUploadImage
&ImageType=default
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateUploadImageResponse>
      <RequestId>25818875-5F78*****EF6-D7393642CA58</RequestId>
      <ImageId>93ab850b4f6f4*****6e91d24d81d4</ImageId>
      <UploadAddress>eyJTZWN1cm*****uIjoiQ0FJU3p3TjF</UploadAddress>
      <UploadAuth>eyJFbmR*****CI6Im</UploadAuth>
      <ImageURL>http://aliyun.com/cover/2017-*****B-4F4C-9373-003AA06012EA.png</ImageURL>
      <FileURL>http://aliyun.com/cover/2017-*****B-4F4C-9373-003AA06012EA.png</FileURL>
</CreateUploadImageResponse>
```

`JSON` format

```
{
    "CreateUploadImageResponse": {
        "RequestId": "25818875-5F78*****EF6-D7393642CA58",
        "ImageId": "93ab850b4f6f4*****6e91d24d81d4",
        "UploadAddress": "eyJTZWN1cm*****uIjoiQ0FJU3p3TjF",
        "UploadAuth": "eyJFbmR*****CI6Im",
        "ImageURL": "http://aliyun.com/cover/2017-*****B-4F4C-9373-003AA06012EA.png",
        "FileURL":"http://aliyun.com/cover/2017-*****B-4F4C-9373-003AA06012EA.png"
    }
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/vod).

## SDK examples

We recommend that you use a [server SDK](~~101789~~) to call this operation. For more information about the sample code that is used to call this operation in various languages, see the following topics:

-   [Java](~~61063~~)
-   [Python](~~61054~~)
-   [PHP](~~61069~~)
-   [.NET](~~84750~~)
-   [Node.js](~~101396~~)
-   [Go](~~101411~~)
-   [C/C++](~~101261~~)


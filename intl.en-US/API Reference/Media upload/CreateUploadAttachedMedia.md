# CreateUploadAttachedMedia

Obtains a URL and a credential for uploading an auxiliary media asset, such as a watermark file or a subtitle file.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=CreateUploadAttachedMedia&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateUploadAttachedMedia|The operation that you want to perform. Set the value to **CreateUploadAttachedMedia**. |
|BusinessType|String|Yes|watermark|The type of the media asset. Valid values:

 -   **watermark**
-   **subtitle**
-   **material** |
|Title|String|No|Test|The title of the media asset. Rules:

 -   The title can be up to 128 bytes in length.
-   The value must be encoded in UTF-8. |
|MediaExt|String|No|png|The file name extension. Valid values:

 -   Valid values for watermark files: **png, gif, apng, and mov**.
-   Valid values for subtitle files: **srt, ass, stl, ttml, and vtt**.
-   Valid values for material files: **jpg, gif, png, mp4, mat, and zip**. |
|FileName|String|No|D:\\test.png|The name of the mezzanine file. |
|FileSize|String|No|123|The size of the file. Unit: byte. |
|Tags|String|No|tag1,tag2|The tag of the file. Rules:

 -   Each tag can be up to 32 bytes in length. A maximum of 16 tags can be specified.
-   Separate multiple tags with commas \(,\).
-   The value must be encoded in UTF-8. |
|StorageLocation|String|No|outin-bfefbb90a47c\*\*\*\*\*\*163e1c7426.oss-cn-shanghai.aliyuncs.com|The storage location.

 If this parameter is set to a specific value, the auxiliary media asset is uploaded to the specified storage location. Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/?spm=a2c4g.11186623.2.15.6948257eaZ4m54#/vod/settings/censored). In the left-side navigation pane, choose **Configuration Management** \> **Media Management** \> **Storage**. On the Storage page, you can view the storage location. |
|Description|String|No|uploadTest|The description of the media asset. Rules:

 -   The description can be up to 1,024 bytes in length.
-   The value must be encoded in UTF-8. |
|UserData|String|No|\{"MessageCallback":\{"CallbackURL":"http://test.test.com"\},"Extend":\{"localId":"xxx","test":"www"\}\}|The custom configurations, including callback configurations and upload acceleration configurations. The value is a JSON string. For more information, see the "UserData" section of the [Request parameters](~~86952~~) topic.

 **Note:**

-   The callback configurations take effect only when you specify the HTTP callback URL and select the specific callback events in the ApsaraVideo VOD console.
-   To use the upload acceleration feature, submit a [ticket](https://ticket-intl.console.aliyun.com/#/ticket/createIndex). For more information, see [Upload instructions](~~55396~~). |
|CateIds|String|No|12984346,08130876|The ID of the category.

 -   Separate multiple IDs with commas \(,\). A maximum of five IDs can be specified.
-   Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/?spm=a2c4g.11186623.2.15.6948257eaZ4m54#/vod/settings/censored). In the left-side navigation pane, choose **Configuration Management** \> **Media Management** \> **Categories**. On the Categories page, you can view the category IDs or modify categories. |
|AppId|String|No|app-\*\*\*\*|The ID of the application. Default value: **app-1000000**. For more information, see [Overview](~~113600~~). |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|FileURL|String|https://sample.oss-cn-shanghai.aliyuncs.com/watermark/\*\*\*\*.mov|The Object Storage Service \(OSS\) URL of the file. The URL does not contain the information used for authentication. You can set the FileUrl parameter to this URL when you call the [AddWatermark](~~98617~~) operation. |
|MediaId|String|97dc17a5a\*\*\*\*\*bc3668489b84ce9|The ID of the media asset. |
|MediaURL|String|http://sample.com/watermark/\*\*\*\*.mov?auth\_key=\*\*\*\*|The URL of the media asset. If a domain name for CDN is specified, a CDN URL is returned. Otherwise, an OSS URL is returned. |
|RequestId|String|73254DE5-F260-47\*\*\*\*\*20-D06856B63C01|The ID of the request. |
|UploadAddress|String|LWNuLXNoYW5\*\*\*\*\*naGFpLmFsaXl1b|The upload URL. |
|UploadAuth|String|UzFnUjFxNkZ0NUI\*\*\*\*\*ZTaklyNWJoQ00zdHF|The upload credential. |

**Note:**

-   This operation does not upload auxiliary media assets. To upload an auxiliary media asset, you must obtain the upload URL and credential, decode the URL and credential by using the [Base64 algorithm](~~55397~~), and then use OSS SDKs to upload the auxiliary media asset to a specified bucket. This process is the same as that of uploading a video or an image.
-   If the upload credential expires after 3,000 seconds, you can call the CreateUploadAttachedMedia operation again to obtain a new upload URL and a new upload credential.
-   If you enable the URL signing feature of ApsaraVideo VOD, you may be unable to access the returned URL of the media asset by using a browser and the HTTP status code 403 may be returned. You can disable the [URL signing](~~86090~~) feature or [generate an authentication signature](~~57007~~).
-   For more information, see [Upload URLs and credentials](~~55397~~).

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=CreateUploadAttachedMedia
&BusinessType=watermark
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateUploadAttachedMediaResponse>
	  <RequestId>73254DE5-F260-47*****20-D06856B63C01</RequestId>
	  <MediaId>97dc17a5a*****bc3668489b84ce9</MediaId>
	  <UploadAddress>LWNuLXNoYW5*****naGFpLmFsaXl1b</UploadAddress>
	  <UploadAuth>UzFnUjFxNkZ0NUI*****ZTaklyNWJoQ00zdHF</UploadAuth>
	  <FileURL>https://sample.oss-cn-shanghai.aliyuncs.com/watermark/****.mov</FileURL>
	  <MediaURL>http://sample.com/watermark/****.mov?auth_key=****</MediaURL>
</CreateUploadAttachedMediaResponse>
```

`JSON` format

```
{
    "RequestId": "73254DE5-F260-47*****20-D06856B63C01",
    "MediaId": "97dc17a5a*****bc3668489b84ce9",
    "UploadAddress": "LWNuLXNoYW5*****naGFpLmFsaXl1b",
    "UploadAuth": "UzFnUjFxNkZ0NUI*****ZTaklyNWJoQ00zdHF",
    "FileURL": "https://sample.oss-cn-shanghai.aliyuncs.com/watermark/****.mov",
    "MediaURL": "http://sample.com/watermark/****.mov?auth_key=****"
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


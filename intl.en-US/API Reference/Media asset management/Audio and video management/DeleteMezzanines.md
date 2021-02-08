# DeleteMezzanines

Deletes one or more mezzanine files at a time.

**Note:** All media processing operations in ApsaraVideo VOD, such as transcoding, snapshot capture, and content moderation, are performed on mezzanine files. If you delete the mezzanine files, you cannot perform follow-up media processing operations. Exercise caution when you call this operation.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=DeleteMezzanines&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteMezzanines|The operation that you want to perform. Set the value to **DeleteMezzanines**. |
|VideoIds|String|Yes|23ab850b4f6\*\*\*\*\*54b6e91d24d8157,93ab850b4f6f4\*\*\*\*\*b6e91d24d81d4|The list of video IDs. A maximum of 20 video IDs can be specified at a time. Separate multiple IDs with commas \(,\). |
|Force|Boolean|No|false|Specifies whether to forcibly delete the mezzanine file. Default value: **false**.

 **Note:** If a video is delivered without transcoding or is asynchronously transcoded, the mezzanine file of the video is used for original-quality playback. By default, the mezzanine file of the video cannot be deleted. To forcibly delete the mezzanine file, set this parameter to **true**. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|NonExistVideoIds|List|93ab850b4f6f4\*\*\*\*\*b6e91d24d81d4|The IDs of the videos that do not exist. |
|RequestId|String|25818875-5F78-4A\*\*\*\*\*F6-D7393642CA58|The ID of the request. |
|UnRemoveableVideoIds|List|23ab850b4f6f44\*\*\*\*\*b6e91d24d8157|The IDs of the videos whose mezzanine files cannot be deleted.

 **Note:** Generally, mezzanine files cannot be deleted if they are used for original-quality playback or you do not have required [permissions](~~113600~~) to delete them. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=DeleteMezzanines
&VideoIds=23ab850b4f6*****54b6e91d24d8157,93ab850b4f6f4*****b6e91d24d81d4
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DeleteMezzaninesResponse>
      <RequestId>25818875-5F78-4A*****F6-D7393642CA58</RequestId>
      <NonExistVideoIds>93ab850b4f6f4*****b6e91d24d81d4</NonExistVideoIds>
      <UnRemoveableVideoIds>23ab850b4f6f44*****b6e91d24d8157</UnRemoveableVideoIds>
</DeleteMezzaninesResponse>
```

`JSON` format

```
{
    "RequestId": "25818875-5F78-4A*****F6-D7393642CA58",
    "NonExistVideoIds": "93ab850b4f6f4*****b6e91d24d81d4",
    "UnRemoveableVideoIds":"23ab850b4f6f44*****b6e91d24d8157"
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


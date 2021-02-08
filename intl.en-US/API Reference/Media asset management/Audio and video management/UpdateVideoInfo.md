# UpdateVideoInfo

Modifies the information about a video.

**Note:** The specific parameter of a video is updated only when a new value is passed in the parameter.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=UpdateVideoInfo&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|UpdateVideoInfo|The operation that you want to perform. Set the value to **UpdateVideoInfo**. |
|VideoId|String|Yes|2deda93265\*\*\*\*\*312baf9b0ed810d|The ID of the video. |
|Title|String|No|Video title in ApsaraVideo VOD|The title of the video.

 -   The value can be up to 128 bytes in length.
-   The string must be encoded in the UTF-8 format. |
|Tags|String|No|Tag 1,Tag 2|The tags of the video.

 -   Each tag can be up to 32 bytes in length. A maximum of 16 tags can be specified.
-   Separate multiple tags with commas \(,\).
-   The string must be encoded in the UTF-8 format. |
|Description|String|No|Video description in ApsaraVideo VOD|The description of the video.

 -   The value can be up to 1,024 bytes in length.
-   The string must be encoded in the UTF-8 format. |
|CoverURL|String|No|https://image.example.com/\*\*\*\*.jpg|The URL of the video thumbnail. |
|CateId|Long|No|384761111|The ID of the video category. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|25818875-5F78-4A\*\*\*\*\*F6-D7393642CA58|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=UpdateVideoInfo
&VideoId=2deda93265*****312baf9b0ed810d
&<Common request parameters>
```

Sample success responses

`XML` format

```
<UpdateVideoInfoResponse>
      <RequestId>25818875-5F78-4A*****F6-D7393642CA58</RequestId>
</UpdateVideoInfoResponse>
```

`JSON` format

```
{
    "RequestId": "25818875-5F78-4A*****F6-D7393642CA58"
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
|InvalidVideo.NotFound

|The video does not exist.

|404

|The error message returned because the video does not exist. |

## SDK examples

We recommend that you use a [server SDK](~~101789~~) to call this operation. For more information about the sample code that is used to call this operation in various languages, see the following topics:

-   [Java](~~61063~~)
-   [Python](~~61054~~)
-   [PHP](~~61069~~)
-   [.NET](~~84750~~)
-   [Node.js](~~101396~~)
-   [Go](~~101411~~)
-   [C/C++](~~101261~~)


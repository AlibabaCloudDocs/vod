# GetVideoPlayAuth

Queries the playback credential that is required for playing a video.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=GetVideoPlayAuth&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GetVideoPlayAuth|The operation that you want to perform. Set the value to **GetVideoPlayAuth**. |
|VideoId|String|Yes|dfde02284a5c466\*\*\*\*\*22a097adaf4a|The ID of the video. |
|AuthInfoTimeout|Long|No|3000|The validity period of the playback credential. Unit: seconds.

 -   Default value: **100**.
-   Valid values: `[100,3000]`. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|25818875-5F78-4A\*\*\*\*\*F6-D7393642CA58|The ID of the request. |
|VideoMeta|Struct| |The metadata of the video. |
|CoverURL|String|https://image.example.com/\*\*\*\*.jpg|The URL of the video thumbnail. |
|Duration|Float|120.0|The duration of the video. Unit: seconds. |
|Status|String|Normal|The status of the video. For more information about the value range and description, see the [Status](~~52839~~) table. |
|Title|String|ApsaraVideo VOD|The title of the video. |
|VideoId|String|93ab850b4f6f\*\*\*\*\*4b6e91d24d81d4|The ID of the video. |
|PlayAuth|String|sstyYuew6789\*\*\*\*\*00000xtt7TYUh|The playback credential of the video. |

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=GetVideoPlayAuth
&VideoId=dfde02284a5c466*****22a097adaf4a
&<Common request parameters>
```

Sample success responses

`XML` format

```
<GetVideoPlayAuthResponse>
      <RequestId>25818875-5F78-4A*****F6-D7393642CA58</RequestId>
      <VideoMeta>
            <VideoId>93ab850b4f6f*****4b6e91d24d81d4</VideoId>
            <Title>ApsaraVideo VOD</Title>
            <Duration>135.6</Duration>
            <CoverURL>https://image.example.com/****.jpg</CoverURL>
            <Status>Normal</Status>
      </VideoMeta>
      <PlayAuth>sstyYuew6789*****00000xtt7TYUh</PlayAuth>
</GetVideoPlayAuthResponse>
```

`JSON` format

```
{
    "RequestId": "25818875-5F78-4A*****F6-D7393642CA58",
    "VideoMeta": {
        "VideoId": "93ab850b4f6f*****4b6e91d24d81d4",
        "Title": "ApsaraVideo VOD",
        "Duration": 135.6,
        "CoverURL": "https://image.example.com/****.jpg",
        "Status": "Normal"
    },
    "PlayAuth": "sstyYuew6789*****00000xtt7TYUh"
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
|Forbidden.IllegalStatus

|Status of the video is illegal.

|403

|The error message returned because the video status is invalid. |
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


# ListDynamicImage

Queries the information about animated stickers of a video based on the video ID.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=ListDynamicImage&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ListDynamicImage|The operation that you want to perform. Set the value to **ListDynamicImage**. |
|VideoId|String|Yes|2e114f110059\*\*\*\*\*0c3193918fd449a|The ID of the video. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|DynamicImageList|Array of DynamicImage| |The list of animated stickers. |
|CreationTime|String|2020-07-28T02:01:06Z|The time when the animated sticker was created. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|Duration|String|2|The duration of the animated sticker. |
|DynamicImageId|String|2b4e51df60\*\*\*\*\*323ef43d6e336ecf|The ID of the animated sticker. |
|FileSize|String|119866|The size of the animated sticker file. |
|FileURL|String|https://vod-test.cn/2e114f110059\*\*\*\*\*0c3193918fd449a/image/dynamic/2b4e51df60\*\*\*\*\*323ef43d6e336ecf.webp?auth\_key=1597296785-0-0-4a48e85\*\*\*\*\*bd2bb358e0b3cade|The URL of the animated sticker file. |
|Format|String|webp|The format of the animated sticker. Valid values: gif and webp. |
|Fps|String|10|The frame rate of the animated sticker. |
|Height|String|360|The height of the animated sticker. |
|JobId|String|2bf4390af9e54\*\*\*\*\*91c09cc720ad|The job ID for creating the animated sticker. |
|VideoId|String|2e114f110059\*\*\*\*\*0c3193918fd449a|The ID of the video. |
|Width|String|640|The width of the animated sticker. |
|RequestId|String|570189B6-572E-49\*\*\*\*\*53-13B4278EE0D8|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=ListDynamicImage
&VideoId=2e114f110059*****0c3193918fd449a
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ListDynamicImageResponse>
      <RequestId>570189B6-572E-49*****53-13B4278EE0D8</RequestId>
      <DynamicImageList>
            <FileURL>https://vod-test.cn/2e114f110059*****0c3193918fd449a/image/dynamic/2b4e51df60*****323ef43d6e336ecf.webp?auth_key=1597296785-0-0-4a48e85*****bd2bb358e0b3cade</FileURL>
            <VideoId>2e114f110059*****0c3193918fd449a</VideoId>
            <Format>webp</Format>
            <Fps>10</Fps>
            <CreationTime>2020-07-28T02:01:06Z</CreationTime>
            <DynamicImageId>2b4e51df60*****323ef43d6e336ecf</DynamicImageId>
            <Height>360</Height>
            <Duration>2</Duration>
            <Width>640</Width>
            <JobId>2bf4390af9e54*****91c09cc720ad</JobId>
            <FileSize>119866</FileSize>
      </DynamicImageList>
</ListDynamicImageResponse>
```

`JSON` format

```
{
    "RequestId": "570189B6-572E-49*****53-13B4278EE0D8",
    "DynamicImageList": [{
        "FileURL": "https://vod-test.cn/2e114f110059*****0c3193918fd449a/image/dynamic/2b4e51df60*****323ef43d6e336ecf.webp?auth_key=1597296785-0-0-4a48e85*****bd2bb358e0b3cade",
        "VideoId": "2e114f110059*****0c3193918fd449a",
        "Format": "webp",
        "Fps": "10",
        "CreationTime": "2020-07-28T02:01:06Z",
        "DynamicImageId": "2b4e51df60*****323ef43d6e336ecf",
        "Height": "360",
        "Duration": "2",
        "Width": "640",
        "JobId": "2bf4390af9e54*****91c09cc720ad",
        "FileSize": "119866"
    }]
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/vod).


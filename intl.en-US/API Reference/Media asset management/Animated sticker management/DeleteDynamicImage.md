# DeleteDynamicImage

Deletes the information about animated stickers.

**Note:** This operation deletes only the information about animated stickers, but not the animated stickers themselves.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=DeleteDynamicImage&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteDynamicImage|The operation that you want to perform. Set the value to **DeleteDynamicImage**. |
|VideoId|String|Yes|2321077d460b\*\*\*\*\*028700ef6c2f4d|The ID of the video associated with the animated stickers whose information you want to delete. |
|DynamicImageIds|String|No|beafec3834\*\*\*\*\*a4e52ea52042a4,8281c8519847\*\*\*\*\*fd8970e79e80b6|The IDs of the animated stickers.

 **Note:**

-   Separate multiple IDs with commas \(,\). You can specify a maximum of 10 IDs.
-   If you do not set this parameter, the system finds the video specified by the VideoId parameter and deletes the information about the animated stickers associated with the video. If more than 10 animated stickers are associated with the video specified by the VideoId parameter, the deletion request is denied. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|0C8F0FDD-A99F-41\*\*\*\*\*88-B41934C97A54|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=DeleteDynamicImage
&VideoId=2321077d460b*****028700ef6c2f4d
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DeleteDynamicImageResponse>
      <RequestId>0C8F0FDD-A99F-41*****88-B41934C97A54</RequestId>
</DeleteDynamicImageResponse>
```

`JSON` format

```
{
    "RequestId":"0C8F0FDD-A99F-41*****88-B41934C97A54"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/vod).


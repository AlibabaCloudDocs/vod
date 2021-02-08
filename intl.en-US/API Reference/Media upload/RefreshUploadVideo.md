# RefreshUploadVideo

Obtains a new upload credential after the video upload times out.

**Note:** If you want to overwrite the video or audio mezzanine file, you can obtain the upload URL of the mezzanine file by calling this operation. Then, you can upload a new mezzanine file without changing the video or audio ID. However, the file overwriting may automatically trigger transcoding and snapshot jobs. For more information, see [Upload URLs and credentials](~~55397~~).

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=RefreshUploadVideo&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|RefreshUploadVideo|The operation that you want to perform. Set the value to **RefreshUploadVideo**. |
|VideoId|String|Yes|c6a23a870c8c4ffc\*\*\*\*\*d40cbd38133|The ID of the video. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|25818875-5F78-4A\*\*\*\*\*F6-D7393642CA58|The ID of the request. |
|UploadAuth|String|FJU3p3T\*\*\*\*\*Z0NUIyeW|The upload credential. |
|UploadAddress|String|eyJTZWN1cml0eVR\*\*\*\*\*iQ0FJU3p3TjFxNkZ0NUIyeW|The upload URL. |
|VideoId|String|c6a23a870c8c4ffc\*\*\*\*\*d40cbd38133|The ID of the video. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=RefreshUploadVideo
&VideoId=c6a23a870c8c4ffc*****d40cbd38133
&<Common request parameters>
```

Sample success responses

`XML` format

```
<RefreshUploadVideoResponse>
      <RequestId>25818875-5F78-4A*****F6-D7393642CA58</RequestId>
      <VideoId>c6a23a870c8c4ffc*****d40cbd38133</VideoId>
      <UploadAddress>eyJTZWN1cml0eVR*****iQ0FJU3p3TjFxNkZ0NUIyeW</UploadAddress>
      <UploadAuth>FJU3p3T*****Z0NUIyeW</UploadAuth>
</RefreshUploadVideoResponse>
```

`JSON` format

```
{
    "RequestId": "25818875-5F78-4A*****F6-D7393642CA58",
    "UploadAuth": "FJU3p3T*****Z0NUIyeW",
    "UploadAddress": "eyJTZWN1cml0eVR*****iQ0FJU3p3TjFxNkZ0NUIyeW",
    "VideoId":"c6a23a870c8c4ffc*****d40cbd38133"
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
|InvalidVideo.Damaged

|The video has been Damaged.

|400

|The error message returned because an error occurred during the video creation or the video was damaged. |
|InvalidVideo.NotFound

|The video not exist.

|404

|The error message returned because the video does not exist. |

## SDK examples

We recommend that you use [server SDKs](~~101789~~) to call this operation. You can view the sample code of different languages to call this operation by clicking the following links:

-   [Java](~~61063~~)
-   [Python](~~61054~~)
-   [PHP](~~61069~~)
-   [.NET](~~84750~~)
-   [Node.js](~~101396~~)
-   [Go](~~101411~~)
-   [C/C++](~~101261~~)


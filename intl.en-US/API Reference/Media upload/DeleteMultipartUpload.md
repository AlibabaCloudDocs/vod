# DeleteMultipartUpload

Immediately deletes the fragments generated during upload.

**Note:**

-   After a media file is uploaded, the fragments are automatically deleted.
-   The buckets allocated by ApsaraVideo VOD automatically delete the fragments after the fragments expire.
-   If you call the DeleteVideo operation, the fragment deletion is automatically triggered.
-   The DeleteMultipartUpload operation does not delete video mezzanine files and output files.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=DeleteMultipartUpload&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteMultipartUpload|The operation that you want to perform. Set the value to **DeleteMultipartUpload**. |
|MediaId|String|Yes|61ccbdb06fa\*\*\*\*\*3012be4d8083f6|The ID of the media file. |
|MediaType|String|Yes|video|The type of the media file. Set the value to **video**, which indicates audio and video files. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|25818875-5F78-4A\*\*\*\*\*F6-D7393642CA58|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=DeleteMultipartUpload
&MediaId=61ccbdb06fa*****3012be4d8083f6
&MediaType=video
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DeleteMultipartUploadResponse>
	  <RequestId>25818875-5F78-4A*****F6-D7393642CA58</RequestId>
</DeleteMultipartUploadResponse>
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
|InvalidParameter

|The specified parameter "MediaType" is invalid.

|400

|The error message returned because the MediaType parameter is invalid. |
|InvalidMultipartUpload.NotFound

|The multipart upload not exist.

|400

|The error message returned because the fragments do not exist. |
|InvalidVideo.NotFound

|The video does not exist.

|400

|The error message returned because the video ID does not exist. |
|InvalidFile.NotFound

|The file does not exist.

|400

|The error message returned because the video file does not exist. |
|InvalidStorage.NotFound

|can't find storage.

|400

|The error message returned because the specified storage location does not exist. |
|AccessDenied

|Access denied by authorizer's policy.

|400

|The error message returned because ApsaraVideo VOD is not authorized to access the self-managed Object Storage Service \(OSS\) bucket and you are not authorized to perform the operation. |


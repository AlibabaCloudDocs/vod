# DeleteVideo

Deletes one or more videos at a time, including their mezzanine files, transcoded stream files, and thumbnail snapshots.

**Note:** This operation physically deletes videos. Deleted videos cannot be recovered. Exercise caution when you call this operation.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=DeleteVideo&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteVideo|The operation that you want to perform. Set the value to **DeleteVideo**. |
|VideoIds|String|Yes|e44ebf114\*\*\*\*\*2d2adbea8bf5b5,e44ebf11\*\*\*\*\*adbea8bf55|The list of video IDs. Separate multiple IDs with commas \(,\). A maximum of 20 IDs can be specified. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|25818875-5F78-4A\*\*\*\*\*F6-D7393642CA58|The ID of the request. |
|ForbiddenVideoIds|List|73ab850b4f6f4\*\*\*\*\*b6e91d24d81d5|The IDs of the videos that cannot be deleted.

 **Note:** Generally, videos cannot be deleted if you do not have required [permissions](~~113600h~~). |
|NonExistVideoIds|List|93ab850b4f6f\*\*\*\*\*4b6e91d24d81d4|The IDs of the videos that do not exist. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=DeleteVideo
&VideoIds=e44ebf114*****2d2adbea8bf5b5,e44ebf11*****adbea8bf55
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DeleteVideoResponse>
      <RequestId>25818875-5F78-4A*****F6-D7393642CA58</RequestId>
      <NonExistVideoIds>73ab850b4f6f4*****b6e91d24d81d5</NonExistVideoIds>
      <UnRemoveableVideoIds>93ab850b4f6f*****4b6e91d24d81d4</UnRemoveableVideoIds>
</DeleteVideoResponse>
```

`JSON` format

```
{
    "RequestId": "25818875-5F78-4A*****F6-D7393642CA58",
    "NonExistVideoIds":"73ab850b4f6f4*****b6e91d24d81d5",
    "ForbiddenVideoIds":"93ab850b4f6f*****4b6e91d24d81d4"
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
|VideoIdsExceededMax

|The VideoIds exceeded maximum.

|400

|The error message returned because the list of video IDs exceeds the maximum length. |
|InvalidVideo.NotFound

|The video does not exist.

|404

|The error message returned because the video does not exist. |
|DeleteVideoFailed

|Deleting video has failed due to some unknown error.

|503

|The error message returned because the system failed to delete the video. Try again later. |

## SDK examples

We recommend that you use a [server SDK](~~101789~~) to call this operation. For more information about the sample code that is used to call this operation in various languages, see the following topics:

-   [Java](~~61063~~)
-   [Python](~~61054~~)
-   [PHP](~~61069~~)
-   [.NET](~~84750~~)
-   [Node.js](~~101396~~)
-   [Go](~~101411~~)
-   [C/C++](~~101261~~)


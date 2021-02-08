# DeleteStream

Deletes one or more video or audio streams and their storage files at a time.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=DeleteStream&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteStream|The operation that you want to perform. Set the value to **DeleteStream**. |
|JobIds|String|Yes|35eb4dbda18c4\*\*\*\*\*9cc0025df374b4|The job IDs for deleting media streams.

 -   Separate multiple IDs with commas \(,\). A maximum of 20 IDs can be specified for one video.
-   You can obtain job IDs from the PlayInfo parameter that is returned after you call the [GetPlayInfo](~~56124~~) operation. Each media stream has a unique job ID. |
|VideoId|String|Yes|e1e243b4254\*\*\*\*\*8248197d6f74f9|The ID of the video. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|25818875-5F78-4A\*\*\*\*\*F6-D7393642CA58|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=DeleteStream
&JobIds=35eb4dbda18c4*****9cc0025df374b4
&VideoId=e1e243b4254*****8248197d6f74f9
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DeleteStreamResponse>
      <RequestId>25818875-5F78-4A*****F6-D7393642CA58</RequestId>
</DeleteStreamResponse>
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
|JobIdsExceededMax

|The JobIds exceeded maximum.

|400

|The error message returned because the list of job IDs exceeds the maximum length. |
|InvalidVideo.NotFound

|The video does not exist.

|404

|The error message returned because the video does not exist. |
|InvalidStream.NotFound

|The stream does not exist.

|404

|The error message returned because the media stream does not exist. |
|DeleteStreamFailed

|Deleting stream has failed due to some unknown error.

|503

|The error message returned because the system failed to delete the media stream. Try again later. |

## SDK examples

We recommend that you use a [server SDK](~~101789~~) to call this operation. For more information about the sample code that is used to call this operation in various languages, see the following topics:

-   [Java](~~61063~~)
-   [Python](~~61054~~)
-   [PHP](~~61069~~)
-   [.NET](~~84750~~)
-   [Node.js](~~101396~~)
-   [Go](~~101411~~)
-   [C/C++](~~101261~~)


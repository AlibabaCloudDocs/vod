# CreateAudit

Performs manual review on media files, such as audio and video files.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=CreateAudit&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateAudit|The operation that you want to perform. Set the value to **CreateAudit**. |
|AuditContent|String|Yes|\[\{"VideoId":"93ab850b4f\*\*\*\*\*b54b6e91d24d81d4","Status":"Normal"\},\{"VideoId":"f867fbfb58\*\*\*\*\*8bbab65c4480ae1d","Status":"Blocked","Reason":"Pornographic video","Comment":"Contains nudity"\}\]|The array of the review content.

You can specify a maximum of **20** videos to be reviewed. The array must be converted into a string as the value of this parameter.

For more information about the parameters in AuditContent, see the **AuditContent** section of this topic. |

## AuditContent

|Parameter

|Type

|Required

|Description |
|-----------|------|----------|-------------|
|VideoId

|String

|Yes

|The ID of the video. |
|Status

|String

|Yes

|The review status of the video. Value values: **Blocked** and **Normal**. |
|Reason

|String

|No

|The reason for blocking the video if the Status parameter is set to Blocked. The reason can be up to 128 bytes in length. |
|Comment

|String

|No

|The review comment. The comment can be up to 512 bytes in length. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|25818875-5F78-4A\*\*\*\*\*F6-D7393642CA58|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=CreateAudit
&AuditContent=[{"VideoId":"93ab850b4f*****b54b6e91d24d81d4","Status":"Normal"},{"VideoId":"f867fbfb58*****8bbab65c4480ae1d","Status":"Blocked","Reason":"Pornographic video","Comment":"Contains nudity"}]
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateAuditResponse>
      <RequestId>25818875-5F78-4A*****F6-D7393642CA58</RequestId>
</CreateAuditResponse>
```

`JSON` format

```
{
    "RequestId": "25818875-5F78-4A*****F6-D7393642CA58"
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


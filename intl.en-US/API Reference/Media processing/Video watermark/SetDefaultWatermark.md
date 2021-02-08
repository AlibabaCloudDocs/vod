# SetDefaultWatermark

Specifies a watermark as the default one.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=SetDefaultWatermark&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SetDefaultWatermark|The operation that you want to perform. Set the value to **SetDefaultWatermark**. |
|WatermarkId|String|Yes|9bcc8bfadb843f\*\*\*\*\*09a2671d0df97|The ID of the watermark. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|25818875-5F78-4A\*\*\*\*\*F6-D7393642CA58|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=SetDefaultWatermark
&WatermarkId=9bcc8bfadb843f*****09a2671d0df97
&<Common request parameters>
```

Sample success responses

`XML` format

```
<SetDefaultWatermarkResponse>
      <RequestId>25818875-5F78-4A*****F6-D7393642CA58</RequestId>
</SetDefaultWatermarkResponse>
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
|NoSuchResource

|The specified resource %s does not exist.

|404

|The error message returned because the user-related resource does not exist. %s indicates the specific resource information. |

## SDK examples

We recommend that you use [server SDKs](~~101789~~) to call this operation. You can view the sample code of different languages to call this operation by clicking the following links:

-   [Java](~~61063~~)
-   [Python](~~61054~~)
-   [PHP](~~61069~~)
-   [.NET](~~84750~~)
-   [Node.js](~~101396~~)
-   [Go](~~101411~~)
-   [C/C++](~~101261~~)


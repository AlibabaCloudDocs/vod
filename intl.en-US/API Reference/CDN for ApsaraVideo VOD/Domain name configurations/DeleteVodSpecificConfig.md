# DeleteVodSpecificConfig

Deletes the configurations of a domain name for CDN.

**Note:**

-   This operation is available only in the **China \(Shanghai\)** region.
-   After the configurations of a domain name for CDN are deleted, the domain name becomes unavailable. We recommend that you restore the A record at your DNS service provider before you delete the configurations of the domain name for CDN.
-   After you call this operation to delete the configurations of a domain name for CDN, all records that are related to the domain name are deleted. If you only want to disable a domain name for CDN, call the [BatchStopVodDomain](~~120208~~) operation.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=DeleteVodSpecificConfig&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteVodSpecificConfig|The operation that you want to perform. Set the value to **DeleteVodSpecificConfig**. |
|ConfigId|String|Yes|2317\*\*\*\*|The ID of the configuration. |
|DomainName|String|Yes|www.example.com|The domain name for CDN. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|04F0F334-1335-436C-\*\*\*\*-6C044FE73368|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=DeleteVodSpecificConfig
&ConfigId=2317****
&DomainName=www.example.com
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DeleteVodSpecificConfigResponse>
  <RequestId>04F0F334-1335-436C-****-6C044FE73368</RequestId>
</DeleteVodSpecificConfigResponse>
```

`JSON` format

```
{
    "RequestId": "04F0F334-1335-436C-****-6C044FE73368"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/vod).

The following table describes the common errors that this operation can return. For more information about errors common to all operations, see [Common errors](~~52841~~).

|Error code

|Error message

|HTTP status code

|Description |
|------------|---------------|------------------|-------------|
|MissingParameter

|The specified value of parameter DomainName can not be empty.

|400

|The error message returned because the DomainName parameter is not specified.

| |
|MissingParameter

|The specified value of parameter ConfigId can not be empty.

|400

|The error message returned because the ConfigId parameter is not specified.

| |
|Invalid%s.ValueNotSupported

|FunctionName \[%s\] is not supported.

|400

|The error message returned because the value of the FunctionName parameter is invalid.

| |


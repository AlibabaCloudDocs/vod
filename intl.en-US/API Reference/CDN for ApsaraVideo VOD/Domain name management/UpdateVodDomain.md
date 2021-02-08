# UpdateVodDomain

Modifies a specified domain name for CDN.

**Note:** This operation is available only in the **China \(Shanghai\)** region.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=UpdateVodDomain&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|UpdateVodDomain|The operation that you want to perform. Set the value to **UpdateVodDomain**. |
|DomainName|String|Yes|example.com|The domain name for CDN. |
|Sources|String|No|\[\{"content":"1.1.1.1","type":"ipaddr","priority":"20","port":80\}\]|The information about the address of the origin server. |
|TopLevelDomain|String|No|example.com|The top-level domain name. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|15C66C7B-671A-4297-\*\*\*\*-2C4477247A74|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=UpdateVodDomain
&DomainName=example.com
&<Common request parameters>
```

Sample success responses

`XML` format

```
<UpdateVodDomainResponse>
  <RequestId>15C66C7B-671A-4297-****-2C4477247A74</RequestId>
</UpdateVodDomainResponse>
```

`JSON` format

```
{
  "RequestId": "15C66C7B-671A-4297-****-2C4477247A74"
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
|InvalidDomainName.Malformed

|Specified DomainName is malformed.

|400

|The error message returned because the value of the DomainName parameter is invalid.

| |
|InvalidSource.Content.Malformed

|Specified source content is malformed.

|400

|The error message returned because the origin address is invalid.

| |
|InvalidSource.Type.Malformed

|Specified source type is malformed.

|400

|The error message returned because the origin type is invalid.

| |
|InvalidTypeContent.Mismatch

|Specified source type does not math the specified source content.

|400

|The error message returned because the origin address does not match the origin type.

| |
|InvalidSource.Priority.Malformed

|Specified source priority is malformed.

|400

|The error message returned because the priority is invalid.

| |
|InvalidScope.Malformed

|Specified Scope is malformed.

|400

|The error message returned because the value of the Scope parameter is invalid.

| |
|IllegalOperation

|Illegal domain operate is not permitted.

|403

|The error message returned because you are not authorized to perform this operation.

| |
|InvalidDomain.NotFound

|The domain provided does not belong to you.

|404

|The error message returned because the domain name does not exist or does not belong to you.

| |


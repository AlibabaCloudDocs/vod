# BatchStartVodDomain

Enables one or more domain names for CDN that are disabled.

**Note:**

-   This operation is available only in the **China \(Shanghai\)** region.
-   If the domain name that you want to enable is invalid or your Alibaba Cloud account has overdue payments, you cannot call this operation to enable the domain name.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=BatchStartVodDomain&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|BatchStartVodDomain|The operation that you want to perform. Set the value to **BatchStartVodDomain**. |
|DomainNames|String|Yes|example.com|The domain name for CDN. Separate multiple domain names with commas \(,\). |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|15C66C7B-671A-4297-\*\*\*\*-2C4477247A74|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=BatchStartVodDomain
&DomainNames=example.com
&<Common request parameters>
```

Sample success responses

`XML` format

```
<BatchStartVodDomainResponse>
      <RequestId>15C66C7B-671A-4297-****-2C4477247A74</RequestId>
</BatchStartVodDomainResponse>
```

`JSON` format

```
{
  "RequestId": "15C66C7B-671A-4297-****-2C4477247A74"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/vod).


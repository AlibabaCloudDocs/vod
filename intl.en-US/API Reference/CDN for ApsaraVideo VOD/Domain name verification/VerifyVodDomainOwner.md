# VerifyVodDomainOwner

Verifies the ownership of a specified domain name.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=VerifyVodDomainOwner&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|VerifyVodDomainOwner|The operation that you want to perform. Set the value to **VerifyVodDomainOwner**. |
|DomainName|String|Yes|example.com|The domain name of which you want to verify the ownership. You can specify only one domain name in each call. |
|VerifyType|String|Yes|dnsCheck|The DNS verification method that is used to verify the ownership of the specified domain name. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Content|String|verify\_dffeb661\*\*\*\*\*\*\*\*\*a59c32cd91f|The verification content. |
|RequestId|String|34AB41F1-04A5-\*\*\*\*\*\*\*\*\*-634BDBE6A9FB|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=VerifyVodDomainOwner
&DomainName=example.com
&VerifyType=dnsCheck
&<Common request parameters>
```

Sample success responses

`XML` format

```
<VerifyVodDomainOwnerResponse>
  <Content>verify_dffeb661*********a59c32cd91f</Content>
  <RequestId>34AB41F1-04A5-*********-634BDBE6A9FB</RequestId>
</VerifyVodDomainOwnerResponse>
```

`JSON` format

```
{
  "Content": "verify_dffeb661*********a59c32cd91f",
  "RequestId": "34AB41F1-04A5-*********-634BDBE6A9FB"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/vod).


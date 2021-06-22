# DescribeVodVerifyContent

Queries the ownership verification content.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=DescribeVodVerifyContent&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeVodVerifyContent|The operation that you want to perform. Set the value to **DescribeVodVerifyContent**. |
|DomainName|String|Yes|example.com|The domain name for which you want to query the ownership verification content. You can specify only one domain name in each call. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Content|String|verify\_dffeb661\*\*\*\*\*3a59c31cd91f|The verification content. |
|RequestId|String|34AB41F1-04A5-\*\*\*\*\*-634BDBE6A9FB|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=DescribeVodVerifyContent
&DomainName=example.com
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeVodVerifyContentResponse>
  <Content>verify_dffeb661*****3a59c31cd91f</Content>
  <RequestId>34AB41F1-04A5-*****-634BDBE6A9FB</RequestId>
</DescribeVodVerifyContentResponse>
```

`JSON` format

```
{
  "Content": "verify_dffeb661*****3a59c31cd91f",
  "RequestId": "34AB41F1-04A5-*****-634BDBE6A9FB"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/vod).


# DescribeVodRefreshQuota

Queries the maximum number and remaining number of requests to refresh or prefetch files on the current day. You can prefetch files based on URLs and refresh files based on URLs or directories.

**Note:**

-   This operation is available only in the **China \(Shanghai\)** region.
-   You can call the [RefreshVodObjectCaches](~~69215~~) operation to refresh content and the [PreloadVodObjectCaches](~~69211~~) operation to prefetch content.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=DescribeVodRefreshQuota&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeVodRefreshQuota|The operation that you want to perform. Set the value to **DescribeVodRefreshQuota**. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|BlockQuota|String|500|The maximum number of Object Storage Service \(OSS\) buckets that can be refreshed each day. |
|DirQuota|String|100|The maximum number of directories of files that can be refreshed each day. |
|DirRemain|String|99|The remaining number of directories of files that can be refreshed on the current day. |
|PreloadQuota|String|500|The maximum number of URLs of files that can be prefetched each day. |
|PreloadRemain|String|500|The remaining number of URLs of files that can be prefetched on the current day. |
|RequestId|String|42E0554B-80F4-4921-\*\*\*\*-ACFB22CAAAD0|The ID of the request. |
|UrlQuota|String|2000|The maximum number of URLs of files that can be refreshed each day. |
|UrlRemain|String|1996|The remaining number of URLs of files that can be refreshed on the current day. |
|blockRemain|String|500|The remaining number of OSS buckets that can be refreshed on the current day. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=DescribeVodRefreshQuota
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeVodRefreshQuotaResponse>
      <DirQuota>100</DirQuota>
      <DirRemain>99</DirRemain>
      <RequestId>A56FC7F8-CA97-482E-****-F77C2135BD22</RequestId>
      <UrlQuota>2000</UrlQuota>
      <UrlRemain>1996</UrlRemain>
      <PreloadQuota>500</PreloadQuota>
      <PreloadRemain>500</PreloadRemain>
</DescribeVodRefreshQuotaResponse>
```

`JSON` format

```
{
    "DirQuota": "100",
    "DirRemain": "99",
    "RequestId": "42E0554B-80F4-4921-****-ACFB22CAAAD0",
    "UrlQuota": "2000",
    "UrlRemain": "1996",
    "PreloadQuota":"500",
    "PreloadRemain":"500"
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
|Throttling

|Request was denied due to request throttling.

|503

|The error message returned because the request was denied due to throttling. |
|OperationDenied

|Your account does not open VOD service yet.

|403

|The error message returned because ApsaraVideo VOD has not been activated for your Alibaba Cloud account. |
|OperationDenied.Suspended

|Your VOD service is suspended.

|403

|The error message returned because your Alibaba Cloud account has overdue payments. Add funds to your account. |


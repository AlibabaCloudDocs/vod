# PreloadVodObjectCaches

Prefetches resources from an origin server to L2 nodes. Users can directly hit the cache upon their first visits. This way, workloads on the origin server can be reduced.

**Note:**

-   This operation is available only in the **China \(Shanghai\)** region.
-   You can submit a maximum of 500 requests to prefetch resources based on URLs each day by using an Alibaba Cloud account. You cannot prefetch resources based on directories.
-   You can call the [RefreshVodObjectCaches](~~69215~~) operation to refresh content and the [PreloadVodObjectCaches](~~69211~~l) operation to prefetch content.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=PreloadVodObjectCaches&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|PreloadVodObjectCaches|The operation that you want to perform. Set the value to **PreloadVodObjectCaches**. |
|ObjectPath|String|Yes|vod.test.com/test.txt|The URL of the file to be prefetched. Separate multiple URLs with line breaks \(\\n or \\r\\n\). |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PreloadTaskId|String|9524\*\*\*\*|The ID of the prefetch task. Separate multiple task IDs with commas \(,\). |
|RequestId|String|E5BD4B50-7A02-493A-\*\*\*\*\*-97B9024B4135|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=PreloadVodObjectCaches
&ObjectPath=vod.test.com/test.txt
&<Common request parameters>
```

Sample success responses

`XML` format

```
<PreloadVodObjectCachesResponse>
    <PreloadTaskId>9525****</PreloadTaskId>
    <RequestId>5FF9B16E-FBAC-48E5-****-65B5F0184DB3</RequestId>
</PreloadVodObjectCachesResponse>
```

`JSON` format

```
{
  "PreloadTaskId": "9524****",
  "RequestId": "E5BD4B50-7A02-493A-****-97B9024B4135"
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
|IllegalOperation

|Illegal domain operate is not permitted.

|403

|The error message returned because the domain name is invalid. |
|OperationDenied

|Your account does not open VOD service yet.

|403

|The error message returned because ApsaraVideo VOD has not been activated for your Alibaba Cloud account. |
|OperationDenied.Suspended

|Your VOD service is suspended.

|403

|The error message returned because your Alibaba Cloud account has overdue payments. Add funds to your account. If you do not settle your overdue payments within 15 days, you must re-activate ApsaraVideo VOD after you settle all the overdue payments. |
|InvalidDomain.NotFound

|The domain provided does not belong to you.

|404

|The error message returned because the domain name does not exist or does not belong to you. |
|InvalidDomain.Offline

|The domain provided is offline.

|404

|The error message returned because the domain name has been disabled. |
|QuotaExceeded.Refresh

|You’ve exceeded the prescribed refresh limits.

|400

|The error message returned because the number of requests to refresh or prefetch the content exceeds the upper limit on the current day. |
|PreloadQueueFull

|Preload queue is full, please try again later!

|403

|The error message returned because the number of URLs of the files being prefetched has reached the upper limit. Try again later. |
|InvalidDomain.Configure\_failed

|Failed to configure the provided domain.

|500

|The error message returned because the system failed to configure the domain name and cannot refresh or prefetch the content. |
|MissingParameter

|The input parameter “ObjectPath” that is mandatory for processing this request is not supplied.

|400

|The error message returned because the ObjectPath parameter is not specified. |
|InvalidObjectPath.Malformed

|The specific value of parameter ObjectPath is malformed.

|400

|The error message returned because the value of the ObjectPath parameter is in an invalid format. |
|InvalidExtensiveDomain.ValueNotSupported

|Extensive domain not supported.

|400

|The error message returned because the domain name contains a wildcard character. |
|InvalidObjectPath.Size.Malformed

|The size of ObjectPath is bigger than 1000.

|400

|The error message returned because a maximum of 1,000 URLs of files can be prefetched at a time. |


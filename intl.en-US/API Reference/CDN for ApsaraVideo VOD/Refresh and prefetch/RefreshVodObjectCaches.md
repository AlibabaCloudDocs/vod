# RefreshVodObjectCaches

Refreshes files on Alibaba Cloud CDN nodes. You can refresh multiple files at a time based on URLs.

**Note:**

-   This operation is available only in the **China \(Shanghai\)** region.
-   You can submit a maximum of 2,000 requests to refresh resources based on URLs and 100 requests to refresh resources based on directories each day by using an Alibaba Cloud account.
-   You can call the [RefreshVodObjectCaches](~~69215~~) operation to refresh content and the [PreloadVodObjectCaches](~~69211~~) operation to prefetch content.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=RefreshVodObjectCaches&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|RefreshVodObjectCaches|The operation that you want to perform. Set the value to **RefreshVodObjectCaches**. |
|ObjectPath|String|Yes|abc.com/image/1.png|The path of the resource to be refreshed. Separate multiple paths with line breaks \(\\n or \\r\\n\). |
|ObjectType|String|No|File|The granularity of the resources to be refreshed. Valid values:

 -   **File**: refreshes one or more files. This is the default value.
-   **Directory**: refreshes the files under one or more directories. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RefreshTaskId|String|70422\*\*\*\*\*2904|The ID of the refresh task. Separate multiple task IDs with commas \(,\). |
|RequestId|String|D61E4801-EAFF-4A63-\*\*\*\*-FBF6CE1CFD1C|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=RefreshVodObjectCaches
&ObjectPath=abc.com/image/1.png
&<Common request parameters>
```

Sample success responses

`XML` format

```
<RefreshVodObjectCachesResponse>
      <RefreshTaskId>70422*****2904</RefreshTaskId>
      <RequestId>D61E4801-EAFF-4A63-****-FBF6CE1CFD1C</RequestId>
</RefreshVodObjectCachesResponse>
```

`JSON` format

```
{
  "RefreshTaskId":"70422*****2904",
  "RequestId":"D61E4801-EAFF-4A63-****-FBF6CE1CFD1C"
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

|The error message returned because your Alibaba Cloud account has overdue payments. Add funds to your account. |
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
|ServiceBusy

|The specified Domain is configuring, please retry later.

|403

|The error message returned because the domain name is being configured. Try again later. |
|InvalidDomain.Configure\_failed

|Failed to configure the provided domain.

|500

|The error message returned because the system failed to configure the domain name and cannot refresh or prefetch the content. |
|MissingParameter

|The input parameter “ObjectPath” that is mandatory for processing this request is not supplied.

|400

|The error message returned because the ObjectPath parameter is not specified. |
|InvalidObjectType.ValueNotSupported

|The specified value of "<ObjectType\>" is not supported.

|400

|The error message returned because the value of the ObjectType parameter is invalid. |
|InvalidObjectPath.Malformed

|The specific value of parameter ObjectPath is malformed.

|400

|The error message returned because the value of the ObjectPath parameter is in an invalid format. |
|InvalidExtensiveDomain.ValueNotSupported

|Extensive domain not supported.

|400

|The error message returned because the domain name contains a wildcard character. |
|QuotaPerMinuteExceeded.Refresh

|You’ve exceeded the prescribed refresh limits per minute.

|400

|The error message returned because the number of requests to refresh the content exceeds the upper limit per minute. |


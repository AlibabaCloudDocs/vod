# DescribeVodDomainUsageData

Queries the traffic or bandwidth data for one or more domain names for CDN.

**Note:**

-   This operation is available only in the **China \(Shanghai\)** region.
-   You can specify a maximum of 100 domain names for CDN at a time. Separate them with commas \(,\). If you do not specify a domain name for CDN, the data of all domain names for CDN within your Alibaba Cloud account is returned.
-   You can query data for the past one year at most and query data for a maximum of three months per request. If you query data for one to three days, the system returns the statistics collected on an hourly basis. If you query data for four days or more, the system returns the statistics collected on a daily basis.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=DescribeVodDomainUsageData&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeVodDomainUsageData|The operation that you want to perform. Set the value to **DescribeVodDomainUsageData**. |
|EndTime|String|Yes|2015-12-10T12:20:00Z|The end of the time range to query. The end time must be later than the start time. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC. |
|Field|String|Yes|bps|The type of the data to be queried. Valid values:

 -   **bps**: bandwidth.
-   **traf**: traffic. |
|StartTime|String|Yes|2015-12-10T10:20:00Z|The beginning of the time range to query. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC. |
|DomainName|String|No|example.com|The domain name for CDN. If you do not specify this parameter, the merged data of all your domain names for CDN is returned. You can specify multiple domain names. Separate them with commas \(,\). |
|Type|String|No|static|The type of the content based on which the data is generated. Valid values:

 -   **static**

 -   **dynamic**
-   **all** |
|Area|String|No|CN|The region where the data is queried. The default value is CN, which indicates mainland China. Valid values:

 -   **CN**: mainland China.
-   **OverSeas**: outside mainland China. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Area|String|CN|The region where the data was queried. |
|DataInterval|String|300|The time interval between the returned entries. Unit: seconds. |
|DomainName|String|example.com|The domain name for CDN. |
|EndTime|String|2015-12-10T12:20:00Z|The end of the time range in which data was queried. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|RequestId|String|B955107D-E658-4E77-\*\*\*\*-E0AC3D31693E|The ID of the request. |
|StartTime|String|2015-12-10T10:20:00Z|The beginning of the time range in which data was queried. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|Type|String|static|The type of the content based on which the data is generated. Valid values:

 -   **static**

 -   **dynamic**
-   **all** |
|UsageDataPerInterval|Array of DataModule| |The details of traffic or bandwidth data. |
|DataModule| | | |
|TimeStamp|String|2015-12-10T10:00:00Z|The timestamp of the returned data. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|Value|String|2592.3920000000003|The traffic or bandwidth data. The unit of bandwidth is bit/s. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=DescribeVodDomainUsageData
&EndTime=2015-12-10T12:20:00Z
&Field=bps
&StartTime=2015-12-10T10:20:00Z
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeVodDomainUsageDataResponse>
      <RequestId>B955107D-E658-4E77-****-E0AC3D31693E</RequestId>
      <StartTime>2015-12-10T10:20:00Z</StartTime>
      <EndTime>2015-12-10T12:21:00Z</EndTime>
      <Area>CN</Area>
      <Type>static</Type>
      <DomainName>example.com</DomainName>
      <DataInterval>300</DataInterval>
      <UsageDataPerInterval>
            <UsageData>
                  <TimeStamp>2015-12-10T11:00:00Z</TimeStamp>
                  <Value>2592.3920000000003</Value>
            </UsageData>
            <UsageData>
                  <TimeStamp>2015-12-10T11:05:00Z</TimeStamp>
                  <Value>2592.3920000000003</Value>
            </UsageData>
      </UsageDataPerInterval>
</DescribeVodDomainUsageDataResponse>
```

`JSON` format

```
{
    "DescribeVodDomainUsageDataResponse": {
        "RequestId": "B955107D-E658-4E77-****-E0AC3D31693E",
        "StartTime": "2015-12-10T10:20:00Z",
        "EndTime": "2015-12-10T12:21:00Z",
        "Area": "CN",
        "Type": "static",
        "DomainName": "example.com",
        "DataInterval": 300,
        "UsageDataPerInterval": {
            "UsageData": [
                {
                    "TimeStamp": "2015-12-10T11:00:00Z",
                    "Value": 2592.3920000000003
                },
                {
                    "TimeStamp": "2015-12-10T11:05:00Z",
                    "Value": 2592.3920000000003
                }
            ]
        }
    }
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

|Illegal domain, operation is not permitted.

|403

|The error message returned because the domain name is invalid. |
|OperationDenied

|Your account does not open CDN service yet.

|403

|The error message returned because Alibaba Cloud CDN has not been activated for your Alibaba Cloud account. |
|OperationDenied

|Your CDN service is suspended.

|403

|The error message returned because Alibaba Cloud CDN has been suspended for your Alibaba Cloud account. |
|InvalidDomain.NotFound

|The domain provided does not belong to you.

|404

|The error message returned because the specified CDN domain does not exist or does not belong to you. |
|InvalidDomain.Offline

|The domain provided is offline.

|404

|The error message returned because the domain name has been disabled. |
|ServiceBusy

|The specified Domain is configuring, please retry later.

|403

|The error message returned because the domain name is being configured. Try again later. |
|InvalidDomain.Configure\_failed

|Failed to configure the provided domain.

|500

|The error message returned because the system failed to configure the domain name. |
|InvalidParameter

|Invalid Parameter.

|400

|The error message returned because one or more parameters are invalid. |
|InvalidParameterProduct

|Invalid Parameter Product.

|400

|The error message returned because the value of the Product parameter is invalid. |
|InvalidParameterArea

|Invalid Parameter Area.

|400

|The error message returned because the value of the Area parameter is invalid. |
|InvalidParameterField

|Invalid Parameter Field.

|400

|The error message returned because the value of the Field parameter is invalid. |
|InvalidParameterStartTime

|Invalid Parameter StartTime.

|400

|The error message returned because the value of the StartTime parameter is invalid. |
|InvalidParameterEndTime

|Invalid Parameter EndTime.

|400

|The error message returned because the value of the EndTime parameter is invalid. |
|InvalidTimeRange

|StartTime and EndTime range should less than 1 month.

|400

|The error message returned because the time range that is specified by the StartTime and EndTime parameters exceeds 31 days. |
|InvalidParameterInterval

|Invalid Parameter Interval.

|400

|The error message returned because the value of the Interval parameter is invalid.

|. |


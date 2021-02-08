# DescribeVodDomainTrafficData

Queries the network traffic for one or more specified domain names for CDN.

**Note:** If you specify neither the StartTime parameter nor the EndTime parameter, the data in the last 24 hours is queried. Alternatively, you can specify both the StartTime and EndTime parameters to query data that is generated in the specified duration. You can query data for the last 90 days at most.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=DescribeVodDomainTrafficData&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeVodDomainTrafficData|The operation that you want to perform. Set the value to **DescribeVodDomainTrafficData**. |
|DomainName|String|No|example.com|The domain name to be queried. If you do not specify this parameter, the merged data of all your domain names for CDN is returned. You can specify multiple domain names. Separate them with commas \(,\). |
|StartTime|String|No|2019-01-20T13:59:58Z|The beginning of the time range to query. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC.

 **Note:** The minimum query interval is 5 minutes. If you do not specify this parameter, the data in the last 24 hours is queried. |
|EndTime|String|No|2019-01-20T14:59:58Z|The end of the time range to query. The end time must be later than the start time. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC. |
|Interval|String|No|300|The query interval. Unit: seconds. Valid values: **300**, **3600**, and **86400**. If you do not specify this parameter or the specified value is invalid, the default value is used.

 -   If the time range to query is less than 3 days, valid values are **300**, **3600**, and **86400**. The default value is 300.
-   If the time range to query is from 3 to less than 31 days, valid values are **3600** and **86400**. The default value is 3600.
-   If the time range to query is from 31 to 90 days, the valid value is **86400**. |
|IspNameEn|String|No|Alibaba|The name of the Internet service provider \(ISP\). If you do not specify this parameter, the data of all ISPs is returned. |
|LocationNameEn|String|No|cn-shanghai|The name of the region. If you do not specify this parameter, the data in all regions is returned. Only data in the China \(Shanghai\) region can be queried. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|DataInterval|String|3600|The time interval between the returned entries. Unit: seconds. |
|DomainName|String|example.com|The domain name for CDN. |
|EndTime|String|2019-01-20T14:59:58Z|The end of the time range in which data was queried. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|RequestId|String|D94E471F-1A27-442E-\*\*\*\*-D4D2000CB492|The ID of the request. |
|StartTime|String|2019-01-20T13:59:58Z|The beginning of the time range in which data was queried. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|TrafficDataPerInterval|Array of DataModule| |The network traffic data that is collected for each interval. |
|DataModule| | | |
|DomesticValue|String|0|The volume of the network traffic in mainland China. Unit: byte. |
|HttpsDomesticValue|String|0|The volume of the HTTPS network traffic on L1 nodes in mainland China. Unit: byte. |
|HttpsOverseasValue|String|0|The volume of the HTTPS network traffic on L1 nodes outside mainland China. Unit: byte. |
|HttpsValue|String|0|The total volume of the HTTPS network traffic on L1 nodes. Unit: byte. |
|OverseasValue|String|0|The volume of the network traffic outside mainland China. Unit: byte. |
|TimeStamp|String|2019-01-15T19:00:00Z|The timestamp of the returned data. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|Value|String|0|The total volume of the network traffic. Unit: byte. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=DescribeVodDomainTrafficData
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeVodDomainTrafficDataResponse>
      <RequestId>D94E471F-1A27-442E-****-D4D2000CB492</RequestId>
      <EndTime>2019-01-20T14:59:58Z</EndTime>
      <TrafficDataPerInterval>
            <DataModule>
                  <OverseasValue>0</OverseasValue>
                  <HttpsValue>0</HttpsValue>
                  <Value>0</Value>
                  <HttpsDomesticValue>0</HttpsDomesticValue>
                  <HttpsOverseasValue>0</HttpsOverseasValue>
                  <TimeStamp>2019-01-15T14:00:00Z</TimeStamp>
                  <DomesticValue>0</DomesticValue>
            </DataModule>
            <DataModule>
                  <OverseasValue>0</OverseasValue>
                  <HttpsValue>0</HttpsValue>
                  <Value>0</Value>
                  <HttpsDomesticValue>0</HttpsDomesticValue>
                  <HttpsOverseasValue>0</HttpsOverseasValue>
                  <TimeStamp>2019-01-15T14:00:00Z</TimeStamp>
                  <DomesticValue>0</DomesticValue>
            </DataModule>
      </TrafficDataPerInterval>
      <DomainName>example.com</DomainName>
      <DataInterval>3600</DataInterval>
      <StartTime>2019-01-15T13:59:59Z</StartTime>
</DescribeVodDomainTrafficDataResponse>
```

`JSON` format

```
{
    "RequestId":"D94E471F-1A27-442E-****-D4D2000CB492",
    "EndTime":"2019-01-20T14:59:58Z",
    "TrafficDataPerInterval":{
        "DataModule":[
            {
                "OverseasValue":0,
                "HttpsValue":0,
                "Value":0,
                "HttpsDomesticValue":0,
                "HttpsOverseasValue":0,
                "TimeStamp":"2019-01-15T14:00:00Z",
                "DomesticValue":0
            },
            {
                "OverseasValue":0,
                "HttpsValue":0,
                "Value":0,
                "HttpsDomesticValue":0,
                "HttpsOverseasValue":0,
                "TimeStamp":"2019-01-15T14:00:00Z",
                "DomesticValue":0
            }
        ]
    },
    "DomainName":"example.com",
    "DataInterval":3600,
    "StartTime":"2019-01-15T13:59:59Z"
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

|The error message returned because the domain name does not exist or does not belong to you. |
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
|MissingParameter

|StartTime and EndTime can not be single.

|400

|The error message returned because the StartTime and EndTime parameters have not been specified at the same time. |
|InvalidStartTime.Malformed

|Specified start time is malformed.

|400

|The error message returned because the format of the start time is invalid. |
|InvalidEndTime.Malformed

|Specified end time is malformed.

|400

|The error message returned because the format of the end time is invalid. |
|InvalidEndTime.Mismatch

|Specified end time does not match the specified start time.

|400

|The error message returned because the end time is earlier than the start time. |
|InvalidStartTime.ValueNotSupported

|Specified end time does not match the specified start time.

|400

|The error message returned because the time range that is specified by the EndTime and StartTime parameters exceeds 90 days. |


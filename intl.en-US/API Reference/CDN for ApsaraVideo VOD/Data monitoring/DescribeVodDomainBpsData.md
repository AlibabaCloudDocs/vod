# DescribeVodDomainBpsData

Queries the bandwidth for one or more specified domain names for CDN.

**Note:** If you specify neither the StartTime parameter nor the EndTime parameter, the data in the last 24 hours is queried. Alternatively, you can specify both the StartTime and EndTime parameters to query data that is generated in the specified duration. You can query data for the last 90 days at most.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=DescribeVodDomainBpsData&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeVodDomainBpsData|The operation that you want to perform. Set the value to **DescribeVodDomainBpsData**. |
|DomainName|String|No|example.com|The domain name to be queried. If you do not specify this parameter, the merged data of all your domain names for CDN is returned. You can specify multiple domain names. Separate them with commas \(,\). |
|StartTime|String|No|2015-12-10T13:00:00Z|The beginning of the time range to query. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC.

 **Note:** The minimum query interval is 5 minutes. If you do not specify this parameter, the data in the last 24 hours is queried. |
|EndTime|String|No|2015-12-10T14:00:00Z|The end of the time range to query. The end time must be later than the start time. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC. |
|Interval|String|No|300|The query interval. Unit: seconds. Valid values: **300**, **3600**, and **86400**.

 -   If the time range to query is less than 3 days, valid values are **300**, **3600**, and **86400**. The default value is 300.
-   If the time range to query is from 3 to less than 31 days, valid values are **3600** and **86400**. The default value is 3600.
-   If the time range to query is from 31 to 90 days, the valid value is **86400**. |
|IspNameEn|String|No|Alibaba|The name of the Internet service provider \(ISP\). If you do not specify this parameter, the data of all ISPs is returned. |
|LocationNameEn|String|No|cn-shanghai|The name of the region. If you do not specify this parameter, the data in all regions is returned. Only data in the China \(Shanghai\) region can be queried. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|BpsDataPerInterval|Array of DataModule| |The bandwidth data that is collected for each interval. |
|DataModule| | | |
|DomesticValue|String|11286111|The bandwidth in mainland China. Unit: bit/s. When the bandwidth data is queried by ISP, no value is returned. |
|HttpsDomesticValue|String|11286111|The HTTPS bandwidth on L1 nodes in mainland China. Unit: bit/s. When the bandwidth data is queried by ISP, no value is returned. |
|HttpsOverseasValue|String|2000|The HTTPS bandwidth on L1 nodes outside mainland China. Unit: bit/s. When the bandwidth data is queried by ISP, no value is returned. |
|HttpsValue|String|11288111|The total HTTPS bandwidth on L1 nodes. Unit: bit/s. |
|OverseasValue|String|2000|The bandwidth outside mainland China. Unit: bit/s. When the bandwidth data is queried by ISP, no value is returned. |
|TimeStamp|String|2015-12-10T13:00:00Z|The timestamp of the returned data. The time follows the ISO 8601 standard in the yyyy-MM-ddTHH:mm:ssZ format. The time is displayed in UTC. |
|Value|String|11288111|The bandwidth. Unit: bit/s. |
|DataInterval|String|300|The time interval between the returned entries. Unit: seconds. |
|DomainName|String|example.com|The domain name for CDN. |
|EndTime|String|2015-12-10T14:00:00Z|The end of the time range in which data was queried. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|IspNameEn|String|Alibaba|The name of the ISP. By default, the data of all ISPs is returned. |
|LocationNameEn|String|cn-shanghai|The name of the region. By default, the data in all regions is returned. |
|RequestId|String|3C6CCEC4-6B88-4D4A-\*\*\*\*-D47B3D92CF8F|The ID of the request. |
|StartTime|String|2015-12-10T13:00:00Z|The beginning of the time range in which data was queried. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=DescribeVodDomainBpsData
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeVodDomainBpsDataResponse>
      <BpsDataPerInterval>
            <DataModule>
                  <TimeStamp>2015-12-10T13:00:00Z</TimeStamp>
                  <Value>11288111</Value>
                  <DomesticValue>11286111</DomesticValue>
                  <OverseasValue>2000</OverseasValue>
                  <HttpsValue>11288111</HttpsValue>
                  <HttpsDomesticValue>11286111</HttpsDomesticValue>
                  <HttpsOverseasValue>2000</HttpsOverseasValue>
            </DataModule>
            <DataModule>
                  <TimeStamp>2015-12-10T13:05:00Z</TimeStamp>
                  <Value>12124821</Value>
                  <DomesticValue>12112821</DomesticValue>
                  <OverseasValue>12000</OverseasValue>
                  <HttpsValue>11288111</HttpsValue>
                  <HttpsDomesticValue>11286111</HttpsDomesticValue>
                  <HttpsOverseasValue>2000</HttpsOverseasValue>
            </DataModule>
      </BpsDataPerInterval>
      <DomainName>example.com</DomainName>
      <DataInterval>300</DataInterval>
      <RequestId>3C6CCEC4-6B88-4D4A-****-D47B3D92CF8F</RequestId>
      <StartTime>2015-12-10T13:00:00Z</StartTime>
      <EndTime>2015-12-10T14:00:00Z</EndTime>
</DescribeVodDomainBpsDataResponse>
```

`JSON` format

```
{
    "BpsDataPerInterval": {
        "DataModule": [
            {
                "TimeStamp": "2015-12-10T13:00:00Z",
                "Value": "11288111",
                "DomesticValue": "11286111",
                "OverseasValue": "2000",
                "HttpsValue": "11288111",
                "HttpsDomesticValue": "11286111",
                "HttpsOverseasValue": "2000"
            },
            {
                "TimeStamp": "2015-12-10T13:05:00Z",
                "Value": "12124821",
                "DomesticValue": "12112821",
                "OverseasValue": "12000",
                "HttpsValue": "11288111",
                "HttpsDomesticValue": "11286111",
                "HttpsOverseasValue": "2000"
            }
        ]
    },
    "DomainName": "example.com",
    "DataInterval": "300",
    "RequestId": "3C6CCEC4-6B88-4D4A-****-D47B3D92CF8F",
    "StartTime": "2015-12-10T13:00:00Z",
    "EndTime": "2015-12-10T14:00:00Z"
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
|InvalidStartTime.Malformed

|Specified StartTime is malformed.

|400

|The error message returned because the format of the start time is invalid. |
|InvalidEndTime.Malformed

|Specified EndTime is malformed.

|400

|The error message returned because the format of the end time is invalid. |
|InvalidStartTime.ValueNotSupported

|The specified value of parameter StartTime is not supported.

|400

|The error message returned because the time range that is specified by the EndTime and StartTime parameters exceeds 90 days. |
|InvalidEndTime.Mismatch

|Specified EndTime does not math the specified StartTime.

|400

|The error message returned because the end time is earlier than the start time. |


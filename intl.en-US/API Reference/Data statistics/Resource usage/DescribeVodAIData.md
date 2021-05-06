# DescribeVodAIData

Queries the statistics on video AI of different types, such as automated review and media fingerprinting.

**Note:**

-   This operation is available only in the **China \(Shanghai\)** region.
-   If the time range to query is less than or equal to seven days, the system returns the statistics collected on an hourly basis. If the time range to query is greater than seven days, the system returns the statistics collected on a daily basis. The maximum time range that you can specify to query is 31 days.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=DescribeVodAIData&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeVodAIData|The operation that you want to perform. Set the value to **DescribeVodAIData**. |
|EndTime|String|Yes|2019-02-01T15:00:00Z|The end of the time range to query. The end time must be later than the start time. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC. |
|StartTime|String|Yes|2019-02-01T13:00:00Z|The beginning of the time range to query. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC. |
|Region|String|No|cn-beijing|The region where the processed file is stored. If you do not set this parameter, the data in all regions is returned. You can specify multiple regions. Separate them with commas \(,\). Valid values:

 -   **cn-shanghai**: China \(Shanghai\)
-   **cn-beijing**: China \(Beijing\)
-   **eu-central-1**: Germany \(Frankfurt\)
-   **ap-southeast-1**: Singapore |
|AIType|String|No|AIVideoCensor|The type of video AI. If you do not set this parameter, the data of all video AI types is returned. You can specify multiple types. Separate them with commas \(,\). Valid values:

 -   **AIVideoCensor**: automated review
-   **AIVideoFPShot**: media fingerprinting
-   **AIVideoTag**: smart tag |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|AIData|Array of AIDataItem| |The statistics on video AI. |
|AIDataItem| | | |
|Data|Array of DataItem| |The statistics on video AI of each type. |
|DataItem| | | |
|Name|String|AIVideoCensor|The type of video AI. Valid values:

 -   **AIVideoCensor**: automated review
-   **AIVideoFPShot**: media fingerprinting
-   **AIVideoTag**: smart tag |
|Value|String|111|The processing duration. Unit: seconds. |
|TimeStamp|String|2019-02-01T13:00:00Z|The timestamp of the returned data. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|DataInterval|String|day|The time granularity at which the data was queried. Valid values:

 -   **hour**
-   **day** |
|RequestId|String|C370DAF1-C838-4288-\*\*\*\*-9A87633D248E|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=DescribeVodAIData
&EndTime=2019-02-01T15:00:00Z
&StartTime=2019-02-01T13:00:00Z
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeVodAIDataResponse>
	  <RequestId>C370DAF1-C838-4288-****-9A87633D248E</RequestId>
	  <DataInterval>day</DataInterval>
	  <AIData>
		    <AIDataItem>
			      <TimeStamp>2019-02-01T16:00:00Z</TimeStamp>
			      <Data>
				        <DataItem>
					          <Name>AIVideoCensor</Name>
					          <Value>111</Value>
				        </DataItem>
			      </Data>
		    </AIDataItem>
		    <AIDataItem>
			      <TimeStamp>2019-02-02T16:00:00Z</TimeStamp>
			      <Data>
				        <DataItem>
					          <Name>AIVideoCensor</Name>
					          <Value>111</Value>
				        </DataItem>
				        <DataItem>
					          <Name>AIVideoFPShot</Name>
					          <Value>222</Value>
				        </DataItem>
			      </Data>
		    </AIDataItem>
	  </AIData>
</DescribeVodAIDataResponse>
```

`JSON` format

```
{
  "RequestId": "C370DAF1-C838-4288-****-9A87633D248E",
  "DataInterval": "day",
  "AIData": {
    "AIDataItem": [
      {
        "TimeStamp": "2019-02-01T16:00:00Z",
        "Data": {
          "DataItem": [
            {
              "Name": "AIVideoCensor",
              "Value": 111
            }
          ]
        }
      },
      {
        "TimeStamp": "2019-02-02T16:00:00Z",
        "Data": {
          "DataItem": [
            {
              "Name": "AIVideoCensor",
              "Value": 111
            },
            {
              "Name": "AIVideoFPShot",
              "Value": 222
            }
          ]
        }
      }
    ]
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
|OperationDenied

|Your account does not open VOD service yet.

|403

|The error message returned because ApsaraVideo VOD has not been activated for your Alibaba Cloud account. |
|OperationDenied

|Your VOD service is suspended.

|403

|The error message returned because ApsaraVideo VOD has been suspended for your Alibaba Cloud account. |
|InvalidParameter

|Invalid Parameter.

|400

|The error message returned because one or more parameters are invalid. |
|InvalidParameterAliUid

|Invalid Parameter AliUid.

|400

|The error message returned because the value of the AliUid parameter is invalid. |
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
|InvalidParameterRegion

|Invalid Parameter Region.

|400

|The error message returned because the value of the Region parameter is invalid. |


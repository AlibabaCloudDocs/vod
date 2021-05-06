# DescribePlayUserAvg

Queries the statistics on average playback each day in a specified time range.

**Note:**

-   This operation is available only in the **China \(Shanghai\)** region.
-   You can call this operation to query only playback statistics collected on videos that are played by using ApsaraVideo Player SDKs.
-   Playback statistics for the previous day are generated at 09:00 on the current day, in UTC+8.
-   You can query data that is generated since January 1, 2018. The maximum time range to query is 180 days.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=DescribePlayUserAvg&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribePlayUserAvg|The operation that you want to perform. Set the value to **DescribePlayUserAvg**. |
|StartTime|String|Yes|2016-06-29T13:00:00Z|The beginning of the time range to query. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC. |
|EndTime|String|Yes|2016-06-30T13:00:00Z|The end of the time range to query. The end time must be later than the start time. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|6C7F90B2-BDA4-4FAC-\*\*\*\*-A38A121DFE19|The ID of the request. |
|UserPlayStatisAvgs|Array of UserPlayStatisAvg| |The statistics on average playback each day. |
|UserPlayStatisAvg| | | |
|AvgPlayCount|String|170|The average number of video views. |
|AvgPlayDuration|String|1035902.8|The average playback duration. Unit: milliseconds. |
|Date|String|20170120|The date when the statistics were generated. The date follows the *yyyy-MM-dd* format. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=DescribePlayUserAvg
&StartTime=2016-06-29T13:00:00Z
&EndTime=2016-06-30T13:00:00Z
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribePlayUserAvgResponse>
	  <UserPlayStatisAvgs>
		    <UserPlayStatisAvg>
			      <AvgPlayDuration>1035902.8</AvgPlayDuration>
			      <Date>20171127</Date>
			      <AvgPlayCount>17.0</AvgPlayCount>
		    </UserPlayStatisAvg>
		    <UserPlayStatisAvg>
			      <AvgPlayDuration>3113356.7</AvgPlayDuration>
			      <Date>20171128</Date>
			      <AvgPlayCount>41.0</AvgPlayCount>
		    </UserPlayStatisAvg>
		    <UserPlayStatisAvg>
			      <AvgPlayDuration>4290368.0</AvgPlayDuration>
			      <Date>20171129</Date>
			      <AvgPlayCount>59.8</AvgPlayCount>
		    </UserPlayStatisAvg>
	  </UserPlayStatisAvgs>
	  <RequestId>6C7F90B2-BDA4-4FAC-****-A38A121DFE19</RequestId>
</DescribePlayUserAvgResponse>
```

`JSON` format

```
{
    "UserPlayStatisAvgs": {
        "UserPlayStatisAvg": [
            {
                "AvgPlayDuration": "1035902.8", 
                "Date": "20171127", 
                "AvgPlayCount": "17.0"
            }, 
            {
                "AvgPlayDuration": "3113356.7", 
                "Date": "20171128", 
                "AvgPlayCount": "41.0"
            }, 
            {
                "AvgPlayDuration": "4290368.0", 
                "Date": "20171129", 
                "AvgPlayCount": "59.8"
            }
        ]
    }, 
    "RequestId": "6C7F90B2-BDA4-4FAC-****-A38A121DFE19"
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
|InternalError

|The request processing has failed due to some unknown error.

|500

|The error message returned because an unknown error has occurred. |
|InvalidStartTime.Malformed

|Specified StartTime is malformed.

|400

|The error message returned because the format of the start time that is specified by the StartTime parameter is invalid. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC. |
|InvalidEndTime.Malformed

|Specified EndTime is malformed.

|400

|The error message returned because the format of the end time that is specified by the EndTime parameter is invalid. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC. |
|InvalidEndTime.BeyondCurrent

|EndTime beyond current time.

|400

|The error message returned because the end time that is specified by the EndTime parameter is later than the current time. |
|InvalidEndTime.Mismatch

|StartTime or EndTime is mismatch.

|400

|The error message returned because the time range that is specified by the StartTime and EndTime parameters is invalid.

|Specify the time in the ISO 8601 standard in the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC. |


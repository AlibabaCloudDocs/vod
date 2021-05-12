# DescribePlayUserTotal

Queries the statistics on total playback each day in a specified time range.

**Note:**

-   This operation is available only in the **China \(Shanghai\)** region.
-   You can call this operation to query only playback statistics collected on videos that are played by using ApsaraVideo Player SDKs.
-   Playback statistics for the previous day are generated at 09:00 on the current day, in UTC+8.
-   You can query data that is generated since January 1, 2018. The maximum time range to query is 180 days.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=DescribePlayUserTotal&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribePlayUserTotal|The operation that you want to perform. Set the value to **DescribePlayUserTotal**. |
|StartTime|String|Yes|2016-06-29T13:00:00Z|The beginning of the time range to query. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC. |
|EndTime|String|Yes|2016-06-30T13:00:00Z|The end of the time range to query. The end time must be later than the start time. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|1FAFB884-D5A7-47D1-\*\*\*\*-8928AA9C8720|The ID of the request. |
|UserPlayStatisTotals|Array of UserPlayStatisTotal| |The statistics on total playback each day. |
|UserPlayStatisTotal| | | |
|Date|String|20170120|The date when the statistics were generated. The date follows the *yyyy-MM-dd* format. |
|PlayDuration|String|9340070|The total playback duration. Unit: milliseconds. |
|PlayRange|String|"<=1m:74.3%;\>1<=5m:22.8%;\>5<=10m:1.0%;\>10<=15m:1.0%;\>15<=30m:1.0%"|The distribution of the playback duration. |
|VV|Struct| |The total number of video views. |
|Android|String|161|The total number of video views that is collected for videos that are played by using ApsaraVideo Player SDK for Android. |
|iOS|String|0|The total number of video views that is collected for videos that are played by using ApsaraVideo Player SDK for iOS. |
|Flash|String|2|The total number of video views that is collected for videos that are played by using ApsaraVideo Player SDK for Flash. |
|HTML5|String|2|The total number of video views that is collected for videos that are played by using ApsaraVideo Player SDK for HTML5. |
|UV|Struct| |The total number of unique visitors. |
|Android|String|2|The total number of unique visitors who use ApsaraVideo Player SDK for Android. |
|iOS|String|0|The total number of unique visitors who use ApsaraVideo Player SDK for iOS. |
|Flash|String|1|The total number of unique visitors who use ApsaraVideo Player SDK for Flash. |
|HTML5|String|1|The total number of unique visitors who use ApsaraVideo Player SDK for HTML5. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=DescribePlayUserTotal
&StartTime=2016-06-29T13:00:00Z
&EndTime=2016-06-30T13:00:00Z
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribePlayUserTotalResponse>
      <UserPlayStatisTotals>
		    <UserPlayStatisTotal>
			      <PlayRange><=1m:74.3%;>1<=5m:22.8%;>5<=10m:1.0%;>10<=15m:1.0%;>15<=30m:1.0%</PlayRange>
			      <Date>20180101</Date>
			      <VV>
				        <Android>101</Android>
				        <iOS>1</iOS>
			      </VV>
			      <PlayDuration>6215417</PlayDuration>
			      <UV>
				        <Android>5</Android>
				        <iOS>1</iOS>
			      </UV>
		    </UserPlayStatisTotal>
		    <UserPlayStatisTotal>
			      <PlayRange><=1m:73.6%;>1<=5m:23.9%;>5<=10m:2.5%</PlayRange>
			      <Date>20180102</Date>
			      <VV>
				        <Android>161</Android>
				        <Flash>2</Flash>
				        <HTML5>1</HTML5>
			      </VV>
			      <PlayDuration>9340070</PlayDuration>
			      <UV>
				        <Android>1</Android>
				        <Flash>2</Flash>
				        <HTML5>1</HTML5>
			      </UV>
		    </UserPlayStatisTotal>
	  </UserPlayStatisTotals>
	  <RequestId>0B9BA42C-8BDE-4611-****-C856BBE20898</RequestId>
</DescribePlayUserTotalResponse>
		     
			       
			       
			       
				         
				         
			       
			       
			       
				         
				         
			       
		     
		     
			       
			       
			       
				         
				         
				         
			       
			       
			       
				         
				         
				         
			       
		     
	   
	   
 
```

`JSON` format

```
{
    "UserPlayStatisTotals": {
        "UserPlayStatisTotal":
        [
            {
                "PlayRange": "<=1m:74.3%;>1<=5m:22.8%;>5<=10m:1.0%;>10<=15m:1.0%;>15<=30m:1.0%", 
                "Date":
            "20180101", 
                "VV":
                {
                    "Android": "101", 
                    "iOS": 
                "1"
                }, 
                "PlayDuration": "6215417", 
                "UV": 
                {
                    "Android": "5", 
                    "iOS":
                    "1"
                }
            }, 
            {
                "PlayRange": "<=1m:73.6%;>1<=5m:23.9%;>5<=10m:2.5%", 
                "Date": 
                    "20180102", 
                "VV": {
                    "Android":
                "161", 
                    "Flash": 
                "2", 
                    "HTML5": "1"
                }, 
                "PlayDuration": 
                "9340070", 
                "UV": {
                    "Android":
                    "1", 
                    "Flash": "2", 
                    "HTML5": 
                    "1"
                }
            }
        ]
    }, 
    "RequestId": "0B9BA42C-8BDE-4611-****-C856BBE20898"
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

|The error message returned because the time range that is specified by the StartTime and EndTime parameters is invalid. |


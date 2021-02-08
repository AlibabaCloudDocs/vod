# DescribeVodDomainLog

Queries the information about the raw access logs for a specific domain name, including the log path.

**Note:**

-   This operation is available only in the **China \(Shanghai\)** region.
-   For more information about the log format and latency, see [Download logs](~~86099~~).
-   If you specify neither the StartTime parameter nor the EndTime parameter, the log data in the last 24 hours is queried.
-   You can specify both the StartTime and EndTime parameters to query the log data that is generated in the specified duration.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=DescribeVodDomainLog&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeVodDomainLog|The operation that you want to perform. Set the value to **DescribeVodDomainLog**. |
|DomainName|String|Yes|example1.com|The domain name.

 **Note:** You can specify only one domain name in each query. |
|PageSize|Long|No|300|The number of entries to return on each page.

 -   Default value: **300.**
-   Maximum value: **1000.** |
|PageNumber|Long|No|1|The number of the page to return. Default value: **1**. |
|StartTime|String|No|2016-10-20T04:00:00Z|The start of the time range to query. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC. |
|EndTime|String|No|2016-10-20T05:00:00Z|The end of the time range to query. The end time must be later than the start time. The time range that is specified by the StartTime and EndTime parameters cannot exceed one year. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|DomainLogDetails|Array of DomainLogDetail| |The detailed data of Alibaba Cloud CDN logs. |
|DomainLogDetail| | | |
|DomainName|String|example1.com|The domain name. |
|LogCount|Long|2|The total number of entries returned on the current page. |
|LogInfos|Array of LogInfoDetail| |The detailed information about Alibaba Cloud CDN logs. |
|LogInfoDetail| | | |
|EndTime|String|2018-05-31T05:00:00Z|The end of the time range in which data was queried. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|LogName|String|example1.com\_2018\_03\_25\_180000\_190000.gz|The name of the log file. |
|LogPath|String|cdntest.example.com/example1.com/2018\_03\_25/example1.com\_2018\_03\_25\_180000\_190000.gz? Expires=1522659931&OSSAccessKeyId=\*\*\*\*&Signature=\*\*\*\*|The path of the log file. |
|LogSize|Long|2645401|The size of the log file. |
|StartTime|String|2018-05-31T04:00:00Z|The beginning of the time range in which data was queried. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|PageInfos|Struct| |The pagination settings of Alibaba Cloud CDN logs. |
|PageNumber|Long|1|The page number of the returned page. |
|PageSize|Long|300|The number of entries returned per page. |
|Total|Long|2|The total number of entries returned. |
|RequestId|String|077D0284-F041-4A41-\*\*\*\*-B48377FDAA25|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=DescribeVodDomainLog
&DomainName=example1.com
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeVodDomainLogResponse>
      <RequestId>077D0284-F041-4A41-****-B48377FDAA25</RequestId>
	  <DomainLogDetails>
		    <DomainLogDetail>
			      <LogInfos>
				        <LogInfoDetail>
					          <LogName>example1.com_2018_03_25_180000_190000.gz</LogName>
					          <LogPath>cdntest.example.com/example1.com/2018_03_25/example1.com_2018_03_25_180000_190000.gz? Expires=1522659931&amp;OSSAccessKeyId=****&amp;Signature=****</LogPath>
					          <EndTime>2018-05-31T04:00:00Z</EndTime>
					          <StartTime>2018-05-31T03:00:00Z</StartTime>
					          <LogSize>2645401</LogSize>
				        </LogInfoDetail>
				        <LogInfoDetail>
					          <LogName>example1.com_2018_03_25_190000_200000.gz</LogName>
					          <LogPath>cdntest.example.com/example1.com/2018_03_25/example1.com_2018_03_25_190000_200000.gz? Expires=1522659931&amp;OSSAccessKeyId=****&amp;Signature=****</LogPath>
					          <EndTime>2018-05-31T06:00:00Z</EndTime>
					          <StartTime>2018-05-31T05:00:00Z</StartTime>
					          <LogSize>2653965</LogSize>
				        </LogInfoDetail>
			      </LogInfos>
			      <LogCount>2</LogCount>
			      <PageInfos>
				        <PageSize>300</PageSize>
				        <Total>2</Total>
				        <PageNumber>1</PageNumber>
			      </PageInfos>
			      <DomainName>example1.com</DomainName>
		    </DomainLogDetail>
	  </DomainLogDetails>
</DescribeVodDomainLogResponse>
```

`JSON` format

```
{
    "RequestId": "077D0284-F041-4A41-****-B48377FDAA25",
    "DomainLogDetails": {
        "DomainLogDetail": [
            {
                "LogInfos": {
                    "LogInfoDetail": [
                        {
                            "LogName": "example1.com_2018_03_25_180000_190000.gz",
                            "LogPath": "cdntest.example.com/example1.com/2018_03_25/example1.com_2018_03_25_180000_190000.gz? Expires=1522659931&OSSAccessKeyId=****&Signature=****",
                            "EndTime": "2018-05-31T04:00:00Z",
                            "StartTime": "2018-05-31T03:00:00Z",
                            "LogSize": 2645401
                        },
                        {
                            "LogName": "example1.com_2018_03_25_190000_200000.gz",
                            "LogPath": "cdntest.example.com/example1.com/2018_03_25/example1.com_2018_03_25_190000_200000.gz? Expires=1522659931&OSSAccessKeyId=****&Signature=****",
                            "EndTime": "2018-05-31T06:00:00Z",
                            "StartTime": "2018-05-31T05:00:00Z",
                            "LogSize": 2653965
                        }
                    ]
                },
                "LogCount": 2,
                "PageInfos": {
                    "PageSize":300,
                    "Total": 2,
                    "PageNumber": 1
                },
                "DomainName": "example1.com"
            }
        ]
    }
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/vod).


# DescribeVodTranscodeData

Queries the statistics on transcoding of different specifications.

**Note:**

-   This operation is available only in the **China \(Shanghai\)** region.
-   If the time range to query is less than or equal to seven days, the system returns the statistics collected on an hourly basis. If the time range to query is greater than seven days, the system returns the statistics collected on a daily basis. The maximum time range that you can specify to query is 31 days.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=DescribeVodTranscodeData&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeVodTranscodeData|The operation that you want to perform. Set the value to **DescribeVodTranscodeData**. |
|EndTime|String|Yes|2019-02-01T15:59:00Z|The end of the time range to query. The end time must be later than the start time. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC. |
|StartTime|String|Yes|2019-02-01T15:00:00Z|The beginning of the time range to query. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC. |
|Region|String|No|cn-shanghai|The region where the transcoded file is stored. If you do not set this parameter, the data in all regions is returned. You can specify multiple regions. Separate them with commas \(,\). Valid values:

-   **cn-shanghai**: China \(Shanghai\)
-   **cn-beijing**: China \(Beijing\)
-   **eu-central-1**: Germany \(Frankfurt\)
-   **ap-southeast-1**: Singapore |
|Interval|String|No|day|The time granularity at which the data is queried. Valid values:

-   **day**
-   **hour** |
|Storage|String|No|bucket01|The name of the Object Storage Service \(OSS\) bucket. If you do not set this parameter, the data of all buckets is returned. You can specify multiple buckets. Separate them with commas \(,\). |
|Specification|String|No|Audio|The transcoding specification. If you do not set this parameter, the data of all transcoding specifications is returned. You can specify multiple transcoding specifications. Separate them with commas \(,\). Valid values:

-   **Audio**: audio transcoding
-   **Segmentation**: container format conversion
-   H.264 and H.265-related video transcoding specifications, such as **H264.LD**, **H264.SD**, **H264.HD**, **H264.2K**, and **H264.4K** |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|DataInterval|String|day|The time granularity at which the data was queried. Valid values:

-   **hour**
-   **day** |
|RequestId|String|C370DAF1-C838-4288-\*\*\*\*-9A87633D248E|The ID of the request. |
|TranscodeData|Array of TranscodeDataItem| |The statistics on transcoding. |
|TranscodeDataItem| | | |
|Data|Array of DataItem| |The statistics on transcoding of different specifications. |
|DataItem| | | |
|Name|String|H264.SD|The transcoding specification. Valid values:

-   **Audio**: audio transcoding
-   **Segmentation**: container format conversion
-   H.264 and H.265-related video transcoding specifications, such as **H264.LD, H264.SD, H264.HD, H264.2K, and H264.4K** |
|Value|String|111|The transcoding length. Unit: seconds. |
|TimeStamp|String|2019-02-01T16:00:00Z|The timestamp of the returned data. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=DescribeVodTranscodeData
&EndTime=2019-02-01T15:59:00Z
&StartTime=2019-02-01T15:00:00Z
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeVodTranscodeDataResponse>
      <RequestId>C370DAF1-C838-4288-****-9A87633D248E</RequestId>
      <DataInterval>day</DataInterval>
      <TranscodeData>
            <TranscodeDataItem>
                  <TimeStamp>2019-02-01T16:00:00Z</TimeStamp>
                  <Data>
                        <DataItem>
                              <Name>H264.SD</Name>
                              <Value>111</Value>
                        </DataItem>
                        <DataItem>
                              <Name>All</Name>
                              <Value>111</Value>
                        </DataItem>
                  </Data>
            </TranscodeDataItem>
            <TranscodeDataItem>
                  <TimeStamp>2019-02-02T16:00:00Z</TimeStamp>
                  <Data>
                        <DataItem>
                              <Name>Audio</Name>
                              <Value>111</Value>
                        </DataItem>
                        <DataItem>
                              <Name>H264.SD</Name>
                              <Value>222</Value>
                        </DataItem>
                        <DataItem>
                              <Name>All</Name>
                              <Value>333</Value>
                        </DataItem>
                  </Data>
            </TranscodeDataItem>
      </TranscodeData>
</DescribeVodTranscodeDataResponse>
      <DataInterval>day</DataInterval>
      <TranscodeData>
            <TranscodeDataItem>
                  <TimeStamp>2019-02-01T16:00:00Z</TimeStamp>
                  <Data>
                        <DataItem>
                              <Name>H264.SD</Name>
                              <Value>111</Value>
                        </DataItem>
                        <DataItem>
                              <Name>All</Name>
                              <Value>111</Value>
                        </DataItem>
                  </Data>
            </TranscodeDataItem>
            <TranscodeDataItem>
                  <TimeStamp>2019-02-02T16:00:00Z</TimeStamp>
                  <Data>
                        <DataItem>
                              <Name>Audio</Name>
                              <Value>111</Value>
                        </DataItem>
                        <DataItem>
                              <Name>H264.SD</Name>
                              <Value>222</Value>
                        </DataItem>
                        <DataItem>
                              <Name>All</Name>
                              <Value>333</Value>
                        </DataItem>
                  </Data>
            </TranscodeDataItem>
      </TranscodeData>
</DescribeVodTranscodeDataResponse>
```

`JSON`格式

```
 {
          "DataItem": [
            {
              "Name": "Audio",
              "Value": 111
            },
            {
              "Name": "H264.SD",
              "Value": 222
            },
            {
              "Name": "All",
              "Value": 333
            }
          ]
        }
      }
    ]
  }
}
            }
          ]
        }
      },
      {
        "TimeStamp": "2019-02-02T16:00:00Z",
        "Data": {
          "DataItem": [
            {
              "Name": "Audio",
              "Value": 111
            },
            {
              "Name": "H264.SD",
              "Value": 222
            },
            {
              "Name": "All",
              "Value": 333
            }
          ]
        }
      }
    ]
  }
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/vod)查看更多错误码。

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


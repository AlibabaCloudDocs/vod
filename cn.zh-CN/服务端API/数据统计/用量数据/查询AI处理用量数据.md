# 查询AI处理用量数据

调用DescribeVodAIData查询AI处理（智能审核、视频DNA等）的用量数据。

**说明：**

-   目前仅支持**上海**地域。
-   当起始结束时间间隔在7天以内时，返回小时粒度的数据；当起始结束时间间隔大于7天时，返回天粒度的数据；最大间隔为31天。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=DescribeVodAIData&type=RPC&version=2017-03-21)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeVodAIData|系统规定参数。取值：**DescribeVodAIData**。 |
|EndTime|String|是|2019-02-01T15:00:00Z|获取数据结束时间点，需晚于起始时间。格式为：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。 |
|StartTime|String|是|2019-02-01T15:00:00Z|获取数据起始时间点。格式为：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。 |
|Region|String|否|cn-beijing|存储地域。默认返回所有区域。支持批量查询，多个地域使用用半角逗号（,）分隔。取值范围：

 -   **cn-shanghai**（上海）
-   **cn-beijing**（北京）
-   **eu-central-1**（德国）
-   **ap-southeast-1**（新加坡） |
|AIType|String|否|AIVideoCensor|AI类型。默认返回类型。支持批量查询，多个区域使用半角逗号（,）分隔。取值范围：

 -   **AIVideoCensor**（智能审核）
-   **AIVideoFPShot**（视频DNA）
-   **AIVideoTag**（智能标签） |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|AIData|Array of AIDataItem| |AI处理用量数据。 |
|AIDataItem| | | |
|Data|Array of DataItem| |AI处理用量详细数据。 |
|DataItem| | | |
|Name|String|AIVideoCensor|AI类型。 取值范围：

 -   **AIVideoCensor**（智能审核）
-   **AIVideoFPShot**（视频DNA）
-   **AIVideoTag**（智能标签） |
|Value|String|111|处理时长。单位：秒。 |
|TimeStamp|String|2019-02-01T13:00:00Z|时间片起始时刻。格式为：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。 |
|DataInterval|String|day|返回数据的时间颗粒度。取值范围：

 -   **hour**（小时数据）
-   **day**（天数据） |
|RequestId|String|C370DAF1-C838-4288-\*\*\*\*-9A87633D248E|请求ID。 |

## 示例

请求示例

```
https://vod.aliyuncs.com/?Action=DescribeVodAIData
&EndTime=2019-02-01T15:00:00Z
&StartTime=2019-02-01T15:00:00Z
&<公共请求参数>
```

正常返回示例

`XML` 格式

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

`JSON` 格式

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

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。

## 接口错误码

下表列举了本接口特有的错误码。

|错误代码

|错误信息

|HTTP 状态码

|说明 |
|------|------|----------|----|
|Throttling

|Request was denied due to request throttling.

|503

|请求被流量控制限制。 |
|OperationDenied

|Your account does not open VOD service yet.

|403

|未开通VOD服务。 |
|OperationDenied

|Your VOD service is suspended.

|403

|VOD服务已被停止。 |
|InvalidParameter

|Invalid Parameter.

|400

|参数错误。 |
|InvalidParameterAliUid

|Invalid Parameter AliUid.

|400

|AliUid参数错误。 |
|InvalidParameterStartTime

|Invalid Parameter StartTime.

|400

|StartTime参数错误。 |
|InvalidParameterEndTime

|Invalid Parameter EndTime.

|400

|EndTime参数错误。 |
|InvalidTimeRange

|StartTime and EndTime range should less than 1 month.

|400

|SndTime和StartTime差值不能超过31天。 |
|InvalidParameterRegion

|Invalid Parameter Region.

|400

|Region参数错误。 |


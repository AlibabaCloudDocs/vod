# DescribeVodTranscodeData {#doc_api_vod_DescribeVodTranscodeData .reference}

调用DescribeVodTranscodeData查询转码用量数据。

**说明：** 起始结束时间间隔在7天以内时，返回小时粒度的数据；大于7天时，返回天粒度的数据；最大间隔为31天。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=DescribeVodTranscodeData&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeVodTranscodeData|系统规定参数，取值：**DescribeVodTranscodeData**。

 |
|EndTime|String|是|2019-02-01T16:00:00Z|获取数据结束时间点，需大于起始时间。

 日期格式按照ISO8601表示法，并使用UTC时间。格式为：**YYYY-MM-DDThh:mm:ssZ**。

 |
|StartTime|String|是|2019-02-01T16:00:00Z|获取数据起始时间点。

 日期格式按照ISO8601表示法，并使用UTC时间。格式为：**YYYY-MM-DDThh:mm:ssZ**。

 |
|Region|String|否|cn-beijing|存储区域，默认返回所有区域。

 支持批量查询，多个区域用逗号（半角）分隔。取值范围：**cn-shanghai\(上海\)**、**cn-beijing\(北京\)**、**eu-central-1\(德国\)**、**ap-southeast-1\(新加坡\)**。

 |
|Specification|String|否|Audio|转码规格，默认返回所有转码规格。

 支持批量查询，多个用逗号（半角）分隔。取值范围：**Audio（音频）**、**Segmentation（转封装）**、**H264.LD**、**H264.SD**、**H264.HD**、**H264.2K**、**H264.4K**等。

 |
|Storage|String|否|bucket01|存储名称（阿里云OSS存储Bucket名称），默认返回所有存储。支持批量查询，多个用逗号（半角）分隔。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|DataInterval|String|day|返回数据的时间颗粒度。取值范围：**hour（小时数据）**，**day（天数据）**。

 |
|RequestId|String|C370DAF1-C838-4288-A1A0-9A87633D248E|请求ID。

 |
|TranscodeData| | |转码用量数据。

 |
|Data| | |转码用量详细数据。

 |
|Name|String|H264.SD|转码规格。

 |
|Value|String|111|转码时长，单位：秒。

 |
|TimeStamp|String|2019-02-01T16:00:00Z|数据时间。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=DescribeVodTranscodeData
&EndTime=2019-02-01T16:00:00Z
&StartTime=2019-02-01T16:00:00Z
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeVodTranscodeDataResponse>
  <RequestId>C370DAF1-C838-4288-A1A0-9A87633D248E</RequestId>
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

`JSON` 格式

``` {#json_return_success_demo}
{
	"DataInterval":"day",
	"RequestId":"C370DAF1-C838-4288-A1A0-9A87633D248E",
	"TranscodeData":{
		"TranscodeDataItem":[
			{
				"TimeStamp":"2019-02-01T16:00:00Z",
				"Data":{
					"DataItem":[
						{
							"Name":"H264.SD",
							"Value":111
						},
						{
							"Name":"All",
							"Value":111
						}
					]
				}
			},
			{
				"TimeStamp":"2019-02-02T16:00:00Z",
				"Data":{
					"DataItem":[
						{
							"Name":"Audio",
							"Value":111
						},
						{
							"Name":"H264.SD",
							"Value":222
						},
						{
							"Name":"All",
							"Value":333
						}
					]
				}
			}
		]
	}
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。


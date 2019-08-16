# DescribeVodAIData {#doc_api_vod_DescribeVodAIData .reference}

调用DescribeVodAIData查询AI处理（智能审核、视频DNA等）的用量数据。

**说明：** 起始结束时间间隔在7天以内时，返回小时粒度的数据；大于7天时，返回天粒度的数据；最大间隔为31天。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=DescribeVodAIData&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeVodAIData|系统规定参数，取值：**DescribeVodAIData**。

 |
|EndTime|String|是|2019-02-01T16:00:00Z|获取数据结束时间点，需大于起始时间。

 日期格式按照ISO8601表示法，并使用UTC时间。格式为：**YYYY-MM-DDThh:mm:ssZ**。

 |
|StartTime|String|是|2019-02-01T16:00:00Z|获取数据起始时间点。

 日期格式按照ISO8601表示法，并使用UTC时间。格式为：**YYYY-MM-DDThh:mm:ssZ**。

 |
|AIType|String|否|AIVideoCensor|AI类型，默认返回类型。

 支持批量查询，多个区域用逗号（半角）分隔。取值范围：**AIVideoCensor（智能审核）**、**AIVideoFPShot（视频DNA）**、**AIVideoTag（多模态标签）**。

 |
|Region|String|否|cn-beijing|存储区域，默认返回所有区域。

 支持批量查询，多个区域用逗号（半角）分隔。取值范围：**cn-shanghai\(上海\)**、**cn-beijing\(北京\)**、**eu-central-1\(德国\)**、**ap-southeast-1\(新加坡\)**。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|AIData| | |转码用量数据。

 |
|Data| | |转码用量详细数据。

 |
|Name|String|AIVideoCensor|AI类型。

 |
|Value|String|111|处理时长，单位：秒。

 |
|TimeStamp|String|2019-02-01T16:00:00Z|时间片起始时刻。

 |
|DataInterval|String|day|返回数据的时间颗粒度。取值范围：**hour（小时数据）**，**day（天数据）**。

 |
|RequestId|String|C370DAF1-C838-4288-A1A0-9A87633D248E|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=DescribeVodAIData
&EndTime=2019-02-01T16:00:00Z
&StartTime=2019-02-01T16:00:00Z
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeVodAIDataResponse>
	  <RequestId>C370DAF1-C838-4288-A1A0-9A87633D248E</RequestId>
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

``` {#json_return_success_demo}
{
	"DataInterval":"day",
	"RequestId":"C370DAF1-C838-4288-A1A0-9A87633D248E",
	"AIData":{
		"AIDataItem":[
			{
				"TimeStamp":"2019-02-01T16:00:00Z",
				"Data":{
					"DataItem":[
						{
							"Name":"AIVideoCensor",
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
							"Name":"AIVideoCensor",
							"Value":111
						},
						{
							"Name":"AIVideoFPShot",
							"Value":222
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


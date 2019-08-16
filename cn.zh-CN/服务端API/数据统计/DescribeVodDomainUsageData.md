# DescribeVodDomainUsageData {#doc_api_vod_DescribeVodDomainUsageData .reference}

调用DescribeVodDomainUsageData查询加速流量或带宽用量数据。

-   支持批量域名查询，多个域名用逗号（半角）分隔，最多可以一次查询100个域名。如果为空则返回账号下所有域名的数据。
-   最长可查询近1年的数据，单次查询跨度最长为3个月，查询时间为1-3天时，数据按小时粒度返回，查询时间大于4天，数据按天粒度返回。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=DescribeVodDomainUsageData&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeVodDomainUsageData|系统规定参数，取值：**DescribeVodDomainUsageData**。

 |
|EndTime|String|是|2015-12-10T20:00Z|获取数据结束时间点，需大于起始时间。

 日期格式按照ISO8601表示法，并使用UTC时间。格式为：**YYYY-MM-DDThh:mm:ssZ**。

 |
|Field|String|是|bps|数据类型。取值范围：**bps（带宽）、traf（流量）**。

 |
|StartTime|String|是|2015-12-10T20:00Z|获取数据起始时间点。

 日期格式按照ISO8601表示法，并使用UTC时间。格式为：**YYYY-MM-DDThh:mm:ssZ**。

 |
|Area|String|否|CN|区域代号，默认为CN中国大陆。

 取值范围：**CN（中国大陆）**、**OverSeas（海外区域）**。

 |
|DomainName|String|否|example.com|加速域名。若参数为空，默认返回所有加速域名合并后数据。支持批量查询，多个用逗号（半角）分隔。

 |
|Type|String|否|traf|用量类型。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Area|String|CN|用量区域。

 |
|DataInterval|String|300|每条记录的时间间隔。单位：秒。

 |
|DomainName|String|example.com|加速域名信息。

 |
|EndTime|String|2015-12-10T20:00Z|结束时间。

 |
|RequestId|String|B955107D-E658-4E77-B913-E0AC3D31693E|请求ID。

 |
|StartTime|String|2015-12-10T20:00Z|开始时间。

 |
|Type|String|traf|用量类型。

 |
|UsageDataPerInterval| | |流量/带宽用量数据。

 |
|TimeStamp|String|2015-12-10T20:00:00Z|时间片起始时刻。

 |
|Value|String|2592.3920000000003|流量/带宽用量。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=DescribeVodDomainUsageData
&EndTime=2015-12-10T20:00Z
&Field=bps
&StartTime=2015-12-10T20:00Z
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeVodDomainUsageDataResponse>
  <RequestId>B955107D-E658-4E77-B913-E0AC3D31693E</RequestId>
	  <StartTime>2015-12-10T20:00Z</StartTime>
	  <EndTime>2015-12-10T21:00Z</EndTime>
	  <Area>CN</Area>
	  <Type>traf</Type>
	  <DomainName>example.com</DomainName>
	  <DataInterval>300</DataInterval>
	  <UsageDataPerInterval>
		    <UsageData>
			      <TimeStamp>2015-12-10T20:00:00Z</TimeStamp>
			      <Value>2592.3920000000003</Value>
		    </UsageData>
		    <UsageData>
			      <TimeStamp>2015-12-10T20:05:00Z</TimeStamp>
			      <Value>2592.3920000000003</Value>
		    </UsageData>
	  </UsageDataPerInterval>
</DescribeVodDomainUsageDataResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"UsageDataPerInterval":{
		"UsageData":[
			{
				"TimeStamp":"2015-12-10T20:00:00Z",
				"Value":2592.3920000000003
			},
			{
				"TimeStamp":"2015-12-10T20:05:00Z",
				"Value":2592.3920000000003
			}
		]
	},
	"DataInterval":"300",
	"Type":"traf",
	"Area":"CN",
	"RequestId":"B955107D-E658-4E77-B913-E0AC3D31693E",
	"DomainName":"example.com",
	"EndTime":"2015-12-10T21:00Z",
	"StartTime":"2015-12-10T20:00Z"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。


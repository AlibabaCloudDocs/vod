# DescribeVodDomainTrafficData {#doc_api_vod_DescribeVodDomainTrafficData .reference}

调用DescribeVodDomainTrafficData获取加速域名的网络流量监控数据，单位：byte。

-   支持域名批量查询，多个域名用半角逗号分隔。
-   不指定StartTime和EndTime时，默认读取过去24小时的数据。
-   也可以按指定的起止时间查询，必须同时指定StartTime和EndTime，最多可获取近90天的数据。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=DescribeVodDomainTrafficData&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeVodDomainTrafficData|系统规定参数。取值：**DescribeVodDomainTrafficData**。

 |
|DomainName|String|否|example.com|要查询的域名。若为空，则默认返回所有加速域名的合并数据。支持批量查询，多个域名用半角逗号分隔。

 |
|EndTime|String|否|2019-01-20T15:59:58Z|结束时间，需大于起始时间。

 日期格式按照ISO8601表示法，使用UTC时间。格式为：**YYYY-MM-DDThh:mmZ**。

 |
|Interval|String|否|300|查询数据的时间粒度，支持**300**，**3600**和**86400**秒。不传和传的值不支持时，使用默认值。

 -   3天以内（不包含3天整）支持300\(默认\), 3600, 86400。
-   3-31天（不包含31天整）支持3600\(默认\)和86400。
-   31天以上支持86400\(默认\)。

 |
|IspNameEn|String|否|Alibaba|运营商英文名。默认为所有运营商。

 |
|LocationNameEn|String|否|cn-shanghai|区域英文名。默认为所有区域。

 |
|StartTime|String|否|2019-01-20T15:59:58Z|获取数据起始时间点。

 -   日期格式按照ISO8601表示法，使用UTC时间。格式为：**YYYY-MM-DDThh:mmZ**。
-   最小数据粒度为5分钟，若为空，则默认读取最近24小时的数据。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|DataInterval|String|3600|每条记录的时间间隔。单位：秒。

 |
|DomainName|String|example.com|加速域名信息。

 |
|EndTime|String|2019-01-20T15:59:58Z|结束时间。

 |
|RequestId|String|D94E471F-1A27-442E-8755-D4D2000CB492|请求ID。

 |
|StartTime|String|2019-01-20T15:59:58Z|开始时间。

 |
|TrafficDataPerInterval| | |每个时间间隔的流量数据。

 |
|DomesticValue|String|0|国内流量。

 |
|HttpsDomesticValue|String|0|L1节点https国内流量。

 |
|HttpsOverseasValue|String|0|L1节点https海外流量。

 |
|HttpsValue|String|0|L1节点https总流量。

 |
|OverseasValue|String|0|海外流量。

 |
|TimeStamp|String|2019-01-15T19:00:00Z|时间片起始时刻。

 |
|Value|String|0|总流量。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=DescribeVodDomainTrafficData
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeVodDomainTrafficDataResponse>
  <RequestId>D94E471F-1A27-442E-8755-D4D2000CB492</RequestId>
	  <EndTime>2019-01-20T15:59:58Z</EndTime>
	  <TrafficDataPerInterval>
		    <DataModule>
			      <OverseasValue>0</OverseasValue>
			      <HttpsValue>0</HttpsValue>
			      <Value>0</Value>
			      <HttpsDomesticValue>0</HttpsDomesticValue>
			      <HttpsOverseasValue>0</HttpsOverseasValue>
			      <TimeStamp>2019-01-15T18:00:00Z</TimeStamp>
			      <DomesticValue>0</DomesticValue>
		    </DataModule>
		    <DataModule>
			      <OverseasValue>0</OverseasValue>
			      <HttpsValue>0</HttpsValue>
			      <Value>0</Value>
			      <HttpsDomesticValue>0</HttpsDomesticValue>
			      <HttpsOverseasValue>0</HttpsOverseasValue>
			      <TimeStamp>2019-01-15T19:00:00Z</TimeStamp>
			      <DomesticValue>0</DomesticValue>
		    </DataModule>
	  </TrafficDataPerInterval>
	  <DomainName>example.com</DomainName>
	  <DataInterval>3600</DataInterval>
	  <StartTime>2019-01-15T15:59:59Z</StartTime>
</DescribeVodDomainTrafficDataResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"DataInterval":3600,
	"TrafficDataPerInterval":{
		"DataModule":[
			{
				"TimeStamp":"2019-01-15T18:00:00Z",
				"HttpsOverseasValue":0,
				"Value":0,
				"OverseasValue":0,
				"HttpsDomesticValue":0,
				"DomesticValue":0,
				"HttpsValue":0
			},
			{
				"TimeStamp":"2019-01-15T19:00:00Z",
				"HttpsOverseasValue":0,
				"Value":0,
				"OverseasValue":0,
				"HttpsDomesticValue":0,
				"DomesticValue":0,
				"HttpsValue":0
			}
		]
	},
	"RequestId":"D94E471F-1A27-442E-8755-D4D2000CB492",
	"DomainName":"example.com",
	"EndTime":"2019-01-20T15:59:58Z",
	"StartTime":"2019-01-15T15:59:59Z"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。


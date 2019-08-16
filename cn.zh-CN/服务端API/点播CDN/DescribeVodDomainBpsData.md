# DescribeVodDomainBpsData {#doc_api_vod_DescribeVodDomainBpsData .reference}

调用DescribeVodDomainBpsData获取加速域名的网络带宽监控数据。

**说明：** 

-   支持域名批量查询，多个域名用半角逗号分隔。
-   不指定StartTime和EndTime时，默认读取过去24小时的数据。
-   也可以按指定的起止时间查询，必须同时指定StartTime和EndTime，最多可获取近90天的数据。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=DescribeVodDomainBpsData&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeVodDomainBpsData|系统规定参数，取值：**DescribeVodDomainBpsData**。

 |
|DomainName|String|否|example.com|要查询的域名。若为空，则默认返回所有加速域名的合并数据。支持批量查询，多个用半角逗号分隔。

 |
|EndTime|String|否|2015-12-10T20:00:00Z|结束时间，需大于起始时间。

 日期格式按照ISO8601表示法，使用UTC时间。格式为：**YYYY-MM-DDThh:mmZ**。

 |
|Interval|String|否|300|查询数据的时间粒度，支持**300**，**3600**和**86400**秒。

 -   3天以内（不包含3天整）支持300\(默认\), 3600, 86400。
-   3-31天（不包含31天整）支持3600\(默认\)和86400。
-   31天以上支持86400\(默认\)。

 |
|IspNameEn|String|否|Alibaba|运营商英文名。默认为所有运营商。

 |
|LocationNameEn|String|否|cn-shanghai|区域英文名。默认为所有区域。

 |
|StartTime|String|否|2015-12-10T20:00:00Z|获取数据起始时间点。

 -   日期格式按照ISO8601表示法，使用UTC时间。格式为：**YYYY-MM-DDThh:mmZ**。
-   最小数据粒度为5分钟，若为空，则默认读取最近24小时的数据。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|BpsDataPerInterval| | |每个时间间隔的网络带宽数据。

 |
|DomesticValue|String|11286111|国内带宽，当按区域运营商查询时，此值为空。

 |
|HttpsDomesticValue|String|11286111|L1节点https国内带宽，当按区域运营商查询时，此值为空。

 |
|HttpsOverseasValue|String|2000|L1节点海外https带宽，当按区域运营商查询时，此值为空。

 |
|HttpsValue|String|11288111|L1节点https的带宽数据值，单位：bit/second。

 |
|OverseasValue|String|2000|海外带宽，当按区域运营商查询时，此值为空。

 |
|TimeStamp|String|2015-12-10T20:00:00Z|时间片起始时刻。

 |
|Value|String|11288111|bps数据值，单位：bit/second。

 |
|DataInterval|String|300|每条记录的时间间隔。单位：秒。

 |
|DomainName|String|example.com|加速域名信息。

 |
|EndTime|String|2015-12-10T20:00:00Z|结束时间。

 |
|IspNameEn|String|Alibaba|运营商英文名。默认为所有运营商。

 |
|LocationNameEn|String|cn-shanghai|区域英文名。默认为所有区域。

 |
|RequestId|String|3C6CCEC4-6B88-4D4A-93E4-D47B3D92CF8F|请求ID。

 |
|StartTime|String|2015-12-10T20:00:00Z|开始时间。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=DescribeVodDomainBpsData
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeVodDomainBpsDataResponse>
	  <BpsDataPerInterval>
		    <DataModule>
			      <TimeStamp>2015-12-10T20:00:00Z</TimeStamp>
			      <Value>11288111</Value>
			      <DomesticValue>11286111</DomesticValue>
			      <OverseasValue>2000</OverseasValue>
			      <HttpsValue>11288111</HttpsValue>
			      <HttpsDomesticValue>11286111</HttpsDomesticValue>
			      <HttpsOverseasValue>2000</HttpsOverseasValue>
		    </DataModule>
		    <DataModule>
			      <TimeStamp>2015-12-10T20:05:00Z</TimeStamp>
			      <Value>12124821</Value>
			      <DomesticValue>12112821</DomesticValue>
			      <OverseasValue>12000</OverseasValue>
			      <HttpsValue>11288111</HttpsValue>
			      <HttpsDomesticValue>11286111</HttpsDomesticValue>
			      <HttpsOverseasValue>2000</HttpsOverseasValue>
		    </DataModule>
	  </BpsDataPerInterval>
	  <DomainName>example.com</DomainName>
	  <DataInterval>300</DataInterval>
	  <RequestId>3C6CCEC4-6B88-4D4A-93E4-D47B3D92CF8F</RequestId>
	  <StartTime>2015-12-10T20:00:00Z</StartTime>
	  <EndTime>2015-12-10T21:00:00Z</EndTime>
</DescribeVodDomainBpsDataResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"DataInterval":"300",
	"BpsDataPerInterval":{
		"DataModule":[
			{
				"HttpsOverseasValue":"2000",
				"TimeStamp":"2015-12-10T20:00:00Z",
				"Value":"11288111",
				"OverseasValue":"2000",
				"HttpsDomesticValue":"11286111",
				"DomesticValue":"11286111",
				"HttpsValue":"11288111"
			},
			{
				"HttpsOverseasValue":"2000",
				"TimeStamp":"2015-12-10T20:05:00Z",
				"Value":"12124821",
				"OverseasValue":"12000",
				"HttpsDomesticValue":"11286111",
				"DomesticValue":"12112821",
				"HttpsValue":"11288111"
			}
		]
	},
	"RequestId":"3C6CCEC4-6B88-4D4A-93E4-D47B3D92CF8F",
	"DomainName":"example.com",
	"EndTime":"2015-12-10T21:00:00Z",
	"StartTime":"2015-12-10T20:00:00Z"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。


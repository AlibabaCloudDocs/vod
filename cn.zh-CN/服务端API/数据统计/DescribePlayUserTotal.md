# DescribePlayUserTotal {#doc_api_vod_DescribePlayUserTotal .reference}

调用DescribePlayUserTotal获取指定时间范围内的每日播放数据总量统计。

-   仅支持使用了阿里云点播播放器SDK的播放数据统计。
-   以北京时间（UTC+8）为基准，每天上午9点生成前一天的播放数据统计。
-   支持查询2018-01-01起的数据，数据查询的起止时间跨度最大为90天。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=DescribePlayUserTotal&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribePlayUserTotal|系统规定参数，取值：**DescribePlayUserTotal**。

 |
|StartTime|String|是|2016-06-29T19:00:00Z|起始时间，UTC格式。

 支持查询2018-01-01起的数据，即StartTime大于等于2018-01-01T00:00:00Z。

 |
|EndTime|String|是|2016-06-30T19:00:00Z|结束时间，UTC格式。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|1FAFB884-D5A7-47D1-82B5-8928AA9C8720|请求ID。

 |
|UserPlayStatisTotals| | |用户每天播放总量统计数据。

 |
|Date|String|20170120|日期，yyyyMMdd格式。

 |
|PlayDuration|String|9340070|播放总时长，单位：毫秒。

 |
|PlayRange|String|"<=1m:74.3%;\>1<=5m:22.8%;\>5<=10m:1.0%;\>10<=15m:1.0%;\>15<=30m:1.0%"|播放时长分布。

 |
|VV| | |播放次数总量统计。

 |
|Android|String|161|Android播放器播放总次数。

 |
|iOS|String|0|IOS播放器播放总次数。

 |
|Flash|String|2|Flash播放器播放总次数。

 |
|HTML5|String|2|Html5播放器播放总次数。

 |
|UV| | |播放用户数总量统计。

 |
|Android|String|2|Android播放器播放总用户数。

 |
|iOS|String|0|IOS播放器播放总用户数。

 |
|Flash|String|1|Flash播放器播放总用户数。

 |
|HTML5|String|1|Html5播放器播放总用户数。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=DescribePlayUserTotal
&StartTime=2016-06-29T19:00:00Z
&EndTime=2016-06-30T19:00:00Z
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribePlayUserTotalResponse>
  <UserPlayStatisTotals>
		    <UserPlayStatisTotal>
			      <PlayRange>&lt;=1m:74.3%;&gt;1&lt;=5m:22.8%;&gt;5&lt;=10m:1.0%;&gt;10&lt;=15m:1.0%;&gt;15&lt;=30m:1.0%</PlayRange>
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
			      <PlayRange>&lt;=1m:73.6%;&gt;1&lt;=5m:23.9%;&gt;5&lt;=10m:2.5%</PlayRange>
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
	  <RequestId>0B9BA42C-8BDE-4611-B096-C856BBE20898</RequestId>
</DescribePlayUserTotalResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"UserPlayStatisTotals":{
		"UserPlayStatisTotal":[
			{
				"PlayDuration":"6215417",
				"PlayRange":"<=1m:74.3%;>1<=5m:22.8%;>5<=10m:1.0%;>10<=15m:1.0%;>15<=30m:1.0%",
				"Date":"20180101",
				"VV":{
					"Android":"101",
					"iOS":"1"
				},
				"UV":{
					"Android":"5",
					"iOS":"1"
				}
			},
			{
				"PlayDuration":"9340070",
				"PlayRange":"<=1m:73.6%;>1<=5m:23.9%;>5<=10m:2.5%",
				"Date":"20180102",
				"VV":{
					"Android":"161",
					"Flash":"2",
					"HTML5":"1"
				},
				"UV":{
					"Android":"1",
					"Flash":"2",
					"HTML5":"1"
				}
			}
		]
	},
	"RequestId":"0B9BA42C-8BDE-4611-B096-C856BBE20898"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。


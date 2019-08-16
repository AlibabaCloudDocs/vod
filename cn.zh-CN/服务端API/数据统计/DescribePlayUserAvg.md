# DescribePlayUserAvg {#doc_api_vod_DescribePlayUserAvg .reference}

调用DescribePlayUserAvg获取指定时间范围内的每日播放数据均量统计。

-   仅支持使用了阿里云点播播放器SDK的播放数据统计。
-   以北京时间（UTC+8）为基准，每天上午9点生成前一天的播放数据统计。
-   支持查询2018-01-01起的数据，数据查询的起止时间跨度最大为90天。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=DescribePlayUserAvg&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribePlayUserAvg|系统规定参数，取值：**DescribePlayUserAvg**。

 |
|StartTime|String|是|2016-06-29T19:00:00Z|起始时间，UTC格式。

 支持查询2018-01-01起的数据，即StartTime大于等于2018-01-01T00:00:00Z。

 |
|EndTime|String|是|2016-06-30T19:00:00Z|结束时间，UTC格式。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|6C7F90B2-BDA4-4FAC-BAAD-A38A121DFE19|请求ID。

 |
|UserPlayStatisAvgs| | |用户每天平均播放均值统计数据。

 |
|AvgPlayCount|String|170|平均播放次数。

 |
|AvgPlayDuration|String|1035902.8|平均播放时长，单位：毫秒。

 |
|Date|String|20170120|日期，yyyyMMdd格式。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=DescribePlayUserAvg
&StartTime=2016-06-29T19:00:00Z
&EndTime=2016-06-30T19:00:00Z
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribePlayUserAvgResponse>
	  <UserPlayStatisAvgs>
		    <UserPlayStatisAvg>
			      <AvgPlayDuration>1035902.8</AvgPlayDuration>
			      <Date>20171127</Date>
			      <AvgPlayCount>17.0</AvgPlayCount>
		    </UserPlayStatisAvg>
		    <UserPlayStatisAvg>
			      <AvgPlayDuration>3113356.7</AvgPlayDuration>
			      <Date>20171128</Date>
			      <AvgPlayCount>41.0</AvgPlayCount>
		    </UserPlayStatisAvg>
		    <UserPlayStatisAvg>
			      <AvgPlayDuration>4290368.0</AvgPlayDuration>
			      <Date>20171129</Date>
			      <AvgPlayCount>59.8</AvgPlayCount>
		    </UserPlayStatisAvg>
	  </UserPlayStatisAvgs>
	  <RequestId>6C7F90B2-BDA4-4FAC-BAAD-A38A121DFE19</RequestId>
</DescribePlayUserAvgResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"UserPlayStatisAvgs":{
		"UserPlayStatisAvg":[
			{
				"AvgPlayDuration":"1035902.8",
				"Date":"20171127",
				"AvgPlayCount":"17.0"
			},
			{
				"AvgPlayDuration":"3113356.7",
				"Date":"20171128",
				"AvgPlayCount":"41.0"
			},
			{
				"AvgPlayDuration":"4290368.0",
				"Date":"20171129",
				"AvgPlayCount":"59.8"
			}
		]
	},
	"RequestId":"6C7F90B2-BDA4-4FAC-BAAD-A38A121DFE19"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。


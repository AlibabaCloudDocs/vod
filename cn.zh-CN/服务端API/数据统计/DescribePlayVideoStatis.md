# DescribePlayVideoStatis {#doc_api_vod_DescribePlayVideoStatis .reference}

调用DescribePlayVideoStatis获取指定视频在指定时间范围内的每日播放统计数据。

-   仅支持使用了阿里云点播播放器SDK的播放数据统计。
-   以北京时间（UTC+8）为基准，每天上午9点生成前一天的播放数据统计。
-   支持查询2018/01/01起的数据，数据查询的起止时间跨度最大为90天。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=DescribePlayVideoStatis&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribePlayVideoStatis|系统规定参数，取值：**DescribePlayVideoStatis**。

 |
|StartTime|String|是|2016-06-29T19:00:00|指定时间段的起始时间，UTC格式。

 |
|EndTime|String|是|2016-06-30T19:00:00Z|指定时间段的结束时间，UTC格式。

 |
|VideoId|String|是|2a8d4cb9ecbb487681473a153aba8fda|指定视频的视频ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|A92D3600-A3E7-43D6-8ED9-B6E3B4A1FE6B|请求ID。

 |
|VideoPlayStatisDetails| | |指定视频每天统计数据。

 |
|Date|String|20170120|日期，yyyyMMdd格式，例如"20170120"。

 |
|PlayDuration|String|967277|播放时长，单位：毫秒。

 |
|PlayRange|String|<=1m:79.2%;\>1<=5m:16.7%;\>5<=10m:4.2%|播放时长分布。

 |
|Title|String|4路（1路加密）：流畅-HLS+标清-MP4+高清-HLS-加密​​​+超清-MP4|视频名称。

 |
|VV|String|24|播放次数。

 |
|UV|String|1|播放用户数。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=DescribePlayVideoStatis
&StartTime=2016-06-29T19:00:00
&EndTime=2016-06-30T19:00:00Z
&VideoId=2a8d4cb9ecbb487681473a153aba8fda
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribePlayVideoStatisResponse>
	  <RequestId>A92D3600-A3E7-43D6-8ED9-B6E3B4A1FE6B</RequestId>
	  <VideoPlayStatisDetails>
		    <VideoPlayStatisDetail>
			      <Date>20180101</Date>
			      <PlayDuration>3288</PlayDuration>
			      <PlayRange>&lt;=1m:79.2%;&gt;1&lt;=5m:16.7%;&gt;5&lt;=10m:4.2%</PlayRange>
			      <Title>4路（1路加密）：流畅-HLS+标清-MP4+高清-HLS-加密​​​+超清-MP4</Title>
			      <UV>1</UV>
			      <VV>1</VV>
		    </VideoPlayStatisDetail>
		    <VideoPlayStatisDetail>
			      <Date>20180102</Date>
			      <PlayDuration>967277</PlayDuration>
			      <PlayRange>&lt;=1m:79.2%;&gt;1&lt;=5m:16.7%;&gt;5&lt;=10m:4.2%</PlayRange>
			      <Title>4路（1路加密）：流畅-HLS+标清-MP4+高清-HLS-加密​​​+超清-MP4</Title>
			      <UV>1</UV>
			      <VV>24</VV>
		    </VideoPlayStatisDetail>
	  </VideoPlayStatisDetails>
</DescribePlayVideoStatisResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"VideoPlayStatisDetails":{
		"VideoPlayStatisDetail":[
			{
				"PlayRange":"<=1m:79.2%;>1<=5m:16.7%;>5<=10m:4.2%",
				"PlayDuration":"3288",
				"Date":"20180101",
				"VV":"1",
				"UV":"1",
				"Title":"4路（1路加密）：流畅-HLS+标清-MP4+高清-HLS-加密​​​+超清-MP4"
			},
			{
				"PlayRange":"<=1m:79.2%;>1<=5m:16.7%;>5<=10m:4.2%",
				"PlayDuration":"967277",
				"Date":"20180102",
				"VV":"24",
				"UV":"1",
				"Title":"4路（1路加密）：流畅-HLS+标清-MP4+高清-HLS-加密​​​+超清-MP4"
			}
		]
	},
	"RequestId":"A92D3600-A3E7-43D6-8ED9-B6E3B4A1FE6B"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。


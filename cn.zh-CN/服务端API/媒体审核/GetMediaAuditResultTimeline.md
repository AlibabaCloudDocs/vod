# GetMediaAuditResultTimeline {#doc_api_vod_GetMediaAuditResultTimeline .reference}

调用GetMediaAuditResultTimeline获取到所有违规内容截图的时间点。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=GetMediaAuditResultTimeline&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetMediaAuditResultTimeline|系统规定参数，取值：**GetMediaAuditResultTimeline**。

 |
|MediaId|String|是|XXXXX|视频ID。

 |
|AccessKeyId|String|否|your\_accesskey\_id|您的AccessKey ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|MediaAuditResultTimeline| | |审核结果时间线的集合。

 |
|Porn| | |鉴黄时间线集合。

 |
|Label|String|porn|审核结果分类。当场景为鉴黄时，取值范围：

 -   porn\(色情\)
-   sexy\(性感\)
-   normal\(普通\)

 |
|Score|String|100.00|审核结果分类的分值。取值范围`[0, 100]`，精度小数点后10位。结果为对应分类Label的概率，值越高，越趋于该分类。

 |
|Timestamp|String|3005|视频中的位置。单位：毫秒。

 |
|Terrorism| | |暴恐时间线集合。

 |
|Label|String|normal|审核结果分类。当场景是暴恐时，取值范围：

 -   terrorism\(暴恐\)
-   outfit\(特殊装束\)
-   logo\(特殊标识\)
-   weapon\(武器\)
-   politics\(渉政\)
-   others\(其它暴恐渉政\)
-   normal\(正常\)

 |
|Score|String|100.00|审核结果分类的分值。

 |
|Timestamp|String|3005|视频中的位置。单位：毫秒。

 |
|RequestId|String|6438BD76-D523-46FC-956F-XXXXXX|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=GetMediaAuditResultTimeline
&MediaId=XXXXX
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<GetMediaAuditResultTimelineResponse>
  <RequestId>6438BD76-D523-46FC-956F-XXXXXX</RequestId>
	  <MediaAuditResultTimeline>
		    <Porn>
			      <Label>porn</Label>
			      <Score>100.0000000000</Score>
			      <Timestamp>5</Timestamp>
		    </Porn>
		    <Porn>
			      <Label>porn</Label>
			      <Score>100.0000000000</Score>
			      <Timestamp>1005</Timestamp>
		    </Porn>
		    <Terrorism>
			      <Label>terrorism</Label>
			      <Score>100.0000000000</Score>
			      <Timestamp>5005</Timestamp>
		    </Terrorism>
		    <Terrorism>
			      <Label>terrorism</Label>
			      <Score>100.0000000000</Score>
			      <Timestamp>7005</Timestamp>
		    </Terrorism>
	  </MediaAuditResultTimeline>
</GetMediaAuditResultTimelineResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"6438BD76-D523-46FC-956F-XXXXXX",
	"MediaAuditResultTimeline":{
		"Terrorism":[
			{
				"Label":"terrorism",
				"Score":"100.0000000000",
				"Timestamp":"5005"
			},
			{
				"Label":"terrorism",
				"Score":"100.0000000000",
				"Timestamp":"7005"
			}
		],
		"Porn":[
			{
				"Label":"porn",
				"Score":"100.0000000000",
				"Timestamp":"5"
			},
			{
				"Label":"porn",
				"Score":"100.0000000000",
				"Timestamp":"1005"
			}
		]
	}
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。


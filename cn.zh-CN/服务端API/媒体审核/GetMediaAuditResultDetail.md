# GetMediaAuditResultDetail {#doc_api_vod_GetMediaAuditResultDetail .reference}

调用GetMediaAuditResultDetail获取智能审核结果详情。通过此接口可实时查询审核结果详情。

**说明：** 

-   默认只返回违规、疑似违规的审核截图详情。
-   审核结果的图片资源仅在点播提供的免费存储上保留2周，超过2周将自动删除。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=GetMediaAuditResultDetail&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetMediaAuditResultDetail|系统规定参数，取值：**GetMediaAuditResultDetail**。

 |
|MediaId|String|是|XXXXX|视频ID。

 |
|PageNo|Integer|是|1|视频内容审核结果页码，默认值为**1**，每页最多返回**20**条记录。

 |
|AccessKeyId|String|否|your\_accesskey\_id|您的AccessKey ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|MediaAuditResultDetail| | |审核结果详情。

 |
|List| | |视频审核结果详情列表。

 |
|PornLabel|String|normal|鉴黄命中标签。取值：

 -   normal\(普通\)
-   porn\(色情\)
-   sexy\(性感\)

 |
|PornScore|String|100.00|取值范围`[0, 100]`，精度小数点后10位。结果为对应分类Label的概率；值越高越趋于该分类；取值为`[0.00-100.00]`。

 |
|TerrorismLabel|String|normal|暴恐涉政命中标签，取值：

 -   normal\(普通\)
-   terrorism\(暴恐\)
-   outfit\(特殊装束\)
-   logo\(特殊标识\)
-   weapon\(武器\)
-   politics\(渉政\)
-   others\(其它暴恐渉政\)

 |
|TerrorismScore|String|100.00|取值范围`[0, 100]`，精度小数点后10位。结果为对应分类Label的概率；值越高越趋于该分类；取值为`[0.00-100.00]`。

 |
|Timestamp|String|3005|视频中的位置。单位：毫秒。

 |
|Url|String|XXXXX|图片的地址。

 |
|Total|Integer|2|视频审核结果截图总数量。

 |
|RequestId|String|6438BD76-D523-46FC-956F-XXXXX|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=GetMediaAuditResultDetail
&MediaId=XXXXX
&PageNo=1
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<GetMediaAuditResultDetailResponse>
	  <RequestId>6438BD76-D523-46FC-956F-XXXXX</RequestId>
	  <MediaAuditResultDetail>
		    <Total>2</Total>
		    <List>
			      <TerrorismLabel>normal</TerrorismLabel>
			      <PornLabel>porn</PornLabel>
			      <TerrorismScore>100.0000000000</TerrorismScore>
			      <PornScore>65.4900000000</PornScore>
			      <Url>XXXXX</Url>
			      <Timestamp>5</Timestamp>
		    </List>
		    <List>
			      <TerrorismLabel>normal</TerrorismLabel>
			      <PornLabel>porn</PornLabel>
			      <TerrorismScore>100.0000000000</TerrorismScore>
			      <PornScore>80.5400000000</PornScore>
			      <Url>XXXXX</Url>
			      <Timestamp>2005</Timestamp>
		    </List>
	  </MediaAuditResultDetail>
</GetMediaAuditResultDetailResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"6438BD76-D523-46FC-956F-XXXXX",
	"MediaAuditResultDetail":{
		"List":[
			{
				"PornLabel":"porn",
				"TerrorismLabel":"normal",
				"Url":"XXXXX",
				"PornScore":"65.4900000000",
				"Timestamp":"5",
				"TerrorismScore":"100.0000000000"
			},
			{
				"PornLabel":"porn",
				"TerrorismLabel":"normal",
				"Url":"XXXXX",
				"PornScore":"80.5400000000",
				"Timestamp":"2005",
				"TerrorismScore":"100.0000000000"
			}
		],
		"Total":2
	}
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。


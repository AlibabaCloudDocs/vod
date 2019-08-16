# CreateAudit {#doc_api_vod_CreateAudit .reference}

调用CreateAudit进行人工审核，可用于审核视频、音频等媒体信息。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=CreateAudit&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateAudit|系统规定参数，取值：**CreateAudit**。

 |
|AuditContent|String|是|\[\{"VideoId":"93ab850b4f6f44eab54b6e91d24d81d4","Status":"Normal"\},\{"VideoId":"43ab850b4f6f44eab54b6e91d24d81d3","Status":"Blocked","Reason":"色情视频","Comment":"有露点镜"\}\]|审核内容数组，一次最多支持20个视频的审核内容。需将数组转为字符串后作为参数值。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|25818875-5F78-4A13-BEF6-D7393642CA58|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=CreateAudit
&AuditContent=[{"VideoId":"93ab850b4f6f44eab54b6e91d24d81d4","Status":"Normal"},{"VideoId":"43ab850b4f6f44eab54b6e91d24d81d3","Status":"Blocked","Reason":"色情视频","Comment":"有露点镜"}]
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CreateAuditResponse>
  <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
</CreateAuditResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"25818875-5F78-4A13-BEF6-D7393642CA58"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。


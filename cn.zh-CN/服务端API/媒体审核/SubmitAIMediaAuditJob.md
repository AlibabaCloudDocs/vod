# SubmitAIMediaAuditJob {#doc_api_vod_SubmitAIMediaAuditJob .reference}

调用SubmitAIMediaAuditJob提交智能审核作业。作业在提交成功后会异步执行，不保证接口返回时作业已处理完成。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=SubmitAIMediaAuditJob&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|SubmitAIMediaAuditJob|系统规定参数，取值：**SubmitAIMediaAuditJob**。

 |
|MediaId|String|是|XXXXX|视频ID。

 |
|TemplateId|String|是|XXXXXXX|AI模版ID。不指定时使用智能审核默认AI模版ID。

 |
|AccessKeyId|String|否|your\_accesskey\_id|您的AccessKey ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|JobId|String|XXXXXXX|作业ID。

 |
|MediaId|String|XXXXXXX|视频ID。

 |
|RequestId|String|25818875-5F78-4A13-BEF6-XXXXXXX|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=SubmitAIMediaAuditJob
&MediaId=XXXXX
&TemplateId=XXXXXXX
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<SubmitAIMediaAuditJobResponse>
	  <RequestId>25818875-5F78-4A13-BEF6-XXXXXXX</RequestId>
	  <MediaId>XXXXXXX</MediaId>
	  <JobId>XXXXXXX</JobId>
</SubmitAIMediaAuditJobResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"JobId":"XXXXXXX",
	"RequestId":"25818875-5F78-4A13-BEF6-XXXXXXX",
	"MediaId":"XXXXXXX"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。


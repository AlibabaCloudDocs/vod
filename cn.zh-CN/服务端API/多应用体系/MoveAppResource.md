# MoveAppResource {#doc_api_vod_MoveAppResource .reference}

调用MoveAppResource将媒资等资源从一个应用迁移到另外一个应用。

应用管理员可以直接转移，子账号或角色需要对资源转移前后的两个应用拥有写权限，支持批量迁移。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=MoveAppResource&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|MoveAppResource|系统规定参数，取值：**MoveAppResource**。

 |
|ResourceIds|String|是|xxx,xxx|资源ID， 多个以英文逗号分隔，一次最多20条。

 |
|ResourceType|String|是|video|资源类型。

 支持video（视频），image（图片），attached（辅助媒资）。

 |
|TargetAppId|String|是|app-xxxxx|目标应用ID。

 |
|AccessKeyId|String|否|your\_accesskey\_id|您的AccessKey ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|FailedResourceIds| |xxxxx|失败的资源ID。

 |
|NonExistResourceIds| |xxxxx|不存在的资源ID。

 |
|RequestId|String|25818875-5F78-4A13-BEF6-XXXXXX|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=MoveAppResource
&ResourceIds=xxx,xxx
&ResourceType=video
&TargetAppId=app-xxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<MoveAppResourceResponse>
	  <RequestId>25818875-5F78-4A13-BEF6-XXXXXX</RequestId>
	  <FailedResourceIds>xxxxx</FailedResourceIds>
	  <NonExistResourceIds>xxxxx</NonExistResourceIds>
</MoveAppResourceResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"FailedResourceIds":"xxxxx",
	"RequestId":"25818875-5F78-4A13-BEF6-XXXXXX",
	"NonExistResourceIds":"xxxxx"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。


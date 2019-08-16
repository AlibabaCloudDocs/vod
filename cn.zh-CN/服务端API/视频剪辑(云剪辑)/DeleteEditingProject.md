# DeleteEditingProject {#doc_api_vod_DeleteEditingProject .reference}

调用DeleteEditingProject删除云剪辑工程，支持批量删除。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=DeleteEditingProject&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteEditingProject|系统规定参数。取值：**DeleteEditingProject**。

 |
|ProjectIds|String|是|fb2101bf24bf41c78b2754cb318787dc|云剪辑工程ID。支持多个云剪辑工程，以逗号分隔。

 |
|AccessKeyId|String|否|your\_accesskey\_id|您的AccessKey ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|25818875-5F78-4A13-BEF6-D7393642CA58|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=DeleteEditingProject
&ProjectIds=fb2101bf24bf41c78b2754cb318787dc
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DeleteEditingProjectResponse>
  <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
</DeleteEditingProjectResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"25818875-5F78-4A13-BEF6-D7393642CA58"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。


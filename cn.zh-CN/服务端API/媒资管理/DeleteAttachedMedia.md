# DeleteAttachedMedia {#doc_api_vod_DeleteAttachedMedia .reference}

调用DeleteAttachedMedia删除辅助媒资，支持批量删除。

**说明：** 此接口为物理删除辅助媒资，且无法恢复，请谨慎操作。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=DeleteAttachedMedia&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteAttachedMedia|系统规定参数。取值：**DeleteAttachedMedia**。

 |
|AccessKeyId|String|否|your\_accesskey\_id|您的AccessKey ID。

 |
|MediaIds|String|否|xxxxxxxx,xxxxxxxxx|辅助媒资ID列表。多个用逗号分隔。最多支持20个。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|NonExistMediaIds| |\["xxxx", "xxxx", "xxxx"\]|删除失败的辅助媒资ID。

 |
|RequestId|String|25818875-5F78-4A13-BEF6-D7393642CA58|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=DeleteAttachedMedia
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DeleteAttachedMediaResponse>
	  <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
	  <NonExistMediaIds>xxxx</NonExistMediaIds>
	  <NonExistMediaIds>xxxx</NonExistMediaIds>
	  <NonExistMediaIds>xxxx</NonExistMediaIds>
</DeleteAttachedMediaResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"NonExistMediaIds":[
		"xxxx",
		"xxxx",
		"xxxx"
	],
	"RequestId":"25818875-5F78-4A13-BEF6-D7393642CA58"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。


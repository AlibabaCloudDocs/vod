# SetEditingProjectMaterials {#doc_api_vod_SetEditingProjectMaterials .reference}

调用SetEditingProjectMaterials设置云剪辑工程的待剪辑素材。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=SetEditingProjectMaterials&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|SetEditingProjectMaterials|系统规定参数。取值：**SetEditingProjectMaterials**。

 |
|MaterialIds|String|是|9e3101bf24bf41c78b275123318788ca|素材ID。即媒资ID，如视频VideoId、图片ImageId、辅助媒资MediaId等。支持多个素材，以逗号分隔。

 |
|ProjectId|String|是|fb2101bf24bf41c78b2754cb318787dc|云剪辑工程ID。

 |
|AccessKeyId|String|否|your\_accesskey\_id|您的AccessKey ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|746FFA07-8BBB-468B-8BB1-3E94E3B2915E|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=SetEditingProjectMaterials
&MaterialIds=9e3101bf24bf41c78b275123318788ca
&ProjectId=fb2101bf24bf41c78b2754cb318787dc
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<SetEditingProjectMaterialsResponse>
  <RequestId>9262E3DA-07FA-48CA-A362-FCBB6BC61D08</RequestId>
</SetEditingProjectMaterialsResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"9262E3DA-07FA-48CA-A362-FCBB6BC61D08"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。


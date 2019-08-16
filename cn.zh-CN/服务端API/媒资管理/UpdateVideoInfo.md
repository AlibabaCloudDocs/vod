# UpdateVideoInfo {#doc_api_vod_UpdateVideoInfo .reference}

调用UpdateVideoInfo修改视频信息。

**说明：** 传入参数则更新相应字段，否则该字段不会被覆盖或更新。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=UpdateVideoInfo&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|UpdateVideoInfo|系统规定参数，取值：**UpdateVideoInfo**。

 |
|VideoId|String|是|2deda932654a40878312baf9b0ed810d|视频ID。

 |
|CateId|Long|否|38476|视频分类ID。

 |
|CoverURL|String|否|https://image.example.com/coversample.jpg|视频封面URL地址。

 |
|Description|String|否|阿里云视频描述|视频描述，长度不超过1024个字节，UTF8编码。

 |
|Tags|String|否|标签1,标签2|视频标签，单个标签不超过32字节，最多不超过16个标签。多个用逗号分隔，UTF8编码。

 |
|Title|String|否|阿里云VOD视频标题|视频标题，长度不超过128个字节，UTF8编码。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|e8366bb2-4be7-4cdd-823d-97fd2d52dacf|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=UpdateVideoInfo
&VideoId=2deda932654a40878312baf9b0ed810d
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<UpdateVideoInfoResponse>
  <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
</UpdateVideoInfoResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"25818875-5F78-4A13-BEF6-D7393642CA58"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。


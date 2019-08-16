# UpdateImageInfos {#doc_api_vod_UpdateImageInfos .reference}

调用UpdateImageInfos批量修改图片信息。

**说明：** 传入参数则更新相应字段。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=UpdateImageInfos&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|UpdateImageInfos|系统规定参数。取值：**UpdateImageInfos**。

 |
|UpdateContent|String|是|\[\{"ImageId":"ff8fe57e3461416c9d40d66a267a4e09","Title":"标题","Description":"描述","Tags":"标签1,标签2"\}\]|更新内容。一次最多支持修改20个图片的视频信息。

 **说明：** Title、Description、Tags 更新内容中不能包含表情符。

 |
|AccessKeyId|String|否|your\_id|您的AccessKey ID。

 |
|ResourceRealOwnerId|Long|否|346547|资源所有者ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|NonExistImageIds| |f45cf4eba5c84d25b90233389558c39|不存在的图片ID列表。

 |
|RequestId|String|25818875-5F78-4A13-BEF6-D7393642CA58|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=UpdateImageInfos
&UpdateContent=[{"ImageId":"ff8fe57e3461416c9d40d66a267a4e09","Title":"标题","Description":"描述","Tags":"标签1,标签2"}]
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<UpdateImageInfosResponse>
	  <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
	  <NonExistImageIds>f45cf4eba5c84d25b90233389558c39</NonExistImageIds>
</UpdateImageInfosResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"25818875-5F78-4A13-BEF6-D7393642CA58",
	"NonExistImageIds":[
		"f45cf4eba5c84d25b90233389558c39"
	]
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。


# UpdateCategory {#doc_api_vod_UpdateCategory .reference}

调用UpdateCategory修改视频分类。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=UpdateCategory&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|UpdateCategory|系统规定参数，取值：**UpdateCategory**。

 |
|CateId|Long|是|706363|分类ID。

 |
|CateName|String|是|阿里云分类名称|分类名称，不能超过64个字节，UTF8编码。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|712437b0-bc30-4e6b-a22c-aea4f4bf397a|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://vod.cn-shanghai.aliyuncs.com/?Action=UpdateCategory
&CateId=706363
&CateName=阿里云分类名称
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<UpdateCategoryResponse>
  <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
</UpdateCategoryResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"25818875-5F78-4A13-BEF6-D7393642CA58"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。


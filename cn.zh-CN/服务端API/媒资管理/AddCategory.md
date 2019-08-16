# AddCategory {#doc_api_vod_AddCategory .reference}

调用AddCategory创建视频分类。最大支持三级分类，每个分类最多支持创建100个子分类。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=AddCategory&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|AddCategory|系统规定参数，取值：**AddCategory**。

 |
|CateName|String|是|35018bc7-efab-420a-abda-777795695b2a|分类名称，不能超过64个字节，UTF8编码。

 |
|ParentId|Long|否|620963913456741794|父分类ID。若不填，则默认生成一级分类，根节点分类ID为**-1**。

 |
|Type|String|否|Video|素材片段类型。取值：

 -   **Video（默认）**：视频
-   **Image**：图片

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|206ae7a0-33d5-4c57-b1da-bef743e21e6e|请求ID。

 |
|Category| | |视频分类信息。

 |
|CateId|Long|100|视频分类ID。

 |
|CateName|String|电影|分类名称，最大64字节，UTF8编码。

 |
|Level|Long|0|分类层级，一级分类层级为**0**。

 |
|ParentId|Long|-1|父分类ID，一级分类父ID为**-1**。

 |
|Type|String|Video|素材片段类型。取值：

 -   **Video（默认）**：视频
-   **Image**：图片

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=AddCategory
&CateName=35018bc7-efab-420a-abda-777795695b2a
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<AddCategoryResponse>
	  <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
	  <Category>
		    <CateId>67788823</CateId>
		    <CateName>exampleCategory</CateName>
		    <ParentId>-1</ParentId>
		    <Level>0</Level>
	  </Category>
</AddCategoryResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Category":{
		"ParentId":-1,
		"CateId":67788823,
		"CateName":"exampleCategory",
		"Level":0
	},
	"RequestId":"25818875-5F78-4A13-BEF6-D7393642CA58"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。


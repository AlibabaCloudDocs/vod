# GetCategories {#doc_api_vod_GetCategories .reference}

调用GetCategories获取指定的分类信息，及其子分类（即下一级分类）的列表。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=GetCategories&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetCategories|系统规定参数，取值：**GetCategories**。

 |
|CateId|Long|否|49339|分类ID，默认为根节点分类ID，即**-1**。

 |
|PageNo|Long|否|1|子分类列表页号，默认值为**1**。

 |
|PageSize|Long|否|10|子分类列表页大小，默认值为**10**，最大值为**100**。

 |
|SortBy|String|否|CreationTime:Desc|排序字段和排序顺序，多个用逗号分隔。按创建时间排序。取值范围：

 -   **CreationTime:Desc**
-   **CreationTime:Asc**

 **说明：** 排序字段示例：[排序字段](https://help.aliyun.com/document_detail/99179.html?spm=a2c4g.11186623.2.20.7e036ad8dnvm2w#%E4%BD%BF%E7%94%A8%E7%A4%BA%E4%BE%8B)。

 获取搜索条件是前5000条的数据时，最多支持三个排序字段。

 获取搜索条件是所有数据时，仅支持一个排序字段。

 |
|Type|String|否|Video|素材片段类型。取值：

 -   **Video（默认值）**：视频
-   **Image**：图片

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|58487735-34c9-41ca-91fd-37b8a4c37ea5|请求ID。

 |
|SubTotal|Long|3795|子分类总数。

 |
|Category| | |指定分类的信息。

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

 -   **Video（默认值）**：视频
-   **Image**：图片

 |
|SubCategories| | |子分类列表。

 |
|CateId|Long|100|视频分类ID。

 |
|CateName|String|电影|分类名称，最大64字节，UTF8编码。

 |
|Level|Long|0|分类层级，一级分类层级为**0**。

 |
|ParentId|Long|-1|父分类ID，一级分类父ID为**-1**。

 |
|SubTotal|Long|3795|子分类总数。

 |
|Type|String|Video|素材片段类型。取值：

 -   **Video（默认值）**：视频
-   **Image**：图片

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=GetCategories
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<GetCategoriesResponse>
  <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
	  <Category>
		    <CateId>67788823</CateId>
		    <CateName>exampleCategory-A</CateName>
		    <ParentId>-1</ParentId>
		    <Level>0</Level>
	  </Category>
	  <SubTotal>2</SubTotal>
	  <SubCategories>
		    <Category>
			      <CateId>87788825</CateId>
			      <CateName>exampleCategory-A-sub1</CateName>
			      <ParentId>67788823</ParentId>
			      <Level>1</Level>
		    </Category>
		    <Category>
			      <CateId>87788826</CateId>
			      <CateName>exampleCategory-A-sub2</CateName>
			      <ParentId>67788823</ParentId>
			      <Level>1</Level>
		    </Category>
	  </SubCategories>
</GetCategoriesResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"SubTotal":2,
	"Category":{
		"ParentId":-1,
		"CateId":67788823,
		"CateName":"exampleCategory-A",
		"Level":0
	},
	"RequestId":"25818875-5F78-4A13-BEF6-D7393642CA58",
	"SubCategories":{
		"Category":[
			{
				"ParentId":67788823,
				"CateId":87788825,
				"CateName":"exampleCategory-A-sub1",
				"Level":1
			},
			{
				"ParentId":67788823,
				"CateId":87788826,
				"CateName":"exampleCategory-A-sub2",
				"Level":1
			}
		]
	}
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。


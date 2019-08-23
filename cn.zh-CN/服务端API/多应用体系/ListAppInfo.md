# ListAppInfo {#doc_api_vod_ListAppInfo .reference}

调用ListAppInfo根据查询条件获取有权限的应用信息列表。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=ListAppInfo&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListAppInfo|系统规定参数，取值：**ListAppInfo**。

 |
|AccessKeyId|String|否|your\_accesskey\_id|您的AccessKey ID。

 |
|PageNo|Integer|否|1|页号。默认从1开始。

 |
|PageSize|Integer|否|10|每页返回条数。默认值为**10**，最大值为**100**。

 |
|Status|String|否|Normal|应用状态。取值范围：**Normal**（正常），**Disable**（停用）。应用创建后默认为Normal。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|AppInfoList| | |应用信息列表。

 |
|AppId|String|app-xxxxxx|应用ID。

 |
|AppName|String|test|应用名称。

 |
|CreationTime|String|2019-03-01T08:00:00Z|UTC创建时间。

 |
|Description|String|my first app.|应用描述。

 |
|ModificationTime|String|2019-03-01T08:00:00Z|UTC更新时间。

 |
|Status|String|Normal|应用状态。取值范围：**Normal**（正常），**Disable**（停用）。

 |
|Type|String|System|应用类型。取值：System（系统默认），Custom（用户创建）。

 |
|RequestId|String|25818875-5F78-4A13-BEF6-D7393642CA58|请求ID。

 |
|Total|Integer|10|总条目。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=ListAppInfo
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ListAppInfoResponse>
	  <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
	  <Total>10</Total>
	  <AppInfoList>
		    <AppId>app-xxxxxx</AppId>
		    <AppName>xxxx</AppName>
		    <Description>xxxx</Description>
		    <Type>Custom</Type>
		    <Status>Normal</Status>
		    <CreationTime>2019-03-01T08:00:00Z</CreationTime>
		    <ModificationTime>2019-03-02T08:00:00Z</ModificationTime>
	  </AppInfoList>
</ListAppInfoResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"25818875-5F78-4A13-BEF6-D7393642CA58",
	"AppInfoList":[
		{
			"CreationTime":"2019-03-01T08:00:00Z",
			"Status":"Normal",
			"Description":"xxxx",
			"ModificationTime":"2019-03-02T08:00:00Z",
			"Type":"Custom",
			"AppId":"app-xxxxxx",
			"AppName":"xxxx"
		}
	],
	"Total":10
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。


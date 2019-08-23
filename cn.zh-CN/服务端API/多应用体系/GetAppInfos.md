# GetAppInfos {#doc_api_vod_GetAppInfos .reference}

调用GetAppInfos通过应用ID查询应用信息，支持批量查询。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=GetAppInfos&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetAppInfos|系统规定参数，取值：**GetAppInfos**。

 |
|AppIds|String|是|app-xxxxx|应用ID列表，最多支持10个，多个使用英文逗号分隔。

 |
|AccessKeyId|String|否|your\_accesskey\_id|您的AccessKey ID。

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
|Status|String|Normal|应用状态。取值：**Normal（正常）**，**Disable（停用）**。

 |
|Type|String|System|应用类型。取值：**System（系统默认）**，**Custom（用户创建）**。

 |
|NonExistAppIds| |xxxx|不存在的应用ID列表。

 |
|RequestId|String|25818875-5F78-4A13-BEF6-D7393642CA58|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=GetAppInfos
&AppIds=app-xxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<GetAppInfosResponse>
	  <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
	  <AppInfoList>
		    <AppId>app-xxxxxx</AppId>
		    <AppName>xxxx</AppName>
		    <Description>xxxx</Description>
		    <Type>Custom</Type>
		    <Status>Normal</Status>
		    <CreationTime>2019-03-01T08:00:00Z</CreationTime>
		    <ModificationTime>2019-03-02T08:00:00Z</ModificationTime>
	  </AppInfoList>
</GetAppInfosResponse>
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
	]
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。


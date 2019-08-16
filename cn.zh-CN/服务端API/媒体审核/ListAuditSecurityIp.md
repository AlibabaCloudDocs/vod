# ListAuditSecurityIp {#doc_api_vod_ListAuditSecurityIp .reference}

调用ListAuditSecurityIp获取审核安全IP列表。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=ListAuditSecurityIp&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListAuditSecurityIp|系统规定参数。取值：**ListAuditSecurityIp**。

 |
|SecurityGroupName|String|否|Default|审核安全IP分组名称，默认获取所有。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|664BBD08-C7DB-4E6C-A873-9D0958D9A899|请求ID。

 |
|SecurityIpList| | |审核安全IP详情。

 |
|CreationTime|String|2018-05-22T06:54:23Z|创建时间。

 |
|Ips|String|30.27.14.0/24,30.39.127.245|安全IP列表。

 |
|ModificationTime|String|2018-05-22T06:54:23Z|更新时间。

 |
|SecurityGroupName|String|Default|安全IP组名称。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=ListAuditSecurityIp
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ListAuditSecurityIpResponse>
	  <SecurityGroupList>
		    <SecurityGroupName>Default</SecurityGroupName>
		    <Ips>30.27.14.0/24,30.39.127.245</Ips>
		    <CreationTime>2018-05-22T06:54:23Z</CreationTime>
		    <ModifyTime>2018-05-22T06:55:14Z</ModifyTime>
	  </SecurityGroupList>
	  <RequestId>664BBD08-C7DB-4E6C-A873-9D0958D9A899</RequestId>
</ListAuditSecurityIpResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"664BBD08-C7DB-4E6C-A873-9D0958D9A899",
	"SecurityGroupList":[
		{
			"CreationTime":"2018-05-22T06:54:23Z",
			"SecurityGroupName":"Default",
			"ModifyTime":"2018-05-22T06:55:14Z",
			"Ips":"30.27.14.0/24,30.39.127.245"
		}
	]
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。


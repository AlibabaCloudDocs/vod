# ListAppPoliciesForIdentity {#doc_api_vod_ListAppPoliciesForIdentity .reference}

调用ListAppPoliciesForIdentity列出指定账号身份（RAM子账号或RAM角色）被授予的应用权限的列表。

-   最多返回前100条数据。
-   只有拥有管理员权限的账号身份调用该接口时，IdentityType和IdentityName有效；否则只返回当前账号身份被授予的应用权限策略。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=ListAppPoliciesForIdentity&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListAppPoliciesForIdentity|系统规定参数，取值：**ListAppPoliciesForIdentity**。

 |
|IdentityName|String|是|xxxxx|-   类型为RamUser时，传入RAM子账号ID。
-   类型为RamRole时，传入角色名称。

 |
|IdentityType|String|是|RamUser|身份类型。取值：**RamUser**（RAM子账号）, **RamRole**（RAM角色）。

 |
|AppId|String|否|app-xxxxxx|应用ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|AppPolicyList| | |权限策略名称列表。

 |
|AppId|String|app-xxxxx|应用ID。

 |
|CreationTime|String|2019-01-01T01:01:01Z|UTC创建时间。

 |
|Description|String|App full access permission|策略描述。

 |
|ModificationTime|String|2019-01-01T01:01:01Z|UTC更新时间。

 |
|PolicyName|String|VODAppFullAccess|策略名称。

 |
|PolicyType|String|System|策略类型。

 |
|PolicyValue|String|xxxxx|策略值。

 |
|RequestId|String|7B8A4E7D-6CFF-471D-84DF-XXXXXX|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=ListAppPoliciesForIdentity
&IdentityName=xxxxx
&IdentityType=RamUser
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ListAppPoliciesForIdentityResponse>
  <AppPolicyList>
		    <AppId>app-xxxxx</AppId>
		    <PolicyType>System</PolicyType>
		    <PolicyName>VODAppFullAccess</PolicyName>
		    <CreationTime>2019-01-01T01:01:01Z</CreationTime>
		    <Description>App full access permission</Description>
	  </AppPolicyList>
	  <AppPolicyList>
		    <AppId>app-xxxxx</AppId>
		    <PolicyType>System</PolicyType>
		    <PolicyName>VODAppReadOnlyAccess</PolicyName>
		    <CreationTime>2019-01-01T01:01:01Z</CreationTime>
		    <Description>App read only access permission</Description>
	  </AppPolicyList>
	  <RequestId>7B8A4E7D-6CFF-471D-84DF-XXXXXX</RequestId>
</ListAppPoliciesForIdentityResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"7B8A4E7D-6CFF-471D-84DF-XXXXXX",
	"AppPolicyList":[
		{
			"CreationTime":"2019-01-01T01:01:01Z",
			"Description":"App full access permission",
			"PolicyName":"VODAppFullAccess",
			"AppId":"app-xxxxx",
			"PolicyType":"System"
		},
		{
			"CreationTime":"2019-01-01T01:01:01Z",
			"Description":"App read only access permission",
			"PolicyName":"VODAppReadOnlyAccess",
			"AppId":"app-xxxxx",
			"PolicyType":"System"
		}
	]
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。


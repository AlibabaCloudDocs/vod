# DetachAppPolicyFromIdentity {#doc_api_vod_DetachAppPolicyFromIdentity .reference}

调用DetachAppPolicyFromIdentity为指定账号身份（RAM子账号或RAM角色）撤销指定的应用授权。

**说明：** 每个子账号或角色最多授予10个应用权限。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=DetachAppPolicyFromIdentity&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DetachAppPolicyFromIdentity|系统规定参数，取值：**DetachAppPolicyFromIdentity**。

 |
|AppId|String|是|app-xxxx|应用ID。当策略名称为VODAppAdministratorAccess时，该字段非必选，其他策略时，该字段必填。

 |
|IdentityName|String|是|xxxxx|-   类型为RamUser时，传入RAM子账号ID。
-   类型为RamRole时，传入角色名称。

 |
|IdentityType|String|是|RamUser|身份类型，取值：**RamUser**（RAM子账号）, **RamRole**（RAM角色）。

 |
|PolicyNames|String|是|VODAppFullAccess|策略名称，暂时只支持设置为系统策略，多个用英文逗号分隔。

 可选值：**VODAppFullAccess**，**VODAppReadOnlyAccess**，**VODAppAdministratorAccess**。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|FailedPolicyNames| |xxxx|失败的策略名称。

 |
|NonExistPolicyNames| |xxxx|不存在的策略名称。

 |
|RequestId|String|25818875-5F78-4A13-BEF6-D7393642C|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=DetachAppPolicyFromIdentity
&AppId=app-xxxx
&IdentityName=xxxxx
&IdentityType=RamUser
&PolicyNames=VODAppFullAccess
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DetachAppPolicyFromIdentityResponse>
	  <RequestId>25818875-5F78-4A13-BEF6-D7393642C</RequestId>
	  <FailedPolicyNames>xxxx</FailedPolicyNames>
	  <NonExistPolicyNames>xxxxx</NonExistPolicyNames>
</DetachAppPolicyFromIdentityResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"NonExistPolicyNames":"xxxxx",
	"RequestId":"25818875-5F78-4A13-BEF6-D7393642C",
	"FailedPolicyNames":"xxxx"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。


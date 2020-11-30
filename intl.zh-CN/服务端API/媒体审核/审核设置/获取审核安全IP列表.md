# 获取审核安全IP列表

调用ListAuditSecurityIp获取审核安全IP列表。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=ListAuditSecurityIp&type=RPC&version=2017-03-21)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListAuditSecurityIp|系统规定参数。取值：**ListAuditSecurityIp**。 |
|SecurityGroupName|String|否|Default|审核安全IP分组名称。默认获取所有。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|664BBD08-C7DB-4E\*\*\*\*\*73-9D0958D9A899|请求ID。 |
|SecurityIpList|Array of SecurityIp| |审核安全IP详情。 |
|CreationTime|String|2018-05-22T06:54:23Z|创建时间。格式为：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。 |
|Ips|String|30.27.14.0/24,30.39.127.245|安全IP列表。 |
|ModificationTime|String|2018-05-22T06:54:23Z|更新时间。格式为：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。 |
|SecurityGroupName|String|Default|安全IP组名称。 |

## 示例

请求示例

```
https://vod.aliyuncs.com/?Action=ListAuditSecurityIp
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<ListAuditSecurityIpResponse>
	  <SecurityGroupList>
		    <SecurityGroupName>Default</SecurityGroupName>
		    <Ips>30.27.14.0/24,30.39.127.245</Ips>
		    <CreationTime>2018-05-22T06:54:23Z</CreationTime>
		    <ModifyTime>2018-05-22T06:55:14Z</ModifyTime>
	  </SecurityGroupList>
	  <RequestId>664BBD08-C7DB-4E*****73-9D0958D9A899</RequestId>
</ListAuditSecurityIpResponse>
```

`JSON` 格式

```
{
    "SecurityGroupList":[
        {
            "SecurityGroupName":"Default",
            "Ips":"30.27.14.0/24,30.39.127.245",
            "CreationTime":"2018-05-22T06:54:23Z",
            "ModifyTime":"2018-05-22T06:55:14Z"
        }
    ],
    "RequestId":"664BBD08-C7DB-4E*****73-9D0958D9A899"
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/vod)查看更多错误码。

## 接口错误码

下表列举了本接口特有的错误码。

|错误代码

|错误信息

|HTTP 状态码

|说明 |
|------|------|----------|----|
|SecurityIp.NotFound

|The audit security ip does not exist.

|404

|审核安全IP不存在。 |
|ListSecurityIpFailed

|List audit security ip has failed due to some unknown error.

|500

|获取安全IP列表遇到未知错误，请刷新重试。 |

## SDK示例

建议使用[服务端SDK](~~101789~~)来调用API，此API各语言调用的示例代码，请参见：

-   [Java](~~61063~~)
-   [Python](~~61054~~)
-   [PHP](~~61069~~)
-   [.NET](~~84750~~)
-   [Node.js](~~101396~~)
-   [Go](~~101411~~)
-   [C/C++](~~101261~~)


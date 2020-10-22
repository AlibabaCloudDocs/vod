# 获取审核安全IP列表

调用ListAuditSecurityIp获取审核安全IP列表。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=ListAuditSecurityIp&type=RPC&version=2017-03-21)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListAuditSecurityIp|系统规定参数。取值：**ListAuditSecurityIp**。 |
|SecurityGroupName|String|否|Default|审核安全IP分组名称，默认获取所有。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|664BBD08-C7DB-4E\*\*\*\*\*73-9D0958D9A899|请求ID。 |
|SecurityIpList|Array of SecurityIp| |审核安全IP详情。 |
|CreationTime|String|2018-05-22T06:54:23Z|创建时间。 |
|Ips|String|30.27.14.0/24,30.39.127.245|安全IP列表。 |
|ModificationTime|String|2018-05-22T06:54:23Z|更新时间。 |
|SecurityGroupName|String|Default|安全IP组名称。 |

**说明：** 下述请求示例中的“公共请求参数”详情，参见[公共参数说明文档](~~44432~~)。

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=ListAuditSecurityIp
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

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。

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

建议使用 [服务端SDK](~~101789~~) 来调用API，此API各语言调用的示例代码，请参考如下：

-   [Java](https://help.aliyun.com/document_detail/101258.html?spm=a2c4g.11186623.2.21.7ed4272bqQsrp1#ListAuditSecurityIp)
-   [Python](https://help.aliyun.com/document_detail/101262.html?spm=a2c4g.11186623.2.22.7ed4272bqQsrp1#ListAuditSecurityIp)
-   [PHP](https://help.aliyun.com/document_detail/101250.html?spm=a2c4g.11186623.2.23.7ed4272bqQsrp1#ListAuditSecurityIp)
-   [.NET](https://help.aliyun.com/document_detail/101443.html?spm=a2c4g.11186623.2.24.7ed4272bqQsrp1#ListAuditSecurityIp)
-   [Node.js](https://help.aliyun.com/document_detail/101563.html?spm=a2c4g.11186623.2.25.7ed4272bqQsrp1#ListAuditSecurityIp)
-   [Go](https://help.aliyun.com/document_detail/101571.html?spm=a2c4g.11186623.2.26.7ed4272bqQsrp1#ListAuditSecurityIp)
-   [C/C++](https://help.aliyun.com/document_detail/102985.html?spm=a2c4g.11186623.2.27.7ed4272bqQsrp1#ListAuditSecurityIp)


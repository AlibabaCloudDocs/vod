# 设置审核安全IP

调用SetAuditSecurityIp设置审核安全IP。

**说明：** 当视频状态为审核中（Checking）或屏蔽（Blocked）状态时，只有来自审核安全IP的请求才可以播放。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=SetAuditSecurityIp&type=RPC&version=2017-03-21)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|SetAuditSecurityIp|系统规定参数。取值：**SetAuditSecurityIp**。 |
|Ips|String|是|10.23.12.24|审核安全IP列表。每个分组最多支持100个，多个IP使用英文逗号（,）隔开，格式如下：

 -   精确IP: 10.23.12.24
-   CIDR模式: 10.23.12.24/24（无类域间路由，/24表示了地址中前缀的长度，范围：`[1,32]`） |
|SecurityGroupName|String|否|Default|审核安全组名称。默认值为：**Default**。最多支持10个安全分组。 |
|OperateMode|String|否|Cover|操作方式，取值范围：

 -   **Append**：默认值，追加IP白名单。
-   **Cover**：覆盖原IP白名单。
-   **Delete**：删除IP白名单。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|25818875-5F78-4\*\*\*\*\*F6-D7393642CA58|请求ID。 |

## 示例

请求示例

```
https://vod.aliyuncs.com/?Action=SetAuditSecurityIp
&Ips=10.23.12.24
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<SetAuditSecurityIpResponse>
      <RequestId>25818875-5F78-4*****F6-D7393642CA58</RequestId>
</SetAuditSecurityIpResponse>
```

`JSON` 格式

```
{
    "RequestId": "25818875-5F78-4*****F6-D7393642CA58"
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
|IpsIsEmpty

|The specified “Ips” can not be empty.

|400

|Ips不允许为空。 |
|IpsExceededMax

|The specified Ips count has exceeded 100.

|403

|添加的IP超过个数限制，每个分组最多支持100个。 |
|SecurityIpGroupExceededMax

|The audit security group count has exceeded 10.

|403

|审核安全IP分组个数超过限制。 |

## SDK示例

建议使用[服务端SDK](~~101789~~)来调用API，此API各语言调用的示例代码，请参见：

-   [Java](~~61063~~)
-   [Python](~~61054~~)
-   [PHP](~~61069~~)
-   [.NET](~~84750~~)
-   [Node.js](~~101396~~)
-   [Go](~~101411~~)
-   [C/C++](~~101261~~)


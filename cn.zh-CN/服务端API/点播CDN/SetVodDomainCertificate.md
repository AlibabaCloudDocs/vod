# SetVodDomainCertificate {#doc_api_vod_SetVodDomainCertificate .reference}

调用SetVodDomainCertificate设置某域名下证书功能是否启用及修改证书信息。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=SetVodDomainCertificate&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|SetVodDomainCertificate|系统规定参数。取值：**SetVodDomainCertificate**。

 |
|DomainName|String|是|example.com|指定证书所属加速域名。需属于HTTPS加速类型。

 |
|SSLProtocol|String|是|off|HTTPS证书是否启用。取值：

 -   **on**：启用
-   **off**（默认值）：不启用

 |
|CertName|String|否|cert\_name|证书名称。

 |
|Region|String|否|cn-shanghai|地域。

 |
|SSLPri|String|否|yyy|私钥内容，不启用证书则无需输入，配置证书请输入私钥内容。

 |
|SSLPub|String|否|xxx|安全证书内容，不启用证书则无需输入，配置证书请输入证书内容。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|04F0F334-1335-436C-A1D7-6C044FE73368|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=SetVodDomainCertificate
&DomainName=example.com
&SSLProtocol=off
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<SetVodDomainCertificateResponse>
  <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
</SetVodDomainCertificateResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。


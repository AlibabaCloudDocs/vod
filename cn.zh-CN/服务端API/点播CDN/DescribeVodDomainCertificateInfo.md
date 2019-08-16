# DescribeVodDomainCertificateInfo {#doc_api_vod_DescribeVodDomainCertificateInfo .reference}

调用DescribeVodDomainCertificateInfo获取指定加速域名的证书信息。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=DescribeVodDomainCertificateInfo&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeVodDomainCertificateInfo|系统规定参数，取值：**DescribeVodDomainCertificateInfo**。

 |
|DomainName|String|是|example.com|点播加速域名。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|CertInfos| | |证书信息。

 |
|CertDomainName|String|example.com|证书匹配的域名。

 |
|CertExpireTime|String|2018-06-03T22:03:39Z|证书过期时间，UTC格式。

 |
|CertLife|String|3 months|证书时长，单位：months：月，years：年。

 |
|CertName|String|cert-example.com|证书名称。

 |
|CertOrg|String|Let's Encrypt|证书组织。

 |
|CertType|String|free|证书类型，取值：

 -   free：免费证书
-   cas：云盾证书
-   upload：自定义上传

 |
|DomainName|String|example.com|加速域名。

 |
|ServerCertificateStatus|String|checking|服务端证书状态。

 |
|Status|String|success|证书状态。

 -   success：已生效
-   checking：检测域名是否在阿里云点播
-   cname\_error：域名没有切到阿里云点播
-   domain\_invalid：域名包含非法字符
-   unsupport\_wildcard：不支持泛域名
-   applying：证书申请中
-   failed：证书申请失败

 |
|RequestId|String|5C1E43DC-9E51-4771-82C0-7D5ECEB547A1|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=DescribeVodDomainCertificateInfo
&DomainName=example.com
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeVodDomainCertificateInfoResponse>
  <CertInfos>
		    <CertInfo>
			      <Status>success</Status>
			      <CertLife>3 months</CertLife>
			      <SSLProtocol>on</SSLProtocol>
			      <CertType>cas</CertType>
			      <CertName>cert-example.com</CertName>
			      <CertDomainName>example.com</CertDomainName>
			      <DomainName>example.com</DomainName>
			      <CertOrg>Let's Encrypt</CertOrg>
			      <CertExpireTime>2018-06-03T22:03:39Z</CertExpireTime>
		    </CertInfo>
	  </CertInfos>
	  <RequestId>5C1E43DC-9E51-4771-82C0-7D5ECEB547A1</RequestId>
</DescribeVodDomainCertificateInfoResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"5C1E43DC-9E51-4771-82C0-7D5ECEB547A1",
	"CertInfos":{
		"CertInfo":[
			{
				"Status":"success",
				"SSLProtocol":"on",
				"CertLife":"3 months",
				"CertType":"cas",
				"CertName":"cert-example.com",
				"DomainName":"example.com",
				"CertDomainName":"example.com",
				"CertExpireTime":"2018-06-03T22:03:39Z",
				"CertOrg":"Let's Encrypt"
			}
		]
	}
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。


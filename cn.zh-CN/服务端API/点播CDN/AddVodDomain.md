# AddVodDomain {#doc_api_vod_AddVodDomain .reference}

调用AddVodDomain添加点播加速域名。每次只能提交一个加速域名，一个用户最多添加20个域名。

**说明：** 

-   创建加速域名之前，您需要先开通[点播服务](https://help.aliyun.com/document_detail/51512.html?spm=a2c4g.11186623.2.15.715f78c81bJXrF)。
-   加速域名必须已备案完成。
-   源站内容，如果不在阿里云平台上，需要审核，审核工作会在下一工作日前完成。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=AddVodDomain&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|AddVodDomain|系统规定参数，取值：**AddVodDomain**。

 |
|DomainName|String|是|example.com|需要接入点播的加速域名。

 支持泛域名，以符号“.”开头，如：.example.com。

 |
|Sources|String|是|\[\{"content":"1.1.1.1","type":"ipaddr","priority":"20","port":80\}\]|回源地址列表。

 |
|CheckUrl|String|否|check\_url|检查域名是否能正常访问url。

 |
|Scope|String|否|domestic|国际用户、国内L3及以上用户设置有效。取值范围：**domestic**\(中国大陆，默认\)，**overseas**\(港澳台及海外\)，**global**\(全球加速\)。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|15C66C7B-671A-4297-9187-2C4477247A74|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=AddVodDomain
&DomainName=example.com
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<AddVodDomainResponse>
  <RequestId>15C66C7B-671A-4297-9187-2C4477247A74</RequestId>
</AddVodDomainResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"15C66C7B-671A-4297-9187-2C4477247A74"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。


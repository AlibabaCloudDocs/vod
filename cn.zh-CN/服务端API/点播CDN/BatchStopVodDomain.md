# BatchStopVodDomain {#doc_api_vod_BatchStopVodDomain .reference}

调用BatchStopVodDomain批量停用点播加速域名，将DomainStatus变更为Offline。

**说明：** 

-   停用该加速域名后，该条加速域名信息仍保留，针对加速域名的请求系统将做自动回源处理。
-   若暂时不需要对某域名进行加速，推荐使用本接口，暂停域名加速效果。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=BatchStopVodDomain&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|BatchStopVodDomain|系统规定参数。取值：**BatchStopVodDomain**。

 |
|DomainNames|String|是|example.com|点播加速域名，多个用英文逗号分隔。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|15C66C7B-671A-4297-9187-2C4477247A74|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=BatchStopVodDomain
&DomainNames=example.com
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<BatchStopVodDomainResponse>
  <RequestId>15C66C7B-671A-4297-9187-2C4477247A74</RequestId>
</BatchStopVodDomainResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"15C66C7B-671A-4297-9187-2C4477247A74"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。


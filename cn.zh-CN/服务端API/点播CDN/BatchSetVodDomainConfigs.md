# BatchSetVodDomainConfigs {#doc_api_vod_BatchSetVodDomainConfigs .reference}

调用BatchSetVodDomainConfigs批量配置加速域名。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=BatchSetVodDomainConfigs&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|BatchSetVodDomainConfigs|系统规定参数，取值：**BatchSetVodDomainConfigs**。

 |
|DomainNames|String|是|example.com|点播加速域名，多个用英文半角逗号分隔。

 |
|Functions|String|是|\[\{"functionArgs":\[\{"argName":"domain\_name","argValue":"www.example.com"\}\],"functionName":"set\_req\_host\_header"\}\]|功能列表。

 -   Functions格式：`[{"functionArgs":[{"argName":"domain_name","argValue":"www.example.com"}],"functionName":"set_req_host_header"}]`
-   某些功能，如filetype\_based\_ttl\_set，可以设置多条纪录，当需要更新其中某条纪录时，可通过该条纪录的configId来指定。 `[{"functionArgs":[{"argName":"file_type","argValue":"jpg"},{"argName":"ttl","argValue":"18"},{"argName":"weight","argValue":"30"}],"functionName":"filetype_based_ttl_set","configId":5068995}]`

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|04F0F334-1335-436C-A1D7-6C044FE73368|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=BatchSetVodDomainConfigs
&DomainNames=example.com
&Functions=[{"functionArgs":[{"argName":"domain_name","argValue":"www.example.com"}],"functionName":"set_req_host_header"}]
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<BatchSetVodDomainConfigsResponse>
  <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
</BatchSetVodDomainConfigsResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。


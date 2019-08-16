# DescribeVodDomainConfigs {#doc_api_vod_DescribeVodDomainConfigs .reference}

调用DescribeVodDomainConfigs查询域名配置，一次可查询多个功能配置。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=DescribeVodDomainConfigs&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeVodDomainConfigs|系统规定参数，取值：**DescribeVodDomainConfigs**。

 |
|DomainName|String|是|www.example.com|点播加速域名。

 |
|FunctionNames|String|是|filetype\_based\_ttl\_set,set\_req\_host\_header|功能列表名称，多个用英文逗号分隔。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|DomainConfigs| | |域名配置。

 |
|ConfigId|String|5003576|配置ID。

 |
|FunctionArgs| | |各个function。

 |
|ArgName|String|file\_type|配置名称。

 |
|ArgValue|String|txt|配置值。

 |
|FunctionName|String|set\_req\_host\_header|function名称。

 |
|Status|String|success|状态，包括success,testing,failed,configuring。

 |
|RequestId|String|F8AA0364-0FDB-4AD5-AC74-D69FAB8924ED|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=DescribeVodDomainConfigs
&DomainName=www.example.com
&FunctionNames=filetype_based_ttl_set,set_req_host_header
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeVodDomainConfigsResponse>
  <RequestId>F8AA0364-0FDB-4AD5-AC74-D69FAB8924ED</RequestId>
	  <DomainConfigs>
		    <DomainConfig>
			      <FunctionArgs>
				        <FunctionArg>
					          <ArgName>domain_name</ArgName>
					          <ArgValue>www.example.com</ArgValue>
				        </FunctionArg>
			      </FunctionArgs>
			      <ConfigId>5003576</ConfigId>
			      <FunctionName>set_req_host_header</FunctionName>
		    </DomainConfig>
		    <DomainConfig>
			      <FunctionArgs>
				        <FunctionArg>
					          <ArgName>file_type</ArgName>
					          <ArgValue>txt</ArgValue>
				        </FunctionArg>
				        <FunctionArg>
					          <ArgName>ttl</ArgName>
					          <ArgValue>13</ArgValue>
				        </FunctionArg>
				        <FunctionArg>
					          <ArgName>weight</ArgName>
					          <ArgValue>8</ArgValue>
				        </FunctionArg>
			      </FunctionArgs>
			      <ConfigId>5068995</ConfigId>
			      <FunctionName>filetype_based_ttl_set</FunctionName>
		    </DomainConfig>
	  </DomainConfigs>
</DescribeVodDomainConfigsResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"F8AA0364-0FDB-4AD5-AC74-D69FAB8924ED",
	"DomainConfigs":{
		"DomainConfig":[
			{
				"FunctionArgs":{
					"FunctionArg":[
						{
							"ArgName":"domain_name",
							"ArgValue":"www.example.com"
						}
					]
				},
				"FunctionName":"set_req_host_header",
				"ConfigId":5003576
			},
			{
				"FunctionArgs":{
					"FunctionArg":[
						{
							"ArgName":"file_type",
							"ArgValue":"txt"
						},
						{
							"ArgName":"ttl",
							"ArgValue":"13"
						},
						{
							"ArgName":"weight",
							"ArgValue":"8"
						}
					]
				},
				"FunctionName":"filetype_based_ttl_set",
				"ConfigId":5068995
			}
		]
	}
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。


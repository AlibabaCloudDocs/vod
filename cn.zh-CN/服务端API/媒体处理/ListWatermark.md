# ListWatermark {#doc_api_vod_ListWatermark .reference}

调用ListWatermark查询用户水印数据列表。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=ListWatermark&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListWatermark|系统规定参数，取值：**ListWatermark**。

 |
|AccessKeyId|String|否|your\_accesskey\_id|您的AccessKey ID。

 |
|AppId|String|否|app-xxxxx|应用ID。

 |
|PageNo|Integer|否|1|当前页码。

 |
|PageSize|Integer|否|10|列表每页大小。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|25818875-5F78-4A13-BEF6-D7393642CA58|请求ID。

 |
|WatermarkInfos| | |水印数据列表。

 |
|AppId|String|app-xxxxx|应用ID。

 |
|CreationTime|String|2018-11-07T09:05:52Z|水印创建时间。

 |
|FileUrl|String|https://outin-3262681cdde1e89f4b3e7.oss-cn-shanghai.aliyuncs.com/image/cover/8CC8B715E6F8A72EC6B-6-2.png?Expires=1541600583&OSSAccessKeyId=XXXXXX&Signature=gmf1eYMoDVg%2BHQCb4UGozBW4xZo%3D|水印文件文件URL\(OSS地址或CDN地址\)，文字水印没有文件地址信息。

 |
|IsDefault|String|NotDefault|是否是默认水印。

 |
|Name|String|文字水印测试|水印名称。

 |
|Type|String|Text|水印类型：**Image\(图片\)**、**Text\(文字\)**。

 |
|WatermarkConfig|String|\{"FontColor": "Blue","FontSize": 80,"Content": "水印测试"\}|水印显示位置、效果等配置信息：文字水印、图片水印。

 |
|WatermarkId|String|9bcc8bfadb843f475c109a2671d0df97|水印ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=ListWatermark
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ListWatermarkResponse>
	  <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
	  <WatermarkInfos>
		    <Name>文字水印测试</Name>
		    <CreationTime>2018-11-07T09:05:52Z</CreationTime>
		    <IsDefault>NotDefault</IsDefault>
		    <Type>Text</Type>
		    <WatermarkId>9bcc8bfadb843f475c109a2671d0df97</WatermarkId>
		    <WatermarkConfig>
			      <FontColor>Blue</FontColor>
			      <FontSize>80</FontSize>
			      <Content>水印测试</Content>
		    </WatermarkConfig>
	  </WatermarkInfos>
</ListWatermarkResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"WatermarkInfos":[
		{
			"CreationTime":"2018-11-07T09:05:52Z",
			"Name":"文字水印测试",
			"WatermarkConfig":{
				"FontColor":"Blue",
				"FontSize":80,
				"Content":"水印测试"
			},
			"Type":"Text",
			"IsDefault":"NotDefault",
			"WatermarkId":"9bcc8bfadb843f475c109a2671d0df97"
		}
	],
	"RequestId":"25818875-5F78-4A13-BEF6-D7393642CA58"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。


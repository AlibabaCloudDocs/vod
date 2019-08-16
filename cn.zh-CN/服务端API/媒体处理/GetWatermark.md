# GetWatermark {#doc_api_vod_GetWatermark .reference}

调用GetWatermark查询单个水印数据。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=GetWatermark&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetWatermark|系统规定参数，取值：**GetWatermark**。

 |
|WatermarkId|String|是|9bcc8bfadb843f475c109a2671d0df97|水印ID。

 |
|AccessKeyId|String|否|your\_accesskey\_id|您的AccessKey ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|25818875-5F78-4A13-BEF6-D7393642CA58|请求ID。

 |
|WatermarkInfo| | |水印数据。

 |
|AppId|String|app-xxxxx|应用ID。

 |
|CreationTime|String|2018-11-06T08:03:17Z|水印创建时间。

 |
|FileUrl|String|https://outin-3262681cdde1189f4b3e7.oss-cn-shanghai.aliyuncs.com/image/cover/F85529C8B715E6F8A72EC6B-6-2.png?Expires=1541600583&OSSAccessKeyId=XXXXXX&Signature=gmf1eYMoDVg%2BHQCb4UGozBW4xZo%3D|水印文件文件URL\(OSS地址或CDN地址\)，文字水印没有文件地址信息。

 |
|IsDefault|String|NotDefault|是否是默认水印：**Default\(默认水印\)**、**NotDefault\(非默认水印\)**。

 |
|Name|String|图片水印测试|水印名称。

 |
|Type|String|Text|水印类型：**Image\(图片\)**、**Text\(文字\)**。

 |
|WatermarkConfig|String|\{"ReferPos": "BottomRight","Height": "55","Width": "55","Dx": "8","Dy": "8" \}|水印显示位置、效果等配置信息：文字水印、图片水印。

 |
|WatermarkId|String|505e2e287ea49c40f8cecfddd386d384|水印ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=GetWatermark
&WatermarkId=9bcc8bfadb843f475c109a2671d0df97
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<GetWatermarkResponse>
	  <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
	  <WatermarkInfo>
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
	  </WatermarkInfo>
</GetWatermarkResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"WatermarkInfo":{
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
	},
	"RequestId":"25818875-5F78-4A13-BEF6-D7393642CA58"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。


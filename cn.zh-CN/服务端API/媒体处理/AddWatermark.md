# AddWatermark {#doc_api_vod_AddWatermark .reference}

调用AddWatermark添加水印数据。

目前支持的图片水印格式包括**静态\(PNG\)**、**动态\(GIF、APNG、MOV\)**。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=AddWatermark&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|AddWatermark|系统规定参数，取值：**AddWatermark**。

 |
|Name|String|是|水印|水印名称。只支持中英文、数字。长度不超过128个字节，UTF-8编码。

 |
|Type|String|是|Text|水印类型：**Image\(图片，默认值\)**、**Text\(文字**\)。

 水印类型不同，WatermarkConfig内容不同。

 |
|WatermarkConfig|String|是|\{"Width":"55","Height":"55","Dx":"9","Dy":"9","ReferPos":"BottonLeft","Type":"Image"\}|水印显示位置、效果等配置\(JSON字符串\)。

 |
|AccessKeyId|String|否|your\_accesskey\_id|您的AccessKey ID。

 |
|AppId|String|否|app-xxxx|应用ID。取值如：**app-1000000**。

 |
|FileUrl|String|否|http://outin-3262681cddeb00163e1403e7.oss-cn-shanghai.aliyuncs.com/image/cover/C9934515B1EF727EBAE7FDEC-6-2.png|水印文件oss地址。图片水印必传。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|25818875-5F78-4A13-BEF6-D7393642CA58|请求ID。

 |
|WatermarkInfo| | |水印信息。

 |
|CreationTime|String|2018-11-07T09:05:52Z|水印创建时间。

 |
|FileUrl|String|https://outin-3262681cdde111e89f4b3e7.oss-cn-shanghai.aliyuncs.com/image/cover/E6C3448CC8B715E6F8A72EC6B-6-2.png?Expires=1541600583&OSSAccessKeyId=XXXXXXX&Signature=gmf1eYMoDVg%2BHQCb4UGozBW4xZo%3D|水印文件文件URL\(OSS地址或CDN地址\)，文字水印没有文件地址信息。

 |
|IsDefault|String|NotDefault|是否是默认水印：**Default\(默认水印\)**、**NotDefault\(非默认水印\)**。

 |
|Name|String|文字水印测试|水印名称。

 |
|Type|String|Text|水印类型。

 |
|WatermarkConfig|String|\{"FontColor": "Blue","FontSize": 80, "Content": "水印测试" \}|水印显示位置、效果等配置信息：文字水印、图片水印。

 |
|WatermarkId|String|9bcc8bfadb843f475c109a2671d0df97|水印ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=AddWatermark
&Name=水印
&Type=Text
&WatermarkConfig={"Width":"55","Height":"55","Dx":"9","Dy":"9","ReferPos":"BottonLeft","Type":"Image"}
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<AddWatermarkResponse>
  <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
	  <WatermarkInfo>
		    <Name>图片水印测试</Name>
		    <CreationTime>2018-11-06T08:03:17Z</CreationTime>
		    <WatermarkId>505e2e287ea49c40f8cecfddd386d384</WatermarkId>
		    <FileUrl>https://outin-3262681cdde111e89f4b3e7.oss-cn-shanghai.aliyuncs.com/image/cover/E6C3448CC8B715E6F8A72EC6B-6-2.png?Expires=1541600583&amp;OSSAccessKeyId=XXXXXXX&amp;Signature=gmf1eYMoDVg%2BHQCb4UGozBW4xZo%3D</FileUrl>
		    <IsDefault>NotDefault</IsDefault>
		    <Type>Image</Type>
		    <WatermarkConfig>
			      <ReferPos>BottomRight</ReferPos>
			      <Type>Image</Type>
			      <Height>55</Height>
			      <Width>55</Width>
			      <Dx>8</Dx>
			      <Dy>8</Dy>
		    </WatermarkConfig>
	  </WatermarkInfo>
</AddWatermarkResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"WatermarkInfo":{
		"CreationTime":"2018-11-06T08:03:17Z",
		"Name":"图片水印测试",
		"WatermarkConfig":{
			"ReferPos":"BottomRight",
			"Type":"Image",
			"Height":"55",
			"Width":"55",
			"Dx":"8",
			"Dy":"8"
		},
		"Type":"Image",
		"IsDefault":"NotDefault",
		"FileUrl":"https://outin-3262681cdde111e89f4b3e7.oss-cn-shanghai.aliyuncs.com/image/cover/E6C3448CC8B715E6F8A72EC6B-6-2.png?Expires=1541600583&OSSAccessKeyId=XXXXXXX&Signature=gmf1eYMoDVg%2BHQCb4UGozBW4xZo%3D",
		"WatermarkId":"505e2e287ea49c40f8cecfddd386d384"
	},
	"RequestId":"25818875-5F78-4A13-BEF6-D7393642CA58"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。


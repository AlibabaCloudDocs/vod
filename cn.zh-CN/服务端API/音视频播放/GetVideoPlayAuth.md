# GetVideoPlayAuth {#doc_api_vod_GetVideoPlayAuth .reference}

调用GetVideoPlayAuth获取视频播放时所需的播放凭证。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=GetVideoPlayAuth&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetVideoPlayAuth|系统规定参数，取值：**GetVideoPlayAuth**。

 |
|VideoId|String|是|dfde02284a5c46618b1722a097adaf4a|视频ID。

 |
|AuthInfoTimeout|Long|否|3600|播放凭证过期时间，默认为**100**秒，取值范围`[100,3600]`。

 |
|PlayConfig|String|否|\{"PlayDomain":"vod.test\_domain","XForwardedFor":"yqCD7Fp1uqChoVj/sl/p5Q==","PreviewTime":"20","MtsHlsUriToken":"yqCD7Fp1uqChoVjslp5Q"\}|媒体播放时的自定义设置字段，为JSON字符串，目前支持指定域名播放的设置。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|1b44a2fa-0378-4b34-b57e-81175948b440|请求ID。

 |
|VideoMeta| | |视频Meta信息。

 |
|CoverURL|String|https://image.example.com/sample.jpg|视频封面。

 |
|Duration|Float|120.0|视频时长\(秒\)。

 |
|Status|String|Normal|视频状态。

 |
|Title|String|阿里云VOD|视频标题。

 |
|VideoId|String|93ab850b4f6f44eab54b6e91d24d81d4|视频ID。

 |
|PlayAuth|String|sstyYuew678999ew90000000xtt7TYUh|视频播放凭证。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=GetVideoPlayAuth
&VideoId=dfde02284a5c46618b1722a097adaf4a
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<GetVideoPlayAuthResponse>
  <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
	  <VideoMeta>
		    <VideoId>93ab850b4f6f44eab54b6e91d24d81d4</VideoId>
		    <Title>阿里云VOD</Title>
		    <Duration>135.6</Duration>
		    <CoverURL>https://image.example.com/sample.jpg</CoverURL>
		    <Status>Normal</Status>
	  </VideoMeta>
	  <PlayAuth>sstyYuew678999ew90000000xtt7TYUh</PlayAuth>
</GetVideoPlayAuthResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"25818875-5F78-4A13-BEF6-D7393642CA58",
	"VideoMeta":{
		"CoverURL":"https://image.example.com/sample.jpg",
		"Status":"Normal",
		"Duration":135.6,
		"VideoId":"93ab850b4f6f44eab54b6e91d24d81d4",
		"Title":"阿里云VOD"
	},
	"PlayAuth":"sstyYuew678999ew90000000xtt7TYUh"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。


# GetMezzanineInfo {#doc_api_vod_GetMezzanineInfo .reference}

调用GetMezzanineInfo获取音视频的源文件信息，包括文件地址、分辨率、码率等。

**说明：** 当一路流转码完成后才可以获取到完整的源文件信息。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=GetMezzanineInfo&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetMezzanineInfo|系统规定参数，取值：**GetMezzanineInfo**。

 |
|VideoId|String|是|1f1a6fc03ca048e594814031b8a6559e|视频ID。

 |
|AdditionType|String|否|video|附加信息类型。多个用逗号分隔，默认只返回基本信息。取值范围 ：

 -   video：视频流信息
-   audio：音频流信息

 |
|AuthTimeout|Long|否|3600|FileURL\(源文件地址\)签名过期时间。单位为秒，默认值为**1800**，支持设置最小值为**1**。

 **说明：** 

-   如果返回的是CDN加速地址：
    -   只有开启了URL鉴权，FileURL才会定期失效，否则会永久有效。
    -   最小值：**1**
    -   最大值：无限制
    -   默认值：未设置时，取值为URL鉴权中设置的默认有效时长。
-   如果返回的是OSS源站地址：
    -   只有存储权限为私有，FileURL才会定期失效，否则会永久有效。
    -   最小值：**1**
    -   最大值：为降低源站安全风险，最大值为**2592000（即30天）**。
    -   默认值：未设置时，取值为**3600**。

 |
|OutputType|String|否|oss|输出地址类型。取值范围 ：

 -   oss：回源地址
-   cdn（默认值）：加速地址

**说明：** 当源文件所在的bucket类型为in时，只返回oss地址。


 |
|PreviewSegment|Boolean|否|false|参数暂不可用。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|73ad78c6-a6cb-4461-bb6d-0f24c0e24d65|请求ID。

 |
|Mezzanine| | |文件信息。

 |
|AudioStreamList| | |音频流信息。

 |
|Bitrate|String|62.885|码率。

 |
|ChannelLayout|String|mono|声道输出样式。

 |
|Channels|String|1|声道数。

 |
|CodecLongName|String|AAC \(Advanced Audio Coding\)|编码格式长述名。

 |
|CodecName|String|aac|编码格式简述名。

 |
|CodecTag|String|0x6134706d|编码格式标记。

 |
|CodecTagString|String|mp4a|编码格式标记文本。

 |
|CodecTimeBase|String|1/44100|编码时基。

 |
|Duration|String|3.227574|时长。

 |
|Index|String|0|音频流序号，标识音频流在整个媒体流中的位置。

 |
|Lang|String|und|语言。

 |
|NumFrames|String|1|总帧数。

 |
|SampleFmt|String|fltp|采样格式。

 |
|SampleRate|String|44100|采样率。

 |
|StartTime|String|0.000000|起始时间。

 |
|Timebase|String|0.000000|时基。

 |
|Bitrate|String|771.2280|文件码率，单位Kbps。

 |
|CRC64|String|461bb6d0f24c0e24d65|文件的CRC64编码，该64位CRC根据ECMA-182标准计算得出。

 |
|CreationTime|String|2017-11-14T09:15:50Z|文件创建时间，为UTC时间。

 |
|Duration|String|42.4930|文件时长\(秒\)。

 |
|FileName|String|cbf317e6c908cd1a224bd85d469781c55.mp4|文件名称。

 |
|FileURL|String|http://in-20170608100704166-453mp83ndi.oss-cn-shanghai.aliyuncs.com/customerTrans/e2bf0614af0254c744a6422806ad8cff/457D396A-15FB9D03164-1389-0829-084-62272.mp4?Expires=1513173337&OSSAccessKeyId=LTAIJ1nnO0yP7cAL&Signature=ngisNAr27V%2FXBtNysLbt9ebYhzU%3D|文件地址。

 |
|Fps|String|25.0000|文件帧率，每秒多少帧。

 |
|Height|Long|540|文件高度，单位px

 |
|OutputType|String|oss|输出地址类型。取值范围 ：

 oss（回源地址）

 cdn（加速地址）

 默认为cdn类型。注意：仅支持播放格式为mp4的oss地址

 |
|PreprocessStatus|String|UnPreprocess|参数暂不可用。

 |
|Size|Long|4096477|文件大小，单位Byte。

 |
|Status|String|Normal|文件状态。

 |
|VideoId|String|73ad78c6a6cb4461bb6d0f24c0e24d65|视频ID。

 |
|VideoStreamList| | |视频流信息。

 |
|AvgFPS|String|30.0|平均帧率。

 |
|CodecLongName|String|H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10|编码格式长述名。

 |
|CodecName|String|h264|编码格式简述名。

 |
|CodecTag|String|0x31637661|编码格式标记。

 |
|CodecTagString|String|avc1|编码格式标记文本。

 |
|CodecTimeBase|String|1/60|编码时基。

 |
|Dar|String|0:1|编码显示分辨率比。

 |
|Duration|String|3.166667|时长。

 |
|Fps|String|30.0|目标帧率。

 |
|HasBFrames|String|0|是否有B帧。

 |
|Height|String|320|视频分辨率长。

 |
|Index|String|1|视频流序号，标识视频流在整个媒体流中的位置。

 |
|Lang|String|und|语言。

 |
|Level|String|30|编码等级。

 |
|NumFrames|String|0|总帧数。

 |
|PixFmt|String|yuv420p|像素格式。

 |
|Profile|String|Main|编码预置。

 |
|Rotate|String|90|视频旋转角度，取值范围：

0，360\)。|
|Sar|String|0:1|编码信号分辨率比。

 |
|StartTime|String|0.000000|起始时间。

 |
|Timebase|String|0.000000|时基。

 |
|Width|String|568|视频分辨率宽。

 |
|Width|Long|960|文件宽度，单位px。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=GetMezzanineInfo
&VideoId=1f1a6fc03ca048e594814031b8a6559e
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<GetMezzanineInfoResponse>
  <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
	  <Mezzanine>
		    <VideoId>93ab850b4f6f44eab54b6e91d24d81d4</VideoId>
		    <FileName>阿里云VOD文件名称</FileName>
		    <Duration>15.278</Duration>
		    <Status>Normal</Status>
		    <CreationTime>2017-06-26T05:38:48Z</CreationTime>
		    <Height>540</Height>
		    <Width>960</Width>
		    <Fps>25.000</Fps>
		    <FileURL>http://in-bucket.example.com.oss-cn-shanghai.aliyuncs.com/video/1CD22DC-15E7B38A3B1-2389-0829-084-62272.mp4?Expires=1505882754&amp;OSSAccessKeyId=STS.L4WDaUk1L2k2inPvhRFNbNE48&amp;Signature=O8z%2B8mJaNhTWtpV4ZncyopPptiE%3D&amp;security-token=CAIS%2FAJ1q6Ft5B2yfSjIrffiD9vhhu5thanZa0jhkmgHSsFOoYCf2jz2IHpKeXduAeAXs%2Fo0mmhZ7%2F</FileURL>
		    <Bitrate>881.087</Bitrate>
		    <Size>1682694</Size>
		    <CRC64>93ab850b4f6f44eab54b6e91d24d81d482bb9bc46ffb414aabbbdb59a8ad29e3</CRC64>
	  </Mezzanine>
</GetMezzanineInfoResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Mezzanine":{
		"CreationTime":"2017-06-26T05:38:48Z",
		"Status":"Normal",
		"FileName":"阿里云VOD文件名称",
		"Duration":"15.278",
		"VideoId":"93ab850b4f6f44eab54b6e91d24d81d4",
		"Height":540,
		"Width":960,
		"Fps":"25.000",
		"Bitrate":"881.087",
		"FileURL":"http://in-bucket.example.com.oss-cn-shanghai.aliyuncs.com/video/1CD22DC-15E7B38A3B1-2389-0829-084-62272.mp4?Expires=1505882754&OSSAccessKeyId=STS.L4WDaUk1L2k2inPvhRFNbNE48&Signature=O8z%2B8mJaNhTWtpV4ZncyopPptiE%3D&security-token=CAIS%2FAJ1q6Ft5B2yfSjIrffiD9vhhu5thanZa0jhkmgHSsFOoYCf2jz2IHpKeXduAeAXs%2Fo0mmhZ7%2F",
		"CRC64":"93ab850b4f6f44eab54b6e91d24d81d482bb9bc46ffb414aabbbdb59a8ad29e3",
		"Size":1682694
	},
	"RequestId":"25818875-5F78-4A13-BEF6-D7393642CA58"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。


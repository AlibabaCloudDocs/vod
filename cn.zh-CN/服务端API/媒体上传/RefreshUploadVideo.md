# RefreshUploadVideo {#doc_api_vod_RefreshUploadVideo .reference}

调用RefreshUploadVideo用于视频文件上传超时后重新获取视频上传凭证。

**说明：** 该接口也可用于视频、音频源文件的覆盖上传（即获取到源文件上传地址后重新上传且视频ID保持不变），但可能会自动触发转码和截图。使用说明参考[上传地址和凭证](https://help.aliyun.com/document_detail/55397.html?spm=a2c4g.11186623.2.16.5c305e928RPgXF)。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=RefreshUploadVideo&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|RefreshUploadVideo|系统规定参数，取值： **RefreshUploadVideo**。

 |
|VideoId|String|是|c6a23a870c8c4ff8b02dcd40cbd38133|视频ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|3de390e0-b9fe-4c68-94f3-a46bfb1d804b|请求ID。

 |
|UploadAuth|String|eyJTZWN1cml0eVRva2VuIjoiQ0FJU3p3TjFxNkZ0NUIyeW|上传凭证。

 |
|UploadAddress|String|eyJTZWN1cml0eVRva2VuIjoiQ0FJU3p3TjFxNkZ0NUIyeW|上传地址。

 |
|VideoId|String|93ab850b4f6f44eab54b6e91d24d81d4|视频ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=RefreshUploadVideo
&VideoId=c6a23a870c8c4ff8b02dcd40cbd38133
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<RefreshUploadVideoResponse>
	  <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
	  <VideoId>93ab850b4f6f44eab54b6e91d24d81d4</VideoId>
	  <UploadAddress>eyJTZWN1cml0eVRva2VuIjoiQ0FJU3p3TjF</UploadAddress>
	  <UploadAuth>eyJFbmRwb2ludCI6Im</UploadAuth>
</RefreshUploadVideoResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"UploadAddress":"eyJTZWN1cml0eVRva2VuIjoiQ0FJU3p3TjFxNkZ0NUIyeW",
	"VideoId":"93ab850b4f6f44eab54b6e91d24d81d4",
	"RequestId":"25818875-5F78-4A13-BEF6-D7393642CA58",
	"UploadAuth":"eyJTZWN1cml0eVRva2VuIjoiQ0FJU3p3TjFxNkZ0NUIyeW"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。


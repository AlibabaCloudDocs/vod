# DeleteStream {#doc_api_vod_DeleteStream .reference}

调用DeleteStream删除媒体流\(视频流，音频流\)信息及存储文件，并且支持批量删除。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=DeleteStream&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteStream|系统规定参数，取值：**DeleteStream**。

 |
|JobIds|String|是|f1a64a67-98f0-4423-b8bd-057d4a20aa94|-   媒体流转码的作业ID列表，多个用逗号分隔，最多支持同一个视频下的20个作业ID。
-   JobId通过获取播放地址接口\(GetPlayInfo\)返回的PlayInfo结构体中获取，每个媒体流对应的JobId不同。

 |
|VideoId|String|是|de3a60c5-759c-4cd4-bb79-6cedfeefdf4d|视频ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|7cd65f58-ccf0-4fc7-a040-8050259ef4d4|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=DeleteStream
&JobIds=f1a64a67-98f0-4423-b8bd-057d4a20aa94
&VideoId=de3a60c5-759c-4cd4-bb79-6cedfeefdf4d
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DeleteStreamResponse>
  <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
</DeleteStreamResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"25818875-5F78-4A13-BEF6-D7393642CA58"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。


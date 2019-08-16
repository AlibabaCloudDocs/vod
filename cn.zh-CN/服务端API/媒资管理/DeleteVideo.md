# DeleteVideo {#doc_api_vod_DeleteVideo .reference}

调用DeleteVideo删除完整视频（包括其源文件、转码后的流文件、封面截图等），支持批量删除。

**说明：** 此接口为物理删除视频，且无法恢复，请谨慎操作。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=DeleteVideo&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteVideo|系统规定参数，取值：**DeleteVideo**。

 |
|VideoIds|String|是|e44ebf114f4d429e9b2d2adbea8bf5b5,e44ebf114f4d429e9b2d2adbea8bf55|视频ID列表，多个用逗号分隔，最多支持10个。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|1126fa0a-89d0-41a3-8564-6ee4db454dad|请求ID。

 |
|ForbiddenVideoIds| |73ab850b4f6f44eab45b6e91d24d81d5|被禁止操作的视频ID列表（一般由于无[权限](https://help.aliyun.com/document_detail/113600.html?spm=a2c4g.11186623.2.16.638eed43Kpbfh0#AppAuth)）。

 |
|NonExistVideoIds| |93ab850b4f6f44eab54b6e91d24d81d4|不存在的视频ID列表。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=DeleteVideo
&VideoIds=e44ebf114f4d429e9b2d2adbea8bf5b5,e44ebf114f4d429e9b2d2adbea8bf55
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DeleteVideoResponse>
      <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
      <NonExistVideoIds>93ab850b4f6f44eab54b6e91d24d81d4</NonExistVideoIds>
	  <UnRemoveableVideoIds>23ab850b4f6f44eab54b6e91d24d8157</UnRemoveableVideoIds>
</DeleteVideoResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"NonExistVideoIds":"93ab850b4f6f44eab54b6e91d24d81d4",
	"ForbiddenVideoIds":"73ab850b4f6f44eab45b6e91d24d81d5",
	"RequestId":"25818875-5F78-4A13-BEF6-D7393642CA58"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。


# DeleteMezzanines {#doc_api_vod_DeleteMezzanines .reference}

调用DeleteMezzanines批量删除源文件信息及存储。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=DeleteMezzanines&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteMezzanines|系统规定参数。取值：**DeleteMezzanines**。

 |
|VideoIds|String|是|23ab850b4f6f44eab54b6e91d24d8157,93ab850b4f6f44eab54b6e91d24d81d4|视频ID列表。一次最多支持20个视频ID，多个用逗号分隔。

 |
|Force|Boolean|否|false|强制删除源文件，默认为**false**。

 **说明：** 当视频转码模式为不转码，即分发或异步转码时，由于源文件会作为原画用于播放，默认不可删除该视频的源文件，若需要强制删除该视频的源文件，可将值置为**true**。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|NonExistVideoIds| |93ab850b4f6f44eab54b6e91d24d81d4|不存在的视频ID列表。

 |
|RequestId|String|25818875-5F78-4A13-BEF6-D7393642CA58|请求ID。

 |
|UnRemoveableVideoIds| |23ab850b4f6f44eab54b6e91d24d8157|不可删除的视频ID列表。\(一般由于源文件作为原画或无\[权限\]\(https://help.aliyun.com/document\_detail/113600.html?spm=a2c4g.11186623.2.15.19153f85Oy1GH3\#AppAuth\)\)。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=DeleteMezzanines
&VideoIds=23ab850b4f6f44eab54b6e91d24d8157,93ab850b4f6f44eab54b6e91d24d81d4
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DeleteMezzaninesResponse>
      <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
	  <NonExistVideoIds>93ab850b4f6f44eab54b6e91d24d81d4</NonExistVideoIds>
	  <UnRemoveableVideoIds>23ab850b4f6f44eab54b6e91d24d8157</UnRemoveableVideoIds>
</DeleteMezzaninesResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"UnRemoveableVideoIds":"23ab850b4f6f44eab54b6e91d24d8157",
	"NonExistVideoIds":"93ab850b4f6f44eab54b6e91d24d81d4",
	"RequestId":"25818875-5F78-4A13-BEF6-D7393642CA58"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。


# UpdateVideoInfos {#doc_api_vod_UpdateVideoInfos .reference}

调用UpdateVideoInfos批量修改视频信息。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=UpdateVideoInfos&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|UpdateVideoInfos|系统规定参数。取值：**UpdateVideoInfos**。

 |
|UpdateContent|String|是|\[\{"VideoId":"f45cf4eba5c84d25b90233389558c39","Title":"测试标题","Description":"测试描述","CoverURL":"http://sample.aliyun.com/sample.jpg","CateId":"6163631","Tags":"测试标签"\},\{"VideoId":"f45cf4eba5c84d25b90233389558c36","Title":"测试标题","Description":"测试描述","CoverURL":"http://sample.aliyun.com/sample.jpg","CateId":"6163631","Tags":"测试标签"\}\]|更新内容。一次最多支持修改20个视频的视频信息。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|ForbiddenVideoIds| |f45cf4eba5c84d25b90233389558c36|被禁止操作的视频ID列表（一般由于无[权限](https://help.aliyun.com/document_detail/113600.html?spm=a2c4g.11186623.2.17.e764cf31OnXW0D#AppAuth)）。

 |
|NonExistVideoIds| |f45cf4eba5c84d25b90233389558c39|不存在的视频ID列表。

 |
|RequestId|String|25818875-5F78-4A13-BEF6-D7393642CA58|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=UpdateVideoInfos
&UpdateContent=[{"VideoId":"f45cf4eba5c84d25b90233389558c39","Title":"测试标题","Description":"测试描述","CoverURL":"http://sample.aliyun.com/sample.jpg","CateId":"6163631","Tags":"测试标签"},{"VideoId":"f45cf4eba5c84d25b90233389558c36","Title":"测试标题","Description":"测试描述","CoverURL":"http://sample.aliyun.com/sample.jpg","CateId":"6163631","Tags":"测试标签"}]
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<UpdateVideoInfosResponse>
	  <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
	  <NonExistVideoIds>f45cf4eba5c84d25b90233389558c39</NonExistVideoIds>
	  <ForbiddenVideoIds>f45cf4eba5c84d25b90233389558c36</ForbiddenVideoIds>
</UpdateVideoInfosResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"NonExistVideoIds":[
		"f45cf4eba5c84d25b90233389558c39"
	],
	"ForbiddenVideoIds":[
		"f45cf4eba5c84d25b90233389558c36"
	],
	"RequestId":"25818875-5F78-4A13-BEF6-D7393642CA58"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。


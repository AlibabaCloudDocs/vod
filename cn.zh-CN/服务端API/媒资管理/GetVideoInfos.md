# GetVideoInfos {#doc_api_vod_GetVideoInfos .reference}

调用GetVideoInfos批量获取视频信息。

**说明：** 通过视频ID列表获取多个视频的基本信息，包括视频标题、描述、时长、封面URL、状态、创建时间、大小、截图、分类和标签等。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=GetVideoInfos&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetVideoInfos|系统规定参数。取值：**GetVideoInfos**。

 |
|VideoIds|String|是|7753d144efd74dfd8e649c6c45fe0579,7753d144efd74dfd8e649c6c45fe0570|视频ID列表。多个用逗号分隔，最多支持20个。

 |
|AdditionType|String|否|aaa|参数暂不可用。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|NonExistVideoIds| |\["b4039216985f4312a5382a4ed2884"\]|不存在的视频ID列表。

 |
|RequestId|String|25818875-5F78-4A13-BEF6-D7393642CA58|请求ID。

 |
|VideoList| | |视频信息列表。

 |
|AppId|String|6985f4312a5382a4ed2884|应用ID。

 |
|CateId|Long|78|视频分类ID。

 |
|CateName|String|分类名|视频分类名称。

 |
|CoverURL|String|https://image.example.com/coversample.jpg|视频封面URL。

 |
|CreationTime|String|2017-06-26T05:38:48Z|视频创建时间。使用UTC时间。

 |
|CustomMediaInfo|String|\{"aa":123\}|参数暂不可用。

 |
|Description|String|阿里云VOD视频描述|视频描述。

 |
|DownloadSwitch|String|on-normal|下载开关。

 |
|Duration|Float|120|视频时长（秒）。

 |
|ModificationTime|String|2017-06-26T05:38:48Z|更新时间。

 |
|PreprocessStatus|String|UnPreprocess|预处理状态。

 |
|RegionId|String|cn-shanghai|存储所在区域。

 |
|Size|Long|453|视频源文件大小（字节）。

 |
|Snapshots| |\["http://image.example.com/snapshot/sample000001.jpg?auth\_key=1498476426-0-0-f00b9455c49a423ce69cf4e273334f52","http://image.example.com/snapshot/sample00002.jpg?auth\_key=1498476426-0-0-f00b9455c49a423ce69cf4e272434f52",...\]|视频截图URL数组。

 |
|Status|String|Normal|视频状态。

 |
|StorageLocation|String|out-xxxx.oss-cn-shanghai.aliyuncs.com|视频文件的存储区域。

 |
|Tags|String|标签1, 标签2|视频标签，多个用逗号分隔。

 |
|TemplateGroupId|String|b4039216985f4312a5382a4ed2883|视频转码时使用的转码组ID。

 |
|ThumbnailList| | |参数暂不可用。

 |
|URL|String|http://test.aliyun.com/7bb18e5afc740939575f1fd694c57e4/covers/webvtt/webvtt.vtt|参数暂不可用。

 |
|Title|String|阿里云VOD视频标题|视频标题。

 |
|VideoId|String|93ab850b4f6f44eab54b6e91d24d81d4|视频ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=GetVideoInfos
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<GetVideoInfosResponse>
	  <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
	  <VideoList>
		    <VideoId>93ab850b4f6f44eab54b6e91d24d81d4</VideoId>
		    <Title>阿里云VOD视频标题</Title>
		    <Description>阿里云VOD视频描述</Description>
		    <Duration>135.6</Duration>
		    <CoverURL>https://image.example.com/coversample.jpg</CoverURL>
		    <Status>Normal</Status>
		    <CreationTime>2017-06-26T05:38:48Z</CreationTime>
		    <Size>10897890</Size>
		    <Snapshots>http://image.example.com/snapshot/sample000001.jpg?auth_key=1498476426-0-0-f00b9455c49a423ce69cf4e273334f52</Snapshots>
		    <Snapshots>http://image.example.com/snapshot/sample00002.jpg?auth_key=1498476426-0-0-f00b9455c49a423ce69cf4e272434f52</Snapshots>
		    <CateId>78</CateId>
		    <CateName>分类名</CateName>
		    <Tags>标签1, 标签2</Tags>
	  </VideoList>
	  <NonExistVideoIds>b4039216985f4312a5382a4ed2884</NonExistVideoIds>
</GetVideoInfosResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"VideoList":[
		{
			"CreationTime":"2017-06-26T05:38:48Z",
			"CoverURL":"https://image.example.com/coversample.jpg",
			"Tags":"标签1, 标签2",
			"Status":"Normal",
			"CateId":78,
			"Description":"阿里云VOD视频描述",
			"CateName":"分类名",
			"Duration":135.6,
			"VideoId":"93ab850b4f6f44eab54b6e91d24d81d4",
			"Snapshots":[
				"http://image.example.com/snapshot/sample000001.jpg?auth_key=1498476426-0-0-f00b9455c49a423ce69cf4e273334f52",
				"http://image.example.com/snapshot/sample00002.jpg?auth_key=1498476426-0-0-f00b9455c49a423ce69cf4e272434f52"
			],
			"Title":"阿里云VOD视频标题",
			"Size":10897890
		}
	],
	"NonExistVideoIds":[
		"b4039216985f4312a5382a4ed2884"
	],
	"RequestId":"25818875-5F78-4A13-BEF6-D7393642CA58"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。


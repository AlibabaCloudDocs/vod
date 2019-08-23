# GetVideoList {#doc_api_vod_GetVideoList .reference}

调用GetVideoList获取视频信息列表。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=GetVideoList&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetVideoList|系统规定参数，取值：**GetVideoList**。

 |
|CateId|Long|否|7249287|视频分类ID。

 |
|EndTime|String|否|2017-01-11T12:00:00Z|CreationTime的结束时间，为闭区间\(小于等于结束时间\)。

 日期格式按照ISO8601标准表示，并需要使用UTC时间。格式为：**YYYY-MM-DDThh:mm:ssZ**。例如，2017-01-11T12:00:00Z（为北京时间2017年1月11日20点0分0秒）。

 |
|PageNo|Integer|否|1|当前页码，默认值为**1**。

 |
|PageSize|Integer|否|10|列表页大小，可选。默认值为**10**，最大值为**100**。

 |
|SortBy|String|否|CreationTime:Asc|结果排序。取值：

 -   **CreationTime:Desc（默认值）**：按创建时间倒序
-   **CreationTime:Asc**

 |
|StartTime|String|否|2017-01-11T12:00:00Z|CreationTime（创建时间）的开始时间，为开区间\(大于开始时间\)。

 日期格式按照ISO8601标准表示，并需要使用UTC时间。格式为：**YYYY-MM-DDThh:mm:ssZ**。例如，2017-01-11T12:00:00Z（为北京时间2017年1月11日20点0分0秒）。

 |
|Status|String|否|Uploading,Normal|视频状态，默认获取所有视频，多个可以用逗号分隔。取值包括：**Uploading\(上传中\)，UploadFail\(上传失败\)，UploadSucc\(上传完成\)，Transcoding\(转码中\)，TranscodeFail\(转码失败\)，Blocked\(屏蔽\)，Normal\(正常\)**。

 |
|StorageLocation|String|否|out-xxxx.oss-cn-shanghai.aliyuncs.com|视频的存储区域。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|16f5a90c-1dde-4721-8e77-c0b5ada7b2b6|请求ID。

 |
|Total|Integer|100|视频总条数。

 |
|VideoList| | |获取视频信息列表。最大支持获取前5000条。

 |
|AppId|String|app-1000000|应用ID。

 |
|CateId|Long|78|视频分类ID。

 |
|CateName|String|分类名|视频分类名称。

 |
|CoverURL|String|https://image.example.com/coversample.jpg|视频封面URL。

 |
|CreateTime|String|2017-11-14 17:15:50|视频创建时间，为GMT时间。

 |
|CreationTime|String|2017-11-14T09:15:50Z|视频创建时间，为UTC时间。

 |
|Description|String|阿里云VOD视频描述|视频描述。

 |
|Duration|Float|135.6|视频时长\(秒\)

 |
|ModificationTime|String|2017-11-14T09:15:50Z|视频更新时间，为UTC时间。

 |
|ModifyTime|String|2017-11-14 17:15:50|视频更新时间，为GMT时间。

 |
|Size|Long|10897890|视频源文件大小\(字节\)。

 |
|Snapshots| |"Snapshot":\["http://image.example.com/snapshot/sample000001.jpg?auth\_key=1498476426-0-0-f00b9455c49a423ce69cf4e273334f52","http://image.example.com/snapshot/sample00002.jpg?auth\_key=1498476426-0-0-f00b9455c49a423ce69cf4e272434f52"\]|视频截图URL数组。

 |
|Status|String|Normal|视频状态。

 |
|StorageLocation|String|out-xxxx.oss-cn-shanghai.aliyuncs.com|视频存储区域。

 |
|Tags|String|标签1, 标签2|视频标签，多个会用逗号分隔。

 |
|Title|String|阿里云VOD视频标题|视频标题。

 |
|VideoId|String|9ae2af636ca64835b0c10412f44891fc|视频ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://vod.cn-shanghai.aliyuncs.com/?Action=GetVideoList
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<GetVideoListResponse>
  <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
	  <Total>100</Total>
	  <VideoList>
		    <Video>
			      <VideoId>93ab850b4f6f44eab54b6e91d24d81d4</VideoId>
			      <Title>阿里云VOD视频标题</Title>
			      <Description>阿里云VOD视频描述</Description>
			      <Duration>135.6</Duration>
			      <CoverURL>https://image.example.com/coversample.jpg</CoverURL>
			      <Status>Normal</Status>
			      <CreationTime>2017-06-26T05:38:48Z</CreationTime>
			      <Size>10897890</Size>
			      <Snapshots>
				        <Snapshot>http://image.example.com/snapshot/sample000001.jpg?auth_key=1498476426-0-0-f00b9455c49a423ce69cf4e273334f52</Snapshot>
				        <Snapshot>http://image.example.com/snapshot/sample00002.jpg?auth_key=1498476426-0-0-f00b9455c49a423ce69cf4e272434f52</Snapshot>
			      </Snapshots>
			      <CateId>78</CateId>
			      <CateName>分类名</CateName>
			      <Tags>标签1, 标签2</Tags>
		    </Video>
	  </VideoList>
</GetVideoListResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"VideoList":{
		"Video":[
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
				"Snapshots":{
					"Snapshot":[
						"http://image.example.com/snapshot/sample000001.jpg?auth_key=1498476426-0-0-f00b9455c49a423ce69cf4e273334f52",
						"http://image.example.com/snapshot/sample00002.jpg?auth_key=1498476426-0-0-f00b9455c49a423ce69cf4e272434f52"
					]
				},
				"Title":"阿里云VOD视频标题",
				"Size":10897890
			}
		]
	},
	"RequestId":"25818875-5F78-4A13-BEF6-D7393642CA58",
	"Total":100
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。


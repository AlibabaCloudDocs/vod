# SubmitSnapshotJob {#doc_api_vod_SubmitSnapshotJob .reference}

调用SubmitSnapshotJob提交视频截图作业，开始异步截图处理。支持普通截图和雪碧图截图。

-   暂时只支持生成**jpg**格式的图片。
-   截图完成会产生EventType=SnapshotComplete,SubType=SpecifiedTime的[截图回调](https://help.aliyun.com/document_detail/57337.html?spm=a2c4g.11186623.2.15.a35d5f28WoLjDw)消息。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=SubmitSnapshotJob&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|SubmitSnapshotJob|系统规定参数。取值：**SubmitSnapshotJob**。

 |
|VideoId|String|是|d3e680e618708fef7cefbf2cae7cc931|视频ID。

 |
|AccessKeyId|String|否|your\_accesskey\_id|您的AccessKey ID。

 |
|Count|Long|否|1|截图的最大数量。默认值：**1**。

 **说明：** **Count**和**Interval**至少指定一个，若同时指定，截图数目以少者为准。

 |
|Height|String|否|8|截图高，取值范围：`[8,4096]`，默认原片高，单位：px。

 |
|Interval|Long|否|1|截图的间隔时间，必须**大于等于0**，单位：秒。其中，Interval为**0**表示按照Count数根据视频时长平均截图。默认值：**1**。

 |
|SnapshotTemplateId|String|否|snapshotTemplateId|截图模板ID，推荐先构建截图模板，再传递截图模板ID。

 **说明：** 如果传递该参数，会忽略除**Action**、**VideoId**之外的请求参数。截图模板创建详细请参考[添加截图模板](https://help.aliyun.com/document_detail/99406.html?spm=a2c4g.11186623.2.17.a35d5f28WoLjDw)。

 |
|SpecifiedOffsetTime|Long|否|0|截图指定时间的起始点，单位：毫秒。默认值：**0**。

 |
|SpriteSnapshotConfig|String|否|\{'CellWidth': 120, 'CellHeight': 68, 'Columns': 3,'Lines': 10, 'Padding': 20, 'Margin': 50\}|生成雪碧图的配置信息，如果不为空则生成雪碧图。

 |
|UserData|String|否|\{"Vod":\{"Title":"test","CateId":"234"\}"\}|自定义数据，将在截图完成时进行回调。

 -   最大长度为1024。
-   建议采用JSON字符串。

 |
|Width|String|否|8|截图宽，取值范围：`[8,4096]`，默认原片宽，单位：px。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|25818875-5F78-4A13-BEF6-D7393642CA58|请求ID。

 |
|SnapshotJob| | |截图作业信息。

 |
|JobId|String|ad90a501b1b94ba6afb72374ad005046|截图作业ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=SubmitSnapshotJob
&VideoId=d3e680e618708fef7cefbf2cae7cc931
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<SubmitSnapshotJobResponse>
	  <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
	  <SnapshotJob>
		    <JobId>ad90a501b1b94ba6afb72374ad005046</JobId>
	  </SnapshotJob>
</SubmitSnapshotJobResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"25818875-5F78-4A13-BEF6-D7393642CA58",
	"SnapshotJob":{
		"JobId":"ad90a501b1b94ba6afb72374ad005046"
	}
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。


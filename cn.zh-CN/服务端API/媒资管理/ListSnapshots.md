# ListSnapshots {#doc_api_vod_ListSnapshots .reference}

调用ListSnapshots查询指定媒体截图。

**说明：** 如有多次视频截图，则返回最近一次成功的截图数据。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=ListSnapshots&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListSnapshots|系统规定参数。取值： **ListSnapshots**。

 |
|VideoId|String|是|d3e680e618708fef7cefbf2cae7cc931|视频ID。

 |
|AccessKeyId|String|否|your\_accesskey\_id|您的AccessKey ID。

 |
|AuthTimeout|String|否|3600|截图地址过期时间。默认值：**3600秒**，最小值：**3600秒**\(当指定时间小于3600秒时，默认为3600秒）。 \> 如果返回的是OSS地址，为降低源站安全风险，最大值为2592000\(即30天\)。该参数只有开启了[URL鉴权](https://help.aliyun.com/document_detail/57007.html?spm=a2c4g.11186623.2.15.52a33d21ZDBetT)才会生效。

 |
|PageNo|String|否|1|翻页页号。默认值：**1**。

 |
|PageSize|String|否|20|翻页大小。默认值：**20**，最大值：**100**。

 |
|SnapshotType|String|否|CoverSnapshot|返回的截图类型。取值范围：

 -   **CoverSnapshot（默认值）**：封面截图
-   **NormalSnapshot**：SubmitSnapshotJob接口发起的普通截图
-   **SpriteSnapshot**：SubmitSnapshotJob接口发起的雪碧截图
-   **SpriteOriginSnapshot**：组成雪碧图的原始小图

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|MediaSnapshot| | |媒体截图数据。

 |
|CreationTime|String|2017-12-20T12:23:45Z|截图作业创建时间，为UTC时间。

 |
|JobId|String|ad90a501b1b94ba6afb72374ad005046|截图作业ID。

 |
|Regular|String|http://image.com/snapshot/sample\{SnapshotCount\}.jpg|截图地址生成规则。

 |
|Snapshots| | |截图数据。

 |
|Index|Long|1|截图索引值。

 |
|Url|String|http://image.com/snapshot/sample00001.jpg|截图地址。

 |
|Total|Long|100|截图总数。

 |
|RequestId|String|25818875-5F78-4A13-BEF6-D7393642CA58|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=ListSnapshots
&VideoId=d3e680e618708fef7cefbf2cae7cc931
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ListSnapshotsResponse>
  <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
	  <MediaSnapshot>
		    <Total>100</Total>
		    <Regular>http://image.com/snapshot/sample{SnapshotCount}.jpg</Regular>
		    <CreationTime>2017-12-20T12:23:45Z</CreationTime>
		    <JobId>ad90a501b1b94ba6afb72374ad005046</JobId>
		    <Snapshots>
			      <Snapshot>
				        <Index>1</Index>
				        <Url>http://image.com/snapshot/sample00001.jpg</Url>
			      </Snapshot>
		    </Snapshots>
	  </MediaSnapshot>
</ListSnapshotsResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"MediaSnapshot":{
		"CreationTime":"2017-12-20T12:23:45Z",
		"Regular":"http://image.com/snapshot/sample{SnapshotCount}.jpg",
		"JobId":"ad90a501b1b94ba6afb72374ad005046",
		"Snapshots":{
			"Snapshot":[
				{
					"Index":1,
					"Url":"http://image.com/snapshot/sample00001.jpg"
				}
			]
		},
		"Total":100
	},
	"RequestId":"25818875-5F78-4A13-BEF6-D7393642CA58"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。


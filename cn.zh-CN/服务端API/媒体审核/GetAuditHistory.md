# GetAuditHistory {#doc_api_vod_GetAuditHistory .reference}

调用GetAuditHistory获取人工审核的历史记录。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=GetAuditHistory&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetAuditHistory|系统规定参数，取值：**GetAuditHistory**。

 |
|VideoId|String|是|93ab850b4f6f44eab54b6e91d24d81d4|视频ID。

 |
|PageNo|Long|否|1|页号，默认值为**1**。

 |
|PageSize|Long|否|10|分页大小。默认值为**10**，最大值为**100**。

 |
|SortBy|String|否|CreationTime:Desc|结果排序。取值范围：

 -   **CreationTime:Desc**（默认值）：按创建时间倒序
-   **CreationTime:Asc**

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Histories| | |审核历史记录列表。

 |
|Auditor|String|auditor|审核员。

 |
|Comment|String|有露点镜头|审核详情，审核员给出的具体评价。

 |
|CreationTime|String|2017-01-11T12:00:00Z|记录创建的时间。

 |
|Reason|String|色情视频|审核不通过理由。若审核结果为不通过，需给出不通过的理由。

 |
|Status|String|Blocked|本次审核结果。

 |
|RequestId|String|04F0F334-1335-436C-A1D7-6C044FE73368|请求ID。

 |
|Status|String|Normal|本次审核结果。

 表示当前人工审核的结果，为枚举值，取值范围：

 -   **Normal**
-   **Blocked**

 |
|Total|Long|2|审核历史记录总条数。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=GetAuditHistory
&VideoId=93ab850b4f6f44eab54b6e91d24d81d4
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<GetAuditHistoryResponse>
  <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
	  <Status>Blocked</Status>
	  <Total>2</Total>
	  <Histories>
		    <CreationTime>2017-12-18T07:39:00Z</CreationTime>
		    <Status>Blocked</Status>
		    <Reason>色情视频</Reason>
		    <Comment>有露点镜头</Comment>
	  </Histories>
	  <Histories>
		    <CreationTime>2017-12-18T07:30:00Z</CreationTime>
		    <Status>Normal</Status>
		    <Reason></Reason>
		    <Comment></Comment>
	  </Histories>
</GetAuditHistoryResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Histories":[
		{
			"CreationTime":"2017-12-18T07:39:00Z",
			"Status":"Blocked",
			"Comment":"有露点镜头",
			"Reason":"色情视频"
		},
		{
			"CreationTime":"2017-12-18T07:30:00Z",
			"Status":"Normal",
			"Comment":"",
			"Reason":""
		}
	],
	"Status":"Blocked",
	"RequestId":"04F0F334-1335-436C-A1D7-6C044FE73368",
	"Total":2
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。


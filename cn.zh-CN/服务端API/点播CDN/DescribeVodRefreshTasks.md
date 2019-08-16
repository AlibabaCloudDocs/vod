# DescribeVodRefreshTasks {#doc_api_vod_DescribeVodRefreshTasks .reference}

调用DescribeVodRefreshTasks查询刷新和预热状态是否生效。

**说明：** 

-   支持根据任务ID或URL查询。
-   若Taskid与Objectpath都不指定，则默认查询3天内，第一页的数据（20条）。
-   Taskid与Objectpath可以同时指定。
-   当指定DomainName或Status时，ObjectType该项为必填。
-   只能查询3天内的数据。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=DescribeVodRefreshTasks&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeVodRefreshTasks|系统规定参数。取值：**DescribeVodRefreshTasks**。

 |
|DomainName|String|否|example.com|域名。

 |
|EndTime|String|否|2017-01-01T12:12:20Z|结束时间。

 |
|ObjectPath|String|否|http://aaa.com/1.txt|按路径查询，准确匹配。

 |
|ObjectType|String|否|file|任务类型。取值范围：

 -   file
-   directory
-   preload

 |
|PageNumber|Integer|否|1|页码。

 |
|PageSize|Integer|否|20|分页大小。默认值：**20**。最大值：**50**。

 |
|ResourceGroupId|String|否|xxxxx|资源组ID。

 |
|StartTime|String|否|2017-01-01T12:12:20Z|开始时间。

 |
|Status|String|否|Complete|任务状态。取值范围：

 -   Complete（完成）
-   Refreshing（刷新中）
-   Failed（刷新失败）

 |
|TaskId|String|否|704225667|按任务ID查询刷新状态。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|PageNumber|Long|1|页码。

 |
|PageSize|Long|10|整页大小。

 |
|RequestId|String|174F6032-AA26-470D-B90E-36F0EB205BEE|请求ID。

 |
|Tasks| | |TaskItem组成的Task任务列表。

 |
|CreationTime|String|2014-11-27T08:23:22Z|任务对象创建时间。

 |
|Description|String|Internal Error|刷新预热失败返回的错误描述。目前有三种：

 -   Internal Error
-   Origin Timeout
-   Origin Return StatusCode 5XX

 |
|ObjectPath|String|http://aaa.com/1.txt|刷新对象路径。

 |
|ObjectType|String|file|任务类型。

 |
|Process|String|100%|进度百分比。

 |
|Status|String|Complete|状态。取值范围：

 -   Complete（完成）
-   Refreshing（刷新中）
-   Failed（刷新失败）
-   Pending（等待刷新）

 |
|TaskId|String|704225667|任务ID。

 |
|TotalCount|Long|2|总条数。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=DescribeVodRefreshTasks
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeVodRefreshTasksResponse>
    <Tasks>
        <Task>
            <CreationTime>2014-11-27T08:23:22Z</CreationTime>
            <ObjectPath>http://aaa.com/1.txt</ObjectPath>
            <Status>Complete</Status>
            <TaskId>704225667</TaskId>
            <ObjectType>file</ObjectType>
            <Process>100%</Process>
        </Task>
        <Task>
            <CreationTime>2014-11-27T08:18:38Z</CreationTime>
            <ObjectPath>http://bbb.com/1.txt</ObjectPath>
            <Status>Complete</Status>
            <TaskId>704222904</TaskId>
            <ObjectType>file</ObjectType>
            <Process>100%</Process>
        </Task>
    </Tasks>
    <PageNumber>1</PageNumber>
    <PageSize>10</PageSize>
    <TotalCount>2</TotalCount>
    <RequestId>13DF2E2F-FBF8-4E1C-9222-98141795443D</RequestId>
</DescribeVodRefreshTasksResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":2,
	"PageSize":10,
	"RequestId":"174F6032-AA26-470D-B90E-36F0EB205BEE",
	"Tasks":{
		"Task":[
			{
				"ObjectPath":"http://aaa.com/1.txt",
				"CreationTime":"2014-11-27T08:23:22Z",
				"Status":"Complete",
				"ObjectType":"file",
				"Process":"100%",
				"TaskId":"704225667"
			},
			{
				"ObjectPath":"http://bbb.com/1.txt",
				"CreationTime":"2014-11-27T08:18:38Z",
				"Status":"Complete",
				"ObjectType":"file",
				"Process":"100%",
				"TaskId":"704222904"
			}
		]
	}
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。


# DescribeVodRefreshTasks

Queries the information about one or more refresh or prefetch tasks.

**Note:**

-   This operation is available only in the **China \(Shanghai\)** region.
-   If you specify neither the TaskId parameter nor the ObjectPath parameter, the data in the last three days on the first page is returned. By default, one page displays a maximum of 20 entries. You can specify the Taskid and Objectpath parameters at the same time.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=DescribeVodRefreshTasks&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeVodRefreshTasks|The operation that you want to perform. Set the value to **DescribeVodRefreshTasks**. |
|TaskId|String|No|70422\*\*\*\*|The task ID based on which the query is performed. |
|ObjectPath|String|No|http://example.com/\*\*\*.txt|The object URL based on which the query is performed. The URL is used as a condition for an exact match. |
|PageNumber|Integer|No|1|The number of the page to return. |
|ObjectType|String|No|file|The type of the task. Valid values:

 -   **file**: refreshes one or more files.
-   **directory**: refreshes the files under one or more directories.
-   **preload**: prefetches one or more files.

 **Note:** If you specify the DomainName or TaskStatus parameter, you must also specify the ObjectType parameter. |
|DomainName|String|No|example.com|The domain name. |
|Status|String|No|Complete|The status of the task. Valid values:

 -   **Complete**: indicates that the task is complete.
-   **Refreshing**: indicates that the task is in progress.
-   **Failed**: indicates that the task failed. |
|PageSize|Integer|No|20|The number of entries to return on each page. Default value: **20**. Maximum value: **50**. |
|StartTime|String|No|2017-01-01T12:12:20Z|The beginning of the time range to query. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC.

 **Note:** You can query data that is collected in the last three days. |
|EndTime|String|No|2017-01-01T12:30:20Z|The end of the time range to query. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageNumber|Long|1|The page number of the returned page. |
|PageSize|Long|10|The number of entries returned per page. |
|RequestId|String|174F6032-AA26-470D-\*\*\*\*-36F0EB205BEE|The ID of the request. |
|Tasks|Array of Task| |The information about the returned tasks. |
|Task| | | |
|CreationTime|String|2014-11-27T08:23:22Z|The time when the task was created. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|Description|String|Internal Error|The type of the error that was returned when the refresh or prefetch task failed. Valid values:

 -   **Internal Error**: indicates that an internal error occurred.
-   **Origin Timeout**: indicates that the response from the origin server timed out.
-   **Origin Return StatusCode 5XX**: indicates that the origin server returned a 5XX error. |
|ObjectPath|String|http://example.com/\*\*\*\*.txt|The URL of the object to which the refresh or prefetch task is applied. |
|ObjectType|String|file|The type of the task. Valid values:

 -   **file**: refreshes one or more files. This is the default value.
-   **directory**: refreshes the files under one or more directories.
-   **preload**: prefetches one or more files. |
|Process|String|100%|The progress of the task, in percentage. |
|Status|String|Complete|The status of the task. Valid values:

 -   **Complete**: indicates that the task is complete.
-   **Refreshing**: indicates that the task is in progress.
-   **Failed**: indicates that the task failed.
-   **Pending**: indicates that the task is pending. |
|TaskId|String|704225667|The ID of the task. |
|TotalCount|Long|2|The total number of entries returned. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=DescribeVodRefreshTasks
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeVodRefreshTasksResponse>
    <Tasks>
        <Task>
            <CreationTime>2014-11-27T08:23:22Z</CreationTime>
            <ObjectPath>http://example.com/****.txt</ObjectPath>
            <Status>Complete</Status>
            <TaskId>704225667</TaskId>
            <ObjectType>file</ObjectType>
            <Process>100%</Process>
        </Task>
        <Task>
            <CreationTime>2014-11-27T08:18:38Z</CreationTime>
            <ObjectPath>http://example.com/****.txt</ObjectPath>
            <Status>Complete</Status>
            <TaskId>704222904</TaskId>
            <ObjectType>file</ObjectType>
            <Process>100%</Process>
        </Task>
    </Tasks>
    <PageNumber>1</PageNumber>
    <PageSize>10</PageSize>
    <TotalCount>2</TotalCount>
    <RequestId>13DF2E2F-FBF8-4E1C-****-98141795443D</RequestId>
</DescribeVodRefreshTasksResponse>
```

`JSON` format

```
{
    "Tasks" : {
        "Task" : [{
                "CreationTime" : "2014-11-27T08:23:22Z",
                "ObjectPath" : "http://example.com/****.txt",
                "Status" : "Complete",
                "TaskId" : "704225667",
                "ObjectType" : "file",
                "Process" : "100%"
            }, {
                "CreationTime" : "2014-11-27T08:18:38Z",
                "ObjectPath" : "http://example.com/****.txt",
                "Status" : "Complete",
                "TaskId" : "704222904",
                "ObjectType" : "file",
                "Process" : "100%"
            }
        ]
    },
    "PageNumber" : 1,
    "PageSize" : 10,
    "TotalCount" : 2,
    "RequestId" : "174F6032-AA26-470D-****-36F0EB205BEE"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/vod).

## Common errors

The following table describes the common errors that this operation can return.

|Error code

|Error message

|HTTP status code

|Description |
|------------|---------------|------------------|-------------|
|Throttling

|Request was denied due to request throttling.

|503

|The error message returned because the request was denied due to throttling. |
|OperationDenied

|Your account does not open VOD service yet.

|403

|The error message returned because ApsaraVideo VOD has not been activated for your Alibaba Cloud account. |
|OperationDenied.Suspended

|Your VOD service is suspended.

|403

|The error message returned because your Alibaba Cloud account has overdue payments. Add funds to your account. |
|InvalidTaskId.Malformed

|Specified TaskId is malformed.

|400

|The error message returned because the value of the TaskId parameter is in an invalid format. |


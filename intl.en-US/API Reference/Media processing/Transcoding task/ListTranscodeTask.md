# ListTranscodeTask

Queries historical transcoding tasks of a video based on the video ID. This operation does not return information about a specific job.

**Note:** You can call the [GetTranscodeTask](~~109121~~) operation to query the detailed information about a job.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=ListTranscodeTask&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ListTranscodeTask|The operation that you want to perform. Set the value to **ListTranscodeTask**. |
|VideoId|String|Yes|d4860fcc6a5\*\*\*\*\*bce9fed52e893824|The ID of the video. |
|StartTime|String|No|2019-01-23T12:35:12Z|The beginning of the time range to query. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC. |
|EndTime|String|No|2019-01-23T12:40:12Z|The end of the time range to query. The end time must be later than the start time. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC. |
|PageSize|Integer|No|10|The number of entries to return on each page. Valid values: 1 to **50**. Default value: **10**. |
|PageNo|Integer|No|1|The number of the page to return. Default value: **1**. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|25818875-5F78-4A\*\*\*\*\*F6-D7393642CA58|The ID of the request. |
|TranscodeTaskList|Array of TranscodeTask| |The transcoding jobs. |
|CompleteTime|String|2019-01-23T12:40:12Z|The time when the transcoding task was complete. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|CreationTime|String|2019-01-23T12:35:12Z|The time when the transcoding task was created. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|TaskStatus|String|Processing|The status of the transcoding task. Valid values:

 -   **Processing**: The transcoding is in progress.
-   **Partial**: The video was partially transcoded.
-   **CompleteAllSucc**: All the transcoding jobs were complete and the video was fully transcoded.
-   **CompleteAllFail**: All the transcoding jobs were complete but the video failed to be transcoded. If an exception occurs in the mezzanine file, no transcoding job is initiated and the transcoding task fails.
-   **CompletePartialSucc**: All the transcoding jobs were complete but the video was partially transcoded. |
|TranscodeTaskId|String|b1b65ab107\*\*\*\*\*ba3dbb900f6c1fe0|The ID of the transcoding task. |
|TranscodeTemplateGroupId|String|b500c7094bd24\*\*\*\*\*f3e9900752d7c3|The ID of the transcoding template group. |
|Trigger|String|Auto|The trigger type. Valid values:

 -   **Auto**: The transcoding task is automatically triggered when the video is uploaded.
-   **Manual**: The transcoding task is triggered after you call the SubmitTranscodeJobs operation. |
|VideoId|String|d4860fcc6a5\*\*\*\*\*bce9fed52e893824|The ID of the video. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=ListTranscodeTask
&VideoId=d4860fcc6a5*****bce9fed52e893824
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ListTranscodeTaskResponse>
      <RequestId>25818875-5F78-4A*****F6-D7393642CA58</RequestId>
	  <TranscodeTaskList>
		    <TranscodeTaskId>b1b65ab107*****ba3dbb900f6c1fe0</TranscodeTaskId>
		    <VideoId>d4860fcc6a5*****bce9fed52e893824</VideoId>
		    <TaskStatus>Processing</TaskStatus>
		    <TranscodeTemplateGroupId>b500c7094bd24*****f3e9900752d7c3</TranscodeTemplateGroupId>
		    <CreationTime>2019-01-23T12:35:12Z</CreationTime>
		    <CompleteTime>2019-01-23T12:40:12Z</CompleteTime>
	  </TranscodeTaskList>
	  <TranscodeTaskList>
		    <TranscodeTaskId>91449a74a9d7*****31e179a1ec1e</TranscodeTaskId>
		    <VideoId>d4860fcc6a5*****bce9fed52e893824</VideoId>
		    <TaskStatus>CompeleteAllSucc</TaskStatus>
		    <TranscodeTemplateGroupId>947b9f5b0eb*****3d985df69d76b7</TranscodeTemplateGroupId>
		    <CreationTime>2019-01-23T12:35:12Z</CreationTime>
		    <CompleteTime>2019-01-23T12:40:12Z</CompleteTime>
	  </TranscodeTaskList>
</ListTranscodeTaskResponse>
```

`JSON` format

```
{
  "RequestId": "25818875-5F78-4A*****F6-D7393642CA58",
  "TranscodeTaskList":[
    {
      "TranscodeTaskId":"b1b65ab107*****ba3dbb900f6c1fe0",
      "VideoId":"d4860fcc6a5*****bce9fed52e893824",
      "TaskStatus":"Processing",
      "TranscodeTemplateGroupId":"b500c7094bd24*****f3e9900752d7c3",
      "CreationTime":"2019-01-23T12:35:12Z",
      "CompleteTime":"2019-01-23T12:40:12Z"
    },
    {
      "TranscodeTaskId":"91449a74a9d7*****31e179a1ec1e",
      "VideoId":"d4860fcc6a5*****bce9fed52e893824",
      "TaskStatus":"CompeleteAllSucc",
      "TranscodeTemplateGroupId":"947b9f5b0eb*****3d985df69d76b7",
      "CreationTime":"2019-01-23T12:35:12Z",
      "CompleteTime":"2019-01-23T12:40:12Z"
    }
  ]
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/vod).


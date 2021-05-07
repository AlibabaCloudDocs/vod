# SubmitWorkflowJob

Initiates a video-on-demand \(VOD\) workflow to process audio and video files.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=SubmitWorkflowJob&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SubmitWorkflowJob|The operation that you want to perform. Set the value to **SubmitWorkflowJob**. |
|WorkflowId|String|Yes|34d577eade6\*\*\*\*\*33860bdf1237|The ID of the workflow. |
|MediaId|String|No|058b39e75269\*\*\*\*\*da42b08f00459|The ID of the media asset. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|A01C8FF4-C106-44\*\*\*\*\*31-418F973DADB7|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=SubmitWorkflowJob
&WorkflowId=34d577eade6*****33860bdf1237
&<Common request parameters>
```

Sample success responses

`XML` format

```
<SubmitWorkflowJobResponse>
      <RequestId>A01C8FF4-C106-44*****31-418F973DADB7</RequestId>
</SubmitWorkflowJobResponse>
```

`JSON` format

```
{
    "RequestId": "A01C8FF4-C106-44*****31-418F973DADB7"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/vod).


# SubmitDynamicImageJob

Submits an animated image job and starts asynchronous processing.

**Note:**

-   You can capture a part of a video and generate animated images only when the video is in the **UploadSucces**, **Transcoding**, **Normal**, **Checking**, or **Blocked** state.
-   The fee for generating animated images is included in the video transcoding fees. Both the services are charged by resolution and duration.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=SubmitDynamicImageJob&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SubmitDynamicImageJob|The operation that you want to perform. Set the value to **SubmitDynamicImageJob**. |
|DynamicImageTemplateId|String|Yes|1a443dc52e\*\*\*\*\*f10abc4794d70|The ID of the animated image template. |
|VideoId|String|Yes|7d2fbc3e273441\*\*\*\*\*bdb0e08e55f|The ID of the video. |
|OverrideParams|String|No|\{"Watermarks":\[\{"Content":"User ID: 66666","WatermarkId":"8ca03c884944bd0\*\*\*\*\*5efccc312367"\}\]\}|The parameters used for overriding. The value is a JSON-formatted string. For more information, see the "OverrideParams" section of the [Media processing parameters](~~98618~~) topic. The parameters are used to replace the parameters in the animated image template. For more information, see the [Basic data types](~~52839~~) topic. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|DynamicImageJob|Struct| |The information about the animated image job. |
|JobId|String|ad90a501b1b\*\*\*\*\*fb72374ad005046|The ID of the animated image job. |
|RequestId|String|25818875-5F78\*\*\*\*\*BEF6-D7393642CA58|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=SubmitDynamicImageJob
&DynamicImageTemplateId=1a443dc52e*****f10abc4794d70
&VideoId=7d2fbc3e273441*****bdb0e08e55f
&<Common request parameters>
```

Sample success responses

`XML` format

```
<SubmitDynamicImageJobResponse>
      <RequestId>25818875-5F78*****BEF6-D7393642CA58</RequestId>
      <DynamicImageJob>
            <JobId>ad90a501b1b*****fb72374ad005046</JobId>
      </DynamicImageJob>
</SubmitDynamicImageJobResponse>
```

`JSON` format

```
{
    "RequestId": "25818875-5F78*****BEF6-D7393642CA58",
    "DynamicImageJob": {
        "JobId": "ad90a501b1b*****fb72374ad005046"
    }
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
|InvalidVideo.NotFound

|The video does not exist.

|404

|The error message returned because the video does not exist. |
|NoSuchResource

|The specified resource %s does not exist.

|404

|The error message returned because the user-related resource does not exist. %s indicates the specific resource information. |
|Forbidden.IllegalStatus

|Status of the video is illegal.

|400

|The error message returned because the video status is invalid. You can capture a part of a video and generate dynamic images only when the video is in the **UploadSucces**, **Transcoding**, **Normal**, **Checking**, or **Blocked** state. |


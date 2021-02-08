# SubmitPreprocessJobs

Preprocesses a video by using the production studio.

**Note:**

-   During video preprocessing, videos are transcoded to meet the playback requirements of the production studio. Therefore, you are **charged** for video preprocessing. You can submit a ticket for information about the **production studio** service.
-   You can obtain the preprocessing result in the [TranscodeComplete](~~55638~~) event notification. If the value of the **Preprocess** parameter is true in the event notification, the video is preprocessed.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=SubmitPreprocessJobs&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SubmitPreprocessJobs|The operation that you want to perform. Set the value to **SubmitPreprocessJobs**. |
|PreprocessType|String|Yes|LivePreprocess|The preprocessing type. Set the value to **LivePreprocess**, which indicates that the video is preprocessed in the production studio. |
|VideoId|String|Yes|7d2fbc3e27\*\*\*\*\*0bdb0e08e55f|The ID of the video. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PreprocessJobs|Array of PreprocessJob| |The job information. |
|PreprocessJob| | | |
|JobId|String|bb396607fd\*\*\*\*\*11fee9effbb99c|The ID of the job. |
|RequestId|String|D08EF493-1A69-42\*\*\*\*\*6D-EC66BE3339B3|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=SubmitPreprocessJobs
&PreprocessType=LivePreprocess
&VideoId=7d2fbc3e27*****0bdb0e08e55f
&<Common request parameters>
```

Sample success responses

`XML` format

```
<SubmitPreprocessJobsRespon>
      <RequestId>D08EF493-1A69-42*****6D-EC66BE3339B3</RequestId>
      <PreprocessJobs>
            <PreprocessJob>
                  <JobId>bb396607fd*****11fee9effbb99c</JobId>
            </PreprocessJob>
      </PreprocessJobs>
</SubmitPreprocessJobsRespon>
```

`JSON` format

```
{
    "SubmitPreprocessJobsRespon": {
        "RequestId": "D08EF493-1A69-42*****6D-EC66BE3339B3",
        "PreprocessJobs": {
            "PreprocessJob": {
                "JobId": "bb396607fd*****11fee9effbb99c"
            }
        }
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

|The error message returned because the specified resource does not exist. |
|Forbidden.IllegalStatus

|Status of the video is illegal.

|400

|The error message returned because the video status is invalid. You can preprocess a video only in the **UploadSucces**, **Normal**, **Checking**, or **Transcoding** state. |

## SDK examples

We recommend that you use [server SDKs](~~101789~~) to call this operation. You can view the sample code of different languages to call this operation by clicking the following links:

-   [Java](~~61063~~)
-   [Python](~~61054~~)
-   [PHP](~~61069~~)
-   [.NET](~~84750~~)
-   [Node.js](~~101396~~)
-   [Go](~~101411~~)
-   [C/C++](~~101261~~)


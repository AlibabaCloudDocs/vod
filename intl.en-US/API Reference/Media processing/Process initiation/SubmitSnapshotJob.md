# SubmitSnapshotJob

Submits a snapshot job for a video and starts asynchronous snapshot processing.

**Note:**

-   Only snapshots in the JPG format are generated.
-   After a snapshot job is complete, ApsaraVideo VOD sends a [SnapshotComplete](~~57337~~) event notification that contains EventType=SnapshotComplete and SubType=SpecifiedTime.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=SubmitSnapshotJob&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SubmitSnapshotJob|The operation that you want to perform. Set the value to **SubmitSnapshotJob**. |
|VideoId|String|Yes|d3e680e618708\*\*\*\*\*efbf2cae7cc931|The ID of the video. |
|SpecifiedOffsetTime|Long|No|0|The start time of the specified snapshot time period.

 -   Unit: milliseconds.
-   Default value: **0**. |
|Width|String|No|1280|The width of each snapshot. Valid values: `[8,4096]`. By default, the width of the video mezzanine file is used. Unit: pixel. |
|Height|String|No|720|The height of each snapshot. Valid values: `[8,4096]`. By default, the height of the video mezzanine file is used. Unit: pixel. |
|Count|Long|No|1|The maximum number of snapshots. Default value: **1**. |
|Interval|Long|No|1|The snapshot interval. The value must be **greater than or equal to 0**. Unit: seconds. If you set this parameter to **0**, snapshots are taken at even intervals based on the video duration divided by the value of the Count parameter. Default value: **1**. |
|SpriteSnapshotConfig|String|No|\{'CellWidth': 120, 'CellHeight': 68, 'Columns': 3,'Lines': 10, 'Padding': 20, 'Margin': 50\}|The sprite snapshot configuration. If you set this parameter, sprite snapshots are generated. For more information, see [SpriteSnapshotConfig](~~86952~~). |
|SnapshotTemplateId|String|No|f5b228fe693\*\*\*\*\*bf55bd87789|The ID of the snapshot template.

 -   We recommend that you create a snapshot template before you specify the ID of the snapshot template.
-   If you set the SnapshotTemplateId parameter, all the other request parameters except the Action and VideoId parameters are ignored.
-   For more information about how to create a snapshot template, see [AddVodTemplate](~~99406~~). |
|UserData|String|No|\{"MessageCallback":\{"CallbackURL":"http://test.test.com"\},"Extend":\{"localId":"xxx","test":"www"\}\}|The custom configurations, including the configuration of transparent data transmission and callback configurations. The value is a JSON-formatted string. For more information, see [UserData](~~86952~~).

 **Note:** The callback configurations take effect only when you specify the HTTP callback URL and select the specific callback events in the ApsaraVideo VOD console. |

**Note:** You must set at least one of the Count and Interval parameters. If you set both of them, the setting with fewer snapshots generated prevails.

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|25818875-5F78-4A\*\*\*\*\*F6-D7393642CA58|The ID of the request. |
|SnapshotJob|Struct| |The information about the snapshot job. |
|JobId|String|ad90a501b1b94b\*\*\*\*\*72374ad005046|The ID of the snapshot job. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=SubmitSnapshotJob
&VideoId=d3e680e618708*****efbf2cae7cc931
&<Common request parameters>
```

Sample success responses

`XML` format

```
<SubmitSnapshotJobResponse>
	  <RequestId>25818875-5F78-4A*****F6-D7393642CA58</RequestId>
	  <SnapshotJob>
		    <JobId>ad90a501b1b94b*****72374ad005046</JobId>
	  </SnapshotJob>
</SubmitSnapshotJobResponse>
```

`JSON` format

```
{
    "RequestId": "25818875-5F78-4A*****F6-D7393642CA58",
    "SnapshotJob": {
        "JobId": "ad90a501b1b94b*****72374ad005046"
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

|The error message returned because the video status is invalid. You can submit a snapshot job for a video only when the video is in the **UploadSucc**, **Normal**, **Checking**, or **Blocked** state. |

## SDK examples

We recommend that you use a [server SDK](~~101789~~) to call this operation. For more information about the sample code that is used to call this operation in various languages, see the following topics:

-   [Java](~~61063~~)
-   [Python](~~61054~~)
-   [PHP](~~61069~~)
-   [.NET](~~84750~~)
-   [Node.js](~~101396~~)
-   [Go](~~101411~~)
-   [C/C++](~~101261~~)


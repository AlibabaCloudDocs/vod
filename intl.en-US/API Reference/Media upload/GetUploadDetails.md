# GetUploadDetails

Queries the upload details, such as the upload time, upload ratio, and upload source, about one or more media assets based on the media asset IDs.

You can query the information such as upload ratio if you use the ApsaraVideo VOD console to upload videos. If you use upload SDKs to upload videos, make sure that the version of [upload SDKs](~~52200~~) meets one of the following requirements:

-   The version of the upload SDK for Java is 1.4.4 or later.
-   The version of the upload SDK for C++ is 1.0.0 or later.
-   The version of the upload SDK for PHP is 1.0.2 or later.
-   The version of the upload SDK for Python is 1.3.0 or later.
-   The version of the upload SDK for JavaScript is 1.4.0 or later.
-   The version of the upload SDK for Android is 1.5.0 or later.
-   The version of the upload SDK for iOS is 1.5.0 or later.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=GetUploadDetails&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GetUploadDetails|The operation that you want to perform. Set the value to **GetUploadDetails**. |
|MediaIds|String|Yes|61ccbdb06fa\*\*\*\*\*83012be4d8083f6,7d2fbc380\*\*\*\*\*b0e08e55f|The ID of the media asset. You can specify multiple video IDs. Separate multiple IDs with commas \(,\). A maximum of 20 IDs can be specified. |
|MediaType|String|No|video|The type of the media file. Set the value to **video**, which indicates audio and video files. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|ForbiddenMediaIds|List|7d2fbc380\*\*\*\*\*b0e08e55f|The IDs of the media files that cannot be accessed. |
|NonExistMediaIds|List|dfsg\*\*\*\*|The IDs of the media files that does not exist. |
|RequestId|String|9E290613-04F4-47\*\*\*\*\*F4-795D30732077|The ID of the request. |
|UploadDetails|Array of UploadDetail| |The upload details. |
|CompletionTime|String|2019-04-28T09:45:07Z|The time when the upload job was complete. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|CreationTime|String|2019-04-28T09:42:07Z|The time when the upload job was created. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|DeviceModel|String|Chrome|The device model. |
|FileSize|Long|46|The size of the file. |
|MediaId|String|61ccbdb06fa\*\*\*\*\*83012be4d8083f6|The ID of the uploaded video. |
|ModificationTime|String|2019-04-28T09:43:12Z|The time when the information about the media file was updated. The time follows the ISO 8601 standard in the yyyy-MM-ddTHH:mm:ssZ format. The time is displayed in UTC. |
|Status|String|UPLOADING|The status of the video. For more information about the valid values and value description of the parameter, see the "Status" section of the [Basic data types](~~52839~~) topic. |
|Title|String|Upload details of the test file|The title of the media file. |
|UploadIP|String|127.0.0.1|The IP address of the server that uploads the media file. |
|UploadRatio|Float|0.038|The upload ratio. |
|UploadSize|Long|346|The upload size. |
|UploadSource|String|WebSDK|The upload SDK. |
|UploadStatus|String|UPLOADING|The status of the upload job. For more information about the valid values and value description of the parameter, see the "Status" section of the [Basic data types](~~52839~~) topic. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=GetUploadDetails
&MediaIds=61ccbdb06fa*****83012be4d8083f6,7d2fbc380*****b0e08e55f
&<Common request parameters>
```

Sample success responses

`XML` format

```
<GetUploadDetailsResponse>
  <NonExistMediaIds>dfsg****</NonExistMediaIds>
  <UploadDetails>
        <DeviceModel>Chrome</DeviceModel>
        <Status>UPLOADING</Status>
        <Title>Upload details of the test file</Title>
        <ModificationTime>2019-04-28T09:43:12Z</ModificationTime>
        <UploadRatio>0.038</UploadRatio>
        <UploadSource>WebSDK</UploadSource>
        <MediaId>61ccbdb06fa*****83012be4d8083f6</MediaId>
        <UploadSize>346</UploadSize>
        <CompletionTime>2019-04-28T09:45:07Z</CompletionTime>
        <UploadStatus>UPLOADING</UploadStatus>
        <CreationTime>2019-04-28T09:42:07Z</CreationTime>
        <UploadIP>127.0.0.1</UploadIP>
        <FileSize>46</FileSize>
  </UploadDetails>
  <RequestId>9E290613-04F4-47*****F4-795D30732077</RequestId>
  <ForbiddenMediaIds>7d2fbc380*****b0e08e55f</ForbiddenMediaIds>
</GetUploadDetailsResponse>
```

`JSON` format

```
{
	"NonExistMediaIds": "dfsg****",
	"UploadDetails": [{
		"DeviceModel": "Chrome",
		"Status": "UPLOADING",
		"Title": "Upload details of the test file",
		"ModificationTime": "2019-04-28T09:43:12Z",
		"UploadRatio": "0.038",
		"UploadSource": "WebSDK",
		"MediaId": "61ccbdb06fa*****83012be4d8083f6",
		"UploadSize": "346",
		"CompletionTime": "2019-04-28T09:45:07Z",
		"UploadStatus": "UPLOADING",
		"CreationTime": "2019-04-28T09:42:07Z",
		"UploadIP": "127.0.0.1",
		"FileSize": "46"
	}],
	"RequestId": "9E290613-04F4-47*****F4-795D30732077",
	"ForbiddenMediaIds": "7d2fbc380*****b0e08e55f"
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
|LimitExceeded.MediaIds

|The input parameter "MediaIds" Exceed the limit.

|400

|The error message returned because the number of media asset IDs exceeds 20. |


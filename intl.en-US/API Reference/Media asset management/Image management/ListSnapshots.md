# ListSnapshots

Queries the snapshots that are captured from the specified media.

**Note:** If multiple snapshots of a video exist, the data of the latest snapshot is returned.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=ListSnapshots&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ListSnapshots|The operation that you want to perform. Set the value to **ListSnapshots**. |
|VideoId|String|Yes|d3e680e618708\*\*\*\*\*fbf2cae7cc931|The ID of the video. |
|SnapshotType|String|No|CoverSnapshot|The type of snapshots that are returned. Valid values:

 -   **CoverSnapshot**: thumbnail snapshot
-   **NormalSnapshot**: normal snapshot
-   **SpriteSnapshot**: sprite snapshot
-   **SpriteOriginSnapshot**: sprite source snapshot
-   **WebVttSnapshot**: WebVTT snapshot |
|AuthTimeout|String|No|3600|The validity period of the snapshot URL. Unit: seconds. Default value: **3600**. Minimum value: **3600**.

 -   If the specified validity period is less than **3600** seconds, the default value is **3600**.
-   If an Object Storage Service \(OSS\) URL is returned, the maximum validity period is limited to **2592000** seconds \(30 days\) to reduce security risks of the origin. This parameter only takes effect when [URL signing](~~57007~~) is enabled. |
|PageSize|String|No|20|The number of entries to return on each page. Default value: **20**. Maximum value: **100**. |
|PageNo|String|No|1|The number of the page to turn. Default value: **1**. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|MediaSnapshot|Struct| |The snapshot data of the media. |
|CreationTime|String|2017-12-20T12:23:45Z|The time when the snapshot job was created. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|JobId|String|ad90a501b1b94\*\*\*\*\*72374ad005046|The ID of the snapshot job. |
|Regular|String|http://image.com/snapshot/sample\{SnapshotCount\}.jpg|The rule for generating snapshot URLs. |
|Snapshots|Array of Snapshot| |The snapshot data. |
|Snapshot| | | |
|Index|Long|1|The index of the snapshot. |
|Url|String|http://image.com/snapshot/sample00001.jpg|The URL of the snapshot. |
|Total|Long|100|The total number of snapshots. |
|RequestId|String|25818875-5F78-4A\*\*\*\*\*F6-D7393642CA58|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=ListSnapshots
&VideoId=d3e680e618708*****fbf2cae7cc931
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ListSnapshotsResponse>
      <RequestId>25818875-5F78-4A*****F6-D7393642CA58</RequestId>
      <MediaSnapshot>
            <Total>100</Total>
            <Regular>http://image.com/snapshot/sample{SnapshotCount}.jpg</Regular>
            <CreationTime>2017-12-20T12:23:45Z</CreationTime>
            <JobId>ad90a501b1b94*****72374ad005046</JobId>
            <Snapshots>
                  <Snapshot>
                        <Index>1</Index>
                        <Url>http://image.com/snapshot/sample00001.jpg</Url>
                  </Snapshot>
            </Snapshots>
      </MediaSnapshot>
</ListSnapshotsResponse>
```

`JSON` format

```
{
    "RequestId": "25818875-5F78-4A*****F6-D7393642CA58",
    "MediaSnapshot":{
        "Total": 100,
        "Regular": "http://image.com/snapshot/sample{SnapshotCount}.jpg",
        "CreationTime":"2017-12-20T12:23:45Z",
        "JobId": "ad90a501b1b94*****72374ad005046",
        "Snapshots":{
        "Snapshot":[
            {
                "Index": 1,
                "Url":"http://image.com/snapshot/sample00001.jpg"
            }
            ]
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

|The error message returned because the video status is invalid. You can query the snapshot data of videos only when they are in the **UploadSucc**, **Normal**, **Checking**, or **Blocked** state. |

## SDK examples

We recommend that you use a [server SDK](~~101789~~) to call this operation. For more information about the sample code that is used to call this operation in various languages, see the following topics:

-   [Java](~~61063~~)
-   [Python](~~61054~~)
-   [PHP](~~61069~~)
-   [.NET](~~84750~~)
-   [Node.js](~~101396~~)
-   [Go](~~101411~~)
-   [C/C++](~~101261~~)


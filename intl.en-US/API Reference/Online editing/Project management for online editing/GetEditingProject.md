# GetEditingProject

Queries the details of an online editing project.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=GetEditingProject&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GetEditingProject|The operation that you want to perform. Set the value to **GetEditingProject**. |
|ProjectId|String|Yes|fb2101bf24b27\*\*\*\*\*54cb318787dc|The ID of the online editing project. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Project|Struct| |The information about the online editing project. |
|CoverURL|String|https://\*\*\*\*.com/6AB4D0E1E1C74468883516C2349\*\*\*\*.png|The thumbnail URL of the online editing project. |
|CreationTime|String|2017-10-23T13:33:40Z|The time when the online editing project was created. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|Description|String|testdescription|The description of the online editing project. |
|ModifiedTime|String|2017-10-23T14:27:26Z|The last time when the online editing project was modified. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|ProjectId|String|fb2101bf24b27\*\*\*\*\*54cb318787dc|The ID of the online editing project. |
|RegionId|String|cn-shanghai|The region where the online editing project was created. |
|Status|String|Normal|The status of the online editing project. Separate multiple states with commas \(,\). By default, all online editing projects were queried. Valid values:

-   **Normal**: indicates that the online editing project is in draft.
-   **Producing**: indicates that the video is being produced.
-   **Produced**: indicates that the video was produced.
-   **ProduceFailed**: indicates that the video failed to be produced. |
|StorageLocation|String|location\_s|The path of the Object Storage Service \(OSS\) bucket where the online editing project is stored.

**Note:** To view the path of the OSS bucket, log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/?spm=a2c4g.11186623.2.15.6948257eaZ4m54#/vod/settings/censored), and choose **Configuration Management** \> **Media Management** \> **Storage**. On the Storage page, you can view the path of the OSS bucket. |
|Timeline|String|\{\\"TimelineIn\\":0,\\"TimelineOut\\":9.42\}|The timeline of the online editing project. |
|Title|String|Video\_1508736815000|The title of the online editing project. |
|RequestId|String|63E8B7C7-4812-46\*\*\*\*\*AD-0FA56029AC86|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=GetEditingProject
&ProjectId=fb2101bf24b27*****54cb318787dc
&<Common request parameters>
```

Sample success responses

`XML` format

```
<GetEditingProjectResponse>
  <Project>
        <Status>Normal</Status>
        <Timeline>{\"TimelineIn\":0,\"TimelineOut\":9.42}</Timeline>
        <Description>testdescription</Description>
        <ModifiedTime>2017-10-23T14:27:26Z</ModifiedTime>
        <CreationTime>2017-10-23T13:33:40Z</CreationTime>
        <ProjectId>fb2101bf24b27*****54cb318787dc</ProjectId>
        <Title>Video_1508736815000</Title>
        <CoverURL>https://****.com/6AB4D0E1E1C74468883516C2349****.png</CoverURL>
        <RegionId>cn-shanghai</RegionId>
        <StorageLocation>location_s</StorageLocation>
  </Project>
  <RequestId>63E8B7C7-4812-46*****AD-0FA56029AC86</RequestId>
</GetEditingProjectResponse>
```

`JSON` format

```
{
    "Project": {
        "Status": "Normal",
        "Timeline": "{\\\"TimelineIn\\\":0,\\\"TimelineOut\\\":9.42}",
        "Description": "testdescription",
        "ModifiedTime": "2017-10-23T14:27:26Z",
        "CreationTime": "2017-10-23T13:33:40Z",
        "ProjectId": "fb2101bf24b27*****54cb318787dc",
        "Title": "Video_1508736815000",
        "CoverURL": "https://****.com/6AB4D0E1E1C74468883516C2349****.png",
        "RegionId": "cn-shanghai",
        "StorageLocation": "location_s"
    },
    "RequestId": "63E8B7C7-4812-46*****AD-0FA56029AC86"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/vod).

## SDK examples

We recommend that you use a [server SDK](~~101789~~) to call this operation. For more information about the sample code that is used to call this operation in various languages, see the following topics:

-   [Java](~~61063~~)
-   [Python](~~61054~~)
-   [PHP](~~61069~~)
-   [.NET](~~84750~~)
-   [Node.js](~~101396~~)
-   [Go](~~101411~~)
-   [C/C++](~~101261~~)


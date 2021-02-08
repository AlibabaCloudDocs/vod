# SearchEditingProject

Queries online editing projects.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=SearchEditingProject&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SearchEditingProject|The operation that you want to perform. Set the value to **SearchEditingProject**. |
|EndTime|String|No|2017-01-11T13:00:00Z|The end of the time range to query. The query is performed based on the time range during which the required online editing projects were created. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC. |
|StartTime|String|No|2017-01-11T12:00:00Z|The beginning of the time range to query. The query is performed based on the time range during which the required online editing projects were created. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC. |
|Status|String|No|Normal|The status of the online editing project. Separate multiple states with commas \(,\). By default, all online editing projects are queried.

Valid values:

-   **Normal**: indicates that the online editing project is in draft.
-   **Producing**: indicates that the video is being produced.
-   **Produced**: indicates that the video was produced.
-   **ProduceFailed**: indicates that the video failed to be produced. |
|PageNo|Integer|No|1|The number of the page to return. Default value: **1**. |
|PageSize|Integer|No|10|The number of entries to return on each page. Default value: **10**. Maximum value: **100**. |
|SortBy|String|No|CreationTime:Desc|The sorting rule of results. Valid values:

-   **CreationTime:Desc**: sorts the results based on the creation time in descending order. This is the default value.
-   **CreationTime:Asc**: sorts the results based on the creation time in ascending order. |
|Title|String|No|test|The title of the online editing project. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|ProjectList|Array of Project| |The list of online editing projects. |
|Project| | | |
|CoverURL|String|cover\_url|The thumbnail URL of the online editing project. |
|CreationTime|String|2017-01-11T12:00:00Z|The time when the online editing project was created. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|Description|String|Storyboard test project 001|The description of the online editing project. |
|Duration|Float|22.65|The duration of the online editing project, which must be consistent with the duration of the timeline.

**Note:** The Timeline parameter is not included in response parameters. |
|ModifiedTime|String|2017-01-11T13:00:00Z|The last time when the online editing project was modified. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|ProjectId|String|25cfc178d2de4\*\*\*\*\*e77aebed6afcd|The ID of the online editing project. |
|RegionId|String|cn-shanghai|The region where the online editing project was created. |
|Status|String|Normal|The status of the online editing project. Separate multiple states with commas \(,\). By default, all online editing projects were queried. Valid values:

-   **Normal**: indicates that the online editing project is in draft.
-   **Producing**: indicates that the video is being produced.
-   **Produced**: indicates that the video was produced.
-   **ProduceFailed**: indicates that the video failed to be produced. |
|StorageLocation|String|location\_s|The path of the Object Storage Service \(OSS\) bucket where the produced video is stored.

**Note:** To view the path of the OSS bucket, log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/?spm=a2c4g.11186623.2.15.6948257eaZ4m54#/vod/settings/censored), and choose **Configuration Management** \> **Media Management** \> **Storage**. On the Storage page, you can view the path of the OSS bucket. |
|Title|String|Video\_150873681\*\*\*\*|The title of the online editing project. |
|RequestId|String|9262E3DA-07FA-48\*\*\*\*\*62-FCBB6BC61D08|The ID of the request. |
|Total|Integer|2|The total number of online editing projects returned. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=SearchEditingProject
&<Common request parameters>
```

Sample success responses

`XML` format

```
<SearchEditingProjectResponse>
  <RequestId>9262E3DA-07FA-48*****62-FCBB6BC61D08</RequestId>
  <Total>2</Total>
  <ProjectList>
        <Project>
              <Status>Normal</Status>
              <Description>Storyboard test project 001</Description>
              <ModifiedTime>2017-01-11T13:00:00Z</ModifiedTime>
              <CreationTime>2017-01-11T12:00:00Z</CreationTime>
              <ProjectId>25cfc178d2de4*****e77aebed6afcd</ProjectId>
              <Title>Video_150873681****</Title>
              <Duration>22.65</Duration>
              <CoverURL>cover_url</CoverURL>
              <RegionId>cn-shanghai</RegionId>
              <StorageLocation>location_s</StorageLocation>
        </Project>
  </ProjectList>
</SearchEditingProjectResponse>
```

`JSON` format

```
{
    "RequestId": "9262E3DA-07FA-48*****62-FCBB6BC61D08",
    "Total": "2",
    "ProjectList": {
        "Project": [{
            "Status": "Normal",
            "Description": "Storyboard test project 001",
            "ModifiedTime": "2017-01-11T13:00:00Z",
            "CreationTime": "2017-01-11T12:00:00Z",
            "ProjectId": "25cfc178d2de4*****e77aebed6afcd",
            "Title": "Video_150873681****",
            "Duration": "22.65",
            "CoverURL": "cover_url",
            "RegionId": "cn-shanghai",
            "StorageLocation": "location_s"
        }]
    }
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


# AddEditingProject

Creates an online editing project.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=AddEditingProject&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|AddEditingProject|The operation that you want to perform. Set the value to **AddEditingProject**. |
|Title|String|Yes|testtimeline|The title of the online editing project. |
|Description|String|No|testtimeline001desciption|The description of the online editing project. |
|Timeline|String|No|\{"VideoTracks":\[\{"VideoTrackClips":\[\{"MediaId":"cc3308ac500\*\*\*\*\*5a54328bc3443"\},\{"MediaId":"da87a9cff64\*\*\*\*\*cd88bc6d8326e4"\}\]\}\]\}|The timeline of the online editing project, in JSON format. For more information about the structure, see [Timeline](~~52839~~).

If you do not specify this parameter, an empty timeline is created and the duration of the online editing project is zero. |
|CoverURL|String|No|https://xxx.com/6AB4D0E1E1C74468883516C2349D1FC2-6-2.png|The thumbnail URL of the online editing project. If you do not specify this parameter and the video track in the timeline has mezzanine files, the thumbnail of the first mezzanine file in the timeline is used. |
|Division|String|No|cn-shanghai|The region where you want to create the online editing project. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Project|Struct| |The information about the online editing project. For more information about the structure, see [EditingProject](~~52839~~). |
|CreationTime|String|2017-01-11T12:00:00Z|The time when the online editing project was created. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|Description|String|testtimeline001desciption|The description of the online editing project. |
|ModifiedTime|String|2017-01-11T13:00:00Z|The last time when the online editing project was modified. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|ProjectId|String|fb2101bf24bf4\*\*\*\*\*4cb318787dc|The ID of the online editing project. |
|Status|String|Normal|The status of the online editing project. Valid values:

-   **Normal**: indicates that the online editing project is in draft.
-   **Producing**: indicates that the video is being produced.
-   **Produced**: indicates that the video was produced.
-   **ProduceFailed**: indicates that the video failed to be produced. |
|Title|String|testtimeline|The title of the online editing project. |
|RequestId|String|C43C2876-6263-4B\*\*\*\*\*2C-CD0F7FCF4FE9|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=AddEditingProject
&Title=testtimeline
&<Common request parameters>
```

Sample success responses

`XML` format

```
<AddEditingProjectResponse>
  <Project>
        <Status>Normal</Status>
        <Description>testtimeline001desciption</Description>
        <ModifiedTime>2017-01-11T13:00:00Z</ModifiedTime>
        <CreationTime>2017-01-11T12:00:00Z</CreationTime>
        <ProjectId>fb2101bf24bf4*****4cb318787dc</ProjectId>
        <Title>testtimeline</Title>
  </Project>
  <RequestId>C43C2876-6263-4B*****2C-CD0F7FCF4FE9</RequestId>
</AddEditingProjectResponse>
```

`JSON` format

```
{
    "Project": {
        "Status": "Normal",
        "Description": "testtimeline001desciption",
        "ModifiedTime": "2017-01-11T13:00:00Z",
        "CreationTime": "2017-01-11T12:00:00Z",
        "ProjectId": "fb2101bf24bf4*****4cb318787dc",
        "Title": "testtimeline"
    },
    "RequestId": "C43C2876-6263-4B*****2C-CD0F7FCF4FE9"
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


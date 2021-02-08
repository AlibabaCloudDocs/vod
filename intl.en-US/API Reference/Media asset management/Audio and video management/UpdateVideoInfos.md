# UpdateVideoInfos

Modifies the information about multiple videos at a time.

**Note:** The specific parameter of a video is updated only when a new value is passed in the parameter.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=UpdateVideoInfos&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|UpdateVideoInfos|The operation that you want to perform. Set the value to **UpdateVideoInfos**. |
|UpdateContent|String|Yes|\[\{"VideoId":"f45cf4eba5c\*\*\*\*\*b90233389558c39","Title":"Test title"\}\]|The new information about videos. You can modify the information about up to 20 videos at a time. The value is a JSON string. For more information, see the **UpdateContent** section of this topic. |

## UpdateContent

**Note:** You must convert the UpdateContent\[\] parameter to a string before you pass it in.

|Parameter

|Type

|Required

|Description |
|-----------|------|----------|-------------|
|VideoId

|String

|Yes

|The ID of the video. |
|Title

|String

|No

|The title of the video. |
|Description

|String

|No

|The description of the video. |
|Tags

|String

|No

|The tag of the video. |
|CoverURL

|String

|No

|The URL of the video thumbnail. |
|CateId

|Long

|No

|The ID of the category. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|ForbiddenVideoIds|List|f45cf4eba5c84\*\*\*\*\*233389558c36|The IDs of the videos that cannot be modified. Generally, videos cannot be modified if you do not have required [permissions](~~113600~~). |
|NonExistVideoIds|List|f45cf4eba5c84\*\*\*\*\*233389558c36|The IDs of the videos that do not exist. |
|RequestId|String|25818875-5F78-4A\*\*\*\*\*F6-D7393642CA58|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=UpdateVideoInfos
&UpdateContent=[{"VideoId":"f45cf4eba5c*****b90233389558c39","Title":"Test title"}]
&<Common request parameters>
```

Sample success responses

`XML` format

```
<UpdateVideoInfosResponse>
      <RequestId>25818875-5F78-4A*****F6-D7393642CA58</RequestId>
      <NonExistVideoIds>f45cf4eba5c84*****233389558c36</NonExistVideoIds>
      <ForbiddenVideoIds>f45cf4eba5c84*****233389558c36</ForbiddenVideoIds>
</UpdateVideoInfosResponse>
```

`JSON` format

```
{
    "RequestId": "25818875-5F78-4A*****F6-D7393642CA58",
    "NonExistVideoIds":["f45cf4eba5c84*****233389558c36"],
    "ForbiddenVideoIds":["f45cf4eba5c84*****233389558c36"]
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/vod).

## SDK examples

We recommend that you use a [server SDK](~~101789~~) to call this operation. For more information about the sample code that is used to call this operation in various languages, see the following topics:

-   [Java](~~61065#title-mt5-4wo-r30~~)
-   [Python](~~61060#h2--div-id-updatevideoinfos-div-6~~)
-   [PHP](~~61071#h2--div-id-updatevideoinfos-div-6~~)
-   [.NET](~~84752#h2--div-id-updatevideoinfos-div-6~~)
-   [Node.js](~~101419#h2--div-id-updatevideoinfos-div-6~~)
-   [Go](~~101427#h2--div-id-updatevideoinfos-div-6~~)
-   [C/C++](~~101266#h2--div-id-updatevideoinfos-div-6~~)


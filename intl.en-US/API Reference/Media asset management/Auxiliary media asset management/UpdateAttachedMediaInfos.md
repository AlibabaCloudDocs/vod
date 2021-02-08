# UpdateAttachedMediaInfos

Modifies the information about multiple auxiliary media assets at a time.

**Note:** The specific parameter of an auxiliary media asset is updated only when a new value is passed in the parameter.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=UpdateAttachedMediaInfos&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|UpdateAttachedMediaInfos|The operation that you want to perform. Set the value to **UpdateAttachedMediaInfos**. |
|UpdateContent|String|Yes|\[\{"MediaId ":"bbc65bba53f\*\*\*\*\*6ed90de118a7849","Title":"Title","Description":"Description","Tags":"Tag 1,Tag 2"\}\]|The new information about auxiliary media assets. You can modify the information about up to 20 auxiliary media assets at a time. For more information, see the **UpdateContent** section of this topic. |

## UpdateContent

**Note:** You must convert the UpdateContent`[]` parameter to a string before you pass it in.

|Parameter

|Type

|Required

|Description |
|-----------|------|----------|-------------|
|MediaId

|String

|Yes

|The ID of the auxiliary media asset. |
|Title

|String

|No

|The title of the auxiliary media asset. The value can be up to 128 bytes in length. The string must be encoded in the UTF-8 format. |
|Description

|String

|No

|The description of the auxiliary media asset. The value can be up to 1,024 bytes in length. The string must be encoded in the UTF-8 format. |
|Tags

|String

|No

|The tags of the auxiliary media asset. Each tag can be up to 32 bytes in length. A maximum of 16 tags can be specified. Separate multiple tags with commas \(,\). The string must be encoded in the UTF-8 format. |
|CateIds

|String

|No

|The ID of the category. Separate multiple IDs with commas \(,\). |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|NonExistMediaIds|List|\["bbc65bba53f\*\*\*\*\*6ed90de118a7849"\]|The IDs of the auxiliary media assets that do not exist. |
|RequestId|String|25818875-5F78-4\*\*\*\*\*F6-D7393642CA58|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=UpdateAttachedMediaInfos
&UpdateContent=[{"MediaId ":"bbc65bba53f*****6ed90de118a7849","Title":"Title","Description":"Description","Tags":"Tag 1,Tag 2"}]
&<Common request parameters>
```

Sample success responses

`XML` format

```
<UpdateAttachedMediaInfosResponse>
      <RequestId>25818875-5F78-4*****F6-D7393642CA58</RequestId>
      <NonExistMediaIds>bbc65bba53f*****6ed90de118a7849</NonExistMediaIds>
</UpdateAttachedMediaInfosResponse>
```

`JSON` format

```
{
    "RequestId": "25818875-5F78-4*****F6-D7393642CA58",
    "NonExistMediaIds":["bbc65bba53f*****6ed90de118a7849"]
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/vod).


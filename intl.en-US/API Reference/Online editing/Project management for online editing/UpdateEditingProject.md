# UpdateEditingProject

Modifies an online editing project.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=UpdateEditingProject&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|UpdateEditingProject|The operation that you want to perform. Set the value to **UpdateEditingProject**. |
|ProjectId|String|Yes|4ee4b97e27\*\*\*\*\*b525142a6b2|The ID of the online editing project. |
|Title|String|No|testtimeline|The title of the online editing project. |
|Timeline|String|No|\{"VideoTracks":\[\{"VideoTrackClips":\[\{"MediaId":"cc3308ac500c\*\*\*\*\*a54328bc3443"\},\{"MediaId":"da87a9cff64\*\*\*\*\*d88bc6d8326e4"\}\]\}\]\}|The timeline of the online editing project. For more information about the structure, see [Timeline](~~52839~~). |
|Description|String|No|testtimeline001desciption|The description of the online editing project. |
|CoverURL|String|No|https://\*\*\*\*.com/6AB4D0E1E1C7446888\*\*\*\*.png|The thumbnail URL of the online editing project. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|25818875-5F78-4A\*\*\*\*\*F6-D7393642CA58|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=UpdateEditingProject
&ProjectId=4ee4b97e27*****b525142a6b2
&<Common request parameters>
```

Sample success responses

`XML` format

```
<UpdateEditingProjectResponse>
      <RequestId>25818875-5F78-4A*****F6-D7393642CA58</RequestId>
</UpdateEditingProjectResponse>
```

`JSON` format

```
{
    "RequestId": "25818875-5F78-4A*****F6-D7393642CA58"
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


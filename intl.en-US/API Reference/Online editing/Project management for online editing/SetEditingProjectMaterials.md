# SetEditingProjectMaterials

Sets materials to be edited for an online editing project.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=SetEditingProjectMaterials&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SetEditingProjectMaterials|The operation that you want to perform. Set the value to **SetEditingProjectMaterials**. |
|MaterialIds|String|Yes|9e3101bf24bf41c\*\*\*\*\*123318788ca|The ID of the material. A material is a media asset, such as a video, an image, or an auxiliary media asset. Separate multiple material IDs with commas \(,\). |
|ProjectId|String|Yes|fb2101bf24bf4\*\*\*\*\*754cb318787dc|The ID of the online editing project. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|746FFA07-8BBB-46\*\*\*\*\*B1-3E94E3B2915E|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=SetEditingProjectMaterials
&MaterialIds=9e3101bf24bf41c*****123318788ca
&ProjectId=fb2101bf24bf4*****754cb318787dc
&<Common request parameters>
```

Sample success responses

`XML` format

```
<SetEditingProjectMaterialsResponse>
      <RequestId>746FFA07-8BBB-46*****B1-3E94E3B2915E</RequestId>
</SetEditingProjectMaterialsResponse>
```

`JSON` format

```
{
    "RequestId": "746FFA07-8BBB-46*****B1-3E94E3B2915E"
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


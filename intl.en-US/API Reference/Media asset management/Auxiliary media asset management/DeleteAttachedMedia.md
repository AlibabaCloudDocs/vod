# DeleteAttachedMedia

Deletes one or more auxiliary media assets at a time.

**Note:** This operation physically deletes auxiliary media assets. Deleted auxiliary media assets cannot be recovered. Exercise caution when you call this operation.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=DeleteAttachedMedia&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteAttachedMedia|The operation that you want to perform. Set the value to **DeleteAttachedMedia**. |
|MediaIds|String|No|8bc8e94fe4\*\*\*\*\*e55abde85718,eb18618\*\*\*\*\*0e989dd56|The list of auxiliary media asset IDs.

 -   Separate multiple IDs with commas \(,\).
-   A maximum of 20 IDs can be specified. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|NonExistMediaIds|List|\["eb18618\*\*\*\*\*0e989dd56"\]|The ID of the auxiliary media asset that failed to be deleted. |
|RequestId|String|25818875-5F78-4A\*\*\*\*\*F6-D7393642CA58|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=DeleteAttachedMedia
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DeleteAttachedMediaResponse>
      <RequestId>25818875-5F78-4A*****F6-D7393642CA58</RequestId>
      <NonExistMediaIds>eb18618*****0e989dd56</NonExistMediaIds>
</DeleteAttachedMediaResponse>
```

`JSON` format

```
{
    "RequestId": "25818875-5F78-4A*****F6-D7393642CA58",
    "NonExistMediaIds": ["eb18618*****0e989dd56"]
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/vod).


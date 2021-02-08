# DeleteTranscodeTemplateGroup

Removes one or more transcoding templates from a transcoding template group or forcibly deletes the entire transcoding template group.

**Note:**

-   You cannot remove the default transcoding template. You can remove it only after it is no longer specified as the default.
-   For security purposes, you cannot add, modify, or remove transcoding templates in a transcoding template group that is locked in the ApsaraVideo VOD console. To manage such transcoding template groups, contact the ApsaraVideo VOD technical support.
-   You can call the GetTranscodeTemplateGroup operation to query the configurations of a transcoding template group and check whether the transcoding template group is locked by using the response parameter Locked.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=DeleteTranscodeTemplateGroup&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteTranscodeTemplateGroup|The operation that you want to perform. Set the value to **DeleteTranscodeTemplateGroup**. |
|TranscodeTemplateGroupId|String|Yes|4c71a339fec\*\*\*\*\*152b4fa6f4527|The ID of the transcoding template group. |
|TranscodeTemplateIds|String|No|\["613702defdc4\*\*\*\*\*6a3b94cace1129e","bfd6c90253a2\*\*\*\*\*7fc054d7c5825"\]|The IDs of the transcoding templates that you want to remove.

 -   Separate multiple IDs with commas \(,\).
-   You can specify a maximum of 10 IDs. |
|ForceDelGroup|String|No|true|Specifies whether to forcibly delete the entire transcoding template group. Valid values:

 -   **true**: deletes the entire transcoding template group and its transcoding templates.
-   **false**: removes the specified transcoding templates from the transcoding template group. This is the default value. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|NonExistTranscodeTemplateIds|List|\["613702defdc4\*\*\*\*\*6a3b94cace1129e","bfd6c90253a2\*\*\*\*\*7fc054d7c5825"\]|The IDs of transcoding templates that were not found when the system removed transcoding templates based on the IDs. |
|RequestId|String|25818875-5F78-4A\*\*\*\*\*F6-D7393642CA58|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=DeleteTranscodeTemplateGroup
&TranscodeTemplateGroupId=4c71a339fec*****152b4fa6f4527
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DeleteTranscodeTemplateGroupResponse>
      <RequestId>25818875-5F78-4A*****F6-D7393642CA58</RequestId>
      <NonExistTranscodeTemplateIds>613702defdc4*****6a3b94cace1129e</NonExistTranscodeTemplateIds>
      <NonExistTranscodeTemplateIds>bfd6c90253a2*****7fc054d7c5825</NonExistTranscodeTemplateIds>
</DeleteTranscodeTemplateGroupResponse>
```

`JSON` format

```
{
    "RequestId": "25818875-5F78-4A*****F6-D7393642CA58",
    "NonExistTranscodeTemplateIds":["613702defdc4*****6a3b94cace1129e","bfd6c90253a2*****7fc054d7c5825"]
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
|InvalidTranscodeTemplateGroup.NotFound

|The transcode template does not exist.

|404

|The error message returned because the specified transcoding template group does not exist. |
|Forbidden.LockedTemplateGroup

|The transcode template group has been locked.

|403

|The error message returned because the specified template group is locked and cannot be managed. To manage the template group, contact the ApsaraVideo VOD technical support. |
|Forbidden.DefaultTemplateGroup

|The transcode template group is default.

|403

|The error message returned because the specified transcoding template group is the default one that cannot be deleted. |

## SDK examples

We recommend that you use [server SDKs](~~101789~~) to call this operation. You can view the sample code of different languages to call this operation by clicking the following links:

-   [Java](~~61063~~)
-   [Python](~~61054~~)
-   [PHP](~~61069~~)
-   [.NET](~~84750~~)
-   [Node.js](~~101396~~)
-   [Go](~~101411~~)
-   [C/C++](~~101261~~)


# GetVodTemplate

Queries a single snapshot template.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=GetVodTemplate&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GetVodTemplate|The operation that you want to perform. Set the value to **GetVodTemplate**. |
|VodTemplateId|String|Yes|7c49f2f4c0969\*\*\*\*\*fcd446690|The ID of the snapshot template. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|DE7A1F49-41C1-47\*\*\*\*\*DF-4CD0C02087DB|The ID of the request. |
|VodTemplateInfo|Struct| |The information about the snapshot template. |
|CreationTime|String|2018-11-30T08:05:59:57Z|The time when the template was created. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|IsDefault|String|NotDefault|Indicates whether the template is the default one. Valid values:

 -   **Default**: The template is the default one.
-   **NotDefault**: The template is not the default one. |
|ModifyTime|String|2018-11-30T09:05:59:57Z|The time when the template was modified. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|Name|String|test|The name of the template. |
|TemplateConfig|String|\{\\"SnapshotConfig\\":\{\\"Count\\":10,\\"SpecifiedOffsetTime\\":0,\\"Interval\\":1\},\\"SnapshotType\\":\\"NormalSnapshot\\"\}|The detailed configurations of the template. The value is a JSON-formatted string. For more information about the data structure, see the "SnapshotTemplateConfig" section of the [Media processing parameters](~~98618~~) topic. |
|TemplateType|String|Snapshot|The type of the template. Valid values:

 -   **Snapshot**
-   **DynamicImage** |
|VodTemplateId|String|7c49f2f4c09\*\*\*\*\*69fcd446690|The ID of the template. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=GetVodTemplate
&VodTemplateId=7c49f2f4c0969*****fcd446690
&<Common request parameters>
```

Sample success responses

`XML` format

```
<GetVodTemplateResponse>
      <RequestId>DE7A1F49-41C1-47*****DF-4CD0C02087DB</RequestId>
      <VodTemplateInfo>
            <Name>test</Name>
            <TemplateType>Snapshot</TemplateType>
            <Source>Custom</Source>
            <CreationTime>2018-11-30T08:05:59:57Z</CreationTime>
            <VodTemplateId>7c49f2f4c09*****69fcd446690</VodTemplateId>
            <IsDefault>NotDefault</IsDefault>
            <TemplateConfig>{"SnapshotConfig":{"Count":10,"SpecifiedOffsetTime":0,"Interval":1},"SnapshotType":"NormalSnapshot"}</TemplateConfig>
            <ModifyTime>2018-11-30T09:05:59:57Z</ModifyTime>
      </VodTemplateInfo>
</GetVodTemplateResponse>
```

`JSON` format

```
{
    "RequestId": "DE7A1F49-41C1-47*****DF-4CD0C02087DB",
    "VodTemplateInfo": {
        "Name": "test",
        "TemplateType": "Snapshot",
        "Source": "Custom",
        "CreationTime": "2018-11-30T08:05:59:57Z",
        "VodTemplateId": "7c49f2f4c09*****69fcd446690",
        "IsDefault": "NotDefault",
        "TemplateConfig": "{\"SnapshotConfig\":{\"Count\":10,\"SpecifiedOffsetTime\":0,\"Interval\":1},\"SnapshotType\":\"NormalSnapshot\"}",
        "ModifyTime": "2018-11-30T09:05:59:57Z"
    }
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/vod).

## SDK examples

We recommend that you use [server SDKs](~~101789~~) to call this operation. You can view the sample code of different languages to call this operation by clicking the following links:

-   [Java](~~61063~~)
-   [Python](~~61054~~)
-   [PHP](~~61069~~)
-   [.NET](~~84750~~)
-   [Node.js](~~101396~~)
-   [Go](~~101411~~)
-   [C/C++](~~101261~~)


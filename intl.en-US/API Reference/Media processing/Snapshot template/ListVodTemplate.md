# ListVodTemplate

Queries snapshot templates.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=ListVodTemplate&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ListVodTemplate|The operation that you want to perform. Set the value to **ListVodTemplate**. |
|TemplateType|String|Yes|Snapshot|The type of the template. Set the value to **Snapshot**. |
|AppId|String|No|app-\*\*\*\*|The ID of the application. Set the value to **app-1000000**. For more information, see [Overview](~~113600~~). |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|2A56B75B-B7E6-48\*\*\*\*\*27-A9BEAA3E50A8|The ID of the request. |
|VodTemplateInfoList|Array of VodTemplateInfo| |The snapshot templates. |
|AppId|String|app-\*\*\*\*|The ID of the application. |
|CreationTime|String|2018-11-30T08:05:59:57Z|The time when the template was created. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|IsDefault|String|NotDefault|Indicates whether the template is the default one. Valid values:

 -   **Default**: The template is the default one.
-   **NotDefault**: The template is not the default one. |
|ModifyTime|String|2018-11-30T09:05:59:97Z|The time when the template was modified. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|Name|String|test|The name of the template. |
|TemplateConfig|String|\{\\"SnapshotConfig\\":\{\\"Count\\":10,\\"SpecifiedOffsetTime\\":0,\\"Interval\\":1\},\\"SnapshotType\\":\\"NormalSnapshot\\"\}|The detailed configurations of the template. The value is a JSON-formatted string. For more information about the data structure, see the "SnapshotTemplateConfig" section of the [Media processing parameters](~~98618~~) topic. |
|TemplateType|String|Snapshot|The type of the template. Valid values:

 -   **Snapshot**
-   **DynamicImage** |
|VodTemplateId|String|7c49f2f42b1c\*\*\*\*\*0969fcd446690|The ID of the template. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=ListVodTemplate
&TemplateType=Snapshot
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ListVodTemplateResponse>
      <RequestId>2A56B75B-B7E6-48*****27-A9BEAA3E50A8</RequestId>
      <VodTemplateInfoList>
            <CreationTime>2018-11-30T08:05:59:57Z</CreationTime>
            <TemplateType>Snapshot</TemplateType>
            <Name>test</Name>
            <VodTemplateId>7c49f2f42b1c*****0969fcd446690</VodTemplateId>
            <TemplateConfig>{"SnapshotConfig":{"Count":10,"SpecifiedOffsetTime":0,"Interval":1},"SnapshotType":"NormalSnapshot"}</TemplateConfig>
            <IsDefault>NotDefault</IsDefault>
            <ModifyTime>2018-11-30T09:05:59:57Z</ModifyTime>
      </VodTemplateInfoList>
      <VodTemplateInfoList>
            <CreationTime>2018-11-29T09:58:01:20Z</CreationTime>
            <TemplateType>Snapshot</TemplateType>
            <Name>snapshottest</Name>
            <VodTemplateId>ee014fd5889b6*****7828cae2bbb2b</VodTemplateId>
            <TemplateConfig>{"SnapshotConfig":{"Count":10,"SpecifiedOffsetTime":0,"Interval":1},"SnapshotType":"NormalSnapshot"}</TemplateConfig>
            <IsDefault>NotDefault</IsDefault>
            <ModifyTime>2018-11-29T10:58:01:20Z</ModifyTime>
      </VodTemplateInfoList>
</ListVodTemplateResponse>
```

`JSON` format

```
{
    "RequestId": "2A56B75B-B7E6-48*****27-A9BEAA3E50A8",
    "VodTemplateInfoList": [
        {
            "CreationTime": "2018-11-30T08:05:59:57Z",
            "TemplateType": "Snapshot",
            "Name": "test",
            "VodTemplateId": "7c49f2f42b1c*****0969fcd446690",
            "TemplateConfig": "{\"SnapshotConfig\":{\"Count\":10,\"SpecifiedOffsetTime\":0,\"Interval\":1},\"SnapshotType\":\"NormalSnapshot\"}",
            "IsDefault": "NotDefault",
            "ModifyTime": "2018-11-30T09:05:59:57Z"
        },
        {
            "CreationTime": "2018-11-29T09:58:01:20Z",
            "TemplateType": "Snapshot",
            "Name": "snapshottest",
            "VodTemplateId": "ee014fd5889b6*****7828cae2bbb2b",
            "TemplateConfig": "{\"SnapshotConfig\":{\"Count\":10,\"SpecifiedOffsetTime\":0,\"Interval\":1},\"SnapshotType\":\"NormalSnapshot\"}",
            "IsDefault": "NotDefault",
            "ModifyTime": "2018-11-29T10:58:01:20Z"
        }
    ]
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


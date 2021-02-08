# AddVodTemplate

Creates a snapshot template.

**Note:**

-   After you create a snapshot template, you can specify the ID of the snapshot template in the request of the [SubmitSnapshotJob](~~72213~~) operation to take snapshots.
-   You can receive the [SnapshotComplete](~~57337~~) event notification by using an HTTP or HTTPS URL or in Message Service \(MNS\). For more information, see [Overview](~~55627~~).

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=AddVodTemplate&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|AddVodTemplate|The operation that you want to perform. Set the value to **AddVodTemplate**. |
|Name|String|Yes|test|The name of the template.

 -   The name can be up to 128 bytes in length.
-   The value must be encoded in UTF-8. |
|TemplateConfig|String|Yes|\{"SnapshotConfig":\{"Count":10,"SpecifiedOffsetTime":0,"Interval":1\},"SnapshotType":"NormalSnapshot"\}|The configurations of the snapshot template. The value is a JSON-formatted string. For more information about the data structure, see the "SnapshotTemplateConfig" section of the [Media processing parameters](~~98618~~) topic. |
|TemplateType|String|Yes|Snapshot|The type of the template. Set the value to **Snapshot**. |
|AppId|String|No|app-\*\*\*\*|The ID of the application. Default value: **app-1000000**. For more information, see [Overview](~~113600~~). |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|25818875-5F78-4A\*\*\*\*\*F6-D7393642CA58|The ID of the request. |
|VodTemplateId|String|f5b228fe6930e\*\*\*\*\*0d6bf55bd87789|The ID of the snapshot template. You can call the [SubmitSnapshotJob](~~72213~~) operation to take snapshots. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=AddVodTemplate
&Name=test
&TemplateConfig={"SnapshotConfig":{"Count":10,"SpecifiedOffsetTime":0,"Interval":1},"SnapshotType":"NormalSnapshot"}
&TemplateType=Snapshot
&<Common request parameters>
```

Sample success responses

`XML` format

```
<AddVodTemplateResponse>
      <RequestId>25818875-5F78-4A*****F6-D7393642CA58</RequestId>
	  <VodTemplateId>f5b228fe6930e*****0d6bf55bd87789</VodTemplateId>
</AddVodTemplateResponse>
```

`JSON` format

```
{
    "RequestId": "25818875-5F78-4A*****F6-D7393642CA58",
    "VodTemplateId":"f5b228fe6930e*****0d6bf55bd87789"
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


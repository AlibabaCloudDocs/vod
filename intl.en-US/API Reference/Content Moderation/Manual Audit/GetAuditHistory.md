# GetAuditHistory

Queries the manual review history.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=GetAuditHistory&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GetAuditHistory|The operation that you want to perform. Set the value to **GetAuditHistory**. |
|VideoId|String|Yes|93ab850b4f6f44\*\*\*\*\*6e91d24d81d4|The ID of the video. |
|PageNo|Long|No|1|The number of the page to return. Default value: **1**. |
|PageSize|Long|No|10|The number of entries to return on each page. Default value: **10**. Maximum value: **100**. |
|SortBy|String|No|CreationTime:Desc|The sorting rule of the results. Valid values:

 -   **CreationTime:Desc**: sorts the results based on the creation time in descending order. This is the default value.
-   **CreationTime:Asc**: sorts the results based on the creation time in ascending order. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Histories|Array of History| |The review records. |
|Auditor|String|auditor|The reviewer. |
|Comment|String|Contains nudity|The review comments, which are provided by the reviewer. |
|CreationTime|String|2017-01-11T12:00:00Z|The time when the review record was created. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|Reason|String|Pornographic video|The reason why the video failed the review. If the video failed the review, specify the reason. |
|Status|String|Blocked|The manual review result. Valid values:

 -   **Normal**: The video can be played.
-   **Blocked**: The video is blocked. |
|RequestId|String|04F0F334-1335-43\*\*\*\*\*D7-6C044FE73368|The ID of the request. |
|Status|String|Normal|The manual review result. Valid values:

 -   **Normal**: The video can be played.
-   **Blocked**: The video is blocked. |
|Total|Long|2|The total number of review records. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=GetAuditHistory
&VideoId=93ab850b4f6f44*****6e91d24d81d4
&<Common request parameters>
```

Sample success responses

`XML` format

```
<GetAuditHistoryResponse>
      <RequestId>04F0F334-1335-43*****D7-6C044FE73368</RequestId>
	  <Status>Blocked</Status>
	  <Total>2</Total>
	  <Histories>
		    <CreationTime>2017-12-18T07:39:00Z</CreationTime>
		    <Status>Blocked</Status>
		    <Reason>Pornographic video</Reason>
		    <Comment>Contains nudity</Comment>
	  </Histories>
	  <Histories>
		    <CreationTime>2017-12-18T07:30:00Z</CreationTime>
		    <Status>Normal</Status>
		    <Reason></Reason>
		    <Comment></Comment>
	  </Histories>
</GetAuditHistoryResponse>
```

`JSON` format

```
{
    "RequestId": "04F0F334-1335-43*****D7-6C044FE73368",
    "Status": "Blocked",
    "Total":2,
    "Histories":[
        {
            "CreationTime": "2017-12-18T07:39:00Z",
            "Status": "Blocked",
            "Reason": "Pornographic video",
            "Comment": "Contains nudity"
        },
        {
            "CreationTime": "2017-12-18T07:30:00Z",
            "Status": "Normal",
            "Reason": "",
            "Comment": ""
        }
    ]
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


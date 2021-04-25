# ListAuditSecurityIp

Queries the IP addresses in a review security group.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=ListAuditSecurityIp&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ListAuditSecurityIp|The operation that you want to perform. Set the value to **ListAuditSecurityIp**. |
|SecurityGroupName|String|No|Default|The name of the review security group where you want to query IP addresses. If you do not set this parameter, IP addresses in all review security groups are queried. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|664BBD08-C7DB-4E\*\*\*\*\*73-9D0958D9A899|The ID of the request. |
|SecurityIpList|Array of SecurityIp| |The details of the review security group. |
|CreationTime|String|2018-05-22T06:54:23Z|The time when the review security group was created. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|Ips|String|30.27.14.0/24,30.39.127.245|The IP addresses in the review security group. |
|ModificationTime|String|2018-05-22T06:55:14Z|The time when the review security group was last modified. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|SecurityGroupName|String|Default|The name of the review security group. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=ListAuditSecurityIp
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ListAuditSecurityIpResponse>
	  <SecurityGroupList>
		    <SecurityGroupName>Default</SecurityGroupName>
		    <Ips>30.27.14.0/24,30.39.127.245</Ips>
		    <CreationTime>2018-05-22T06:54:23Z</CreationTime>
		    <ModifyTime>2018-05-22T06:55:14Z</ModifyTime>
	  </SecurityGroupList>
	  <RequestId>664BBD08-C7DB-4E*****73-9D0958D9A899</RequestId>
</ListAuditSecurityIpResponse>
```

`JSON` format

```
{
    "SecurityGroupList":[
        {
            "SecurityGroupName":"Default",
            "Ips":"30.27.14.0/24,30.39.127.245",
            "CreationTime":"2018-05-22T06:54:23Z",
            "ModifyTime":"2018-05-22T06:55:14Z"
        }
    ],
    "RequestId":"664BBD08-C7DB-4E*****73-9D0958D9A899"
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
|SecurityIp.NotFound

|The audit security ip does not exist.

|404

|The error message returned because no IP addresses are found in the review security group. |
|ListSecurityIpFailed

|List audit security ip has failed due to some unknown error.

|500

|The error message returned because the IP addresses in the review security group fail to be queried due to an unknown error. Refresh the page and try again. |

## SDK examples

We recommend that you use a [server SDK](~~101789~~) to call this operation. For more information about the sample code that is used to call this operation in various languages, see the following topics:

-   [Java](~~61063~~)
-   [Python](~~61054~~)
-   [PHP](~~61069~~)
-   [.NET](~~84750~~)
-   [Node.js](~~101396~~)
-   [Go](~~101411~~)
-   [C/C++](~~101261~~)


# SetAuditSecurityIp

Manages the IP addresses in review security groups.

**Note:** You can play videos in the Checking or Blocked state only from the IP addresses that are added to review security groups.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=SetAuditSecurityIp&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SetAuditSecurityIp|The operation that you want to perform. Set the value to **SetAuditSecurityIp**. |
|Ips|String|Yes|10.23.12.24|The IP addresses to be added to a review security group. You can add a maximum of 100 IP addresses to each review security group. Separate multiple IP addresses with commas \(,\). You can enter individual IP addresses or a CIDR block.

 -   Individual IP address: for example, 10.23.12.24
-   CIDR block: for example, 10.23.12.24/24, where /24 indicates that the prefix of the CIDR block is 24 bits in length. You can replace 24 with a value that ranges from `1 to 32`. |
|SecurityGroupName|String|No|Default|The name of the review security group. Default value: **Default**. You can specify a maximum of 10 review security groups. |
|OperateMode|String|No|Cover|The operation type. Valid values:

 -   **Append**: adds the IP addresses to the original whitelist. This is the default value.
-   **Cover**: overwrites the original whitelist.
-   **Delete**: removes the IP addresses from the original whitelist. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|25818875-5F78-4\*\*\*\*\*F6-D7393642CA58|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=SetAuditSecurityIp
&Ips=10.23.12.24
&<Common request parameters>
```

Sample success responses

`XML` format

```
<SetAuditSecurityIpResponse>
      <RequestId>25818875-5F78-4*****F6-D7393642CA58</RequestId>
</SetAuditSecurityIpResponse>
```

`JSON` format

```
{
    "RequestId": "25818875-5F78-4*****F6-D7393642CA58"
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
|IpsIsEmpty

|The specified "Ips" can not be empty.

|400

|The error message returned because the Ips parameter is not specified. |
|IpsExceededMax

|The specified Ips count has exceeded 100.

|403

|The error message returned because more than 100 IP addresses are added to a review security group. |
|SecurityIpGroupExceededMax

|The audit security group count has exceeded 10.

|403

|The error message returned because the number of review security groups exceeds the upper limit. |

## SDK examples

We recommend that you use a [server SDK](~~101789~~) to call this operation. For more information about the sample code that is used to call this operation in various languages, see the following topics:

-   [Java](~~61063~~)
-   [Python](~~61054~~)
-   [PHP](~~61069~~)
-   [.NET](~~84750~~)
-   [Node.js](~~101396~~)
-   [Go](~~101411~~)
-   [C/C++](~~101261~~)


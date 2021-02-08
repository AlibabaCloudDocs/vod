# DescribeVodUserDomains

Queries the domain names for CDN within your Alibaba Cloud account. You can filter domain names by name or by state. When you filter domain names by name, a fuzzy match is supported.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=DescribeVodUserDomains&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeVodUserDomains|The operation that you want to perform. Set the value to **DescribeVodUserDomains**. |
|PageSize|Integer|No|20|The number of entries to return on each page. Default value: **20**. Maximum value: **50**. Valid values: integers in the range of **1** to **50**. |
|PageNumber|Integer|No|1|The number of the page to return. |
|DomainName|String|No|Parameters.DomainName.example|The domain name. The value of this parameter is used as a filter condition for a fuzzy match. |
|DomainStatus|String|No|online|The status of the domain name. The value of this parameter is used as a condition to filter domain names. Value values:

 -   **online**: indicates that the domain name is enabled.
-   **offline**: indicates that the domain name is disabled.
-   **configuring**: indicates that the domain name is being configured.
-   **configure\_failed**: indicates that the domain name failed to be configured.
-   **checking**: indicates that the domain name is under review.
-   **check\_failed**: indicates that the domain name failed the review. |
|DomainSearchType|String|No|fuzzy\_match|The search method. Valid values:

 -   **fuzzy\_match**: fuzzy match. This is the default value.
-   **pre\_match**: prefix match.
-   **suf\_match**: suffix match.
-   **full\_match**: exact match. |
|Tag.N.Key|String|No|key|The key of tag N. Valid values of N: **1** to **20**.

 If you do not specify this parameter, all tag keys are queried. |
|Tag.N.Value|String|No|value|The value of tag N. Valid values of N: **1** to **20**.

 If you do not specify this parameter, all tag values are queried. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Domains|Array of PageData| |The detailed information about each domain name for CDN. The returned information is displayed in the format that is specified by the PageData parameter. |
|PageData| | | |
|Cname|String|api1.example.com.w.alikunlun.net|The canonical domain name that is assigned to the domain name for CDN. |
|Description|String|Zhejiang ICP Filing No. \*\*\*\*|The remarks. |
|DomainName|String|api1.example.com|The domain name for CDN. |
|DomainStatus|String|online|The status of the domain name for CDN. Valid values:

 -   **online**: indicates that the domain name is enabled.
-   **offline**: indicates that the domain name is disabled.
-   **configuring**: indicates that the domain name is being configured.
-   **configure\_failed**: indicates that the domain name failed to be configured.
-   **checking**: indicates that the domain name is under review.
-   **check\_failed**: indicates that the domain name failed the review. |
|GmtCreated|String|2017-08-29T08:40:53Z|The time when the domain name for CDN was added. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|GmtModified|String|2017-12-29T09:24:12Z|The last time when the domain name for CDN was modified. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|Sandbox|String|normal|Indicates whether the domain name for CDN is in a sandbox environment. |
|Sources|Array of Source| |The information about the origin server. |
|Source| | | |
|Content|String|1.1.1.1|The address of the origin server. |
|Port|Integer|80|The port number. Valid values: **443** and **80**. |
|Priority|String|5|The priority of the origin server. |
|Type|String|oss|The type of the origin server. Valid values:

 -   **ipaddr**: a server that you can access by using an IP address.
-   **domain**: a server that you can access by using a domain name.
-   **oss**: an Object Storage Service \(OSS\) bucket. |
|SslProtocol|String|on|Indicates whether HTTPS is enabled.

 -   **on**: indicates that HTTPS is enabled.
-   **off**: indicates that HTTPS is disabled. |
|PageNumber|Long|1|The page number of the returned page. |
|PageSize|Long|100|The number of entries returned per page. |
|RequestId|String|E4EBD2BF-5EB0-4476-\*\*\*\*-9D94E1B15267|The ID of the request. |
|TotalCount|Long|2|The total number of entries returned. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=DescribeVodUserDomains
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeVodUserDomainsResponse>
	  <Domains>
		    <PageData>
			      <SslProtocol>on</SslProtocol>
			      <Description>Zhejiang ICP Filing No. ****</Description>
			      <DomainName>api1.example.com</DomainName>
			      <GmtModified>2017-12-29T09:24:12Z</GmtModified>
			      <GmtCreated>2017-08-29T08:40:53Z</GmtCreated>
			      <Cname>api1.example.com.w.alikunlun.net</Cname>
			      <Weight>10</Weight>
			      <DomainStatus>online</DomainStatus>
			      <Sandbox>normal</Sandbox>
		    </PageData>
		    <PageData>
			      <Sources>
				        <Source>
					          <Type>oss</Type>
					          <Priority>5</Priority>
					          <Content>1.1.1.1</Content>
					          <Port>80</Port>
				        </Source>
			      </Sources>
		    </PageData>
	  </Domains>
	  <TotalCount>2</TotalCount>
	  <PageSize>100</PageSize>
	  <RequestId>E4EBD2BF-5EB0-4476-****-9D94E1B15267</RequestId>
	  <PageNumber>1</PageNumber>
</DescribeVodUserDomainsResponse>
```

`JSON` format

```
{
	"Domains": {
		"PageData": [{
			"SslProtocol": "on",
			"Description": "Zhejiang ICP Filing No. ****",
			"DomainName": "api1.example.com",
			"GmtModified": "2017-12-29T09:24:12Z",
			"GmtCreated": "2017-08-29T08:40:53Z",
			"Cname": "api1.example.com.w.alikunlun.net",
			"Weight": "10",
			"DomainStatus": "online",
			"Sandbox": "normal"
		}, {
			"Sources": {
				"Source": [{
					"Type": "oss",
					"Priority": "5",
					"Content": "1.1.1.1",
					"Port": "80"
				}]
			}
		}]
	},
	"TotalCount": "2",
	"PageSize": "100",
	"RequestId": "E4EBD2BF-5EB0-4476-****-9D94E1B15267",
	"PageNumber": "1"
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
|InvalidPageNumber.ValueNotSupported

|The specified value of parameter PageNumber is not supported.

|400

|The error message returned because the value of the PageNumber parameter is invalid. |
|InvalidPageSize.ValueNotSupported

|The specified value of parameter PageSize is not supported.

|400

|The error message returned because the value of the PageSize parameter is invalid. |
|InvalidDomainName.Malformed

|The specific value of parameter DomainName is malformed.

|400

|The error message returned because the value of the DomainName parameter is invalid. |
|InvalidDomainStatus.ValueNotSupported

|The specified value of parameter DomainStatus is not supported.

|400

|The error message returned because the value of the DomainStatus parameter is invalid. |
|InvalidDomainSearchType.ValueNotSupported

|The specified value of parameter DomainSearchType is not supported.

|400

|The error message returned because the value of the DomainSearchType parameter is invalid. |


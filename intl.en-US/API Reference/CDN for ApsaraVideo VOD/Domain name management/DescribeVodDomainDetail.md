# DescribeVodDomainDetail

Queries the basic information about a specified domain name for CDN.

**Note:** This operation is available only in the **China \(Shanghai\)** region.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=DescribeVodDomainDetail&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeVodDomainDetail|The operation that you want to perform. Set the value to **DescribeVodDomainDetail**. |
|DomainName|String|Yes|example.com|The domain name for CDN. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|DomainDetail|Struct| |The basic information about the domain name for CDN. |
|CertName|String|\*\*\*\*|The name of the certificate. The value of this parameter is returned if HTTPS is enabled. |
|Cname|String|www.example.com.alikunlun.net|The canonical domain name that is assigned to the domain name for CDN. You must add the CNAME record at your DNS service provider to map the domain name for CDN to the canonical domain name. |
|Description|String|\*\*\*\*|The description of the domain name for CDN. |
|DomainName|String|www.example.com|The domain name for CDN. |
|DomainStatus|String|online|The status of the domain name for CDN. Value values:

 -   **online**: indicates that the domain name is enabled.
-   **offline**: indicates that the domain name is disabled.
-   **configuring**: indicates that the domain name is being configured.
-   **configure\_failed**: indicates that the domain name failed to be configured.
-   **checking**: indicates that the domain name is under review.
-   **check\_failed**: indicates that the domain name failed the review. |
|GmtCreated|String|2017-11-27T06:51:26Z|The time when the domain name for CDN was added. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|GmtModified|String|2017-11-27T06:55:26Z|The last time when the domain name for CDN was modified. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|SSLProtocol|String|on|Indicates whether the Secure Sockets Layer \(SSL\) certificate is enabled. Valid values:

 -   **on**: indicates that the SSL certificate is enabled.
-   **off**: indicates that the SSL certificate is disabled. |
|SSLPub|String|\*\*\*\*|The public key of the certificate. The value of this parameter is returned if HTTPS is enabled. |
|Scope|String|domestic|This parameter is applicable to users of level 3 or higher in mainland China and users outside mainland China. Valid values:

 -   **domestic**: mainland China. This is the default value.
-   **overseas**: outside mainland China.
-   **global**: regions in and outside mainland China. |
|Sources|Array of Source| |The information about the origin server. |
|Source| | | |
|Content|String|\*\*\*\*.oss-cn-hangzhou.aliyuncs.com|The address of the origin server. |
|Enabled|String|online|The status of the origin server. Valid values:

 -   **online**: indicates that the origin server is enabled.
-   **offline**: indicates that the origin server is disabled. |
|Port|Integer|80|The port number. Valid values: 443 and 80. |
|Priority|String|50|The priority of the origin server. |
|Type|String|oss|The type of the origin server. Valid values:

 -   **ipaddr**: a server that you can access by using an IP address.
-   **domain**: a server that you can access by using a domain name.
-   **oss**: an Object Storage Service \(OSS\) bucket. |
|Weight|String|1|The weight of the origin server. |
|RequestId|String|09ABE829-6CD3-4FE0-\*\*\*\*-556113E29727|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=DescribeVodDomainDetail
&DomainName=example.com
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeVodDomainDetailResponse>
	  <RequestId>09ABE829-6CD3-4FE0-****-556113E29727</RequestId>
	  <DomainDetail>
		    <Cname>www.example.com.alikunlun.net</Cname>
		    <DomainStatus>online</DomainStatus>
		    <DomainName>www.example.com</DomainName>
		    <Sources>
			      <Source>
				        <Enabled>online</Enabled>
				        <Port>80</Port>
				        <Type>oss</Type>
				        <Content>****.oss-cn-hangzhou.aliyuncs.com</Content>
				        <Priority>50</Priority>
			      </Source>
		    </Sources>
		    <GmtModified>2017-11-27T06:55:26Z</GmtModified>
		    <GmtCreated>2017-11-27T06:51:25Z</GmtCreated>
	  </DomainDetail>
</DescribeVodDomainDetailResponse>
```

`JSON` format

```
{
  "RequestId": "09ABE829-6CD3-4FE0-****-556113E29727",
  "DomainDetail": {
    "Cname": "www.example.com.alikunlun.net",
    "DomainStatus": "online",
    "DomainName": "www.example.com",
    "Sources": {
      "Source": [
        {
          "Enabled": "online",
          "Port": 80,
          "Type": "oss",
          "Content": "****.oss-cn-hangzhou.aliyuncs.com",
          "Priority": "50"
        }
      ]
    },
    "GmtModified": "2017-11-27T06:55:26Z",
    "GmtCreated": "2017-11-27T06:51:25Z"
  }
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/vod).

The following table describes the common errors that this operation can return. For more information about errors common to all operations, see [Common errors](https://help.aliyun.com/document_detail/52841.html?spm=a2c4g.11186623.2.17.72657c55cS5tmj).

|Error code

|Error message

|HTTP status code

|Description |
|------------|---------------|------------------|-------------|
|InvalidDomain.NotFound

|The domain provided does not belong to you.

|404

|The error message returned because the domain name does not exist or does not belong to you.

| |
|ServiceBusy

|The specified Domain is configuring, please retry again later.

|403

|The error message returned because the domain name is being configured. Try again later.

| |


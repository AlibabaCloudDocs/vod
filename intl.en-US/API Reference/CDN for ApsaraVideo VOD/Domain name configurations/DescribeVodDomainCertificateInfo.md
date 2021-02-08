# DescribeVodDomainCertificateInfo

Queries the certificate information about a specific domain name for CDN.

**Note:** This operation is available only in the **China \(Shanghai\)** region.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=DescribeVodDomainCertificateInfo&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeVodDomainCertificateInfo|The operation that you want to perform. Set the value to **DescribeVodDomainCertificateInfo**. |
|DomainName|String|Yes|example.com|The domain name for CDN. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|CertInfos|Array of CertInfo| |The certificate information. |
|CertInfo| | | |
|CertDomainName|String|example.com|The domain name that matches the certificate. |
|CertExpireTime|String|2018-06-03T13:03:39Z|The time when the certificate expires. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|CertLife|String|3 months|The validity period of the certificate. Unit: month or year. |
|CertName|String|cert-example.com|The name of the certificate. |
|CertOrg|String|Let's Encrypt|The certificate authority \(CA\) that issued the certificate. |
|CertType|String|free|The type of the certificate. Valid values:

 -   **free**: a free certificate.
-   **cas**: a certificate that is purchased from Alibaba Cloud SSL Certificates Service.
-   **upload**: a user-uploaded certificate. |
|DomainName|String|example.com|The domain name for CDN. |
|ServerCertificateStatus|String|checking|The status of the server certificate.

 -   **success**: indicates that the certificate has taken effect.
-   **checking**: indicates that the system is checking whether the domain name has been added to ApsaraVideo VOD.
-   **cname\_error**: indicates that the domain name has not been added to ApsaraVideo VOD.
-   **domain\_invalid**: indicates that the domain name contains invalid characters.
-   **unsupport\_wildcard**: indicates that wildcard domain names are not supported.
-   **applying**: indicates that the certificate is in the application process.
-   **failed**: indicates that the request of applying for the certificate has failed. |
|Status|String|success|The status of the certificate.

 -   **success**: indicates that the certificate has taken effect.
-   **checking**: indicates that the system is checking whether the domain name has been added to ApsaraVideo VOD.
-   **cname\_error**: indicates that the domain name has not been added to ApsaraVideo VOD.
-   **domain\_invalid**: indicates that the domain name contains invalid characters.
-   **unsupport\_wildcard**: indicates that wildcard domain names are not supported.
-   **applying**: indicates that the certificate is in the application process.
-   **failed**: indicates that the request of applying for the certificate has failed. |
|RequestId|String|5C1E43DC-9E51-4771-\*\*\*\*-7D5ECEB547A1|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=DescribeVodDomainCertificateInfo
&DomainName=example.com
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeVodDomainCertificateInfoResponse>
      <CertInfos>
		    <CertInfo>
			      <Status>success</Status>
			      <CertLife>3 months</CertLife>
			      <SSLProtocol>on</SSLProtocol>
			      <CertType>cas</CertType>
			      <CertName>cert-example.com</CertName>
			      <CertDomainName>example.com</CertDomainName>
			      <DomainName>example.com</DomainName>
			      <CertOrg>Let's Encrypt</CertOrg>
			      <CertExpireTime>2018-06-03T13:03:39Z</CertExpireTime>
		    </CertInfo>
	  </CertInfos>
	  <RequestId>5C1E43DC-9E51-4771-****-7D5ECEB547A1</RequestId>
</DescribeVodDomainCertificateInfoResponse>
```

`JSON` format

```
{
  "CertInfos": {
    "CertInfo": [
      {
        "Status": "success",
        "CertLife": "3 months",
        "SSLProtocol": "on",
        "CertType": "cas",
        "CertName": "cert-example.com",
        "CertDomainName": "example.com",
        "DomainName": "example.com",
        "CertOrg": "Let's Encrypt",
        "CertExpireTime": "2018-06-03T13:03:39Z"
      }
    ]
  },
  "RequestId": "5C1E43DC-9E51-4771-****-7D5ECEB547A1"
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
|InvalidDomain.NotFound

|The domain provided does not belong to you.

|404

|The error message returned because the domain name does not exist or does not belong to you. |


# DescribeVodCertificateList

Queries the certificates of a specified domain name for CDN or all the domain names for CDN within your Alibaba Cloud account.

**Note:** This operation is available only in the **China \(Shanghai\)** region.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=DescribeVodCertificateList&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeVodCertificateList|The operation that you want to perform. Set the value to **DescribeVodCertificateList**. |
|DomainName|String|No|example.com|The domain name for CDN. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|CertificateListModel|Struct| |The information about the returned certificates. |
|CertList|Array of Cert| |The details of each certificate. |
|Cert| | | |
|CertId|Long|235437|The ID of the certificate. |
|CertName|String|Certificate|The name of the certificate. |
|Common|String|test|The common name of the certificate. |
|Fingerprint|String|\*\*\*\*|The fingerprint of the certificate. |
|Issuer|String|\*\*\*\*|The certificate authority \(CA\) that issued the certificate. |
|LastTime|Long|1512388610|The time when the certificate was issued. Unit: seconds. |
|Count|Integer|2|The number of certificates. |
|RequestId|String|FC0E34AC-0239-44A7-\*\*\*\*-800DE522C8DA|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=DescribeVodCertificateList
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeVodCertificateListResponse>
  <RequestId>FC0E34AC-0239-44A7-****-800DE522C8DA</RequestId>
  <CertificateListModel>
        <CertList>
              <Cert>
                    <Fingerprint>****</Fingerprint>
                    <Issuer>****</Issuer>
                    <CertId>235437</CertId>
                    <CertName>Certificate</CertName>
                    <LastTime>1512388610</LastTime>
                    <Common>test</Common>
              </Cert>
        </CertList>
        <Count>2</Count>
  </CertificateListModel>
</DescribeVodCertificateListResponse>
```

`JSON` format

```
{
	"RequestId": "FC0E34AC-0239-44A7-****-800DE522C8DA",
	"CertificateListModel": {
		"CertList": {
			"Cert": [{
				"Fingerprint": "****",
				"Issuer": "****",
				"CertId": "235437",
				"CertName": "Certificate",
				"LastTime": "1512388610",
				"Common": "test"
			}]
		},
		"Count": "2"
	}
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/vod).


# SetVodDomainCertificate

Enables or disables the Secure Sockets Layer \(SSL\) certificate for a specified domain name for CDN. When you call this operation to enable the SSL certificate, you can also modify the certificate information.

**Note:** This operation is available only in the **China \(Shanghai\)** region.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=SetVodDomainCertificate&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SetVodDomainCertificate|The operation that you want to perform. Set the value to **SetVodDomainCertificate**. |
|DomainName|String|Yes|example.com|The domain name that is secured by the certificate. The domain name uses HTTPS acceleration. |
|SSLProtocol|String|Yes|off|Specifies whether to enable the SSL certificate. Valid values:

 -   **on**: enables the SSL certificate.
-   **off**: disables the SSL certificate. Default value: off. |
|CertName|String|No|cert\_name|The name of the certificate. |
|SSLPub|String|No|\*\*\*\*|The content of the certificate. This parameter is required only if you enable the SSL certificate. |
|SSLPri|String|No|\*\*\*\*|The private key. This parameter is required only if you enable the SSL certificate. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|04F0F334-1335-436C-\*\*\*\*-6C044FE73368|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=SetVodDomainCertificate
&DomainName=example.com
&SSLProtocol=off
&<Common request parameters>
```

Sample success responses

`XML` format

```
<SetVodDomainCertificateResponse>
      <RequestId>04F0F334-1335-436C-****-6C044FE73368</RequestId>
</SetVodDomainCertificateResponse>
```

`JSON` format

```
{
    "RequestId": "04F0F334-1335-436C-****-6C044FE73368"
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
|IllegalOperation

|Illegal domain operate is not permitted.

|403

|The error message returned because you are not authorized to perform this operation. |
|ServiceBusy

|The specified Domain is configuring, please retry later.

|403

|The error message returned because the domain name is being configured. Try again later. |
|InvalidDomain.Offline

|The domain provided is offline.

|400

|The error message returned because the domain name has been disabled. |
|OperationDenied

|Your CDN service is suspended.

|403

|The error message returned because your Alibaba Cloud account has overdue payments. Add funds to your account. |
|InvalidSSLProtocol.ValueNotSupported

|The specified value of parameter Enable is not supported.

|400

|The error message returned because the value of the SSLProtocol parameter is invalid. |
|SSLPub.MissingParameter

|An input parameter SSLPub that is mandatory for processing the request is not supplied.

|400

|The error message returned because the SSLPub parameter is not specified. |
|SSLPri.MissingParameter

|An input parameter SSLPri that is mandatory for processing the request is not supplied.

|400

|The error message returned because the SSLPri parameter is not specified. |
|InvalidCertificate

|The Certificate you provided is malformed!

|400

|The error message returned because the certificate content is invalid. |
|InvalidSSLPri

|The SSLPri you provided is malformed!

|400

|The error message returned because the private key is invalid. |
|Certificate.MissMatch

|The SSLPri does not math the specified Certificate!

|400

|The error message returned because the certificate content and private key do not match. |
|InvalidCertificate.TooLong

|The Certificate you provided is over the max length!

|400

|The error message returned because the length of the certificate content exceeds the upper limit. |
|InvalidCertName.TooLong

|The Certificate name you provided is over the max length 128!

|400

|The error message returned because the certificate name contains more than 128 characters. |
|SetDomainSSLPub.ParameterError

|Parameters have error.

|400

|The error message returned because one or more parameters are invalid. |
|Certificate.StatusError

|Certificate is not exist or its status is error.

|400

|The error message returned because the certificate does not exist or the certificate is in an invalid state. |
|DeleteFailed

|Delete certificate is failed.

|400

|The error message returned because the system failed to delete the certificate. |
|Certificate.NotFind

|Not find the certificate info.

|400

|The error message returned because the certificate was not found. |
|Certificate.Duplicated

|The certificate name is duplicated.

|400

|The error message returned because the certificate name already exists. |
|Certificate.FormatError

|The certificate format is error.

|400

|The error message returned because the format of the certificate is invalid. |
|Certificate.StatusError

|The certificate status is error.

|400

|The error message returned because the certificate is in an invalid state. |
|Certificate.KeyNull

|The SSLPri is not null.

|400

|The error message returned because the private key is not specified. |
|SSLPri.Malformed

|The SSLPri format is error.

|400

|The error message returned because the format of the private key is invalid. |
|Certificate.NotPermittedOff

|Turn off certificate will change domain scheduling, please contact customer service.

|400

|The error message returned because disabling the certificate may affect the scheduling of the domain name. Contact Customer Service. |
|Certificate.SettedNotEffect

|Certificate was successfully setted but does’t take effect for protecting current service, please contact customer service.

|400

|The error message returned because the certificate is configured but temporarily disabled to protect your service. To enable the certificate, contact Customer Service. |


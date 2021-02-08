# BatchSetVodDomainConfigs

Configures one or more domain names for CDN.

**Note:** This operation is available only in the **China \(Shanghai\)** region.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=BatchSetVodDomainConfigs&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|BatchSetVodDomainConfigs|The operation that you want to perform. Set the value to **BatchSetVodDomainConfigs**. |
|DomainNames|String|Yes|example.com|The domain name for CDN. Separate multiple domain names with commas \(,\). |
|Functions|String|Yes|\[\{"functionArgs":\[\{"argName":"domain\_name","argValue":"www.example.com"\}\],"functionName":"set\_req\_host\_header"\}\]|The features to configure.

 -   Set this parameter in the following format: `[{"functionArgs":[{"argName":"domain_name","argValue":"www.example.com"}],"functionName":"set_req_host_header"}]`.
-   Specific features, such as filetype\_based\_ttl\_set, support more than one configuration record. To update one of the configuration records, use the configId field to specify the record. `[{"functionArgs":[{"argName":"file_type","argValue":"jpg"},{"argName":"ttl","argValue":"18"},{"argName":"weight","argValue":"30"}],"functionName":"filetype_based_ttl_set","configId":5068995}]`
-   For more information, see the **Feature description** section. |

## Feature description

All parameter values are of the string type.

|Feature

|Description

|Parameter |
|---------|-------------|-----------|
|referer\_white\_list\_set

|Specifies the referer whitelist.

|refer\_domain\_allow\_list: the referers to be added to the whitelist. Separate multiple referers with commas \(,\).

 allow\_empty: specifies whether an empty referer is allowed. Valid values: **on and off**. |
|referer\_black\_list\_set

|Specifies the referer blacklist.

|refer\_domain\_deny\_list: the referers to be added to the blacklist. Separate multiple referers with commas \(,\).

 allow\_empty: specifies whether an empty referer is allowed. Valid values: **on and off**. |
|filetype\_based\_ttl\_set

|Specifies the time period after which a file expires.

|ttl: the expiration time of the cached content. Unit: seconds.

 file\_type: the file type. Separate multiple file types with commas \(,\). Example: txt,jpg.

 weight: the weight of the file in the cache. Valid values: **1** to **199**. |
|path\_based\_ttl\_set

|Specifies the time period after which a directory expires.

|ttl: the expiration time of the cached content. Unit: seconds.

 path: the directory, which must start with a forward slash \(/\).

 weight: the weight of the directory in the cache. Valid values: **1** to **99**. |
|oss\_auth

|Configures authentication for the access to an Object Storage Service \(OSS\) bucket.

|oss\_bucket\_id: the ID of the bucket. |
|ip\_black\_list\_set

|Specifies the IP address blacklist.

|ip\_list: the IP addresses to be added to the whitelist. Separate multiple IP addresses with commas \(,\). |
|ip\_allow\_list\_set

|Specifies the IP address whitelist.

|ip\_list: the IP addresses to be added to the whitelist. Separate multiple IP addresses with commas \(,\). |
|ip\_white\_list\_set

|Specifies the Taobao Missile Defense \(TMD\) whitelist.

|ip\_list: the IP addresses to be added to the whitelist. Separate multiple IP addresses with commas \(,\). |
|error\_page

|Redirects an error page to a specified page.

|error\_code: the error code.

 rewrite\_page: the page to which the error page is redirected. |
|set\_req\_host\_header

|Modifies the custom header of back-to-origin requests.

|domain\_name: the custom host header of back-to-origin requests. |
|set\_hashkey\_args

|Ignores the specified URL parameters.

|hashkey\_args: the parameters to be reserved. Separate multiple parameters with commas \(,\).

 disable: specifies whether to ignore all parameters. A value of on indicates that all parameters are ignored. A value of off indicates that none of the parameters are ignored. |
|aliauth

|Configures Alibaba Cloud authentication.

|auth\_type: the authentication type. Valid values: **no\_auth**, **type\_a**, **type\_b**, and **type\_c**.

 auth\_key1: the primary authentication key.

 auth\_key2: the secondary authentication key.

 ali\_auth\_delta: the custom buffer time for authentication.

 ali\_auth\_remote\_desc: the pattern matching string. |
|set\_resp\_header

|Specifies a response header. To verify the setting, you can check the response message in a browser.

|key: the name of the response header. Valid values: **Content-Type**, **Cache-Control**, **Content-Disposition**, **Content-Language**, **Expires**, **Access-Control-Allow-Origin**, **Access-Control-Allow-Methods**, **Access-Control-Allow-Headers**, **Access-Control-Max-Age**, and **Access-Control-Expose-Headers**.

 value: the content of the response header. If you want to delete the header, enter null. |
|https\_force

|Configures force redirect to HTTPS.

|enable: specifies whether to enable force redirect to HTTPS. Valid values: **on and off**. |
|http\_force

|Configures force redirect to HTTP.

|enable: specifies whether to enable force redirect to HTTP. Valid values: **on and off**. |
|l2\_oss\_key

|Configures private key authentication for back-to-origin requests from L2 nodes to private OSS buckets.

|private\_oss\_auth: specifies whether to authenticate the access to a private OSS bucket. Valid values: **on and off**. |
|green\_manager

|Configures pornography detection.

|enable: specifies whether to enable pornography detection. Valid values: **on and off**. |
|range

|Configures object chunking.

|enable: specifies whether to enable object chunking. Valid values: on, off, and force. |
|video\_seek

|Configures video seeking.

|enable: specifies whether to enable video seeking. Valid values: on and off. |
|set\_hashkey\_args

|Ignores the specified URL parameters.

|hashkey\_args: the parameters to be reserved. Separate multiple parameters with commas \(,\).

 disable: specifies whether to ignore all parameters. A value of on indicates that all parameters are ignored. A value of off indicates that none of the parameters are ignored. |
|tmd\_signature

|Specifies TMD rules.

|name: the name of the rule, which must be unique in the domain name.

 path: the URI path. You can specify duplicate URI paths. However, you must verify their validity.

 pathType: the matching rule. Valid values: 0 and 1. A value of **0** indicates a prefix match. A value of **1** indicates an exact match.

 interval: the interval at which data is monitored. Unit: seconds. The interval must be greater than or equal to **10** seconds.

 count: the number of visits from an IP address.

 action: the operation to be performed after the specified conditions are met. Valid values: 0 and 1. A value of **0** indicates blocking. A value of **1** indicates bot detection.

 ttl: the time period during which access is blocked. Unit: seconds. |
|ali\_business

|Configures custom features.

|ali\_business\_type: required. The business type.

 ali\_business\_table: the pattern matching string. |
|hls\_token\_rewrite

|Configures M3U8 encryption and rewriting.

|enable: required. Specifies whether to enable M3U8 encryption and rewriting. Valid values: on and off.

 hls\_token\_arg\_name: the name of the appended parameter. If you do not specify the name, the parameter name MtsHlsUriToken is used. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|04F0F334-1335-436C-\*\*\*\*-6C044FE73368|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=BatchSetVodDomainConfigs
&DomainNames=example.com
&Functions=[{"functionArgs":[{"argName":"domain_name","argValue":"www.example.com"}],"functionName":"set_req_host_header"}]
&<Common request parameters>
```

Sample success responses

`XML` format

```
<BatchSetVodDomainConfigsResponse>
  <RequestId>04F0F334-1335-436C-****-6C044FE73368</RequestId>
</BatchSetVodDomainConfigsResponse>
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
|InvalidFunctions.Malformed

|Specified Functions is malformed.

|400

|The error message returned because the value of the Functions parameter is invalid. |
|InvalidFunctionName.ValueNotSupported

|FunctionName %s is not supported.

|400

|The error message returned because the %s feature name is invalid. |
|InvalidArgName.ValueNotSupported

|ArgName %s is not supported.

|400

|The error message returned because the %s parameter is invalid. |
|InvalidArgValue.Malformed

|Specified ArgValue is malformed.

|400

|The error message returned because the value of the argValue field is invalid. |


# DescribeVodDomainConfigs

Queries the configurations of a specified domain name for CDN. You can query the configurations of one or more features at a time.

**Note:** This operation is available only in the **China \(Shanghai\)** region.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=DescribeVodDomainConfigs&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeVodDomainConfigs|The operation that you want to perform. Set the value to **DescribeVodDomainConfigs**. |
|DomainName|String|Yes|www.example.com|The domain name for CDN. |
|FunctionNames|String|Yes|filetype\_based\_ttl\_set,set\_req\_host\_header|The name of the feature. Separate multiple names with commas \(,\). For more information, see the **Feature description** section. |

## Feature description

|Feature

|Description |
|---------|-------------|
|referer\_white\_list\_set

|Specifies the referer whitelist. |
|referer\_black\_list\_set

|Specifies the referer blacklist. |
|filetype\_based\_ttl\_set

|Specifies the time period after which a file expires. |
|path\_based\_ttl\_set

|Specifies the time period after which a directory expires. |
|cc\_defense

|Configures protection against HTTP flood attacks. |
|oss\_auth

|Configures authentication for the access to an Object Storage Service \(OSS\) bucket. |
|ip\_black\_list\_set

|Specifies the IP address blacklist. |
|ip\_white\_list\_set

|Specifies the IP address whitelist. |
|error\_page

|Redirects an error page to a specified page. |
|tesla

|Optimizes pages to accelerate access. |
|set\_req\_host\_header

|Modifies the custom header of back-to-origin requests. |
|set\_hashkey\_args

|Ignores the specified URL parameters. |
|aliauth

|Configures Alibaba Cloud authentication. |
|set\_resp\_header

|Specifies a response header. To verify the setting, you can check the response message in a browser. |
|video\_seek

|Configures video seeking. |
|range

|Configures object chunking. |
|gzip

|Optimizes pages by using GNU zip \(Gzip\) compression. |
|https\_force

|Configures force redirect to HTTPS. |
|http\_force

|Configures force redirect to HTTP. |
|alivod

|Configures ApsaraVideo VOD. |
|forward\_scheme

|Specifies the origin protocol policy or configures whether to enable adaptive origin fetch. |
|tmd\_signature

|Specifies Taobao Missile Defense \(TMD\) rules. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|DomainConfigs|Array of DomainConfig| |The configurations of the domain name. |
|DomainConfig| | | |
|ConfigId|String|5003576|The ID of the configuration. |
|FunctionArgs|Array of FunctionArg| |The parameters of each feature. |
|FunctionArg| | | |
|ArgName|String|file\_type|The name of the parameter. |
|ArgValue|String|txt|The value of the parameter. |
|FunctionName|String|set\_req\_host\_header|The name of the feature. |
|Status|String|success|The status of the configuration. Valid values:

 -   **success**
-   **testing**
-   **failed**
-   **configuring** |
|RequestId|String|F8AA0364-0FDB-4AD5-\*\*\*\*-D69FAB8924ED|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=DescribeVodDomainConfigs
&DomainName=www.example.com
&FunctionNames=filetype_based_ttl_set,set_req_host_header
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeVodDomainConfigsResponse>
      <RequestId>F8AA0364-0FDB-4AD5-****-D69FAB8924ED</RequestId>
	  <DomainConfigs>
		    <DomainConfig>
			      <FunctionArgs>
				        <FunctionArg>
					          <ArgName>domain_name</ArgName>
					          <ArgValue>www.example.com</ArgValue>
				        </FunctionArg>
			      </FunctionArgs>
			      <ConfigId>5003576</ConfigId>
			      <FunctionName>set_req_host_header</FunctionName>
		    </DomainConfig>
		    <DomainConfig>
			      <FunctionArgs>
				        <FunctionArg>
					          <ArgName>file_type</ArgName>
					          <ArgValue>txt</ArgValue>
				        </FunctionArg>
				        <FunctionArg>
					          <ArgName>ttl</ArgName>
					          <ArgValue>13</ArgValue>
				        </FunctionArg>
				        <FunctionArg>
					          <ArgName>weight</ArgName>
					          <ArgValue>8</ArgValue>
				        </FunctionArg>
			      </FunctionArgs>
			      <ConfigId>5068995</ConfigId>
			      <FunctionName>filetype_based_ttl_set</FunctionName>
		    </DomainConfig>
	  </DomainConfigs>
</DescribeVodDomainConfigsResponse>
```

`JSON` format

```
{
  "RequestId": "F8AA0364-0FDB-4AD5-****-D69FAB8924ED",
  "DomainConfigs": {
    "DomainConfig": [
      {
        "FunctionArgs": {
          "FunctionArg": [
            {
              "ArgName": "domain_name",
              "ArgValue": "www.example.com"
            }
          ]
        },
        "ConfigId": 5003576,
        "FunctionName": "set_req_host_header"
      },
      {
        "FunctionArgs": {
          "FunctionArg": [
            {
              "ArgName": "file_type",
              "ArgValue": "txt"
            },
            {
              "ArgName": "ttl",
              "ArgValue": "13"
            },
            {
              "ArgName": "weight",
              "ArgValue": "8"
            }
          ]
        },
        "ConfigId": 5068995,
        "FunctionName": "filetype_based_ttl_set"
      }
    ]
  }
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
|DeleteFunctionFailed

|Batch delete functions failed.

|400

|The error message returned because you failed to delete multiple features. |
|InvalidFunctionName.ValueNotSupported

|FunctionName %s is not supported.

|400

|The error message returned because the %s feature name is invalid. |


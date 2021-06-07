Common parameters 
======================================

This topic describes the name and description of the common parameters of the ApsaraVideo VOD API.

Common request parameters 
----------------------------------------------

Common request parameters must be included in all API requests.




|    Parameter     |  Type  | Required |                                                                                                                                                                                           Description                                                                                                                                                                                            |
|------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Format           | String | No       | The format in which to return the response. Valid values: JSON and XML. Default value: XML.                                                                                                                                                                                                                                                                                                      |
| Version          | String | Yes      | The version number of the API, in the format of YYYY-MM-DD. Set the value to 2017-03-21.                                                                                                                                                                                                                                                                                         |
| AccessKeyId      | String | Yes      | The AccessKey ID provided by Alibaba Cloud for you to access services. For more information, see [Overview]().                                                                                                                                                                                                                                                |
| Signature        | String | Yes      | The signature string of the current request. For more information about how signatures are calculated, see [Signature method](/intl.en-US/API Reference/Calling methods/Signature method.md). For more information about the sample code, see [Signature](/intl.en-US/API Reference/Calling methods/Signature method.md).                  |
| SignatureMethod  | String | Yes      | The encryption method of the signature string. Set the value to HMAC-SHA1.                                                                                                                                                                                                                                                                                                                       |
| Timestamp        | String | Yes      | The timestamp of the request. Specify the time in the ISO 8601 standard in the YYYY-MM-DDThh:mm:ssZ format. The time must be in UTC. For example, 2017-3-29T12:00:00Z indicates 20:00:00, March 29, 2017 (UTC+8). For more information about the sample code, see [TimeStamp](/intl.en-US/API Reference/Calling methods/Signature method.md). |
| SignatureVersion | String | Yes      | The version of the signature algorithm. Set the value to 1.0.                                                                                                                                                                                                                                                                                                                                    |
| SignatureNonce   | String | Yes      | A unique and random number. You must use different numbers for multiple requests to prevent replay attacks. For more information about the sample code, see [SignatureNonce](/intl.en-US/API Reference/Calling methods/Signature method.md).                                                                                                  |
| SecurityToken    | String | No       | The temporary token provided by Security Token Service (STS). By default, the value of this parameter is empty. For more information about the token, see STS temporary AccessKey pairs in the [Overview]() topic. For more information about how to generate the token, see [Use STS to authorize access]().                              |



Examples 
-----------------------------

        http://vod.cn-shanghai.aliyuncs.com/
        ? Format=json 
        &Version=2017-03-21
        &Signature=vpEEL0zFHfxXYzSFV0n7%2FZiFL9o%3D 
        &SignatureMethod=Hmac-SHA1
        &SignatureNonce=9166ab59-f445-4005-911d-664c1570df0f
        &SignatureVersion=1.0
        &Action=GetVideoPlayAuth
        &AccessKeyId=XXXXXXX  
        &Timestamp=2017-03-29T09%3A22%3A32Z
                    



Common response parameters 
-----------------------------------------------

Every response returns a unique request ID regardless of whether the call is successful.

**XML format** 

        <? xml version="1.0" encoding="UTF-8"? >
        <!--Result root node--> 
        <Operation name+Response>
                <!--Return request tag-->
                <RequestId>4C467B38-3910-447D-87BC-AC049166F216</RequestId>
            <!--Return result data--> 
        </Operation name+Response>
                    



**JSON format** 

        {
                    "RequestId": "4C467B38-3910-447D-87BC-AC049166F216", /* Return result data */
        }
                    



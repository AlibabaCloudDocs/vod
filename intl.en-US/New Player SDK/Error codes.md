# Error codes

This topic describes the error codes of ApsaraVideo Player SDK, including the definitions, examples, and descriptions of the error codes. You can query the error codes and seek for help during actual operations after an error occurs.

## Request error codes

|Error definition|Error code in hexadecimal notation|Error code in decimal notation|Description|
|----------------|----------------------------------|------------------------------|-----------|
|ERROR\_SERVER\_NO\_RESPONSE|20010001|536936449|The error message returned because the server returns no response.|
|ERROR\_SERVER\_WRONG\_JSON|20010002|536936450|The error message returned because the response that is returned by the server is not in the JSON format.|
|ERROR\_NO\_MATCH\_QUALITY|20010003|536936451|The error message returned because no resolution matches.|
|ERROR\_PLAYAUTH\_WRONG|20010004|536936452|The error message returned because a playback credential parsing error has occurred.|
|ERROR\_REQUEST\_FAIL|20010005|536936453|The error message returned because the request fails.|

## POP error codes

|Error definition|Error code in hexadecimal notation|Error code in decimal notation|Description|
|----------------|----------------------------------|------------------------------|-----------|
|ERROR\_SERVER\_POP\_UNKNOWN|20010100|536936704|The error message returned because an unknown Post Office Protocol \(POP\) error has occurred. For more information about POP error messages, see [Error codes](/intl.en-US/API Reference/Error codes.md).|
|ERROR\_SERVER\_POP\_MISSING\_PARAMETER|20010101|536936705|The error message returned because a required parameter is not specified.|
|ERROR\_SERVER\_POP\_INVALID\_PARAMETER|20010102|536936706|The error message returned because a specified parameter is invalid.|
|ERROR\_SERVER\_POP\_OPERATION\_DENIED|20010103|536936707|The error message returned because ApsaraVideo VOD is not activated for your Alibaba Cloud account.|
|ERROR\_SERVER\_POP\_OPERATION\_SUSPENED|20010104|536936708|The error message returned because your Alibaba Cloud account has overdue payments. Add funds to your account.|
|ERROR\_SERVER\_POP\_FORBIDDEN|20010105|536936709|The error message returned because you are not authorized to perform the operation.|
|ERROR\_SERVER\_POP\_INTERNAL\_ERROR|20010106|536936710|The error message returned because an unknown error has occurred.|
|ERROR\_SERVER\_POP\_SERVICE\_UNAVALIABLE|20010107|536936711|The error message returned because the service is unavailable.|
|ERROR\_SERVER\_POP\_SIGNATUREANONCE\_USED|20010108|536936712|The error message returned because the signature has been used.|
|ERROR\_SERVER\_POP\_SECURITYTOKEN\_MAILFORMED|20010109|536936713|The error message returned because the security token is invalid.|
|ERROR\_SERVER\_POP\_SECURITYTOKEN\_MISMATCH\_ACCESSKEY|2001010A|536936714|The error message returned because the security token and AccessKey pair do not match.|
|ERROR\_SERVER\_POP\_SIGNATURE\_NOT\_MATCH|2001010B|536936715|The error message returned because the signature for verification is invalid.|
|ERROR\_SERVER\_POP\_ACCESSKEYID\_NOT\_FOUND|2001010C|536936716|The error message returned because the AccessKey ID does not exist.|
|ERROR\_SERVER\_POP\_TOKEN\_EXPIRED|2001010D|536936717|The error message returned because the token expires.|

## ApsaraVideo VOD error codes

|Error definition|Error code in hexadecimal notation|Error code in decimal notation|Description|
|----------------|----------------------------------|------------------------------|-----------|
|ERROR\_SERVER\_VOD\_UNKNOWN|20010200|536936960|The error message returned because an unknown error has occurred in ApsaraVideo VOD. For more information, see [GetPlayInfo](/intl.en-US/API Reference/Audio and video playback/GetPlayInfo.md).|
|ERROR\_SERVER\_VOD\_FORBIDDEN\_ILLEGALSTATUS|20010201|536936961|The error message returned because the video status is invalid.|
|ERROR\_SERVER\_VOD\_INVALIDVIDEO\_NOTFOUND|20010202|536936962|The error message returned because the video does not exist.|
|ERROR\_SERVER\_VOD\_INVALIDVIDEO\_NOSTREAM|20010203|536936963|The error message returned because no transcoded stream can be used for playback based on your filter criteria.|
|ERROR\_SERVER\_VOD\_FORBIDDEN\_ALIYUNVODENCRYPTION|20010204|536936964|The error message returned because transcoded streams are encrypted by using Alibaba Cloud video encryption. You must use ApsaraVideo Player to play the transcoded streams or set the ResultType parameter to **Multiple**.|
|ERROR\_SERVER\_VOD\_INVALIDAUTH\_MEDIAID|20010205|536936965|The error message returned because the authentication information and the video ID do not match.|
|ERROR\_SERVER\_VOD\_INVALIDAUTHINFO\_EXPIRETIME|20010206|536936966|The error message returned because the authentication information expires.|

## ApsaraVideo for Media Processing error codes

|Error definition|Error code in hexadecimal notation|Error code in decimal notation|Description|
|----------------|----------------------------------|------------------------------|-----------|
|ERROR\_SERVER\_MPS\_UNKNOWN|20010300|536937216|The error message returned because an unknown error has occurred in ApsaraVideo for Media Processing.|
|ERROR\_SERVER\_MPS\_INVALID\_MEDIAID|20010301|536937217|The error message returned because the media ID is invalid.|
|ERROR\_SERVER\_MPS\_INVALID\_AUTHTIMEOUT|20010302|536937218|The error message returned because the authentication expiration time is invalid.|
|ERROR\_SERVER\_MPS\_INVALID\_FORMATS|20010303|536937219|The error message returned because the format is invalid.|
|ERROR\_SERVER\_MPS\_INVALID\_AUTHINFO|20010304|536937220|The error message returned because the authentication information is invalid.|
|ERROR\_SERVER\_MPS\_SIGNATURE\_CHECK\_FAILED|20010305|536937221|The error message returned because the signature verification fails.|
|ERROR\_SERVER\_MPS\_MEDIAID\_NOT\_EXIST|20010306|536937222|The error message returned because the media ID does not exist.|
|ERROR\_SERVER\_MPS\_MEDIA\_RESOURCE\_NOT\_EXIST|20010307|536937223|The error message returned because the media resource does not exist.|
|ERROR\_SERVER\_MPS\_MEDIA\_NOT\_PUBLISHED|20010308|536937224|The error message returned because the media are not published.|
|ERROR\_SERVER\_MPS\_MEDIA\_NOT\_ENCRYPTED|20010309|536937225|The error message returned because the media are not encrypted.|
|ERROR\_SERVER\_MPS\_INVALID\_CIPHERTEXTBLOB|2001030A|536937226|The error message returned because the CiphertextBlob string is invalid.|
|ERROR\_SERVER\_MPS\_CIPHERBLOB\_NOT\_EXIST|2001030B|536937227|The error message returned because the CiphertextBlob string does not exist.|
|ERROR\_SERVER\_MPS\_INTERNAL\_ERROR|2001030C|536937228|The error message returned because an internal server error has occurred.|
|ERROR\_SERVER\_MPS\_INVALID\_IDENTITY\_NOT\_ORDER\_VIDEO\_SERVICE|2001030D|536937229|The error message returned because you are not authorized to perform the operation.|
|ERROR\_SERVER\_MPS\_UPDATE\_CDN\_DOMAIN\_CONFIGS\_FAIL|2001030E|536937230|The error message returned because the host configuration fails to be updated.|
|ERROR\_SERVER\_MPS\_AUTH\_KEY\_EXIST|2001030F|536937231|The error message returned because the AccessKey secret for authentication has been used.|
|ERROR\_SERVER\_MPS\_AUTH\_KEY\_NOT\_EXIST|20010310|536937232|The error message returned because the AccessKey secret for authentication does not exist.|
|ERROR\_SERVER\_MPS\_INVALID\_PARAMETER\_OUT\_OF\_BOUND|20010311|536937233|The error message returned because a parameter value is beyond the value range.|
|ERROR\_SERVER\_MPS\_INVALID\_PARAMETER|20010312|536937234|The error message returned because a specified parameter is invalid.|
|ERROR\_SERVER\_MPS\_INVALID\_PARAMETER\_NULL\_VALUE|20010313|536937235|The error message returned because a parameter value is null. Set the parameter to a non-null value.|
|ERROR\_SERVER\_MPS\_INVALID\_PARAMETER\_EMPTY\_VALUE|20010314|536937236|The error message returned because a required parameter is not specified.|
|ERROR\_SERVER\_MPS\_MEDIA\_RESOURCE\_NOT\_MATCH|20010315|536937237|The error message returned because the media resource is not supported.|
|ERROR\_SERVER\_MPS\_MEDIA\_NOT\_FOUND\_CIPHERTEXT|20010316|536937238|The error message returned because the ciphertext of the media ID is not found.|
|ERROR\_SERVER\_MPS\_INVALID\_PARAMETER\_RAND|20010317|536937239|The error message returned because the specified rand parameter is invalid.|
|ERROR\_SERVER\_MPS\_REDIS\_POOL\_IS\_EMPTY|20010318|536937240|The error message returned because the cache connection pool is empty.|
|ERROR\_SERVER\_MPS\_SIGNATURE\_CHECK\_MEDIA\_FAILED|20010319|536937241|The error message returned because the signature and the media ID do not match.|
|ERROR\_SERVER\_MPS\_SIGNATURE\_CHECK\_EXPIREDTIME\_FAILED|2001031A|536937242|The error message returned because the specified timeout value expires.|
|ERROR\_SERVER\_MPS\_INVALID\_SESSION\_TIME|2001031B|536937243|The error message returned because the specified SessionTime parameter is invalid. Set the SessionTime parameter to a value greater than **0**.|
|ERROR\_SERVER\_MPS\_INVALID\_END\_USER\_ID|2001031C|536937244|The error message returned because the length of the EndUserId parameter is invalid.|
|ERROR\_SERVER\_MPS\_INVALID\_URL|2001031D|536937245|The error message returned because the format of the LicenseUrl parameter is invalid.|
|ERROR\_SERVER\_MPS\_HTTP\_REQUEST\_FAILED|2001031E|536937246|The error message returned because the request fails.|
|ERROR\_SERVER\_MPS\_XML\_FORMAT\_ERROR|2001031F|536937247|The error message returned because the XML format is invalid.|
|ERROR\_SERVER\_MPS\_SESSION\_NOT\_EXIST|20010320|536937248|The error message returned because the session does not exist.|
|ERROR\_SERVER\_MPS\_REGION\_NOT\_SUPPORTED\_API|20010321|536937249|The error message returned because the API is not supported.|
|ERROR\_SERVER\_MPS\_DRM\_NOT\_ACTIVATED|20010322|536937250|The error message returned because digital rights management \(DRM\) is not authorized in this region. Seek for technical support.|
|ERROR\_SERVER\_MPS\_DRM\_AUTH\_ERROR|20010323|536937251|The error message returned because DRM verification fails. Authorize DRM for the media.|
|ERROR\_SERVER\_MPS\_CDN\_CONFIG\_NOT\_EXIST|20010324|536937252|The error message returned because no domain name for the content delivery network \(CDN\) is bound to your Object Storage Service \(OSS\) bucket.|

## Error codes of time-shifting live streaming

|Error definition|Error code in hexadecimal notation|Error code in decimal notation|Description|
|----------------|----------------------------------|------------------------------|-----------|
|ERROR\_SERVER\_LIVESHIFT\_UNKNOWN|20010400|536937472|The error message returned because an unknown error has occurred in time shifting.|
|ERROR\_SERVER\_LIVESHIFT\_REQUEST\_ERROR|20010401|536937473|The error message returned because the time shifting request fails.|
|ERROR\_SERVER\_LIVESHIFT\_DATA\_PARSER\_ERROR|20010402|536937474|The error message returned because the time shifting data fails to be parsed.|

## Error codes of proprietary cryptography

|Error definition|Error code in hexadecimal notation|Error code in decimal notation|Description|
|----------------|----------------------------------|------------------------------|-----------|
|ERROR\_TBDRM\_UNKNOWN|0x20012000|536944640|The error message returned because an unknown error has occurred in proprietary cryptography.|
|ERROR\_TBDRM\_DEMUXER\_UNIMPLEMENTED|20012001|536944641|The error message returned because the file that is encrypted by proprietary cryptography fails to be decapsulated.|

## ARTP error codes

|Error definition|Error code in hexadecimal notation|Error code in decimal notation|Description|
|----------------|----------------------------------|------------------------------|-----------|
|ERROR\_ARTP\_UNKNOWN|0x20013000|536948736|The error message returned because an unknown Alibaba Real-time Transport Protocol \(ARTP\) error has occurred.|
|ERROR\_ARTP\_DEMUXER\_UNIMPLEMENTED|0x20013001|536948737|The error message returned because the ARTP module fails to be loaded. Check the dynamic-link library.|
|ERROR\_ARTP\_LOAD\_FAILED|0x20013002|536948738|The error message returned because the player fails to load data for ARTP-based playback.|
|ERROR\_ARTP\_STREAM\_ILLEGAL|0x20013003|536948739|The error message returned because the URL of the ARTP stream is invalid.|
|ERROR\_ARTP\_STREAM\_NOT\_FOUND|0x20013004|536948740|The error message returned because the ARTP stream does not exist.|
|ERROR\_ARTP\_STREAM\_STOPPED|0x20013005|536948741|The error message returned because the ARTP stream stops.|
|ERROR\_ARTP\_PLAY\_TIMEOUT|0x20013006|536948742|The error message returned because the startup loading of the ARTP stream times out.|
|ERROR\_ARTP\_SPSPPS\_AACCONF\_TIMEOUT|0x20013007|536948743|The error message returned because the time expires for receiving the ARTP sequence parameter set \(SPS\) or picture parameter set \(PPS\) or AAC configurations.|
|ERROR\_ARTP\_ARTP\_MEDIA\_INFO\_TIMEOUT|0x20013007|536948743|The error message returned because the time expires for receiving the ARTP SPS or PPS or AAC configurations.|
|ERROR\_ARTP\_PACKET\_RECV\_TIMEOUT|0x20013008|536948744|The error message returned because the time expires for receiving ARTP packets that carry audio and video streams.|
|ERROR\_ARTP\_MEDIA\_PROBE\_FAILED|0x20013009|536948745|The error message returned because the connectivity test fails for the transmission of ARTP packets.|

## Playback error codes

|Error definition|Error code in hexadecimal notation|Error code in decimal notation|Description|
|----------------|----------------------------------|------------------------------|-----------|
|ERROR\_UNKNOWN\_ERROR|2001FFFF|537001983|The error message returned because an unknown error has occurred.|
|ERROR\_DEMUXER\_OPENURL|20030001|537067521|The error message returned because the URL is invalid.|
|ERROR\_DEMUXER\_NO\_VALID\_STREAM|20030002|537067522|The error message returned because the stream is invalid.|
|ERROR\_DEMUXER\_OPENSTREAM|20030003|537067523|The error message returned because the stream file fails to be opened.|
|ERROR\_LOADING\_TIMEOUT|20030004|537067524|The error message returned because the loading times out.|
|ERROR\_DATASOURCE\_EMPTYURL|20030005|537067525|The error message returned because the URL of the source file is not specified.|
|ERROR\_DECODE\_VIDEO|20040001|537133057|The error message returned because the video fails to be decoded.|
|ERROR\_DECODE\_AUDIO|20040002|537133058|The error message returned because the audio fails to be decoded.|
|ERROR\_NETWORK\_UNKNOWN|20050000|537198592|The error message returned because an unknown network error has occurred.|
|ERROR\_NETWORK\_UNSUPPORTED|20050001|537198593|The error message returned because the protocol is not supported.|
|ERROR\_NETWORK\_RESOLVE|20050002|537198594|The error message returned because the domain name cannot be resolved.|
|ERROR\_NETWORK\_CONNECT\_TIMEOUT|20050003|537198595|The error message returned because the network connection times out.|
|ERROR\_NETWORK\_COULD\_NOT\_CONNECT|20050004|537198596|The error message returned because the server fails to be connected.|
|ERROR\_NETWORK\_HTTP\_403|20050005|537198597|The error message returned because an HTTP 403 error has occurred.|
|ERROR\_NETWORK\_HTTP\_404|20050006|537198598|The error message returned because an HTTP 404 error has occurred.|
|ERROR\_NETWORK\_HTTP\_4XX|20050007|537198599|The error message returned because an HTTP 4xx error other than HTTP 403 or HTTP 404 has occurred.|
|ERROR\_NETWORK\_HTTP\_5XX|20050008|537198600|The error message returned because an HTTP 5xx error has occurred.|
|ERROR\_NETWORK\_HTTP\_RANGE|20050009|537198601|The error message returned because the HTTP range request is not supported.|
|ERROR\_NETWORK\_HTTP\_400|2005000A|537198602|The error message returned because an HTTP 400 error has occurred.|
|ERROR\_CODEC\_UNKNOWN|20060000|537264128|The error message returned because an unknown decoding error has occurred.|
|ERROR\_CODEC\_VIDEO\_NOT\_SUPPORT|20060001|537264129|The error message returned because the video coding format is not supported.|
|ERROR\_CODEC\_AUDIO\_NOT\_SUPPORT|20060002|537264130|The error message returned because the audio coding format is not supported.|
|ERROR\_GENERAL\_UNKNOWN|20080000|537395200|The error message returned because a standard error has occurred.|
|ERROR\_GENERAL\_EPERM|20080001|537395201|The error message returned because the "EPERM: Operation not permitted" error has occurred.|
|ERROR\_GENERAL\_ENOENT|20080002|537395202|The error message returned because the "ENOENT: No such file or directory" error has occurred.|
|ERROR\_GENERAL\_EIO|20080005|537395205|The error message returned because the "EIO: I/O error" error has occurred.|
|ERROR\_UNKNOWN|0x2FFFFFFF|805306367|The error message returned because an unknown error has occurred.|

## Download-related error codes

|Error definition|Error code in hexadecimal notation|Error code in decimal notation|Description|
|----------------|----------------------------------|------------------------------|-----------|
|DOWNLOAD\_ERROR\_NOT\_SELECT\_ITEM|30010000|805371904|The error message returned because no track is selected for download.|
|DOWNLOAD\_ERROR\_NO\_DOWNLOAD\_ITEM|30010001|805371905|The error message returned because no track can be used for download.|
|DOWNLOAD\_ERROR\_STS\_SOURCE\_NULL|30010002|805371906|The error message returned because the source for Security Token Service \(STS\)-based playback is not specified.|
|DOWNLOAD\_ERROR\_AUTH\_SOURCE\_NULL|30010003|805371907|The error message returned because the source for playback credential-based playback is not specified.|
|DOWNLOAD\_ERROR\_AUTH\_SOURCE\_WRONG|30010004|805371908|The error message returned because the format of the playback credential is invalid.|
|DOWNLOAD\_ERROR\_INVALID\_ITEM|30010005|805371909|The error message returned because the selected track for download is invalid.|
|DOWNLOAD\_ERROR\_URL\_CANNOT\_REACH|30010006|805371910|The error message returned because the URL is invalid.|
|DOWNLOAD\_ERROR\_NOT\_SUPPORT\_FORMAT|30010007|805371911|The error message returned because the download format is not supported.|
|DOWNLOAD\_ERROR\_ENCRYPT\_FILE\_NOT\_MATCH|30010008|805371912|The error message returned because the security file for encryption verification is invalid.|
|DOWNLOAD\_ERROR\_DOWNLOAD\_SWITCH\_OFF|30010009|805371913|The error message returned because the download feature is disabled.|
|DOWNLOAD\_ERROR\_NET\_ERROR|3001000A|805371914|The error message returned because a network error has occurred.|
|DOWNLOAD\_ERROR\_NOT\_SET\_SAVE\_DIR|3001000B|805371915|The error message returned because the download directory is not specified.|
|DOWNLOAD\_ERROR\_CANNOT\_CREATE\_SAVE\_DIR|3001000C|805371916|The error message returned because the download directory cannot be created.|
|DOWNLOAD\_ERROR\_NO\_SPACE|3001000D|805371917|The error message returned because no space can be used.|
|DOWNLOAD\_ERROR\_WRITE\_ERROR|3001000E|805371918|The error message returned because an error has occurred and data cannot be written to the file.|
|DOWNLOAD\_ERROR\_ENCRYPT\_ERROR|3001000F|805371919|The error message returned because the decryption fails.|
|DOWNLOAD\_ERROR\_FILE\_NOT\_EXIST|30010010|805371920|The error message returned because the file does not exist.|
|DOWNLOAD\_ERROR\_CLEAN\_INVALID\_PARAM|30010011|805371921|The error message returned because a parameter that is specified when you delete the file is invalid.|
|DOWNLOAD\_ERROR\_CLEAN\_WRONG\_STATUS|30010012|805371922|The error message returned because the status of the file to be deleted is invalid.|
|DOWNLOAD\_ERROR\_GET\_AES\_KEY\_FAIL|30010013|805371923|The error message returned because the Advanced Encryption Standard \(AES\) key fails to be obtained.|
|DOWNLOAD\_ERROR\_ENCRYPTION\_NOT\_SUPPORT|30010014|805371924|The error message returned because the encryption method is not supported.|


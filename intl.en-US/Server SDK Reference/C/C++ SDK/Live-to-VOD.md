Live-to-VOD 
================================

This topic provides examples on how to use the API operations of the live-to-VOD module. The API operations are encapsulated in ApsaraVideo VOD SDK for C/C++. You can call the API operations to query live-to-VOD videos.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/C/C++ SDK/Initialization.md).

Query live-to-VOD videos {#h2-u67E5u8BE2u76F4u8F6Cu70B9u89C6u9891u5217u88682}
-----------------------------------------------------------------------------

You can call the ListLiveRecordVideo operation to query live-to-VOD videos.

For more information about the request and response parameters of this operation, see [ListLiveRecordVideo](/intl.en-US/API Reference/Conversion/ListLiveRecordVideo.md). Example:

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /* Query live-to-VOD videos. */
    VodApiResponse listLiveRecordVideo(VodCredential authInfo) {
        string apiName = "ListLiveRecordVideo";
        map<string, string> args;
        args["StartTime"] = "2018-04-24T03:21:04Z";
        args["EndTime"] = "2018-05-21T03:21:44Z";
        args["StreamName"] = "testStreamName";
        args["DomainName"] = "testdomain.aliyun.com";
        args["AppName"] = "testAppName";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = listLiveRecordVideo(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



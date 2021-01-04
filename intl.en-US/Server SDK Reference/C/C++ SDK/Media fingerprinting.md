Media fingerprinting 
=========================================

This topic provides examples on how to use the API operations of the media fingerprinting module. The API operations are encapsulated in ApsaraVideo VOD SDK for C/C++. You can call the API operations to submit media fingerprinting jobs, query media fingerprinting jobs, and query media fingerprinting results.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/C/C++ SDK/Initialization.md).

Submit a media fingerprinting job {#h2--dna-div-id-submitaijob-div-2}
---------------------------------------------------------------------

You can call the SubmitAIJob operation to submit a media fingerprinting job.
For more information about the request and response parameters of this operation, see [SubmitAIJob](). Example: {#h2--dna-div-id-submitaijob-div-2}
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Submit a media fingerprinting job.
     */
    VodApiResponse submitAIJob(VodCredential authInfo) {
        string apiName = "SubmitAIJob";
        map<string, string> args;
        // The ID of the video.
        args["MediaId"] = "3eb19a4585bc475e995bdd78fd****";
        // The AI type. Set the value to AIMediaDNA.
        args["Types"] = "AIMediaDNA";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = submitAIJob(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Query media fingerprinting jobs {#h2--dna-div-id-listaijob-div-3}
-----------------------------------------------------------------

You can call the ListAIJob operation to query media fingerprinting jobs.
For more information about the request and response parameters of this operation, see [ListAIJob](). Example: {#h2--dna-div-id-listaijob-div-3}
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Query media fingerprinting jobs.
     */
    VodApiResponse listAIJob(VodCredential authInfo) {
        string apiName = "ListAIJob";
        map<string, string> args;
        // The ID of the job.
        args["JobIds"] = "979d4d7a36ae41b1a945a288****,3eb19a4585bc475e995bddea65****";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = listAIJob(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Query media fingerprinting results {#h2--dna-div-id-getmediadnaresult-div-4}
----------------------------------------------------------------------------

You can call the GetMediaDNAResult operation to query media fingerprinting results.
For more information about the request and response parameters of this operation, see [GetMediaDNAResult](). Example: {#h2--dna-div-id-getmediadnaresult-div-4}
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Query media fingerprinting results.
     */
    VodApiResponse getMediaDNAResult(VodCredential authInfo) {
        string apiName = "GetMediaDNAResult";
        map<string, string> args;
        // The ID of the video.
        args["MediaId"] = "3eb19a4585bc475e995bdd78****";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = getMediaDNAResult(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



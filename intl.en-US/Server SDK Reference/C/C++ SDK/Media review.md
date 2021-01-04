Media review 
=================================

This topic provides examples on how to use the API operations of the media review module. The API operations are encapsulated in ApsaraVideo VOD SDK for C/C++. You can call the API operations to submit and query automated review jobs. You can also query automated review results, create manual reviews, and set an IP address whitelist for reviews.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/C/C++ SDK/Initialization.md).

Submit an automated review job {#h2--div-id-submitaimediaauditjob-div-2}
------------------------------------------------------------------------

You can call the SubmitAIMediaAuditJob operation to submit an automated review job.
For more information about the request and response parameters of this operation, see [SubmitAIMediaAuditJob](). Example: {#h2--div-id-submitaimediaauditjob-div-2}
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Submit an automated review job.
     */
    VodApiResponse submitAIMediaAuditJob(VodCredential authInfo) {
        string apiName = "SubmitAIMediaAuditJob";
        map<string, string> args;
        // The ID of the video.
        args["MediaId"] = "dc063078c1d845139e2a5bd8ff54****";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = submitAIMediaAuditJob(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Query an automated review job {#h2--div-id-getaimediaauditjob-div-3}
--------------------------------------------------------------------

You can call GetAIMediaAuditJob operation to query details about an automated review job.
For more information about the request and response parameters of this operation, see [GetAIMediaAuditJob](). Example: {#h2--div-id-getaimediaauditjob-div-3}
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Query an automated review job.
     */
    VodApiResponse getAIMediaAuditJob(VodCredential authInfo) {
        string apiName = "GetAIMediaAuditJob";
        map<string, string> args;
        // The ID of the job.
        args["JobId"] = "7dc69b893c8b4f13b47aae8de085****";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = getAIMediaAuditJob(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Query the summary of automated review results {#h2--div-id-getmediaauditresult-div-4}
-------------------------------------------------------------------------------------

You can call the GetMediaAuditResult operation to query the summary of automated review results.
For more information about the request and response parameters of this operation, see [GetMediaAuditResult](). Example: {#h2--div-id-getmediaauditresult-div-4}
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Query the summary of automated review results.
     */
    VodApiResponse getMediaAuditResult(VodCredential authInfo) {
        string apiName = "GetMediaAuditResult";
        map<string, string> args;
        // The ID of the video.
        args["MediaId"] = "dc063078c1d845139e2a5bd8f58****";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = getMediaAuditResult(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Query details about automated review results {#h2--div-id-getmediaauditresultdetail-div-5}
------------------------------------------------------------------------------------------

You can call the GetMediaAuditResultDetail operation to query details about automated review results.
For more information about the request and response parameters of this operation, see [GetMediaAuditResultDetail](). Example: {#h2--div-id-getmediaauditresultdetail-div-5}
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Query details about automated review results.
     */
    VodApiResponse getMediaAuditResultDetail(VodCredential authInfo) {
        string apiName = "GetMediaAuditResultDetail";
        map<string, string> args;
        // The ID of the video.
        args["MediaId"] = "dc063078c1d845139e2a5bd8f23****";
        // The number of the page to return.
        args["PageNo"] = "1";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = getMediaAuditResultDetail(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Query the timeline of automated review results {#h2--div-id-getmediaauditresulttimeline-div-6}
----------------------------------------------------------------------------------------------

You can call the GetMediaAuditResultTimeline operation to query the timeline of automated review results.
For more information about the request and response parameters of this operation, see [GetMediaAuditResultTimeline](). Example: {#h2--div-id-getmediaauditresulttimeline-div-6}
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Query the timeline of automated review results.
     */
    VodApiResponse getMediaAuditResultTimeline(VodCredential authInfo) {
        string apiName = "GetMediaAuditResultTimeline";
        map<string, string> args;
        // The ID of the video.
        args["MediaId"] = "dc063078c1d845139e2a5bd8f85****";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = getMediaAuditResultTimeline(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Create a manual review {#h2--div-id-createaudit-div-7}
------------------------------------------------------

You can call the CreateAudit operation to create a manual review.
For more information about the request and response parameters of this operation, see [CreateAudit](/intl.en-US/API Reference/Content Moderation/Manual Audit/CreateAudit.md). Example: {#h2--div-id-createaudit-div-7}
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Build parameters for a review.
     */
    Json::Value buildAuditContent() {
            Json::Value auditContents;
            Json::Value auditContent;
            auditContent["VideoId"] = "3ebc10160bda481ca9b6858a0b32****"; // The ID of the video.
            auditContent["Status"] = "Blocked"; // The review status.
            auditContent["Reason"] = "Including porn"; // If the review status is Blocked, a reason must be provided. The reason can contain a maximum of 128 bytes.
            auditContents.append(auditContent);
            return auditContents;
    }
    
    /**
     * Create a manual review.
     */
    VodApiResponse createAudit(VodCredential authInfo) {
        string apiName = "CreateAudit";
        map<string, string> args;
        // The review content.
        args["AuditContent"] = buildAuditContent().toStyledString();
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = createAudit(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Query the historical records of manual reviews {#h2--div-id-getaudithistory-div-8}
----------------------------------------------------------------------------------

You can call the GetAuditHistory operation to query the historical records of manual reviews.
For more information about the request and response parameters of this operation, see [GetAuditHistory](/intl.en-US/API Reference/Content Moderation/Manual Audit/GetAuditHistory.md). Example: {#h2--div-id-getaudithistory-div-8}
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Query the historical records of manual reviews.
     */
    VodApiResponse getAuditHistory(VodCredential authInfo) {
        string apiName = "GetAuditHistory";
        map<string, string> args;
        // The ID of the video.
        args["VideoId"] = "3ebc10160bda481ca9b6858a0b32****";
        // The number of the page to return.
        args["PageNo"] = "1";
        // The number of entries to return on each page.
        args["PageSize"] = "10";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = getAuditHistory(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Set an IP address whitelist for reviews {#h2--ip-div-id-setauditsecurityip-div-9}
---------------------------------------------------------------------------------

You can call the SetAuditSecurityIp operation to set an IP address whitelist for reviews.
For more information about the request and response parameters of this operation, see [SetAuditSecurityIp](/intl.en-US/API Reference/Content Moderation/Audit Config/SetAuditSecurityIp.md). Example: {#h2--ip-div-id-setauditsecurityip-div-9}
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Set an IP address whitelist for reviews.
     */
    VodApiResponse setAuditSecurityIp(VodCredential authInfo) {
        string apiName = "SetAuditSecurityIp";
        map<string, string> args;
        // The name of the IP address whitelist for reviews. The default value is Default.
        args["SecurityGroupName"] = "MyGroupName";
        // The operation type. The default value is Append, which indicates that IP addresses are added to the whitelist.
        args["OperateMode"] = "Cover";
        // The IP addresses that are added to the whitelist.
        args["Ips"] = "10.23.12.20,10.23.12.21,10.23.12.22";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = setAuditSecurityIp(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Query the IP addresses in a whitelist {#h2--ip-div-id-listauditsecurityip-div-10}
---------------------------------------------------------------------------------

You can call the ListAuditSecurityIp operation to query the IP addresses in a whitelist.
For more information about the request and response parameters of this operation, see [ListAuditSecurityIp](/intl.en-US/API Reference/Content Moderation/Audit Config/ListAuditSecurityIp.md). Example: {#h2--ip-div-id-listauditsecurityip-div-10}
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Query the IP addresses in a whitelist.
     */
    VodApiResponse listAuditSecurityIp(VodCredential authInfo) {
        string apiName = "ListAuditSecurityIp";
        map<string, string> args;
        // The name of the whitelist.
        args["SecurityGroupName"] = "MyGroupName";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = listAuditSecurityIp(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



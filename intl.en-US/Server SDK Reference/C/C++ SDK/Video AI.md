Video AI 
=============================

This topic provides examples on how to use the API operations of the video AI module. The API operations are encapsulated in ApsaraVideo VOD SDK for C/C++. You can call the API operations to submit or query AI jobs, specify an AI template as the default one, and query the default AI template. You can also create, delete, modify, and query AI templates.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/C/C++ SDK/Initialization.md).

Submit an AI job {#h2--ai-div-id-submitaijob-div-2}
---------------------------------------------------

You can call the SubmitAIJob operation to submit an AI job.
For more information about the request and response parameters of this operation, see [SubmitAIJob](). Example: {#h2--ai-div-id-submitaijob-div-2}
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Submit an AI job.
     */
    VodApiResponse submitAIJob(VodCredential authInfo) {
        string apiName = "SubmitAIJob";
        map<string, string> args;
        // The ID of the video.
        args["MediaId"] = "3eb19a4585bc475e995bddfd****";
        // The AI type. Make sure that this AI type is enabled.
        args["Types"] = "AIVideoCover";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = submitAIJob(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Query AI jobs {#h2--ai-div-id-listaijob-div-3}
----------------------------------------------

You can call the ListAIJob operation to query AI jobs.
For more information about the request and response parameters of this operation, see [ListAIJob](). Example: {#h2--ai-div-id-listaijob-div-3}
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Query AI jobs.
     */
    VodApiResponse listAIJob(VodCredential authInfo) {
        string apiName = "ListAIJob";
        map<string, string> args;
        // The ID of the job.
        args["JobIds"] = "979d4d7a36ae41b1a945a252****,3eb19a4585bc475e995bddea5****";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = listAIJob(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Create an AI template {#h2--ai-div-id-addaitemplate-div-4}
----------------------------------------------------------

You can call the AddAITemplate operation to create an AI template.
For more information about the request and response parameters of this operation, see [AddAITemplate](). Example: {#h2--ai-div-id-addaitemplate-div-4}
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Create an AI template.
     */
    VodApiResponse addAITemplate(VodCredential authInfo) {
        string apiName = "AddAITemplate";
        map<string, string> args;
        // The template type. For this example, specify an automated review template.
        args["TemplateType"] = "AIMediaAudit";
        // The name of the template.
        args["TemplateName"] = "The custom template";
        // The detailed configurations of the template.
        Json::Value templateConfig;
        Json::Value auditItem;
        auditItem.append("terrorism");
        auditItem.append("porn");
        templateConfig["AuditItem"] = auditItem;
    
        Json::Value auditRange;
        auditRange.append("video");
        auditRange.append("image-cover");
        auditRange.append("text-title");
        templateConfig["AuditRange"] = auditRange;
    
        Json::Value auditContent;
        auditContent.append("screen");
        templateConfig["AuditContent"] = auditContent;
        templateConfig["AuditAutoBlock"] = "no";
        args["TemplateConfig"] = templateConfig.toStyledString();
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = addAITemplate(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Delete an AI template {#h2--ai-div-id-deleteaitemplate-div-5}
-------------------------------------------------------------

You can call the DeleteAITemplate operation to delete an AI template.
For more information about the request and response parameters of this operation, see [DeleteAITemplate](). Example: {#h2--ai-div-id-deleteaitemplate-div-5}
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Delete an AI template.
     */
    VodApiResponse deleteAITemplate(VodCredential authInfo) {
        string apiName = "DeleteAITemplate";
        map<string, string> args;
        // The ID of the template.
        args["TemplateId"] = "1d763dd8987a122ab8596eb7d2c8****";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = deleteAITemplate(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Modify an AI template {#h2--ai-div-id-updateaitemplate-div-6}
-------------------------------------------------------------

You can call the UpdateAITemplate operation to modify an AI template.
For more information about the request and response parameters of this operation, see [UpdateAITemplate](). Example: {#h2--ai-div-id-updateaitemplate-div-6}
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Modify an AI template.
     */
    VodApiResponse updateAITemplate(VodCredential authInfo) {
        string apiName = "UpdateAITemplate";
        map<string, string> args;
        // The ID of the template.
        args["TemplateId"] = "1d763dd8987a122ab8596eb7d258****";
        // The name of the template.
        args["TemplateName"] = "The custom template";
        // The detailed configurations of the template.
        Json::Value templateConfig;
        Json::Value auditItem;
        auditItem.append("terrorism");
        auditItem.append("porn");
        templateConfig["AuditItem"] = auditItem;
    
        Json::Value auditRange;
        auditRange.append("video");
        auditRange.append("image-cover");
        auditRange.append("text-title");
        templateConfig["AuditRange"] = auditRange;
    
        Json::Value auditContent;
        auditContent.append("screen");
        templateConfig["AuditContent"] = auditContent;
        templateConfig["AuditAutoBlock"] = "no";
        args["TemplateConfig"] = templateConfig.toStyledString();
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = updateAITemplate(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Query an AI template {#h2--ai-div-id-getaitemplate-div-7}
---------------------------------------------------------

You can call the GetAITemplate operation to query details about an AI template.
For more information about the request and response parameters of this operation, see [GetAITemplate](). Example: {#h2--ai-div-id-getaitemplate-div-7}
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Query details about an AI template.
     */
    VodApiResponse getAITemplate(VodCredential authInfo) {
        string apiName = "GetAITemplate";
        map<string, string> args;
        // The ID of the template.
        args["TemplateId"] = "1d763dd8987a122ab8596eb7d2c832****";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = getAITemplate(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Query AI templates {#h2--ai-div-id-listaitemplate-div-8}
--------------------------------------------------------

You can call the ListAITemplate operation to query AI templates.
For more information about the request and response parameters of this operation, see [ListAITemplate](). Example: {#h2--ai-div-id-listaitemplate-div-8}
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Query AI templates.
     */
    VodApiResponse listAITemplate(VodCredential authInfo) {
        string apiName = "ListAITemplate";
        map<string, string> args;
        // The template type. For this example, specify an automated review template.
        args["TemplateType"] = "AIMediaAudit";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = listAITemplate(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Specify an AI template as the default one {#h2--ai-div-id-setdefaultaitemplate-div-9}
-------------------------------------------------------------------------------------

You can call the SetDefaultAITemplate operation to specify an AI template as the default one.
For more information about the request and response parameters of this operation, see [SetDefaultAITemplate](). Example: {#h2--ai-div-id-setdefaultaitemplate-div-9}
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Specify an AI template as the default one.
     */
    VodApiResponse setDefaultAITemplate(VodCredential authInfo) {
        string apiName = "SetDefaultAITemplate";
        map<string, string> args;
        // The ID of the template.
        args["TemplateId"] = "1d763dd8987a122ab8596eb7d2c8****";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = setDefaultAITemplate(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Query the default AI template {#h2--ai-div-id-getdefaultaitemplate-div-10}
--------------------------------------------------------------------------

You can call the GetDefaultAITemplate operation to query details about the default AI template.
For more information about the request and response parameters of this operation, see [GetDefaultAITemplate](). Example: {#h2--ai-div-id-getdefaultaitemplate-div-10}
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    /**
     * Query details about the default AI template.
     */
    VodApiResponse getDefaultAITemplate(VodCredential authInfo) {
        string apiName = "GetDefaultAITemplate";
        map<string, string> args;
        // The template type. For this example, specify an automated review template.
        args["TemplateType"] = "AIMediaAudit";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = getDefaultAITemplate(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



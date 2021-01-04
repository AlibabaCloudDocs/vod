Transcoding template 
=========================================

This topic provides examples on how to use the API operations of the transcoding template module. The API operations are encapsulated in ApsaraVideo VOD SDK for C/C++. You can call the API operations to create, modify, delete, and query transcoding template groups. You can also specify a transcoding template group as the default one.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/C/C++ SDK/Initialization.md).

Create a transcoding template group {#h2--div-id-addtranscodetemplategroup-div-2}
---------------------------------------------------------------------------------

You can call the AddTranscodeTemplateGroup operation to create a transcoding template group.
For more information about the request and response parameters of this operation, see [AddTranscodeTemplateGroup](). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Build the configurations of the transcoding template.
     */
    Json::Value buildTranscodeTemplateList() {
        Json::Value transcodeTemplateList;
        Json::Value transcodeTemplate;
        // The configurations of video stream transcoding.
        Json::Value video;
        video["Width"] = 640;
        video["Bitrate"] = 400;
        video["Fps"] = 25;
        video["Remove"] = false;
        video["Codec"] = "H.264";
        video["Gop"] = "250";
        transcodeTemplate["Video"] = video;
    
        // The configurations of audio stream transcoding.
        Json::Value audio;
        audio["Codec"] = "AAC";
        audio["Bitrate"] = "64";
        audio["Channels"] = "2";
        audio["Samplerate"] = "32000";
        transcodeTemplate["Audio"] = audio;
    
        // The container for encapsulation.
        Json::Value container;
        container["Format"] = "mp4";
        transcodeTemplate["Container"] = container;
    
        // The configurations of conditional transcoding.
        Json::Value transconfig;
        transconfig["IsCheckReso"] = false;
        transconfig["IsCheckResoFail"] = false;
        transconfig["IsCheckVideoBitrate"] = false;
        transconfig["IsCheckVideoBitrateFail"] = false;
        transconfig["IsCheckAudioBitrate"] = false;
        transconfig["IsCheckAudioBitrateFail"] = false;
        transcodeTemplate["TransConfig"] = transconfig;
    
        // The configurations of encryption, which is supported only for m3u8 videos.
        //Json::Value encryptSetting;
        //encryptSetting["EncryptType"] = "Private";
        //transcodeTemplate["EncryptSetting"] = encryptSetting;
    
        // The definition.
        transcodeTemplate["Definition"] = "LD";
    
        // The name of the template.
        transcodeTemplate["TemplateName"] = "testtemplate";
    
        // The IDs of associated watermarks.
        Json::Value watermarkIdList;
        watermarkIdList.append("263261bdc1ff65782f8995c6dd22****");
        // USER_DEFAULT_WATERMARK, which indicates the ID of the default watermark.
        watermarkIdList.append("USER_DEFAULT_WATERMARK");
        transcodeTemplate["WatermarkIds"] = watermarkIdList;
        transcodeTemplateList.append(transcodeTemplate);
        return transcodeTemplateList;
    }
    
    /**
     * Create a transcoding template group.
     */
    VodApiResponse addTranscodeTemplateGroup(VodCredential authInfo) {
        string apiName = "AddTranscodeTemplateGroup";
        map<string, string> args;
        args["Name"] = "grouptest";
        args["TranscodeTemplateList"] = buildTranscodeTemplateList().toStyledString();
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = addTranscodeTemplateGroup(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Modify a transcoding template group {#h2--div-id-updatetranscodetemplategroup-div-3}
------------------------------------------------------------------------------------

You can call the UpdateTranscodeTemplateGroup operation to modify a transcoding template group.
For more information about the request and response parameters of this operation, see [UpdateTranscodeTemplateGroup](). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Build the configurations of the transcoding template.
     */
    Json::Value buildTranscodeTemplateList() {
        Json::Value transcodeTemplateList;
        Json::Value transcodeTemplate;
        // The configurations of video stream transcoding.
        Json::Value video;
        video["Width"] = 640;
        video["Bitrate"] = 400;
        video["Fps"] = 25;
        video["Remove"] = false;
        video["Codec"] = "H.264";
        video["Gop"] = "250";
        transcodeTemplate["Video"] = video;
    
        // The configurations of audio stream transcoding.
        Json::Value audio;
        audio["Codec"] = "AAC";
        audio["Bitrate"] = "64";
        audio["Channels"] = "2";
        audio["Samplerate"] = "32000";
        transcodeTemplate["Audio"] = audio;
    
        // The container for encapsulation.
        Json::Value container;
        container["Format"] = "mp4";
        transcodeTemplate["Container"] = container;
    
        // The configurations of conditional transcoding.
        Json::Value transconfig;
        transconfig["IsCheckReso"] = false;
        transconfig["IsCheckResoFail"] = false;
        transconfig["IsCheckVideoBitrate"] = false;
        transconfig["IsCheckVideoBitrateFail"] = false;
        transconfig["IsCheckAudioBitrate"] = false;
        transconfig["IsCheckAudioBitrateFail"] = false;
        transcodeTemplate["TransConfig"] = transconfig;
    
        // The configurations of encryption, which is supported only for m3u8 videos.
        //Json::Value encryptSetting;
        //encryptSetting["EncryptType"] = "Private";
        //transcodeTemplate["EncryptSetting"] = encryptSetting;
    
        // The name of the template.
        transcodeTemplate["TemplateName"] = "testtemplate";
    
        // The ID of the transcoding template that you want to modify.
        transcodeTemplate["TranscodeTemplateId"] = "85c2b18ac08fda33e8f6d9c56****";
    
        // The IDs of associated watermarks.
        Json::Value watermarkIdList;
        watermarkIdList.append("263261bdc1ff65782f8995c6dd22****");
        // USER_DEFAULT_WATERMARK, which indicates the ID of the default watermark.
        watermarkIdList.append("USER_DEFAULT_WATERMARK");
        transcodeTemplate["WatermarkIds"] = watermarkIdList;
        transcodeTemplateList.append(transcodeTemplate);
        return transcodeTemplateList;
    }
    
    /**
     * Modify the configurations of the transcoding template group.
     */
    VodApiResponse updateTranscodeTemplateGroup(VodCredential authInfo) {
        string apiName = "UpdateTranscodeTemplateGroup";
        map<string, string> args;
        // The ID of the transcoding template group.
        args["TranscodeTemplateGroupId"] = "4c71a339fecec0152b4fa6f452****";
        args["Name"] = "grouptest";
        args["TranscodeTemplateList"] = buildTranscodeTemplateList().toStyledString();
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = updateTranscodeTemplateGroup(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Query transcoding template groups {#h2--div-id-listtranscodetemplategroup-div-4}
--------------------------------------------------------------------------------

You can call the ListTranscodeTemplateGroup operation to query transcoding template groups.
For more information about the request and response parameters of this operation, see [ListTranscodeTemplateGroup](). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Query transcoding template groups.
     */
    VodApiResponse listTranscodeTemplateGroup(VodCredential authInfo) {
        string apiName = "ListTranscodeTemplateGroup";
        map<string, string> args;
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = listTranscodeTemplateGroup(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Query a transcoding template group {#h2--div-id-gettranscodetemplategroup-div-5}
--------------------------------------------------------------------------------

You can call the GetTranscodeTemplateGroup operation to query a transcoding template group.
For more information about the request and response parameters of this operation, see [GetTranscodeTemplateGroup](). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Query the configurations of a transcoding template group.
     */
    VodApiResponse getTranscodeTemplateGroup(VodCredential authInfo) {
        string apiName = "GetTranscodeTemplateGroup";
        map<string, string> args;
        args["TranscodeTemplateGroupId"] = "a0fa0fda545e50e7a3eb75491****";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = getTranscodeTemplateGroup(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Specify a transcoding template group as the default one {#h2--div-id-setdefaulttranscodetemplategroup-div-6}
------------------------------------------------------------------------------------------------------------

You can call the SetDefaultTranscodeTemplateGroup operation to specify a transcoding template group as the default one.
For more information about the request and response parameters of this operation, see [SetDefaultTranscodeTemplateGroup](). Example: 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Specify a transcoding template group as the default one.
     */
    VodApiResponse setDefaultTranscodeTemplateGroup(VodCredential authInfo) {
        string apiName = "SetDefaultTranscodeTemplateGroup";
        map<string, string> args;
        args["TranscodeTemplateGroupId"] = "a0fa0fda545e50e7a3eb75491****";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = setDefaultTranscodeTemplateGroup(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Delete a transcoding template group {#h2--div-id-deletetranscodetemplategroup-div-7}
------------------------------------------------------------------------------------

You can call the DeleteTranscodeTemplateGroup operation to delete a transcoding template group.
For more information about the request and response parameters of this operation, see [DeleteTranscodeTemplateGroup](). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    
    /**
     // Delete the configurations of the transcoding template group.
     */
    VodApiResponse deleteTranscodeTemplateGroup(VodCredential authInfo) {
        string apiName = "DeleteTranscodeTemplateGroup";
        map<string, string> args;
        args["TranscodeTemplateGroupId"] = "a0fa0fda545e50e7a3eb75491****";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = deleteTranscodeTemplateGroup(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



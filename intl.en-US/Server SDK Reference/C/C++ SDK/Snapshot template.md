Snapshot template 
======================================

This topic provides examples on how to use the API operations of the snapshot template module. The API operations are encapsulated in ApsaraVideo VOD SDK for C/C++. You can call the API operations to create, delete, modify, and query snapshot templates.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/C/C++ SDK/Initialization.md).

Create a snapshot template {#h2--div-id-addvodtemplate-div-2}
-------------------------------------------------------------

You can call the AddVodTemplate operation to create a snapshot template.
For more information about the request and response parameters of this operation, see [AddVodTemplate](/intl.en-US/API Reference/Media processing/Snapshot template/AddVodTemplate.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Modify a snapshot template. Configure the parameters as required.
     * The following sample code shows the complete configuration of image sprites.
     * @return
     */
    Json::Value buildSnapshotTemplateConfig() {
        Json::Value templateConfig;
        Json::Value snapshotConfig;
        snapshotConfig["Count"] = "50";
        snapshotConfig["Interval"] = "1";
        snapshotConfig["SpecifiedOffsetTime"] = "0";
        snapshotConfig["Width"] = "200";
        snapshotConfig["Height"] = "200";
        snapshotConfig["FrameType"] = "normal";
    
        // The configurations of image sprites. The configurations must be based on those of common snapshots.
        Json::Value spriteSnapshotConfig;
        spriteSnapshotConfig["CellWidth"] = "120";
        spriteSnapshotConfig["CellHeight"] = "68";
        spriteSnapshotConfig["Columns"] = "3";
        spriteSnapshotConfig["Lines"] = "10";
        spriteSnapshotConfig["Padding"] = "20";
        spriteSnapshotConfig["Margin"] = "50";
        spriteSnapshotConfig["KeepCellPic"] = "keep";
        spriteSnapshotConfig["Color"] = "tomato";
        snapshotConfig["SpriteSnapshotConfig"] = spriteSnapshotConfig;
    
        // The configurations of common snapshots. The configurations are also used by image sprites.
        templateConfig["SnapshotConfig"] = snapshotConfig;
    
        // The type of the snapshot. Set the value to SpriteSnapshot for image sprites and to NormalSnapshot in other scenarios.
        templateConfig["SnapshotType"] = "SpriteSnapshot";
        return templateConfig;
    }
    
    /**
     * Create a snapshot template.
     */
    VodApiResponse addSnapshotVodTemplate(VodCredential authInfo) {
        string apiName = "AddVodTemplate";
        map<string, string> args;
        // The name of the template.
        args["Name"] = "Addtest";
        // The type of the template. Set the value to Snapshot.
        args["TemplateType"] = "Snapshot";
        // The template configurations.
        Json::Value templateConfig = buildSnapshotTemplateConfig();
        args["TemplateConfig"] = templateConfig.toStyledString();
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = addSnapshotVodTemplate(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Modify a snapshot template {#h2--div-id-updatevodtemplate-div-3}
----------------------------------------------------------------

You can call the UpdateVodTemplate operation to modify a snapshot template.
For more information about the request and response parameters of this operation, see [UpdateVodTemplate](/intl.en-US/API Reference/Media processing/Snapshot template/UpdateVodTemplate.md). Example: 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Modify a snapshot template. Configure the parameters as required.
     * The following sample code shows the complete configuration of image sprites.
     * @return
     */
    Json::Value buildSnapshotTemplateConfig() {
        Json::Value templateConfig;
        Json::Value snapshotConfig;
        snapshotConfig["Count"] = "50";
        snapshotConfig["Interval"] = "1";
        snapshotConfig["SpecifiedOffsetTime"] = "0";
        snapshotConfig["Width"] = "200";
        snapshotConfig["Height"] = "200";
        snapshotConfig["FrameType"] = "normal";
    
        // The configurations of image sprites. The configurations must be based on those of common snapshots.
        Json::Value spriteSnapshotConfig;
        spriteSnapshotConfig["CellWidth"] = "120";
        spriteSnapshotConfig["CellHeight"] = "68";
        spriteSnapshotConfig["Columns"] = "3";
        spriteSnapshotConfig["Lines"] = "10";
        spriteSnapshotConfig["Padding"] = "20";
        spriteSnapshotConfig["Margin"] = "50";
        spriteSnapshotConfig["KeepCellPic"] = "keep";
        spriteSnapshotConfig["Color"] = "tomato";
        snapshotConfig["SpriteSnapshotConfig"] = spriteSnapshotConfig;
    
        // The configurations of common snapshots. The configurations are also used by image sprites.
        templateConfig["SnapshotConfig"] = snapshotConfig;
    
        // The type of the snapshot. Set the value to SpriteSnapshot for image sprites and to NormalSnapshot in other scenarios.
        templateConfig["SnapshotType"] = "SpriteSnapshot";
        return templateConfig;
    }
    
    /**
     * Modify a snapshot template.
     */
    VodApiResponse updateSnapshotVodTemplate(VodCredential authInfo) {
        string apiName = "UpdateVodTemplate";
        map<string, string> args;
        // The ID of the template that you want to modify.
        args["VodTemplateId"] = "53azf9d796fad9d7b862b2e****";
        // The name of the template.
        args["Name"] = "updatetest";
        // The template configurations.
        Json::Value templateConfig = buildSnapshotTemplateConfig();
        args["TemplateConfig"] = templateConfig.toStyledString();
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = updateSnapshotVodTemplate(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Delete a snapshot template {#h2--div-id-deletevodtemplate-div-4}
----------------------------------------------------------------

You can call the DeleteVodTemplate operation to delete a snapshot template.
For more information about the request and response parameters of this operation, see [DeleteVodTemplate](/intl.en-US/API Reference/Media processing/Snapshot template/DeleteVodTemplate.md). Example: 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    
    /**
     * Delete a snapshot template.
     */
    VodApiResponse deleteSnapshotVodTemplate(VodCredential authInfo) {
        string apiName = "DeleteVodTemplate";
        map<string, string> args;
        // The ID of the template that you want to delete.
        args["VodTemplateId"] = "53azf9d796fad9d7b862b2e****";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = deleteSnapshotVodTemplate(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Query snapshot templates {#h2--div-id-listvodtemplate-div-5}
------------------------------------------------------------

You can call the ListVodTemplate operation to query snapshot templates.
For more information about the request and response parameters of this operation, see [ListVodTemplate](/intl.en-US/API Reference/Media processing/Snapshot template/ListVodTemplate.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Query snapshot templates.
     */
    VodApiResponse listSnapshotVodTemplate(VodCredential authInfo) {
        string apiName = "ListVodTemplate";
        map<string, string> args;
        // The type of the template. Set the value to Snapshot.
        args["TemplateType"] = "Snapshot";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = listSnapshotVodTemplate(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Query a snapshot template {#h2--div-id-getvodtemplate-div-6}
------------------------------------------------------------

You can call the GetVodTemplate operation to query details about a snapshot template.
For more information about the request and response parameters of this operation, see [GetVodTemplate](/intl.en-US/API Reference/Media processing/Snapshot template/GetVodTemplate.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /**
    * Query details about a snapshot template.
    */
    VodApiResponse getSnapshotVodTemplate(VodCredential authInfo) {
        string apiName = "GetVodTemplate";
        map<string, string> args;
        // The ID of the template that you want to query.
        args["VodTemplateId"] = "53azf9d796fad9d7b862b2e****";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = getSnapshotVodTemplate(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



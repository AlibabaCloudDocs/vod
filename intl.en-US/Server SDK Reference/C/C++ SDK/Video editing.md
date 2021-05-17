Video editing 
==================================

This topic provides examples on how to use the API operations of the video editing module. The API operations are encapsulated in ApsaraVideo VOD SDK for C/C++. You can call the API operations to create, modify, and delete online editing projects. You can also query details about an online editing project, configure materials for an online project, and create a video assembly task.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/C/C++ SDK/Initialization.md).

Create a video assembly task based on a timeline {#h2--div-id-produceeditingprojectvideo-div-2}
-----------------------------------------------------------------------------------------------

You can call the ProduceEditingProjectVideo operation to create a video assembly task based on a timeline.
The timeline method is most commonly used to assemble videos. For more information about the request and response parameters of this operation, see [ProduceEditingProjectVideo](/intl.en-US/API Reference/Online editing/ProduceEditingProjectVideo.md). Example:
**Note**
For more examples on how to assemble videos based on timelines, see [Video assembly](/intl.en-US/Developer Guide/Online editing/Overview.md). {#h2--div-id-produceeditingprojectvideo-div-2}
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    Json::Value buildMediaMetadata(){
        Json::Value mediaMetadata;
        // Produce Media Title
        mediaMetadata["Title"] = "TestTitle";
        // Produce Media Description
        mediaMetadata["Description"] = "TestDescription";
        // Produce Media UserDefined Cover URL
        mediaMetadata["CoverURL"] = "http://192.168.0.0/16/media/cover/mediaid.jpg";
        // Produce Media Category ID
        mediaMetadata["CateId"] = "<your cateid>";
        // Produce Media Category Name
        mediaMetadata["Tags"] = "Tag1,Tag2";
        return mediaMetadata;
    }
    
    Json::Value buildProduceConfig(){
        Json::Value produceConfig;
        /*
        The produce process can generate media mezzanine file. You can use the mezzanine file to transcode other media files. This transcoding process is similar to that after file upload is finished. This field describe the Transocde TemplateGroup ID after produce mezzanine finished.
        1. Not required 
        2. Use default transcode template group id when empty
        */
        produceConfig["TemplateGroupId"] = "<your TemplateGroupId>";
        return produceConfig;
    }
    
    /**
    * This Sample shows how to merge two videos
    */
    Json::Value buildTimeline(){
        Json::Value timeline;
    
        // Video Track
        Json::Value videoTracks;
        Json::Value videoTrack;
        // Video Track Clips
        Json::Value videoTrackClips;
        Json::Value videoTrackClip1;
        videoTrackClip1["MediaId"] = "11119b4d7cf14dc7b83b0e801cbe****";
        videoTrackClips.append(videoTrackClip1);
        Json::Value videoTrackClip2;
        videoTrackClip2["MediaId"] = "22229b4d7cf14dc7b83b0e801cbe****";
        videoTrackClips.append(videoTrackClip2);
    
        videoTrack["VideoTrackClips"] = videoTrackClips;
        videoTracks.append(videoTrack);
    
        timeline["VideoTracks"] = videoTracks;
    
        return timeline;
    }
    
    VodApiResponse produceEditingProjectVideo(VodCredential authInfo) {
        string apiName = "ProduceEditingProjectVideo";
        map<string, string> args;
        args["Timeline"] = buildTimeline().toStyledString();
        args["MediaMetadata"] = buildMediaMetadata().toStyledString();
        args["ProduceConfig"] = buildProduceConfig().toStyledString();
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = produceEditingProjectVideo(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Create a video assembly task based on an online editing project {#h2--div-id-produceeditingprojectvideoprojectid-div-3}
-----------------------------------------------------------------------------------------------------------------------

You can call the ProduceEditingProjectVideo operation to create a video assembly task based on an online editing project.
If you have high requirements for online editing and management, we recommend that you use this method. For more information about the request and response parameters of this operation, see [ProduceEditingProjectVideo](/intl.en-US/API Reference/Online editing/ProduceEditingProjectVideo.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    Json::Value buildMediaMetadata(){
        Json::Value mediaMetadata;
        // Produce Media Title
        mediaMetadata["Title"] = "TestTitle";
        // Produce Media Description
        mediaMetadata["Description"] = "TestDescription";
        // Produce Media UserDefined Cover URL
        mediaMetadata["CoverURL"] = "http://192.168.0.0/16/media/cover/mediaid.jpg";
        // Produce Media Category ID
        mediaMetadata["CateId"] = "<your cateid>";
        // Produce Media Category Name
        mediaMetadata["Tags"] = "Tag1,Tag2";
        return mediaMetadata;
    }
    
    Json::Value buildProduceConfig(){
        Json::Value produceConfig;
        /*
        The produce process can generate media mezzanine file. You can use the mezzanine file to transcode other media files. This transcoding process is similar to that after file upload is finished. This field describe the Transocde TemplateGroup ID after produce mezzanine finished.
        1. Not required 
        2. Use default transcode template group id when empty
        */
        produceConfig["TemplateGroupId"] = "<your TemplateGroupId>";
        return produceConfig;
    }
    
    VodApiResponse produceEditingProjectVideo(VodCredential authInfo) {
        string apiName = "ProduceEditingProjectVideo";
        map<string, string> args;
        // Set Editing Project ID need to produce
        args["ProjectId"] = "<your ProjectId>";
        // Set Produce Media Metadata
        args["MediaMetadata"] = buildMediaMetadata().toStyledString();
        // Set Produce Configuration
        args["ProduceConfig"] = buildProduceConfig().toStyledString();
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = produceEditingProjectVideo(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Create an online editing project {#h2--div-id-addeditingproject-div-4}
----------------------------------------------------------------------

You can call the AddEditingProject operation to create an online editing project.
For more information about the request and response parameters of this operation, see [AddEditingProject](/intl.en-US/API Reference/Online editing/Project management for online editing/AddEditingProject.md). Example: 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /**
    * This Sample shows how to merge two videos
    */
    Json::Value buildTimeline(){
        Json::Value timeline;
    
        // Video Track
        Json::Value videoTracks;
        Json::Value videoTrack;
        // Video Track Clips
        Json::Value videoTrackClips;
        Json::Value videoTrackClip1;
        videoTrackClip1["MediaId"] = "11119b4d7cf14dc7b83b0e801cbe****";
        videoTrackClips.append(videoTrackClip1);
        Json::Value videoTrackClip2;
        videoTrackClip2["MediaId"] = "22229b4d7cf14dc7b83b0e801cbe****";
        videoTrackClips.append(videoTrackClip2);
    
        videoTrack["VideoTrackClips"] = videoTrackClips;
        videoTracks.append(videoTrack);
    
        timeline["VideoTracks"] = videoTracks;
    
        return timeline;
    }
    
    VodApiResponse addEditingProject(VodCredential authInfo) {
        string apiName = "AddEditingProject";
        map<string, string> args;
        // Build Editing Project Timeline
        args["Timeline"] = buildTimeline().toStyledString();
        // Set Editing Project Title
        args["Title"] = "Editing Project Title";
        // Set Editing Project Cover URL
        args["CoverURL"] = "http://192.168.0.0/16/editingproject/cover/projectid.jpg";
        // Set Editing Project Description
        args["Description"] = "Editing Project Description";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = addEditingProject(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Modify an online editing project {#h2--div-id-updateeditingproject-div-5}
-------------------------------------------------------------------------

You can call the UpdateEditingProject operation to modify an online editing project.
For more information about the request and response parameters of this operation, see [UpdateEditingProject](/intl.en-US/API Reference/Online editing/Project management for online editing/UpdateEditingProject.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /**
    * This Sample shows how to merge two videos
    */
    Json::Value buildTimeline(){
        Json::Value timeline;
    
        // Video Track
        Json::Value videoTracks;
        Json::Value videoTrack;
        // Video Track Clips
        Json::Value videoTrackClips;
        Json::Value videoTrackClip1;
        videoTrackClip1["MediaId"] = "11119b4d7cf14dc7b83b0e801cbe****";
        videoTrackClips.append(videoTrackClip1);
        Json::Value videoTrackClip2;
        videoTrackClip2["MediaId"] = "22229b4d7cf14dc7b83b0e801cbe****";
        videoTrackClips.append(videoTrackClip2);
    
        videoTrack["VideoTrackClips"] = videoTrackClips;
        videoTracks.append(videoTrack);
    
        timeline["VideoTracks"] = videoTracks;
    
        return timeline;
    }
    
    VodApiResponse updateEditingProject(VodCredential authInfo) {
        string apiName = "UpdateEditingProject";
        map<string, string> args;
        args["ProjectId"] = "YourProjectId";
        // Build Editing Project Timeline
        args["Timeline"] = buildTimeline().toStyledString();
        // Set Editing Project Title
        args["Title"] = "Editing Project Title";
        // Set Editing Project Cover URL
        args["CoverURL"] = "http://192.168.0.0/16/editingproject/cover/projectid.jpg";
        // Set Editing Project Description
        args["Description"] = "Editing Project Description";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = updateEditingProject(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Delete an online editing project {#h2--div-id-deleteeditingproject-div-6}
-------------------------------------------------------------------------

You can call the DeleteEditingProject operation to delete an online editing project.
For more information about the request and response parameters of this operation, see [DeleteEditingProject](/intl.en-US/API Reference/Online editing/Project management for online editing/DeleteEditingProject.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    VodApiResponse deleteEditingProject(VodCredential authInfo) {
        string apiName = "DeleteEditingProject";
        map<string, string> args;
        args["ProjectIds"] = "projectid1,projectid2";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = deleteEditingProject(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Query an online editing project {#h2--div-id-geteditingproject-div-7}
---------------------------------------------------------------------

You can call the GetEditingProject operation to query details about an online editing project.
For more information about the request and response parameters of this operation, see [GetEditingProject](/intl.en-US/API Reference/Online editing/Project management for online editing/GetEditingProject.md). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    VodApiResponse getEditingProject(VodCredential authInfo) {
        string apiName = "GetEditingProject";
        map<string, string> args;
        args["ProjectId"] = "your projectId";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = getEditingProject(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Search for online editing projects {#h2--div-id-searcheditingproject-div-8}
---------------------------------------------------------------------------

You can call the SearchEditingProject operation to search for online editing projects.
For more information about the request and response parameters of this operation, see [SearchEditingProject](/intl.en-US/API Reference/Online editing/Project management for online editing/SearchEditingProject.md). Example: 
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    VodApiResponse searchEditingProject(VodCredential authInfo) {
        string apiName = "SearchEditingProject";
        map<string, string> args;
        args["Title"] = "Title Keywords";
        args["StartTime"] = "2017-01-11T12:00:00Z";
        args["EndTime"] = "2017-01-12T12:00:00Z";
        args["PageSize"] = "10";
        args["PageNo"] = "1";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = searchEditingProject(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Configure materials for an online editing project {#h2--div-id-seteditingprojectmaterials-div-9}
------------------------------------------------------------------------------------------------

You can call the SetEditingProjectMaterials operation to configure materials for an online editing project.
For more information about the request and response parameters of this operation, see [SetEditingProjectMaterials](/intl.en-US/API Reference/Online editing/Project management for online editing/SetEditingProjectMaterials.md). Example: 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    VodApiResponse setEditingProjectMaterials(VodCredential authInfo) {
        string apiName = "SetEditingProjectMaterials";
        map<string, string> args;
        args["ProjectId"] = "<Your ProjectId>";
        args["MaterialIds"] = "materialId1,materialId2";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = setEditingProjectMaterials(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Query the materials of an online editing project {#h2--div-id-geteditingprojectmaterials-div-10}
------------------------------------------------------------------------------------------------

You can call the GetEditingProjectMaterials operation to query the materials of an online editing project.
For more information about the request and response parameters of this operation, see [GetEditingProjectMaterials](/intl.en-US/API Reference/Online editing/Project management for online editing/GetEditingProjectMaterials.md). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    VodApiResponse getEditingProjectMaterials(VodCredential authInfo) {
        string apiName = "GetEditingProjectMaterials";
        map<string, string> args;
        args["ProjectId"] = "<Your ProjectId>";
        args["Type"] = "video";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = getEditingProjectMaterials(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



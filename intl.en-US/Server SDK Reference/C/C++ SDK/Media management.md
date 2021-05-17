Media management 
=====================================

This topic provides examples on how to use the API operations of the media management module. The API operations are encapsulated in ApsaraVideo VOD SDK for C/C++. You can call the API operations to search for media asset information, modify video information, and query source file information. You can also query and delete videos and images.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/C/C++ SDK/Initialization.md).

Search for media asset information {#h2--div-id-searchmedia-div-2}
------------------------------------------------------------------

You can call the SearchMedia operation to search for media asset information.
For more information about the request and response parameters of this operation, see [SearchMedia](/intl.en-US/API Reference/Media asset management/Media asset search/SearchMedia.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Search for media asset information.
    */
    VodApiResponse searchMedia(VodCredential authInfo) {
        string apiName = "SearchMedia";
        map<string, string> args;
        args["Fields"] = "Title,CoverURL,Status";
        args["Match"] = "Status in ('Normal','Checking') and CreationTime = ('2018-07-01T08:00:00Z','2018-08-01T08:00:00Z')";
        args["PageNo"] = "1";
        args["PageSize"] = "10";
        args["SearchType"] = "video";
        args["SortBy"] = "CreationTime:Desc";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = searchMedia(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Query a video {#h2--div-id-getvideoinfo-div-3}
----------------------------------------------

You can call the GetVideoInfo operation to query details about a video.
For more information about the request and response parameters of this operation, see [GetVideoInfo](/intl.en-US/API Reference/Media asset management/Audio and video management/GetVideoInfo.md). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Query details about a video.
    */
    VodApiResponse getVideoInfo(VodCredential authInfo) {
        string apiName = "GetVideoInfo";
        map<string, string> args;
        args["VideoId"] = "<VideoId>";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = getVideoInfo(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Query videos by using filter conditions {#h2--div-id-getvideoinfos-div-4}
-------------------------------------------------------------------------

You can call the GetVideoInfos operation to query videos by using filter conditions.
For more information about the request and response parameters of this operation, see [GetVideoInfos](/intl.en-US/API Reference/Media asset management/Audio and video management/GetVideoInfos.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Query videos.
    */
    VodApiResponse getVideoInfos(VodCredential authInfo) {
        string apiName = "GetVideoInfos";
        map<string, string> args;
        args["VideoIds"] = "VideoId1,VideoId2";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = getVideoInfos(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Modify the information about a video {#h2--div-id-updatevideoinfo-div-5}
------------------------------------------------------------------------

You can call the UpdateVideoInfo operation to modify the information about a video.
For more information about the request and response parameters of this operation, see [UpdateVideoInfo](/intl.en-US/API Reference/Media asset management/Audio and video management/UpdateVideoInfo.md). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Modify the information about a video.
    */
    VodApiResponse updateVideoInfo(VodCredential authInfo) {
        string apiName = "UpdateVideoInfo";
        map<string, string> args;
        args["VideoId"] = "VideoId";
        args["Title"] = "new Title";
        args["Description"] = "new Description";
        args["Tags"] = "new Tag1,new Tag2";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = updateVideoInfo(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Modify the information about videos {#h2--div-id-updatevideoinfos-div-6}
------------------------------------------------------------------------

You can call the UpdateVideoInfos operation to modify the information about videos.
For more information about the request and response parameters of this operation, see [UpdateVideoInfos](/intl.en-US/API Reference/Media asset management/Audio and video management/UpdateVideoInfos.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Modify the information about videos.
    */
    VodApiResponse updateVideoInfos(VodCredential authInfo) {
        string apiName = "UpdateVideoInfos";
        map<string, string> args;
        Json::Value updateContentArray;
        Json::Value updateContent1;
        updateContent1["VideoId"] = "VideoId1";
        // updateContent1["Title"] = "new Title";
        // updateContent1["Tags"] = "new Tag1,new Tag2";
        updateContentArray.append(updateContent1);
        Json::Value updateContent2;
        updateContent2["VideoId"] = "VideoId2";
        // updateContent2["Title"] = "new Title";
        // updateContent2["Tags"] = "new Tag1,new Tag2";
        updateContentArray.append(updateContent2);
        args["UpdateContent"] = updateContentArray.toStyledString();
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = updateVideoInfos(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Delete videos {#h2--div-id-deletevideo-div-7}
---------------------------------------------

You can call the DeleteVideo operation to delete videos.
For more information about the request and response parameters of this operation, see [DeleteVideo](/intl.en-US/API Reference/Media asset management/Audio and video management/DeleteVideo.md). Example: 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Delete videos.
    */
    VodApiResponse deleteVideo(VodCredential authInfo) {
        string apiName = "DeleteVideo";
        map<string, string> args;
        // Separate multiple IDs with commas (,).
        args["VideoIds"] = "VideoId1,VideoId2";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = deleteVideo(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Query source file information (including the file URL) {#h2--div-id-getmezzanineinfo-div-8}
-------------------------------------------------------------------------------------------

You can call the GetMezzanineInfo operation to query source file information.
For more information about the request and response parameters of this operation, see [GetMezzanineInfo](/intl.en-US/API Reference/Media asset management/Audio and video management/GetMezzanineInfo.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Query source file information.
    */
    VodApiResponse getMezzanineInfo(VodCredential authInfo) {
        string apiName = "GetMezzanineInfo";
        map<string, string> args;
        args["VideoId"] = "<VideoId>";
        // The expiration time of the file URL, in seconds.
        args["AuthTimeout"] = "3600";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = getMezzanineInfo(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Query videos {#h2--div-id-getvideolist-div-9}
---------------------------------------------

You can call the GetVideoList operation to query videos 
For more information about the request and response parameters of this operation, see [GetVideoList](/intl.en-US/API Reference/Media asset management/Audio and video management/GetVideoList.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Query videos.
    */
    VodApiResponse getVideoList(VodCredential authInfo) {
        string apiName = "GetVideoList";
        map<string, string> args;
        args["PageNo"] = "1";
        args["PageSize"] = "20";
        args["StartTime"] = "2018-12-27T09:00:38Z";
        args["EndTime"] = "2018-12-28T09:00:38Z";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = getVideoList(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Delete a media stream {#h2--div-id-deletestream-div-10}
-------------------------------------------------------

You can call the DeleteStream operation to delete a media stream.
For more information about the request and response parameters of this operation, see [DeleteStream](/intl.en-US/API Reference/Media asset management/Audio and video management/DeleteStream.md). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Delete a media stream.
    */
    VodApiResponse deleteStream(VodCredential authInfo) {
        string apiName = "DeleteStream";
        map<string, string> args;
        args["VideoId"] = "<VideoId>";
        args["JobIds"] = "JobId1,JobId2";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = deleteStream(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Delete source files {#h2--div-id-deletemezzanines-div-11}
---------------------------------------------------------

You can call the DeleteMezzanines operation to delete source files.
For more information about the request and response parameters of this operation, see [DeleteMezzanines](/intl.en-US/API Reference/Media asset management/Audio and video management/DeleteMezzanines.md). Example: 
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Delete source files.
    */
    VodApiResponse deleteMezzanines(VodCredential authInfo) {
        string apiName = "DeleteMezzanines";
        map<string, string> args;
        args["VideoIds"] = "VideoId1,VideoId2";
        args["Force"] = "false";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = deleteMezzanines(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Modify the information about images {#h2--div-id-updateimageinfos-div-12}
-------------------------------------------------------------------------

You can call the UpdateImageInfos operation to modify the information about images.
For more information about the request and response parameters of this operation, see [UpdateImageInfos](/intl.en-US/API Reference/Media asset management/Image management/UpdateImageInfos.md). Example: 
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Modify the information about images.
    */
    VodApiResponse updateImageInfos(VodCredential authInfo) {
        string apiName = "UpdateImageInfos";
        map<string, string> args;
        Json::Value updateContentArray;
        Json::Value updateContent1;
        updateContent1["ImageId"] = "ImageId1";
        // updateContent1["Title"] = "new Title";
        // updateContent1["Tags"] = "new Tag1,new Tag2";
        updateContentArray.append(updateContent1);
        Json::Value updateContent2;
        updateContent2["ImageId"] = "ImageId2";
        // updateContent2["Title"] = "new Title";
        // updateContent2["Tags"] = "new Tag1,new Tag2";
        updateContentArray.append(updateContent2);
        args["UpdateContent"] = updateContentArray.toStyledString();
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = updateImageInfos(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Query an image {#h2--div-id-getimageinfo-div-13}
------------------------------------------------

You can call the GetImageInfo operation to query details about an image.
For more information about the request and response parameters of this operation, see [GetImageInfo](/intl.en-US/API Reference/Media asset management/Image management/GetImageInfo.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Query an image.
    */
    VodApiResponse getImageInfo(VodCredential authInfo) {
        string apiName = "GetImageInfo";
        map<string, string> args;
        args["ImageId"] = "<ImageId>";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = getImageInfo(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Delete images {#h2--div-id-deleteimage-div-14}
----------------------------------------------

You can call the DeleteImage operation to delete images.
For more information about the request and response parameters of this operation, see [DeleteImage](/intl.en-US/API Reference/Media asset management/Image management/DeleteImage.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Delete images.
    */
    VodApiResponse deleteImage(VodCredential authInfo) {
        string apiName = "DeleteImage";
        map<string, string> args;
        // Delete an image file based on ImageURL.
        args["DeleteImageType"] = "ImageURL";
        args["ImageURLs"] = "http://sample.192.168.0.0/16/cover.jpg";    
        // Delete image files based on ImageId.
        args["DeleteImageType"] = "ImageId";
        args["ImageIds"] = "ImageId1,ImageId2";
        // Delete image files based on VideoId and ImageType.
        args["DeleteImageType"] = "VideoId";
        args["VideoId"] = "<VideoId>";
        args["ImageType"] = "SpriteSnapshot";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = deleteImage(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



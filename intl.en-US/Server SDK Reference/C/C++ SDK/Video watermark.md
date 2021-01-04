Video watermark 
====================================

This topic provides examples on how to use the API operations of the video watermark module. The API operations are encapsulated in ApsaraVideo VOD SDK for C/C++. You can call the API operations to create, modify, delete, and query watermarks. You can also specify a watermark as the default one.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/C/C++ SDK/Initialization.md).

Create a watermark {#h2--div-id-addwatermark-div-2}
---------------------------------------------------

You can call the AddWatermark operation to create a watermark.
For more information about the request and response parameters of this operation, see [AddWatermark](/intl.en-US/API Reference/Media processing/Video Watermark/AddWatermark.md). Example:
**Note**

* For more information about how to query the upload URL and credential, see [CreateUploadAttachedMedia](/intl.en-US/API Reference/Media upload/CreateUploadAttachedMedia.md).


* For more information about how to upload a watermark file to an Object Storage Service (OSS) bucket, see [Upload OSS objects](/intl.en-US/API Reference/Media upload/Upload OSS objects.md).


 {#h2--div-id-addwatermark-div-2}
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Build the parameters of an image watermark. Configure the parameters as required.
     */
    Json::Value buildImageWatermarkConfig() {
        Json::Value watermarkConfig;
        // The horizontal offset of the watermark on the output video.
        watermarkConfig["Dx"] = "8";
        // The vertical offset of the watermark on the output video.
        watermarkConfig["Dy"] = "8";
        // The width of the watermark on the output video.
        watermarkConfig["Width"] = "55";
        // The height of the watermark on the output video.
        watermarkConfig["Height"] = "55";
        // The approximate position of the watermark relative to the output video. The watermark can be in the upper-left corner, upper-right corner, lower-left corner, or lower-right corner.
        watermarkConfig["ReferPos"] = "BottomRight";
        // The timeline of the watermark display. You can specify the start time and duration for the watermark display.
        Json::Value timeline;
        // The start time for the watermark display.
        timeline["Start"] = "2";
        // The duration for the watermark display.
        timeline["Duration"] = "ToEND";
        watermarkConfig["Timeline"] = timeline;
        return watermarkConfig;
    }
    
    /**
     * Build the parameters of a text watermark. Configure the parameters as required.
     */
    Json::Value buildTextWatermarkConfig() {
        Json::Value watermarkConfig;
        // The text to use as the watermark.
        watermarkConfig["Content"] = "testwatermark";
        // The font to use for the watermark.
        watermarkConfig["FontName"] = "SimSun";
        // The font size to use for the watermark.
        watermarkConfig["FontSize"] = "25";
        // The font color to use for the watermark. You can specify a color name or RGB color code, such as #000000.
        watermarkConfig["FontColor"] = "Black";
        // The transparency to use for the watermark.
        watermarkConfig["FontAlpha"] = "0.2";
        // The stroke color to use for the watermark. You can specify a color name or RGB color code, such as #ffffff.
        watermarkConfig["BorderColor"] = "White";
        // The stroke width to use for the watermark.
        watermarkConfig["BorderWidth"] = "1";
        // The distance between the upper-left vertex of the watermark and the upper edge of the output video.
        watermarkConfig["Top"] = "20";
        // The distance between the upper-left vertex of the watermark and the left edge of the output video.
        watermarkConfig["Left"] = "15";
        return watermarkConfig;
    }
    
    /**
     * Create a watermark.
     */
    VodApiResponse addWatermark(VodCredential authInfo) {
        string apiName = "AddWatermark";
        map<string, string> args;
        // The name of the watermark.
        args["Name"] = "testaddwatermark";
        // Query the URL of the watermark file that is stored in an OSS bucket.
        string fileUrl = "http://test-bucket.oss-cn-shanghai.aliyuncs.com/watermark/test.png";
        // If you want to create an image watermark, you must specify the URL of the watermark file. The OSS bucket that stores the watermark file must reside in the same region as the region where the video is stored. For example, if a video is stored in the China (Shanghai) region, it can use only a watermark file that is stored in the same region.
        args["FileUrl"] = fileUrl;
        // The configurations of the watermark.
        Json::Value watermarkConfig;
        // The position configurations of the image watermark.
        watermarkConfig = buildImageWatermarkConfig();
        // The position configurations of the text watermark.
        //watermarkConfig = buildTextWatermarkConfig();
        args["WatermarkConfig"] = watermarkConfig.toStyledString();
        // The type of the watermark. Set the value to Text for text watermarks and Image for image watermarks.
        args["Type"] = "Image";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = addWatermark(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Modify a watermark {#h2--div-id-updatewatermark-div-3}
------------------------------------------------------

You can call the UpdateWatermark operation to modify a watermark.
For more information about the request and response parameters of this operation, see [UpdateWatermark](/intl.en-US/API Reference/Media processing/Video Watermark/UpdateWatermark.md). Example: {#h2--div-id-updatewatermark-div-3}
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Build the parameters of an image watermark. Configure the parameters as required.
     */
    Json::Value buildImageWatermarkConfig() {
        Json::Value watermarkConfig;
        // The horizontal offset of the watermark on the output video.
        watermarkConfig["Dx"] = "8";
        // The vertical offset of the watermark on the output video.
        watermarkConfig["Dy"] = "8";
        // The width of the watermark on the output video.
        watermarkConfig["Width"] = "55";
        // The height of the watermark on the output video.
        watermarkConfig["Height"] = "55";
        // The approximate position of the watermark relative to the output video. The watermark can be in the upper-left corner, upper-right corner, lower-left corner, or lower-right corner.
        watermarkConfig["ReferPos"] = "BottomRight";
        // The timeline of the watermark display. You can specify the start time and duration for the watermark display.
        Json::Value timeline;
        // The start time for the watermark display.
        timeline["Start"] = "2";
        // The duration for the watermark display.
        timeline["Duration"] = "ToEND";
        watermarkConfig["Timeline"] = timeline;
        return watermarkConfig;
    }
    
    /**
     * Build the parameters of a text watermark. Configure the parameters as required.
     */
    Json::Value buildTextWatermarkConfig() {
        Json::Value watermarkConfig;
        // The text to use as the watermark.
        watermarkConfig["Content"] = "testwatermark";
        // The font to use for the watermark.
        watermarkConfig["FontName"] = "SimSun";
        // The font size to use for the watermark.
        watermarkConfig["FontSize"] = "25";
        // The font color to use for the watermark. You can specify a color name or RGB color code, such as #000000.
        watermarkConfig["FontColor"] = "Black";
        // The transparency to use for the watermark.
        watermarkConfig["FontAlpha"] = "0.2";
        // The stroke color to use for the watermark. You can specify a color name or RGB color code, such as #ffffff.
        watermarkConfig["BorderColor"] = "White";
        // The stroke width to use for the watermark.
        watermarkConfig["BorderWidth"] = "1";
        // The distance between the upper-left vertex of the watermark and the upper edge of the output video.
        watermarkConfig["Top"] = "20";
        // The distance between the upper-left vertex of the watermark and the left edge of the output video.
        watermarkConfig["Left"] = "15";
        return watermarkConfig;
    }
    
    /**
     * Modify a watermark.
     * Note: The file URL of an image watermark cannot be modified. If you want to modify the URL, you must create an image watermark.
     */
    VodApiResponse updateWatermark(VodCredential authInfo) {
        string apiName = "UpdateWatermark";
        map<string, string> args;
        // The ID of the watermark for which you want to modify the configurations.
        args["WatermarkId"] = "421ddddd4f6e734a526fd2e****;
        // The configurations of the watermark.
        Json::Value watermarkConfig;
        // The position configurations of the image watermark.
        watermarkConfig = buildImageWatermarkConfig();
        // The position configurations of the text watermark.
        //watermarkConfig = buildTextWatermarkConfig();
        args["WatermarkConfig"] = watermarkConfig.toStyledString();
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = updateWatermark(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Delete a watermark {#h2--div-id-deletewatermark-div-4}
------------------------------------------------------

You can call the DeleteWatermark operation to delete a watermark.
For more information about the request and response parameters of this operation, see [DeleteWatermark](/intl.en-US/API Reference/Media processing/Video Watermark/DeleteWatermark.md). Example: {#h2--div-id-deletewatermark-div-4}
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Delete a watermark.
     */
    VodApiResponse deleteWatermark(VodCredential authInfo) {
        string apiName = "DeleteWatermark";
        map<string, string> args;
        args["WatermarkId"] = "53f9d796fad9d7b862b2e5****;
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = deleteWatermark(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Query watermarks {#h2--div-id-listwatermark-div-5}
--------------------------------------------------

You can call the ListWatermark operation to query watermarks.
For more information about the request and response parameters of this operation, see [ListWatermark](/intl.en-US/API Reference/Media processing/Video Watermark/ListWatermark.md). Example: {#h2--div-id-listwatermark-div-5}
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Query watermarks.
     */
    VodApiResponse listWatermark(VodCredential authInfo) {
        string apiName = "ListWatermark";
        map<string, string> args;
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = listWatermark(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Query a watermark {#h2--div-id-getwatermark-div-6}
--------------------------------------------------

You can call the GetWatermark operation to query details about a watermark.
For more information about the request and response parameters of this operation, see [GetWatermark](/intl.en-US/API Reference/Media processing/Video Watermark/GetWatermark.md). Example: {#h2--div-id-getwatermark-div-6}
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Query details about a watermark.
     */
    VodApiResponse getWatermark(VodCredential authInfo) {
        string apiName = "GetWatermark";
        map<string, string> args;
        args["WatermarkId"] = "96d4f6e734a526fd2****";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = getWatermark(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Specify a watermark as the default one {#h2--div-id-setdefaultwatermark-div-7}
------------------------------------------------------------------------------

You can call the SetDefaultWatermark operation to specify a watermark as the default one.
For more information about the request and response parameters of this operation, see [SetDefaultWatermark](/intl.en-US/API Reference/Media processing/Video Watermark/SetDefaultWatermark.md). Example: {#h2--div-id-setdefaultwatermark-div-7}
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Specify a watermark as the default one.
     */
    VodApiResponse setDefaultWatermark(VodCredential authInfo) {
        string apiName = "SetDefaultWatermark";
        map<string, string> args;
        args["WatermarkId"] = "96d4f6e734a526fd2****";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = setDefaultWatermark(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



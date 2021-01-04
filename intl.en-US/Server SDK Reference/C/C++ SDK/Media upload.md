Media upload 
=================================

This topic provides examples on how to use the API operations of the media upload module. The API operations are encapsulated in ApsaraVideo VOD SDK for C/C++. You can call the API operations to create upload URLs and credentials. You can also register media assets. To upload the complete media files, you can use the client SDK for C/C++ or the upload server SDK for C/C++.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/C/C++ SDK/Initialization.md).

Create a URL and a credential for uploading videos {#h2--div-id-createuploadvideo-div-2}
----------------------------------------------------------------------------------------

You can call the CreateUploadVideo operation to create a URL and a credential for uploading videos.
For more information about the request and response parameters of this operation, see [CreateUploadVideo](/intl.en-US/API Reference/Media upload/CreateUploadVideo.md). Example: 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Create a URL and a credential for uploading videos.
    */
    VodApiResponse createUploadVideo(VodCredential authInfo) {
        string apiName = "CreateUploadVideo";
        map<string, string> args;
        args["Title"] = "sample title";
        args["FileName"] = "filename.mp4";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = createUploadVideo(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Refresh the credential for uploading videos {#h2--div-id-refreshuploadvideo-div-3}
----------------------------------------------------------------------------------

You can call the RefreshUploadVideo operation to refresh the credential for uploading videos.
For more information about the request and response parameters of this operation, see [RefreshUploadVideo](/intl.en-US/API Reference/Media upload/RefreshUploadVideo.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Refresh the credential for uploading videos.
    */
    VodApiResponse refreshUploadVideo(VodCredential authInfo) {
        string apiName = "RefreshUploadVideo";
        map<string, string> args;
        args["VideoId"] = "<VideoId>"; // The ID of the video for which you want to refresh the credential.
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = refreshUploadVideo(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Create a URL and a credential for uploading images {#h2--div-id-createuploadimage-div-4}
----------------------------------------------------------------------------------------

You can call the CreateUploadImage operation to create a URL and a credential for uploading images.
For more information about the request and response parameters of this operation, see [CreateUploadImage](/intl.en-US/API Reference/Media upload/CreateUploadImage.md). Example: 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Create a URL and a credential for uploading images.
    */
    
    VodApiResponse createUploadImage(VodCredential authInfo) {
        string apiName = "CreateUploadImage";
        map<string, string> args;
        args["ImageType"] = "cover";
        args["ImageExt"] = "jpg";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = createUploadImage(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Create a URL and a credential for uploading attached media assets {#h2--div-id-createuploadattachedmedia-div-5}
---------------------------------------------------------------------------------------------------------------

You can call the CreateUploadAttachedMedia operation to create a URL and a credential for uploading attached media assets.
For more information about the request and response parameters of this operation, see [CreateUploadAttachedMedia](/intl.en-US/API Reference/Media upload/CreateUploadAttachedMedia.md). Example: 
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Create a URL and a credential for uploading attached media assets, such as watermarks and subtitles.
     */
    
    VodApiResponse createUploadAttachedMedia(VodCredential authInfo) {
        string apiName = "CreateUploadAttachedMedia";
        map<string, string> args;
        args["BusinessType"] = "watermark";
        args["MediaExt"] = "gif";
        args["Title"] = "this is a sample title";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = createUploadAttachedMedia(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Upload media files by using a source file URL {#h2-url-div-id-uploadmediabyurl-div-6}
-------------------------------------------------------------------------------------

You can call the UploadMediaByURL operation to upload media files by using a source file URL.
For more information about the request and response parameters of this operation, see [UploadMediaByURL](/intl.en-US/API Reference/Media upload/UploadMediaByURL.md). Example: 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Upload media files by using a source file URL.
    */
    
    VodApiResponse uploadMediaByURL(VodCredential authInfo) {
        string apiName = "UploadMediaByURL";
        map<string, string> args;
        args["UploadURLs"] = "http://192.168.0.0/16.mp4";
        Json::Value uploadMetadataList;
        Json::Value uploadMetadata;
        uploadMetadata["SourceUrl"] = "http://192.168.0.0/16.mp4";
        uploadMetadata["Title"] = "upload by url sample";
        uploadMetadataList.append(uploadMetadata);
        args["UploadMetadatas"] = uploadMetadataList.toStyledString();
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = uploadMediaByURL(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Register media assets {#h2--div-id-registermedia-div-7}
-------------------------------------------------------

You can call the RegisterMedia operation to register media assets.
For more information about the request and response parameters of this operation, see [RegisterMedia](/intl.en-US/API Reference/Media upload/RegisterMedia.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Register media assets.
    */
    
    VodApiResponse registerMedia(VodCredential authInfo) {
        string apiName = "RegisterMedia";
        map<string, string> args;
        Json: Value metaDataArray;
        Json: Value metaData;
        metaData["Title"] = "this is a sample";
        metaData["FileURL"] = "https://192.168.0.0/16/vod_sample.mp4";
        metaDataArray.append(metaData);
        args["RegisterMetadatas"] = metaDataArray.toStyledString();
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = registerMedia(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



# Upload SDK for C or C++

You can use the upload SDKs of ApsaraVideo VOD to upload media files with efficiency. This topic provides an example to describe how to use the upload SDK for C or C++.

## Features

The upload SDK provides the following major features:

-   Allows you to upload various types of media files to ApsaraVideo VOD, including video and audio files, images, and auxiliary media assets such as watermarks and subtitle files.
-   Allows you to upload on-premises media files: By default, multipart upload is used. A single file to upload can be up to 48.8 TB in size. Resumable upload is supported.
-   Allows you to upload online media files to ApsaraVideo VOD: A single file to upload can be up to 48.8 TB in size. Online media files are downloaded to on-premises temporary directories and then uploaded to ApsaraVideo VOD. Resumable upload is not supported.
-   Allows you to upload M3U8 video files: ApsaraVideo VOD provides an operation to parse the M3U8 index files to obtain the lists of part URLs. You can also specify the URLs of part files as needed.

The upload SDK provides the following additional features:

-   Provides an upload progress bar and supports the callbacks for default and custom upload progress.
-   Allows you to specify the region of an Elastic Compute Service \(ECS\) instance on which the upload script is to be deployed. If the region of the ECS instance is the same as the storage region in ApsaraVideo VOD, the specified file is automatically uploaded by using an internal network. This can accelerate the upload speed and save the public network traffic.
-   Allows you to specify the VOD center and storage region to facilitate upload outside China. The default VOD center is in the China \(Shanghai\) region.
-   Allows you to set the metadata, such as the title, storage locations, user data, and transcoding templates for the upload.

For more information about the file formats that are supported by ApsaraVideo VOD, see the "Supported file formats" section of [Overview](/intl.en-US/Developer Guide/Upload Medias/Overview.md).

## Prerequisites

The upload SDK for C or C++ shares the same prerequisites, installation method, and initialization method with the server SDK for C or C++. For more information, see [C/C++ SDK](/intl.en-US/Server SDK Reference/C/C++ SDK/Installation.md).

## Install the SDK

1.  Download the VodSDK-C\_1.0.0.gz package, which contains the upload SDK for C or C++ and sample code. For more information, see [SDK download](/intl.en-US/SDK Downloads/SDK download.md).

    **Note:** In this topic, the SDK V1.0.0 is used as an example. You can use other versions based on your business requirements.

2.  Install the upload SDK for C or C++ based on the installation method of the server SDK for C or C++. For more information, see [Installation](/intl.en-US/Server SDK Reference/C/C++ SDK/Installation.md).


## Update the SDK

If new operations or new features of existing operations are unavailable in the current SDK, download the latest version of the SDK, extract files, and then save them by replacing existing ones. For more information, see [SDK download](/intl.en-US/SDK Downloads/SDK download.md).

**Note:** You can check the version number and release date of the current SDK in the first line of the ChangeLog.txt file in the aliyun-c-sdk-vod directory.

## Description of directories

-   /VodSDK-C\_1.0.0.gz decompress directory/VodSDK-C\_1.0.0/aliyun-c-sdk-vod/src/upload.h
    -   CreateUploadVideoRequest: the request class for uploading videos. For more information about the parameters, see [CreateUploadVideo](/intl.en-US/API Reference/Media upload/CreateUploadVideo.md).
    -   CreateUploadImageRequest: the request class for uploading images. For more information about the parameters, see [CreateUploadImage](/intl.en-US/API Reference/Media upload/CreateUploadImage.md).
    -   CreateUploadAttachedMediaRequest: the request class for uploading auxiliary media assets. For more information about the parameters, see [CreateUploadAttachedMedia](/intl.en-US/API Reference/Media upload/CreateUploadAttachedMedia.md).
    -   UploadOptions: the upload parameter structure. It contains the following parameters:
        -   void \(\*uploadProgressCallback\) \(int64\_t, int64\_t\): customizes the callbacks for upload progress. If you do not set this parameter, the default callback is used. If you set this parameter to Null, no callback for upload progress will be fired.
        -   ecsRegionId: specifies the region of the ECS instance on which the upload script is to be deployed. If the region of the ECS instance is the same as the storage region in ApsaraVideo VOD, the file is automatically uploaded over the internal network.
        -   multipartUploadLimit: specifies the threshold of the file size based on which multipart upload starts, in bytes. The default value is 10 MB. This parameter is valid only for the upload of videos.
        -   multipartUploadOnceSize: specifies the size of each part in multipart upload, in bytes. The default value is 10 MB. This parameter is valid only for the upload of videos.
        -   tmpDir: specifies an on-premises temporary directory for storing the downloaded online files. This parameter is valid only for the upload of online files.
    -   uploadLocalVideo: a method used to upload on-premises videos.
    -   uploadWebVideo: a method used to upload online videos.
    -   uploadLocalImage: a method used to upload on-premises images.
    -   uploadWebImage: a method used to upload online images.
    -   uploadLocalAttachedMedia: a method used to upload on-premises auxiliary media assets.
    -   uploadWebAttachedMedia: a method used to upload online auxiliary media assets.
    -   uploadLocalM3u8: a method used to upload on-premises M3U8 videos.
    -   uploadWebM3u8: a method used to upload online M3U8 videos.
-   /VodSDK-C\_1.0.0.gz decompress directory/VodSDK-C\_1.0.0/aliyun-c-sdk-vod/samples directory
    -   uploadVideo.cpp: provides the sample code for uploading videos.
    -   uploadImage.cpp: provides the sample code for uploading images.
    -   uploadAttachedMedia.cpp: provides the sample code for uploading auxiliary media assets.

## Sample code

The following sample code shows you how to upload an on-premises video and an online video:

```
void testCallback(int64_t consumed_bytes, int64_t total_bytes)
{
    printf("total :%ld, %ld\n", consumed_bytes, total_bytes);
}
// Test the upload of an on-premises video.
VodApiResponse testUploadLocalVideo(VodCredential authInfo) {
    CreateUploadVideoRequest request;
    request.fileName = "testLocal.mp4";
    request.title = "testUploadLocalVideo";
    request.cateId = "1";
    request.coverURL = "http://xxxx.jpg";
    request.tags = "test1,test2";
    request.templateGroupId = "6ae347b0140181ad371d197ebe28****";
    requests.torageLocation. = "outin-xx.oss-cn-beijing.aliyuncs.com";
    Json::Value userData;
    Json::Value callbackUrl;
    callbackUrl["CallbackURL"] = "https://demo.sample.com/ProcessMessageCallback";
    userData["MessageCallback"] = callbackUrl;
    Json::Value extend;
    extend["localId"] = "xxx";
    extend["test"] = "www";
    userData["Extend"] = extend;
    request.userData = userData.toStyledString();
    UploadOptions uploadOptions;
    // Specify the region of the ECS instance on which the upload script is to be deployed. If the region of the ECS instance is the same as the storage region in ApsaraVideo VOD, the file is automatically uploaded over the internal network.
    //uploadOptions.ecsRegionId = "cn-shanghai";
    // Customize the callback for upload progress. If you do not set this parameter, the default callback is used. If you set this parameter to Null, no callback for upload progress will be fired.
    //uploadOptions.uploadProgressCallback = testCallback;
    //uploadOptions.multipartUploadLimit = 20*1024*1024;// Specify the threshold of the file size based on which multipart upload starts.
    //uploadOptions.multipartUploadOnceSize = 10*1024*1024;// Specifies the size of each part in multipart upload.
    VodApiResponse result = uploadLocalVideo(authInfo, request, "./test.mp4", uploadOptions);
    return result;
}
// Tests the upload of an online video.
VodApiResponse testUploadWebVideo(VodCredential authInfo) {
    CreateUploadVideoRequest request;
    request.fileName = "testWeb.mp4";
    request.title = "testUploadWebVideo";
    UploadOptions uploadOptions;
    // Specify the region of the ECS instance on which the upload script is to be deployed. If the region of the ECS instance is the same as the storage region in ApsaraVideo VOD, the file is automatically uploaded over the internal network.
    //uploadOptions.ecsRegionId = "cn-shanghai";
    // Customize the callback for upload progress. If you do not set this parameter, the default callback is used. If you set this parameter to Null, no callback for upload progress will be fired.
    //uploadOptions.uploadProgressCallback = testCallback;
    //uploadOptions.multipartUploadLimit = 20*1024*1024;// Specify the threshold of the file size based on which multipart upload starts.
    //uploadOptions.multipartUploadOnceSize = 10*1024*1024;// Specifies the size of each part in multipart upload.
    // Specifies an on-premises temporary directory for storing the downloaded online files. The default value is /tmp/.
    //uploadOptions.tmpDir = "/tmp/";
    VodApiResponse result = uploadWebVideo(authInfo, request, "<Your Download Url>", uploadOptions);
    return result;
}
// Test the upload of an on-premises M3U8 video.
VodApiResponse testUploadLocalM3u8(VodCredential authInfo) {
    CreateUploadVideoRequest request;
    request.fileName = "testLocal.m3u8";
    request.title = "testUploadLocalM3u8";
    list<string> tsList;
    // Note: If you do not specify the URLs of parts, the file is automatically parsed.
    //tsList.push_back("/tmp/1.ts");
    UploadOptions uploadOptions;
    VodApiResponse result = uploadLocalM3u8(authInfo, request, "./test.m3u8", tsList, uploadOptions);
    return result;
}
// Test the upload of an online M3U8 video.
VodApiResponse testUploadWebM3u8(VodCredential authInfo) {
    CreateUploadVideoRequest request;
    request.fileName = "testWeb.m3u8";
    request.title = "testUploadWebM3u8";
    list<string> tsList;
    // Note: If you do not specify the URLs of parts, the file is automatically parsed.
    //tsList.push_back("<Ts1 Download Url>");
    //tsList.push_back("<Ts2 Download Url>");
    UploadOptions uploadOptions;
    VodApiResponse result = uploadWebM3u8(authInfo, request, "<Your M3u8 Download Url>", tsList, uploadOptions);
    return result;
}
####   Run the test code.   ####
VodCredential initVodClient(std::string accessKeyId, std::string accessKeySecret) {
    VodCredential authInfo;
    authInfo.accessKeyId = accessKeyId;
    authInfo.accessKeySecret = accessKeySecret;
    authInfo.regionId = "cn-shanghai";
    return authInfo;
}
int main(int argc, char * argv[]) {
    VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    VodApiResponse response;
    response = testUploadLocalVideo(authInfo);
    //response = testUploadWebVideo(authInfo);
    //response = testUploadLocalM3u8(authInfo);
    //response = testUploadWebM3u8(authInfo);
    printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
}
```

For more sample code, see the files in the samples directory.


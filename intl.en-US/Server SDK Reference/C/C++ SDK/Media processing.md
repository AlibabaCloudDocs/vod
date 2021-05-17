Media processing 
=====================================

This topic provides examples on how to use the API operations of the media processing module. The API operations are encapsulated in ApsaraVideo VOD SDK for C/C++. You can call the API operations to submit transcoding jobs and snapshot jobs. You can also query snapshot jobs and preprocess videos in production studios.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/C/C++ SDK/Initialization.md).

Submit transcoding jobs {#h2--div-id-submittranscodejobs-div-2}
---------------------------------------------------------------

You can call the SubmitTranscodeJobs operation to submit transcoding jobs.
For more information about the request and response parameters of this operation, see [SubmitTranscodeJobs](/intl.en-US/API Reference/Media processing/Process initiation/SubmitTranscodeJobs.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * 1. Build overriding parameters, which override only the file URL of an image watermark or the content of a text watermark.
     * 2. Make sure that the ID of the watermark is associated with the ID of the transcoding template that you use. The ID of the transcoding template is specified by TranscodeTemplateId.
     * 3. You can call this operation to add only a watermark whose ID is associated with the ID of the transcoding template that you use.
     * Note: The watermark file and the video must be stored on the same origin server.
     */
    Json::Value buildOverrideParams() {
        Json::Value overrideParams;
        Json::Value watermarks;
        Json::Value watermark1;
        watermark1["WatermarkId"] = "2ea587477c5a1bc8b57****";
        // The file URL of the new image that is stored in an Object Storage Service (OSS) bucket. The new image and the video must be stored on the same origin server.
        watermark1["FileUrl"] = "https://outin-40564284ef05113e1403e7.oss-cn-shanghai.192.168.0.0/16/watermarks/02A1B22DF25D46C3C725A4****.png";
        watermarks.append(watermark1);
        // Override the content of the text watermark.
        Json::Value watermark2;
        // The ID of the new text watermark that you want to use. The ID of the text watermark must be associated with a template ID.
        watermark2["WatermarkId"] = "d297ba31ac5242d207****";
        // The new content of the text watermark.
        watermark2["Content"] = "User ID: 6****",
        watermarks.append(watermark2);
        overrideParams["Watermarks"] = watermarks;
        return overrideParams;
     }
    
     /**
     * Create a data key for encryption. The response contains the plaintext and ciphertext of the data key. You need only to transfer the ciphertext to ApsaraVideo VOD.
     * Note: You must set the value of the KeySpec parameter to AES_128. The NumberOfBytes parameter is not supported.
     * @param serviceKey. The service key that is provided by ApsaraVideo VOD to generate data keys. The description of this service key is vod in the Key Management Service (KMS) console.
     */
    string generateDataKey(string serviceKey) {
        string ciphertextBlob;
        /* Call the GenerateDataKey operation of KMS to generate the ciphertext of the data key. */
        return ciphertextBlob;
    }
    
    /**
     * Create the configurations of HTTP Live Streaming (HLS) encryption.
     */
    Json::Value buildEncryptConfig() {
        // The service key that is provided by ApsaraVideo VOD. To view the service key, you must select the region where the key resides and find the key whose description is vod in the KMS console.
        string serviceKey = "<Your Service Key>";
        // Generate a random data key for encryption. The response contains the plaintext and ciphertext of the data key.
        // Pass only the ciphertext of the data key for standard video encryption.
        string ciphertextBlob = generateDataKey(serviceKey);
        Json::Value encryptConfig;
        // The URI of the operation that is used to decrypt the data key. To obtain the URI, concatenate the URL of the decryption service and the ciphertext of the data key. The ciphertext to decrypt varies among videos.
        // You can customize the name of the Ciphertext parameter. The name in this example is only for reference.
        encryptConfig["DecryptKeyUri"] = "http://192.168.0.0/16/decrypt?Ciphertext=" + ciphertextBlob;
        // The type of the key service. Set the value to KMS.
        encryptConfig["KeyServiceType"] = "KMS";
        // The ciphertext of the data key.
        encryptConfig["CipherText"] = ciphertextBlob;
        return encryptConfig;
    }
    
    /**
     * Submit a transcoding job.
     */
    VodApiResponse submitTranscodeJobs(VodCredential authInfo) {
        string apiName = "SubmitTranscodeJobs";
        map<string, string> args;
        // The ID of the video that you want to transcode.
        args["VideoId"] = "34a6ca54f5c140eece85a289****";
        // The ID of the transcoding template.
        args["TemplateGroupId"] = "e8aa925a9798c630d30cd7****";
        // Build the parameters that are required to replace a watermark. You must create these parameters only when you want to replace a watermark.
        //Json::Value overrideParams = buildOverrideParams();
        // The overriding parameters. You can change the values of some watermark-related parameters. You must specify these parameters only when you want to replace a watermark.
        //args["OverrideParams"] = overrideParams.toStyledString();
    
        // Build the configuration parameters that are required for standard encryption. You must create these parameters only for standard encryption.
        //Json::Value encryptConfig = buildEncryptConfig();
        // The configurations for HLS standard encryption. You must specify these parameters only for standard encryption.
        //args["EncryptConfig"] = encryptConfig.toStyledString();
        return getAcsResponse(authInfo, apiName, args);
    }
    
    /**
     * Call example
     */
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = submitTranscodeJobs(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Submit a snapshot job {#h2--div-id-submitsnapshotjob-div-3}
-----------------------------------------------------------

You can call the SubmitSnapshotJob operation to submit a snapshot job.
For more information about the request and response parameters of this operation, see [SubmitSnapshotJob](/intl.en-US/API Reference/Media processing/Process initiation/SubmitSnapshotJob.md). Example:
**Note**
For more information about how to create a snapshot template, see [Create snapshot templates](/intl.en-US/API Reference/Media processing/Snapshot template/AddVodTemplate.md). {#h2--div-id-submitsnapshotjob-div-3}
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include <jsoncpp/json/json.h>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Build the configurations of the image sprite snapshot.
     * @return
     */
    Json::Value buildSnapshotTemplateConfig() {
        Json::Value spriteSnapshotConfig;
        spriteSnapshotConfig["CellWidth"] = "120";
        spriteSnapshotConfig["CellHeight"] = "68";
        spriteSnapshotConfig["Columns"] = "3";
        spriteSnapshotConfig["Lines"] = "10";
        spriteSnapshotConfig["Padding"] = "20";
        spriteSnapshotConfig["Margin"] = "50";
        // Whether to retain the source image after an image sprite is generated.
        spriteSnapshotConfig["KeepCellPic"] = "keep";
        spriteSnapshotConfig["Color"] = "tomato";
        return spriteSnapshotConfig;
    }
    
    /**
     * Submit the snapshot job.
     */
     VodApiResponse submitSnapshotJob(VodCredential authInfo) {
        string apiName = "SubmitSnapshotJob";
        map<string, string> args;
        // The ID of the video for which you want to create snapshots. We recommend that you specify SnapshotTemplateId.
        args["VideoId"] = "4d237a8270084849bf4207876181****";
        // The ID of the snapshot template.
        args["SnapshotTemplateId"] = "5d745e6b8baadf589e0702426cfc6****";
        // If the SnapshotTemplateId parameter is specified, the following parameters are ignored:
        args["Count"] = "50";
        args["SpecifiedOffsetTime"] = "0";
        args["Interval"] = "1";
        args["Width"] = "200";
        args["Height"] = "200";
        // Optional. The configurations of the image sprites.
        Json::Value spriteSnapshotConfig = buildSnapshotTemplateConfig();
        args["SpriteSnapshotConfig"] = spriteSnapshotConfig.toStyledString();
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = submitSnapshotJob(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Query snapshot data {#h2--div-id-listsnapshots-div-4}
-----------------------------------------------------

You can call the ListSnapshots operation to query snapshot data.
For more information about the request and response parameters of this operation, see [ListSnapshots](/intl.en-US/API Reference/Media asset management/Image management/ListSnapshots.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include "vod_sdk/openApiUtil.h"
    
    /**
     * Query snapshot data.
     */
     VodApiResponse listSnapshots(VodCredential authInfo) {
        string apiName = "ListSnapshots";
        map<string, string> args;
        // The ID of the video.
        args["VideoId"] = "c86c0ceba9796535****";
        args["SnapshotType"] = "CoverSnapshot";
        args["PageNo"] = "1";
        args["PageSize"] = "20";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = listSnapshots(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



Preprocess videos in the production studio {#h2--div-id-submitpreprocessjobs-div-5}
-----------------------------------------------------------------------------------

You can call the SubmitPreprocessJobs operation to preprocess videos in the production studio.
For more information about the request and response parameters of this operation, see [SubmitPreprocessJobs](/intl.en-US/API Reference/Media processing/Process initiation/SubmitPreprocessJobs.md). Example: 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    #include <stdio.h>
    #include <string>
    #include <map>
    #include "vod_sdk/openApiUtil.h"
    
    
    /**
     * Preprocess a video in the production studio.
     */
     VodApiResponse submitPreprocessJobs(VodCredential authInfo) {
        string apiName = "SubmitPreprocessJobs";
        map<string, string> args;
        // The ID of the video.
        args["VideoId"] = "c86c0ceba97965352418";
        args["PreprocessType"] = "PreprocessType";
        return getAcsResponse(authInfo, apiName, args);
    }
    
    // Call example
    void main() {
        VodCredential authInfo = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        VodApiResponse response = submitPreprocessJobs(authInfo);
        printf("httpCode: %d, result: %s\n", response.httpCode, response.result.c_str());
    }



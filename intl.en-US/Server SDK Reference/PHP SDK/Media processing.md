Media processing 
=====================================

This topic provides examples on how to use the API operations of the media processing module. The API operations are encapsulated in ApsaraVideo VOD SDK for Python. You can call the API operations to submit transcoding and snapshot jobs, query snapshot data, and preprocess videos in the production studio.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/PHP SDK/Install the SDK/Initialization.md).

Submit a transcoding job {#h2--div-id-submittranscodejobs-div-2}
----------------------------------------------------------------

You can call the SubmitTranscodeJobs operation to submit a transcoding job.

For more information about the request and response parameters of this operation, see [SubmitTranscodeJobs](/intl.en-US/API Reference/Media processing/Process initiation/SubmitTranscodeJobs.md). Example:

    use Kms\Request\V20160120 as kms;
    
    /**
     * Build overriding parameters, which override only the file URL of an image watermark or the content of a text watermark. If you do not need these parameters, leave overrideParams empty.
     * Make sure that the ID of the watermark is associated with the ID of the transcoding template that you use. The ID of the transcoding template is specified by TranscodeTemplateId.
     * You can call this operation to add only a watermark whose ID is associated with the ID of the transcoding template that you use.
     */
    function buildOverrideParams() {
        $overrideParams = array();
    
        // Take watermark overriding as an example.
        $watermarks = array();
    
        // Override an image watermark.
        $watermarks1 = array();
        $watermarks1["WatermarkId"] = "2ea587477c5a1bc8b52****";
        $watermarks1["FileUrl"] = "https://outin-40564284ef05113e1403e7.oss-cn-shanghai.aliyuncs.com/watermarks/02A1B22DF25D46C3C725A4-6-2.png";
        $watermarks[] = $watermarks1;
    
        // Override a text watermark.
        $watermarks2 = array();
        $watermarks2["WatermarkId"] = "d297ba31ac5242d2052****";
        $watermarks2["Content"] = "User ID: 6****";
        $watermarks[] = $watermarks2;
    
        $overrideParams["Watermarks"] = $watermarks;
        return json_encode($overrideParams);
    }
    
    /**
     * Optional configurations of HLS encryption. If you do not use HLS encryption, leave the parameters empty.
     * HLS encryption configurations depend on KMS. You must install the KMS dependency aliyun-php-sdk-kms.
     * API reference for key generation: https://192.168.0.0/16/document_detail/28948.html.
     */
    function buildEncryptConfig($client) {
        try {
            // Generate a random data key for encryption. The response contains the plaintext and ciphertext of the data key.
            // Only the ciphertext key is used for standard video encryption.
            $request = new kms\GenerateDataKeyRequest();
            $request->setKeyId('<serviceKey>');
            $request->setKeySpec("AES_128");
            $response = $client->getAcsResponse($request);
    
           $encryptConfig = array();
            # The URI of the operation that is used to decrypt the data key. To obtain the URI, concatenate the URL of the decryption service and the ciphertext of the data key. The ciphertext to decrypt varies among videos. You must deploy the decryption service. 
            $encryptConfig["DecryptKeyUri"] = "http://192.168.0.0/16/decrypt?Ciphertext=" + $response->getCiphertextBlob();
            // The type of the key service. Set the value to KMS.
            $encryptConfig["KeyServiceType"] = "KMS";
            # You can customize the name of the Ciphertext parameter. The name in this example is only for reference.
            $encryptConfig["CipherText"] = $response->getCiphertextBlob();
    
            return json_encode($encryptConfig);
        } catch (Exception $e) {
            print $e->getMessage()."\n";
            return null;
        }
    }
    
    /**
     * Submit a transcoding job.
     */
    function submitTranscodeJobs($client) {
        $request = new vod\SubmitTranscodeJobsRequest();
        // The ID of the video to be transcoded.
        $request->setVideoId("6893fca9814640c8821efa523e52****");
        // The ID of the transcoding template.
        $request->setTemplateGroupId("44f915b63a2375a6121533c6b252****");
        // Build watermark overriding parameters. These parameters are required only when you want to override watermark-related information.
        $request->setOverrideParams(buildOverrideParams());
        // The configurations of HLS encryption. These configurations are required only when you want to use HLS encryption.
        $request->setEncryptConfig(buildEncryptConfig($client));
    
        return $client->getAcsResponse($request);
    }
    
    /**
     * Call example
     */
    try {
        $client = initVodClient("<AccessKeyId>", "<AccessKeySecret>");
    
        $result = submitTranscodeJobs($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Submit a snapshot job {#h2--div-id-submitsnapshotjob-div-3}
-----------------------------------------------------------

You can call the SubmitSnapshotJob operation to submit a snapshot job.
For more information about the request and response parameters of this operation, see [SubmitSnapshotJob](/intl.en-US/API Reference/Media processing/Process initiation/SubmitSnapshotJob.md). Example:
**Note**
For more information about how to create a snapshot template, see [Create a snapshot template](/intl.en-US/API Reference/Media processing/Snapshot template/AddVodTemplate.md). {#h2--div-id-submitsnapshotjob-div-3}
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    /**
     * Create the configurations of the image sprite snapshot.
     * @return
     */
    function buildSnapshotTemplateConfig() {
        $spriteSnapshotConfig = array();
        $spriteSnapshotConfig["CellWidth"] = "120";
        $spriteSnapshotConfig["CellHeight"] = "68";
        $spriteSnapshotConfig["Columns"] = "3";
        $spriteSnapshotConfig["Lines"] = "10";
        $spriteSnapshotConfig["Padding"] = "20";
        $spriteSnapshotConfig["Margin"] = "50";
    
        // Whether to retain the source image after an image sprite is generated.
        $spriteSnapshotConfig["KeepCellPic"] = "keep";
        $spriteSnapshotConfig["Color"] = "tomato";
    
        return json_encode($spriteSnapshotConfig);
    }
    
    
    /**
     * Submit a media snapshot processing job.
     */
    function submitSnapshotJob($client) {
        $request = new vod\SubmitSnapshotJobRequest();
        // The ID of the video for which you want to create a snapshot.
        $request->setVideoId("6893fca9814640c8821efa523e52****");
        // The ID of the snapshot template.
        $request->setSnapshotTemplateId("44f915b63a2375a6121533c6b252****");
    
        // If you specify the SnapshotTemplateId parameter, the following parameters are ignored:
        $request->setCount(50);
        $request->setSpecifiedOffsetTime(0);
        $request->setInterval(1);
        $request->setWidth("200");
        $request->setHeight("200");
        $request->setSpriteSnapshotConfig(buildSnapshotTemplateConfig());
    
        return $client->getAcsResponse($request);
    }
    
    /**
     * Call example
     */
    try {
        $client = initVodClient("<AccessKeyId>", "<AccessKeySecret>");
    
        $result = submitSnapshotJob($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Query snapshot data {#h2--div-id-listsnapshots-div-4}
-----------------------------------------------------

You can call the listSnapshots operation to query snapshot data.
For more information about the request and response parameters of this operation, see [listSnapshots](/intl.en-US/API Reference/Media asset management/Image management/ListSnapshots.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    /**
     * Query snapshot data.
     */
    function listSnapshots($client) {
        $request = new vod\ListSnapshotsRequest();
        // The video ID.
        $request->setVideoId("6893fca9814640c8821efa523e52****");
        /// The snapshot type.
        $request->setSnapshotType("CoverSnapshot");
        // The page number.
        $request->setPageNo("1");
        $request->setPageSize("20");
    
        return $client->getAcsResponse($request);
    }
    
    /**
     * Call example
     */
    try {
        $client = initVodClient("<AccessKeyId>", "<AccessKeySecret>");
    
        $result = listSnapshots($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Preprocess videos in the production studio {#h2--div-id-submitpreprocessjobs-div-5}
-----------------------------------------------------------------------------------

You can call the SubmitPreprocessJobs operation to preprocess videos in the production studio.
For more information about the request and response parameters of this operation, see [SubmitPreprocessJobs](/intl.en-US/API Reference/Media processing/Process initiation/SubmitPreprocessJobs.md). Example: 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    /**
     * Preprocess videos in the production studio.
     */
    function submitPreprocessJobs($client) {
        $request = new vod\SubmitPreprocessJobsRequest();
        // The video ID.
        $request->setVideoId("6893fca9814640c8821efa523e52****");
        /// The preprocess type.
        $request->setPreprocessType("PreprocessType");
    
        return $client->getAcsResponse($request);
    }
    
    /**
     * Call example
     */
    try {
        $client = initVodClient("<AccessKeyId>", "<AccessKeySecret>");
    
        $result = submitPreprocessJobs($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



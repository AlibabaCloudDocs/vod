Media processing 
=====================================

This topic provides examples on how to use the API operations of the media processing module. The API operations are encapsulated in ApsaraVideo VOD SDK for Node.js. You can call the API operations to submit transcoding and snapshot jobs, query snapshot data, and preprocess videos in the production studio.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/Node.js SDK/Initialization.md).

Submit a transcoding job without encryption {#h2--amp-div-id-submittranscodejobs-div-2}
---------------------------------------------------------------------------------------

You can call the SubmitTranscodeJobs operation to submit a transcoding job without encryption.
For more information about the request and response parameters of this operation, see [SubmitTranscodeJobs](/intl.en-US/API Reference/Media processing/Initiate Process/SubmitTranscodeJobs.md). Example:
**Note**
The following code provides an example on transcoding without encryption. For more information about video encryption supported by Alibaba Cloud, see [Alibaba Cloud video encryption](/intl.en-US/Developer Guide/Video security/Alibaba Cloud video encryption.md). {#h2--amp-div-id-submittranscodejobs-div-2}
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    /**
     * Build overriding parameters, which override only the file URL of an image watermark or the content of a text watermark. If you do not need these parameters, leave overrideParams empty.
     * Make sure that the ID of the watermark is associated with the ID of the transcoding template that you use. The ID of the transcoding template is specified by TranscodeTemplateId.
     * You can call this operation to add only a watermark whose ID is associated with the ID of the transcoding template that you use.
     */
    var overrideParams = {
        Watermarks: [{
            // The ID of the watermark whose image you want to override. The ID must be associated with the transcoding template.
            WatermarkId: 'WatermarkId1',
            // The file URL of the new image that is stored in an Object Storage Service (OSS) bucket. The new image and the video must be stored on the same origin server.
            FileUrl: 'https://192.168.0.0/16/watermarks/sample.png'
        },{
            // The ID of the watermark whose content you want to override. The ID must be associated with the transcoding template.
            WatermarkId: 'WatermarkId2',
            // The new content of the watermark.
            Content: 'User ID: 6****'
        }]
    };
    
    client.request("SubmitTranscodeJobs", {
        VideoId: '34a6ca54f5c140eece85a289****',
        TemplateGroupId: 'e8aa925a9798c630d30cd7****',
        OverrideParams: JSON.stringify(overrideParams)
    }, {}).then(function (response) {
        if (response.TranscodeJobs && response.TranscodeJobs.TranscodeJob && response.TranscodeJobs.TranscodeJob.length > 0){
            for(var i=0; i<response.TranscodeJobs.TranscodeJob.length; i++){
                console.log('JobId = ' + response.TranscodeJobs.TranscodeJob[i].JobId);
            }
        }
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Submit a transcoding job with HLS encryption enabled {#h2--hls-div-id-submittranscodejobs-div-3}
------------------------------------------------------------------------------------------------

You can call the SubmitTranscodeJobs operation to submit a transcoding job with HTTP Live Streaming (HLS) encryption enabled.
For more information about the request and response parameters of this operation, see [SubmitTranscodeJobs](/intl.en-US/API Reference/Media processing/Initiate Process/SubmitTranscodeJobs.md). Example:
**Note**
The following code provides an example on transcoding with HLS encryption enabled. For more information, see [Standard HLS encryption](/intl.en-US/Developer Guide/Video security/Standard HLS encryption.md). {#h2--hls-div-id-submittranscodejobs-div-3}
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    /**
     * Submit a transcoding job.
     */
    function submitTranscodeJobs(overrideParams, encryptConfig) {
        var paras = {
            VideoId: '34a6ca54f5c140eece85a289****',
            TemplateGroupId: 'e8aa925a9798c630d30cd7****'
        };
        // The overriding parameters, which override only watermark-related information. These parameters are required only when you want to override watermark-related information.
        if (! overrideParams){
            paras.OverrideParams = JSON.stringify(overrideParams);
        }
        // The configurations of HLS encryption. These configurations are required only when you want to use HLS encryption.
        if (! encryptConfig){
            paras.EncryptConfig = JSON.stringify(encryptConfig);
        }
    
        client.request("SubmitTranscodeJobs", paras, {}).then(function (response) {
            console.log(response);
            if (response.TranscodeJobs && response.TranscodeJobs.TranscodeJob && response.TranscodeJobs.TranscodeJob.length > 0){
                for(var i=0; i<response.TranscodeJobs.TranscodeJob.length; i++){
                    console.log('JobId = ' + response.TranscodeJobs.TranscodeJob[i].JobId);
                }
            }
            console.log('RequestId = ' + response.RequestId);
        }).catch(function (response) {
            console.log('ErrorCode = ' + response.data.Code);
            console.log('ErrorMessage = ' + response.data.Message);
            console.log('RequestId = ' + response.data.RequestId);
        });
    }
    
    /**
     * Create a data key for encryption. The response contains the plaintext and ciphertext of the data key. You need only to transfer the ciphertext to ApsaraVideo VOD.
     * Note: You must set the value of the KeySpec parameter to AES_128. The NumberOfBytes parameter is not supported.
     */
    client.request("GenerateDataKey", {
        KeyId: 'KeyId',   // The service key that is provided by ApsaraVideo VOD to generate data keys. The description of this service key is vod in the Key Management Service (KMS) console.
        KeySpec: 'AES_128'
    }, {}).then(function (response) {
        console.log('GenerateDataKey RequestId = ' + response.RequestId);
        var encryptConfig = {
            // The URI of the operation that is used to decrypt the data key. To obtain the URI, concatenate the URL of the decryption service and the ciphertext of the data key. The ciphertext to decrypt varies among videos.
            // You can customize the name of the Ciphertext parameter. The name in this example is only for reference.
            DecryptKeyUri: 'http://decrypt.demo.com/decrypt?Ciphertext=' + response.CiphertextBlob,
            // The type of the key service. Set the value to KMS.
            KeyServiceType: 'KMS',
            // The ciphertext of the data key.
            CipherText: response.CiphertextBlob
        };
    
        /**
         * Build overriding parameters, which override only the file URL of an image watermark or the content of a text watermark. If you do not need these parameters, leave overrideParams empty.
         * Make sure that the ID of the watermark is associated with the ID of the transcoding template that you use. The ID of the transcoding template is specified by TranscodeTemplateId.
         * You can call this operation to add only a watermark whose ID is associated with the ID of the transcoding template that you use.
         */
        var overrideParams = {
            Watermarks: [{
                // The ID of the watermark whose image you want to override. The ID must be associated with the transcoding template.
                WatermarkId: 'WatermarkId1',
                // The file URL of the new image that is stored in an OSS bucket. The new image and the video must be stored on the same origin server.
                FileUrl: 'https://sample.oss-cn-shanghai.aliyuncs.com/watermarks/sample.png'
            },{
                // The ID of the watermark whose content you want to override. The ID must be associated with the transcoding template.
                WatermarkId: 'WatermarkId2',
                // The new content of the watermark.
                Content: 'User ID: 66666'
            }]
        };
    
        submitTranscodeJobs(overrideParams, encryptConfig);
    }).catch(function (response) {
        console.log('GenerateDataKey ErrorCode = ' + response.data.Code);
        console.log('GenerateDataKey ErrorMessage = ' + response.data.Message);
        console.log('GenerateDataKey RequestId = ' + response.data.RequestId);
    });



Submit a snapshot job {#h2--div-id-submitsnapshotjob-div-4}
-----------------------------------------------------------

You can call the SubmitSnapshotJob operation to submit a snapshot job.
For more information about the request and response parameters of this operation, see [SubmitSnapshotJob](/intl.en-US/API Reference/Media processing/Initiate Process/SubmitSnapshotJob.md). Example:
**Note**
For more information about how to create a snapshot template, see [Create a snapshot template](/intl.en-US/API Reference/Media processing/Snapshot Template/AddVodTemplate.md). {#h2--div-id-submitsnapshotjob-div-4}
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    var spriteSnapshotConfig = {
        CellWidth: '120',
        CellHeight: '68',
        Columns: '3',
        Lines: '10',
        Padding: '20',
        Margin: '50',
        // Whether to retain the source image after an image sprite is generated.
        KeepCellPic: 'keep',
        Color: 'tomato'
    };
    client.request("SubmitSnapshotJob", {
        VideoId: '52b440eabcc8ae1cbffcxxxxxx',  // The ID of the video for which you want to create a snapshot.
        SnapshotTemplateId: '1111e6b8baadf589cbffc58****',  // The ID of the snapshot template.
        // If you specify the SnapshotTemplateId parameter, the following parameters are ignored:
        Count: 50,
        SpecifiedOffsetTime: 0,
        Interval: 1,
        Width: '200',
        Height: '200',
        SpriteSnapshotConfig: JSON.stringify(spriteSnapshotConfig)
    }, {}).then(function (response) {
        if (response.SnapshotJob){
            // The task ID.
            console.log('JobId = ' + response.SnapshotJob.JobId);
        }
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Query snapshot data {#h2--div-id-listsnapshots-div-5}
-----------------------------------------------------

You can call the ListSnapshots operation to query snapshot data.
For more information about the request and response parameters of this operation, see [ListSnapshots](/intl.en-US/API Reference/Media management/Image Management/ListSnapshots.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("ListSnapshots", {
        VideoId: '1111121b52b440eabcc8ae1cbff58****',  // The video ID.
        SnapshotType: 'CoverSnapshot',  // The snapshot type.
        PageNo: '1',
        PageSize: '20'
    }, {}).then(function (response) {
        if (response.MediaSnapshot && response.MediaSnapshot.Snapshots && response.MediaSnapshot.Snapshots.Snapshot){
            for (var i=0; i<response.MediaSnapshot.Snapshots.Snapshot.length; i++){
                // The snapshot URL.
                console.log('Url = ' + response.MediaSnapshot.Snapshots.Snapshot[i].Url);
            }
        }
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Preprocess videos in the production studio {#h2--div-id-submitpreprocessjobs-div-6}
-----------------------------------------------------------------------------------

You can call the SubmitPreprocessJobs operation to preprocess videos in the production studio.
For more information about the request and response parameters of this operation, see [SubmitPreprocessJobs](). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("SubmitPreprocessJobs", {
        VideoId: '111111192e8e48c1ad51f237c54****',  // The video ID.
        PreprocessType: 'PreprocessType'
    }, {}).then(function (response) {
        if (response.PreprocessJobs && response.PreprocessJobs.PreprocessJob && response.PreprocessJobs.PreprocessJob.length > 0){
            for (var i=0; i<response.PreprocessJobs.PreprocessJob.length; i++){
                // The task ID.
                console.log('JobId = ' + response.PreprocessJobs.PreprocessJob[i].JobId);
            }
        }
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



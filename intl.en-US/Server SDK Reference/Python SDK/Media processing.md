Media processing 
=====================================

This topic provides examples on how to use the API operations of the media processing module. The API operations are encapsulated in ApsaraVideo VOD SDK for Python. You can call the API operations to submit transcoding and snapshot jobs, query snapshot data, and preprocess videos in the production studio.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/Python SDK/Initialization.md).

Submit a transcoding job without encryption {#h2--amp-div-id-submittranscodejobs-div-2}
---------------------------------------------------------------------------------------

You can call the SubmitTranscodeJobs operation to submit a transcoding job without encryption.

For more information about the request and response parameters of this operation, see [SubmitTranscodeJobs](/intl.en-US/API Reference/Media processing/Process initiation/SubmitTranscodeJobs.md). Example:
**Note**

The following code provides an example on transcoding without encryption. For more information about video encryption supported by Alibaba Cloud, see [Alibaba Cloud video encryption](/intl.en-US/Developer Guide/Video security/Alibaba Cloud video encryption.md).

    """
    * Build overriding parameters, which override only the file URL of an image watermark or the content of a text watermark. If you do not need these parameters, leave overrideParams empty.
    * Make sure that the ID of the watermark is associated with the ID of the transcoding template that you use. The ID of the transcoding template is specified by TranscodeTemplateId.
    * You can call this operation to add only a watermark whose ID is associated with the ID of the transcoding template that you use.
    """
    def build_override_params():
        # Take watermark overriding as an example.
        watermarks = []
    
        # Override the file of an image watermark.
        watermark1 = {'WatermarkId': '<watermarkId>', 'FileUrl': 'https://192.168.0.0/16/watermarks/sample.png'}
        watermarks.append(watermark1)
    
        # Override a text watermark.
        watermark2 = {'WatermarkId': '<watermarkId>', 'Content': 'new Text'}
        watermarks.append(watermark2)
    
        return {'Watermarks': watermarks}
    
    
    """  Start transcoding process   """
    from aliyunsdkvod.request.v20170321 import SubmitTranscodeJobsRequest
    def normal_submit_transcode_jobs(clt):
        request = SubmitTranscodeJobsRequest.SubmitTranscodeJobsRequest()
    
        # Specify the ID of the video to be transcoded.
        request.set_VideoId('<videoId>')
    
        # Specify the transcoding template group.
        request.set_TemplateGroupId('<templateGroupId>')
    
        """
        # Set optional overriding parameters, such as parameters related to watermark information overriding.
        overrideParams = build_override_params()
        request.set_OverrideParams(json.dumps(overrideParams))
        """
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        jobs = normal_submit_transcode_jobs(clt)
        print(jobs['TranscodeJobs']['TranscodeJob'])
        print(json.dumps(jobs, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Submit a transcoding job with HLS encryption enabled {#h2--hls-div-id-submittranscodejobs-div-3}
------------------------------------------------------------------------------------------------

You can call the SubmitTranscodeJobs operation to submit a transcoding job with HTTP Live Streaming (HLS) encryption enabled.

For more information about the request and response parameters of this operation, see [SubmitTranscodeJobs](/intl.en-US/API Reference/Media processing/Process initiation/SubmitTranscodeJobs.md). Example:
**Note**

The following code provides an example on transcoding with HLS encryption enabled. For more information, see [Standard HLS encryption](/intl.en-US/Developer Guide/Video security/HLS Encryption.md).

    """
    * Optional configurations of HLS encryption. If you do not use HLS encryption, leave the parameters empty.
    * HLS encryption configurations depend on KMS. You must install the KMS dependency aliyun-php-sdk-kms. If you want to call an API operation, you must import related classes.
    * API reference for key generation: https://192.168.0.0/16/document_detail/28948.html.
    """
    from aliyunsdkkms.request.v20160120 import GenerateDataKeyRequest
    from aliyunsdkcore.http import protocol_type
    def build_encrypt_config(clt):
        try:
            # Generate a random data key for encryption. The response contains the plaintext and ciphertext of the data key.
            # Only the ciphertext key is used for standard video encryption.
            request = GenerateDataKeyRequest.GenerateDataKeyRequest()
            request.set_KeyId('<serviceKey>')
            request.set_KeySpec('AES_128')
    
            # Set the value to HTTPS for KMS API operations.
            request.set_protocol_type(protocol_type.HTTPS)
            request.set_accept_format('JSON')
            response = json.loads(clt.do_action_with_exception(request))
    
            # The URI of the operation that is used to decrypt the data key. To obtain the URI, concatenate the URL of the decryption service and the ciphertext of the data key. The ciphertext to decrypt varies among videos. You must deploy the decryption service.
            # You can customize the name of the Ciphertext parameter. The name in this example is only for reference.
            decryptKeyUri = 'http://decrypt.demo.com/decrypt?' + 'Ciphertext=' + response['CiphertextBlob']
    
            return {'DecryptKeyUri': decryptKeyUri, 'KeyServiceType': 'KMS', 'CipherText': response['CiphertextBlob']}
    
        except Exception as e:
            print(e)
            #print(traceback.format_exc())
            return None
    
    
    """  Start transcoding process   """
    from aliyunsdkvod.request.v20170321 import SubmitTranscodeJobsRequest
    def hlsencrypt_submit_transcode_jobs(clt):
        request = SubmitTranscodeJobsRequest.SubmitTranscodeJobsRequest()
    
        # Specify the ID of the video to be transcoded.
        request.set_VideoId('<videoId>')
    
        # Specify the transcoding template group.
        request.set_TemplateGroupId('<templateGroupId>')
    
        # Use KMS to generate a random encryption key.
        encryptConfig = build_encrypt_config(clt)
        if encryptConfig is not None:
            request.set_EncryptConfig(json.dumps(encryptConfig))
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        jobs = hlsencrypt_submit_transcode_jobs(clt)
        print(jobs['TranscodeJobs']['TranscodeJob'])
        print(json.dumps(jobs, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Submit a snapshot job {#h2--div-id-submitsnapshotjob-div-4}
-----------------------------------------------------------

You can call the SubmitSnapshotJob operation to submit the snapshot job.

For more information about the request and response parameters of this operation, see [SubmitSnapshotJob](/intl.en-US/API Reference/Media processing/Process initiation/SubmitSnapshotJob.md). Example:
**Note**

For more information about how to create a snapshot template, see [Create a snapshot template](/intl.en-US/API Reference/Media processing/Snapshot template/AddVodTemplate.md).

    from aliyunsdkvod.request.v20170321 import SubmitSnapshotJobRequest
    def submit_snapshot_job(clt):
        request = SubmitSnapshotJobRequest.SubmitSnapshotJobRequest()
    
        # The ID of the video for which you want to create a snapshot.
        request.set_VideoId('<videoId>')
    
        # The ID of the snapshot template.
        #request.set_SnapshotTemplateId('<snapshotTemplateId>')
    
        # snapshotIf you specify the ID of the snapshot template parameter, the following parameters are ignored:
        request.set_Count(50L)
        request.set_SpecifiedOffsetTime(0L)
        request.set_Interval(1L)
        request.set_Width(200)
        request.set_Height(200)
    
        # Image sprite-related parameters, which are optional.
        spriteSnapshotConfig = {'CellWidth': 120, 'CellHeight': 68, 'Columns': 3,
                                'Lines': 10, 'Padding': 20, 'Margin': 50}
        # Whether to retain the source image after an image sprite is generated.
        spriteSnapshotConfig['KeepCellPic'] = 'keep'
        spriteSnapshotConfig['Color'] = 'tomato'
        request.set_SpriteSnapshotConfig(json.dumps(spriteSnapshotConfig))
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        job = submit_snapshot_job(clt)
        print(json.dumps(job, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Query snapshot data {#h2--div-id-listsnapshots-div-5}
-----------------------------------------------------

You can call the ListSnapshots operation to query snapshot data.
For more information about the request and response parameters of this operation, see [ListSnapshots](/intl.en-US/API Reference/Media asset management/Image management/ListSnapshots.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import ListSnapshotsRequest
    def list_snapshots(clt):
        request = ListSnapshotsRequest.ListSnapshotsRequest()
    
        request.set_VideoId('<videoId>')
        request.set_SnapshotType('CoverSnapshot')
        request.set_PageNo(1)
        request.set_PageSize(20)
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        snapshots = list_snapshots(clt)
        print(snapshots['MediaSnapshot'])
        print(json.dumps(snapshots, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Preprocess videos in the production studio {#h2--div-id-submitpreprocessjobs-div-6}
-----------------------------------------------------------------------------------

You can call the SubmitPreprocessJobs operation to preprocess the video in production studios.
For more information about the request and response parameters of this operation, see [SubmitPreprocessJobs](/intl.en-US/API Reference/Media processing/Process initiation/SubmitPreprocessJobs.md). Example: 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.req uest.v20170321 import SubmitPreprocessJobsRequest
    def submit_preprocess_jobs(clt):
        request = SubmitPreprocessJobsRequest.SubmitPreprocessJobsRequest()
    
        request.set_VideoId('<videoId>')
        request.set_PreprocessType('PreprocessType')
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        jobs = submit_preprocess_jobs(clt)
        print(json.dumps(jobs, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



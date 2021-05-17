Transcoding template 
=========================================

This topic provides examples on how to use the API operations of the transcoding template module. The API operations are encapsulated in ApsaraVideo VOD SDK for Python. You can call the API operations to create, modify, delete, and query transcoding template groups. You can also specify a transcoding template group as the default one.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/Python SDK/Initialization.md).

Create a transcoding template group {#h2--div-id-addtranscodetemplategroup-div-2}
---------------------------------------------------------------------------------

You can call the AddTranscodeTemplateGroup operation to create a transcoding template group.

For more information about the request and response parameters of this operation, see [AddTranscodeTemplateGroup](/intl.en-US/API Reference/Media processing/Transcoding template/AddTranscodeTemplateGroup.md). Example:

    from aliyunsdkvod.request.v20170321 import AddTranscodeTemplateGroupRequest
    
    """ Build the configurations of the transcoding template. """
    def build_transcode_template_list():
        transcodeTemplateList = []
        transcodeTemplate = {}
    
        # The template name.
        transcodeTemplate["TemplateName"] = "MP4-for-Low-Definition"
    
        # The definition.
        transcodeTemplate["Definition"] = "LD"
    
        # The configurations of video stream transcoding.
        videoConfig = {"Width": 640, "Bitrate": 400, "Fps": 25, "Remove": False, "Codec": "H.264", "Gop": "250"}
        transcodeTemplate["Video"] = videoConfig
    
        # The configurations of audio stream transcoding.
        audioConfig = {"Codec": "AAC", "Bitrate": "64", "Channels": "2", "Samplerate": "32000"}
        transcodeTemplate["Audio"] = audioConfig
    
        # The container for encapsulation.
        container = {"Format": "mp4"}
        transcodeTemplate["Container"] = container
    
        # The configurations of conditional transcoding.
        condition = {"IsCheckReso": False, "IsCheckResoFail": False, "IsCheckVideoBitrate": False,
                     "IsCheckVideoBitrateFail": False, "IsCheckAudioBitrate": False, "IsCheckAudioBitrateFail": False}
        transcodeTemplate["TransConfig"] = condition
    
        """
        # The configurations of encryption. Only HLS encryption is supported.
        encryptSetting = {"EncryptType": "Private"}
        transcodeTemplate["EncryptSetting"] = encryptSetting
        """
    
        # The IDs of associated watermarks.
        watermarkIdList = []
        #watermarkIdList.append("<WatermarkId>")
        watermarkIdList.append("USER_DEFAULT_WATERMARK")
        transcodeTemplate["WatermarkIds"] = watermarkIdList
    
        transcodeTemplateList.append(transcodeTemplate)
    
        return transcodeTemplateList
    
    
    """  Add the configurations of the transcoding template ."""
    def add_transcode_template_group(clt):
        request = AddTranscodeTemplateGroupRequest.AddTranscodeTemplateGroupRequest()
    
        request.set_Name("SampleTranscodeTemplateGroup")
    
        transcodeTemplateList = build_transcode_template_list()
        request.set_TranscodeTemplateList(json.dumps(transcodeTemplateList))
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        res = add_transcode_template_group(clt)
        print(json.dumps(res, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Modify a transcoding template group {#h2--div-id-updatetranscodetemplategroup-div-3}
------------------------------------------------------------------------------------

You can call the UpdateTranscodeTemplateGroup operation to modify a transcoding template group.

For more information about the request and response parameters of this operation, see [UpdateTranscodeTemplateGroup](/intl.en-US/API Reference/Media processing/Transcoding template/UpdateTranscodeTemplateGroup.md). Example:

    from aliyunsdkvod.request.v20170321 import UpdateTranscodeTemplateGroupRequest
    
    """  Build the configurations of the transcoding template."""
    def build_transcode_template_list():
        transcodeTemplateList = []
        transcodeTemplate = {}
    
        # The ID of the transcoding template. Required.
        transcodeTemplate["TranscodeTemplateId"] = "<TranscodeTemplateId>"
    
        # The following parameters are optional:
    
        # Set a new template name.
        transcodeTemplate["TemplateName"] = "new-MP4-for-Low-Definition"
    
        # The configurations of video stream transcoding.
        videoConfig = {"Width": 640, "Bitrate": 500, "Fps": 60, "Remove": False, "Codec": "H.264", "Gop": "250"}
        transcodeTemplate["Video"] = videoConfig
    
        # The configurations of audio stream transcoding.
        audioConfig = {"Codec": "AAC", "Bitrate": "128", "Channels": "2", "Samplerate": "32000"}
        transcodeTemplate["Audio"] = audioConfig
    
        # The container for encapsulation.
        container = {"Format": "mp4"}
        transcodeTemplate["Container"] = container
    
        # The configurations of conditional transcoding.
        condition = {"IsCheckReso": False, "IsCheckResoFail": False, "IsCheckVideoBitrate": False,
                     "IsCheckVideoBitrateFail": False, "IsCheckAudioBitrate": False, "IsCheckAudioBitrateFail": False}
        transcodeTemplate["TransConfig"] = condition
    
        """
        # The configurations of encryption. Only HLS encryption is supported.
        encryptSetting = {"EncryptType": "Private"}
        transcodeTemplate["EncryptSetting"] = encryptSetting
        """
    
        # The IDs of associated watermarks.
        watermarkIdList = []
        #watermarkIdList.append("<WatermarkId>")
        watermarkIdList.append("USER_DEFAULT_WATERMARK")
        transcodeTemplate["WatermarkIds"] = watermarkIdList
    
        transcodeTemplateList.append(transcodeTemplate)
    
        return transcodeTemplateList
    
    
    """  Modify a transcoding template."""
    def update_transcode_template_group(clt):
        request = UpdateTranscodeTemplateGroupRequest.UpdateTranscodeTemplateGroupRequest()
    
        # Specify the transcoding template group ID.
        request.set_TranscodeTemplateGroupId("<TranscodeTemplateGroupId>")
    
        # Specify the transcoding template configuration.
        transcodeTemplateList = build_transcode_template_list()
        request.set_TranscodeTemplateList(json.dumps(transcodeTemplateList))
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        res = update_transcode_template_group(clt)
        print(json.dumps(res, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Query transcoding template groups {#h2--div-id-listtranscodetemplategroup-div-4}
--------------------------------------------------------------------------------

You can call the ListTranscodeTemplateGroup operation to query transcoding template groups.
For more information about the request and response parameters of this operation, see [ListTranscodeTemplateGroup](/intl.en-US/API Reference/Media processing/Transcoding template/ListTranscodeTemplateGroup.md). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import ListTranscodeTemplateGroupRequest
    def list_transcode_template_group(clt):
        request = ListTranscodeTemplateGroupRequest.ListTranscodeTemplateGroupRequest()
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        data = list_transcode_template_group(clt)
        for item in data['TranscodeTemplateGroupList']:
            print("TranscodeTemplateGroupId: %s, Name: %s" % (item['TranscodeTemplateGroupId'], item['Name']))
    
        print(json.dumps(data, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Query a transcoding template group {#h2--div-id-gettranscodetemplategroup-div-5}
--------------------------------------------------------------------------------

You can call the GetTranscodeTemplateGroup operation to query details about a transcoding template group.
For more information about the request and response parameters of this operation, see [GetTranscodeTemplateGroup](/intl.en-US/API Reference/Media processing/Transcoding template/GetTranscodeTemplateGroup.md). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import GetTranscodeTemplateGroupRequest
    def get_transcode_template_group(clt):
        request = GetTranscodeTemplateGroupRequest.GetTranscodeTemplateGroupRequest()
        request.set_TranscodeTemplateGroupId("<TranscodeTemplateGroupId>")
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        templateGroup = get_transcode_template_group(clt)
        for item in templateGroup['TranscodeTemplateGroup']['TranscodeTemplateList']:
            print("TranscodeTemplateId: %s, TemplateName: %s, Definition: %s" %
                  (item['TranscodeTemplateId'], item['TemplateName'], item['Definition']))
    
        print(json.dumps(templateGroup, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Specify a transcoding template group as the default one {#h2--div-id-setdefaulttranscodetemplategroup-div-6}
------------------------------------------------------------------------------------------------------------

You can call the SetDefaultTranscodeTemplateGroup operation to specify a transcoding template group as the default one.
For more information about the request and response parameters of this operation, see [SetDefaultTranscodeTemplateGroup](/intl.en-US/API Reference/Media processing/Transcoding template/SetDefaultTranscodeTemplateGroup.md). Example: 
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import SetDefaultTranscodeTemplateGroupRequest
    def set_default_transcode_template_group(clt):
        request = SetDefaultTranscodeTemplateGroupRequest.SetDefaultTranscodeTemplateGroupRequest()
        request.set_TranscodeTemplateGroupId("<TranscodeTemplateGroupId>")
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        res = set_default_transcode_template_group(clt)
        print(json.dumps(res, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Delete a transcoding template group {#h2--div-id-deletetranscodetemplategroup-div-7}
------------------------------------------------------------------------------------

You can call the DeleteTranscodeTemplateGroup operation to delete a transcoding template group.
For more information about the request and response parameters of this operation, see [DeleteTranscodeTemplateGroup](/intl.en-US/API Reference/Media processing/Transcoding template/DeleteTranscodeTemplateGroup.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import DeleteTranscodeTemplateGroupRequest
    def delete_transcode_template_group(clt):
        request = DeleteTranscodeTemplateGroupRequest.DeleteTranscodeTemplateGroupRequest()
        request.set_TranscodeTemplateGroupId("<TranscodeTemplateGroupId>")
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        res = delete_transcode_template_group(clt)
        print(json.dumps(res, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



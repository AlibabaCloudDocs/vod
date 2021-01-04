Transcoding template 
=========================================

This topic provides examples on how to use the API operations of the transcoding template module. The API operations are encapsulated in ApsaraVideo VOD SDK for Java. You can call the API operations to create, modify, delete, and query transcoding template groups. You can also specify a transcoding template group as the default one.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/SDK for Java/Initialization.md).

Create a transcoding template group {#h2--div-id-addtranscodetemplategroup-div-2}
---------------------------------------------------------------------------------

You can call the AddTranscodeTemplateGroup operation to create a transcoding template group.

For more information about the request and response parameters of this operation, see [AddTranscodeTemplateGroup](). Example:

    import com.aliyuncs.vod.model.v20170321.AddTranscodeTemplateGroupRequest;
    import com.aliyuncs.vod.model.v20170321.AddTranscodeTemplateGroupResponse;
    
    /**
     * Create a transcoding template group.
     */
    public static AddTranscodeTemplateGroupResponse addTranscodeTemplateGroup(DefaultAcsClient client) throws Exception {
        AddTranscodeTemplateGroupRequest request = new AddTranscodeTemplateGroupRequest();
        // The ID of the transcoding template.
        request.setName("grouptest");
        request.setTranscodeTemplateList(buildTranscodeTemplateList().toJSONString());
        return client.getAcsResponse(request);
    }
    
    /**
     * Build the parameters of the transcoding template that you want to add.
     *
     * @return
     */
    public static JSONArray buildTranscodeTemplateList() {
        JSONObject transcodeTemplate = new JSONObject();
        // The name of the template.
        transcodeTemplate.put("TemplateName", "testtemplate");
    
        // The definition.
        transcodeTemplate.put("Definition", "LD");
    
        // The configurations of video stream transcoding.
        JSONObject video = new JSONObject();
        video.put("Width", 640);
        video.put("Bitrate", 400);
        video.put("Fps", 25);
        video.put("Remove", false);
        video.put("Codec", "H.264");
        video.put("Gop", "250");
        transcodeTemplate.put("Video", video);
    
        // The configurations of audio stream transcoding.
        JSONObject audio = new JSONObject();
        audio.put("Codec", "AAC");
        audio.put("Bitrate", "64");
        audio.put("Channels", "2");
        audio.put("Samplerate", "32000");
        transcodeTemplate.put("Audio", audio);
    
        // The container for encapsulation.
        JSONObject container = new JSONObject();
        container.put("Format", "mp4");
        transcodeTemplate.put("Container", container);
    
        // The configurations of conditional transcoding.
        JSONObject transconfig = new JSONObject();
        transconfig.put("IsCheckReso", false);
        transconfig.put("IsCheckResoFail", false);
        transconfig.put("IsCheckVideoBitrate", false);
        transconfig.put("IsCheckVideoBitrateFail", false);
        transconfig.put("IsCheckAudioBitrate", false);
        transconfig.put("IsCheckAudioBitrateFail", false);
        transcodeTemplate.put("TransConfig", transconfig);
    
        // The configurations of encryption, which is supported only for M3U8 videos.
        //JSONObject encryptSetting = new JSONObject();
        //encryptSetting.put("EncryptType", "Private");
        //transcodeTemplate.put("EncryptSetting", encryptSetting);
    
        // The IDs of associated watermarks.
        JSONArray watermarkIdList = new JSONArray();
        watermarkIdList.add("263261bdc1ff65782f8995c6dd22a16a");
        // USER_DEFAULT_WATERMARK indicates the ID of the default watermark.
        watermarkIdList.add("USER_DEFAULT_WATERMARK");
        transcodeTemplate.put("WatermarkIds", watermarkIdList);
    
        JSONArray transcodeTemplateList = new JSONArray();
        transcodeTemplateList.add(transcodeTemplate);
        return transcodeTemplateList;
    }
    
    /**
     * Call example
     */
    public static void main(String[] args) throws ClientException {
        DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        AddTranscodeTemplateGroupResponse response = new AddTranscodeTemplateGroupResponse();
        try {
            response = addTranscodeTemplateGroup(client);
            System.out.println("TranscodeTemplateGroupId = " + response.getTranscodeTemplateGroupId());
        } catch (Exception e) {
            System.out.println("ErrorMessage = " + e.getLocalizedMessage());
        }
        System.out.println("RequestId = " + response.getRequestId());
    }



Modify a transcoding template group {#h2--div-id-updatetranscodetemplategroup-div-3}
------------------------------------------------------------------------------------

You can call the UpdateTranscodeTemplateGroup operation to modify a transcoding template group.

For more information about the request and response parameters of this operation, see [UpdateTranscodeTemplateGroup](). Example:

    import com.aliyuncs.vod.model.v20170321.UpdateTranscodeTemplateGroupRequest;
    import com.aliyuncs.vod.model.v20170321.UpdateTranscodeTemplateGroupResponse;
    
    /**
     * Modify a transcoding template group.
     */
    public static UpdateTranscodeTemplateGroupResponse updateTranscodeTemplateGroup(DefaultAcsClient client) throws Exception {
        UpdateTranscodeTemplateGroupRequest request = new UpdateTranscodeTemplateGroupRequest();
        request.setName("grouptest1");
        // The ID of the transcoding template group.
        request.setTranscodeTemplateGroupId("4c71a339fecec0152b4fa6f452****");
        request.setTranscodeTemplateList(buildTranscodeTemplateList().toJSONString());
        return client.getAcsResponse(request);
    }
    
    /**
     * Build the parameters of the transcoding template that you want to modify.
     *
     * @return
     */
    public static JSONArray buildTranscodeTemplateList() {
        JSONObject transcodeTemplate = new JSONObject();
        // The ID of the transcoding template.
        transcodeTemplate.put("TranscodeTemplateId", "85c2b18ac08fda33e8f6d9c56242f");
    
         // The name of the template.
        transcodeTemplate.put("TemplateName", "testtemplate");
    
        // The configurations of video stream transcoding.
        JSONObject video = new JSONObject();
        video.put("Width", 960);
        video.put("Bitrate", 900);
        video.put("Fps", 25);
        video.put("Remove", false);
        video.put("Codec", "H.264");
        video.put("Gop", "250");
        transcodeTemplate.put("Video", video);
    
        // The configurations of audio stream transcoding.
        JSONObject audio = new JSONObject();
        audio.put("Codec", "AAC");
        audio.put("Bitrate", "96");
        audio.put("Channels", "2");
        audio.put("Samplerate", "32000");
        transcodeTemplate.put("Audio", audio);
    
        // The container for encapsulation.
        JSONObject container = new JSONObject();
        container.put("Format", "mp4");
        transcodeTemplate.put("Container", container);
    
        // The configurations of conditional transcoding.
        JSONObject transconfig = new JSONObject();
        transconfig.put("IsCheckReso", false);
        transconfig.put("IsCheckResoFail", false);
        transconfig.put("IsCheckVideoBitrate", false);
        transconfig.put("IsCheckVideoBitrateFail", false);
        transconfig.put("IsCheckAudioBitrate", false);
        transconfig.put("IsCheckAudioBitrateFail", false);
        transcodeTemplate.put("TransConfig", transconfig);
    
        // The configurations of encryption, which is supported only for M3U8 videos.
        JSONObject encryptSetting = new JSONObject();
        encryptSetting.put("EncryptType", "Private");
    
        // The IDs of associated watermarks.
        JSONArray watermarkIdList = new JSONArray();
        watermarkIdList.add("263261bdc1ff65782f95c6dd22a16a");
        // USER_DEFAULT_WATERMARK indicates the ID of the default watermark.
        watermarkIdList.add("USER_DEFAULT_WATERMARK");
        transcodeTemplate.put("WatermarkIds", watermarkIdList);
    
        JSONArray transcodeTemplateList = new JSONArray();
        transcodeTemplateList.add(transcodeTemplate);
        return transcodeTemplateList;
    }
    
    /**
     * Call example
     */
    public static void main(String[] args) throws ClientException {
        DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        UpdateTranscodeTemplateGroupResponse response = new UpdateTranscodeTemplateGroupResponse();
        try {
            response = updateTranscodeTemplateGroup(client);
            System.out.println("TranscodeTemplateGroupId = " + response.getTranscodeTemplateGroupId());
        } catch (Exception e) {
            System.out.println("ErrorMessage = " + e.getLocalizedMessage());
        }
        System.out.println("RequestId = " + response.getRequestId());
    }



Query transcoding template groups {#h2--div-id-listtranscodetemplategroup-div-4}
--------------------------------------------------------------------------------

You can call the ListTranscodeTemplateGroup operation to query transcoding template groups.
For more information about the request and response parameters of this operation, see [ListTranscodeTemplateGroup](). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.aliyuncs.vod.model.v20170321.ListTranscodeTemplateGroupRequest;
    import com.aliyuncs.vod.model.v20170321.ListTranscodeTemplateGroupResponse;
    
    /**
     * Query transcoding template groups.
     */
    public static ListTranscodeTemplateGroupResponse listTranscodeTemplateGroup(DefaultAcsClient client) throws Exception {
        ListTranscodeTemplateGroupRequest request = new ListTranscodeTemplateGroupRequest();
        return client.getAcsResponse(request);
    }
    
    /**
     * Call example
     */
    public static void main(String[] args) throws ClientException {
        DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        ListTranscodeTemplateGroupResponse response = new ListTranscodeTemplateGroupResponse();
        try {
            response = listTranscodeTemplateGroup(client);
            System.out.println("TranscodeTemplateGroupId = " + response.getTranscodeTemplateGroupList().get(0).getTranscodeTemplateGroupId());
            System.out.println("GroupName = " + response.getTranscodeTemplateGroupList().get(0).getName());
        } catch (Exception e) {
            System.out.println("ErrorMessage = " + e.getLocalizedMessage());
        }
        System.out.println("RequestId = " + response.getRequestId());
    }



Query a transcoding template group {#h2--div-id-gettranscodetemplategroup-div-5}
--------------------------------------------------------------------------------

You can call the GetTranscodeTemplateGroup operation to query details about a transcoding template group.
For more information about the request and response parameters of this operation, see [GetTranscodeTemplateGroup](). Example: 
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.aliyuncs.vod.model.v20170321.GetTranscodeTemplateGroupRequest;
    import com.aliyuncs.vod.model.v20170321.GetTranscodeTemplateGroupResponse;
    
    /**
     * Query a transcoding template group.
     */
    public static GetTranscodeTemplateGroupResponse getTranscodeTemplateGroup(DefaultAcsClient client) throws Exception {
        GetTranscodeTemplateGroupRequest request = new GetTranscodeTemplateGroupRequest();
        request.setTranscodeTemplateGroupId("a0fa0fda545e50e7a3eb75491f9f4");
        return client.getAcsResponse(request);
    }
    
    /**
     * Call example
     */
    public static void main(String[] args) throws ClientException {
        DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        GetTranscodeTemplateGroupResponse response = new GetTranscodeTemplateGroupResponse();
        try {
            response = getTranscodeTemplateGroup(client);
           if (response.getTranscodeTemplateGroup().getTranscodeTemplateList().size() > 0) {
                    // The ID of the transcoding template group.
                    System.out.println("TranscodeTemplateGroupId = " + response.getTranscodeTemplateGroup().getTranscodeTemplateGroupId());
                    // The name of the transcoding template group.
                    System.out.println("Name = " + response.getTranscodeTemplateGroup().getName());
                    // Whether the transcoding template group is the default group.
                    System.out.println("Name = " + response.getTranscodeTemplateGroup().getIsDefault());
                    // The configurations of video stream transcoding in the template.
                    System.out.println("Video = " + response.getTranscodeTemplateGroup().getTranscodeTemplateList().get(0).getVideo());
                    // The configurations of audio stream transcoding in the template.
                    System.out.println("Audio = " + response.getTranscodeTemplateGroup().getTranscodeTemplateList().get(0).getAudio());
                    // The definition of the transcoding template.
                    System.out.println("Definition = " + response.getTranscodeTemplateGroup().getTranscodeTemplateList().get(0).getDefinition());
                    // The IDs of associated watermarks for transcoding.
                    System.out.println("WatermarkIds = " + response.getTranscodeTemplateGroup().getTranscodeTemplateList().get(0).getWatermarkIds());
                    // The container for encapsulation that the transcoding template uses.
                    System.out.println("Container = " + response.getTranscodeTemplateGroup().getTranscodeTemplateList().get(0).getContainer());
                    // The ID of the transcoding template.
                    System.out.println("TranscodeTemplateId = " + response.getTranscodeTemplateGroup().getTranscodeTemplateList().get(0).getTranscodeTemplateId());
                    // The name of the transcoding template.
                    System.out.println("TemplateName = " + response.getTranscodeTemplateGroup().getTranscodeTemplateList().get(0).getTemplateName());
                }
        } catch (Exception e) {
            System.out.println("ErrorMessage = " + e.getLocalizedMessage());
        }
        System.out.println("RequestId = " + response.getRequestId());
    }



Specify a transcoding template group as the default one {#h2--div-id-setdefaulttranscodetemplategroup-div-6}
------------------------------------------------------------------------------------------------------------

You can call the SetDefaultTranscodeTemplateGroup operation to specify a transcoding template group as the default one.
For more information about the request and response parameters of this operation, see [SetDefaultTranscodeTemplateGroup](). Example: 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.aliyuncs.vod.model.v20170321.SetDefaultTranscodeTemplateGroupRequest;
    import com.aliyuncs.vod.model.v20170321.SetDefaultTranscodeTemplateGroupResponse;
    
    /**
     * Specify a transcoding template group as the default one.
     */
    public static SetDefaultTranscodeTemplateGroupResponse setDefaultTranscodeTemplateGroup(DefaultAcsClient client) throws Exception {
        SetDefaultTranscodeTemplateGroupRequest request = new SetDefaultTranscodeTemplateGroupRequest();
        request.setTranscodeTemplateGroupId("ecf03526c945ae022165c469f4548e");
        return client.getAcsResponse(request);
    }
    
    /**
     * Call example
     */
    public static void main(String[] args) throws ClientException {
        DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        SetDefaultTranscodeTemplateGroupResponse response = new SetDefaultTranscodeTemplateGroupResponse();
        try {
            response = setDefaultTranscodeTemplateGroup(client);
        } catch (Exception e) {
            System.out.println("ErrorMessage = " + e.getLocalizedMessage());
        }
        System.out.println("RequestId = " + response.getRequestId());
    }



Delete a transcoding template group {#h2--div-id-deletetranscodetemplategroup-div-7}
------------------------------------------------------------------------------------

You can call the DeleteTranscodeTemplateGroup operation to delete a transcoding template group.
For more information about the request and response parameters of this operation, see [DeleteTranscodeTemplateGroup](). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.aliyuncs.vod.model.v20170321.DeleteTranscodeTemplateGroupRequest;
    import com.aliyuncs.vod.model.v20170321.DeleteTranscodeTemplateGroupResponse;
    
    /**
     * Delete a transcoding template group.
     */
    public static DeleteTranscodeTemplateGroupResponse deleteTranscodeTemplateGroup(DefaultAcsClient client) throws Exception {
        DeleteTranscodeTemplateGroupRequest request = new DeleteTranscodeTemplateGroupRequest();
        request.setTranscodeTemplateGroupId("a0fa0fda545e50e91a3eb75491****");
        request.setForceDelGroup("false");
        request.setTranscodeTemplateIds("ddddddd,ffffffff");
        return client.getAcsResponse(request);
    }
    
    /**
     * Call example
     */
    public static void main(String[] args) throws ClientException {
        DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        DeleteTranscodeTemplateGroupResponse response = new DeleteTranscodeTemplateGroupResponse();
        try {
            response = deleteTranscodeTemplateGroup(client);
        } catch (Exception e) {
            System.out.println("ErrorMessage = " + e.getLocalizedMessage());
        }
        System.out.println("RequestId = " + response.getRequestId());
    }



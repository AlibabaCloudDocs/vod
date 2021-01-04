Transcoding template 
=========================================

This topic provides examples on how to use the API operations of the transcoding template module. The API operations are encapsulated in ApsaraVideo VOD SDK for PHP. You can call the API operations to create, modify, delete, and query transcoding template groups. You can also specify a transcoding template group as the default one.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/PHP SDK/Install the SDK/Initialization.md).

Create a transcoding template group {#h2--div-id-addtranscodetemplategroup-div-2}
---------------------------------------------------------------------------------

You can call the AddTranscodeTemplateGroup operation to create a transcoding template group.

For more information about the request and response parameters of this operation, see [AddTranscodeTemplateGroup](). Example:

    /**
     * Create a transcoding template group.
     * @return
     */
    function buildTranscodeTemplateList() {
        $transcodeTemplateList = array();
        $transcodeTemplate = array();
    
        // The configurations of video stream transcoding.
        $video = array();
        $video["Width"] = 640;
        $video["Bitrate"] = 400;
        $video["Fps"] = 25;
        $video["Remove"] = false;
        $video["Codec"] = "H.264";
        $video["Gop"] = 250;
        $transcodeTemplate["Video"] = $video;
    
        // The configurations of audio stream transcoding.
        $audio = array();
        $audio["Codec"] = "AAC";
        $audio["Bitrate"] = 64;
        $audio["Channels"] = 2;
        $audio["Samplerate"] = 32000;
        $transcodeTemplate["Audio"] = $audio;
    
        // The container for encapsulation.
        $container = array();
        $container["Format"] = "mp4";
        $transcodeTemplate["Container"] = $container;
    
        // The configurations of conditional transcoding.
        $transconfig = array();
        $transconfig["IsCheckReso"] = false;
        $transconfig["IsCheckResoFail"] = false;
        $transconfig["IsCheckVideoBitrate"] = false;
        $transconfig["IsCheckVideoBitrateFail"] = false;
        $transconfig["IsCheckAudioBitrate"] = false;
        $transconfig["IsCheckAudioBitrateFail"] = false;
        $transcodeTemplate["TransConfig"] = $transconfig;
    
        // The configurations of encryption, which is supported only for M3U8 videos.
        //$encryptSetting= array();
        //$encryptSetting["EncryptType"] = "Private";
        //$transcodeTemplate["EncryptSetting"] = $encryptSetting;
    
        // The definition.
        $transcodeTemplate["Definition"] = "LD";
    
        // The name of the template.
        $transcodeTemplate["TemplateName"] = "testtemplate";
    
        // The IDs of associated watermarks.
        $watermarkIdList= array();
        $watermarkIdList[] = "263261bdc1ff65782f8995c6dd52****";
        // USER_DEFAULT_WATERMARK indicates the ID of the default watermark.
        $watermarkIdList[] = "USER_DEFAULT_WATERMARK";
        $transcodeTemplate["WatermarkIds"] = $watermarkIdList;
        $transcodeTemplateList[] = $transcodeTemplate;
    
        return json_encode($transcodeTemplateList);
    }
    
    /**
     * Add a transcoding template group.
     */
    function addTranscodeTemplateGroup($client) {
        $request = new vod\AddTranscodeTemplateGroupRequest();
        // The name of the transcoding template group.
        $request->setName("grouptest");
        // The configurations of the transcoding template group.
        $request->setTranscodeTemplateList(buildTranscodeTemplateList());
    
        return $client->getAcsResponse($request);
    }
    
    /**
     * Call example
     */
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
        $result = addTranscodeTemplateGroup($client);
    
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Modify a transcoding template group {#h2--div-id-updatetranscodetemplategroup-div-3}
------------------------------------------------------------------------------------

You can call the UpdateTranscodeTemplateGroup operation to modify a transcoding template group.
For more information about the request and response parameters of this operation, see [UpdateTranscodeTemplateGroup](). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    /**
     * Create a transcoding template group.
     * @return
     */
    function buildTranscodeTemplateList() {
        $transcodeTemplateList = array();
        $transcodeTemplate = array();
    
        // The configurations of video stream transcoding.
        $video = array();
        $video["Width"] = 960;
        $video["Bitrate"] = 900;
        $video["Fps"] = 25;
        $video["Remove"] = false;
        $video["Codec"] = "H.264";
        $video["Gop"] = 250;
        $transcodeTemplate["Video"] = $video;
    
        // The configurations of audio stream transcoding.
        $audio = array();
        $audio["Codec"] = "AAC";
        $audio["Bitrate"] = 96;
        $audio["Channels"] = 2;
        $audio["Samplerate"] = 32000;
        $transcodeTemplate["Audio"] = $audio;
    
        // The container for encapsulation.
        $container = array();
        $container["Format"] = "mp4";
        $transcodeTemplate["Container"] = $container;
    
        // The configurations of conditional transcoding.
        $transconfig = array();
        $transconfig["IsCheckReso"] = false;
        $transconfig["IsCheckResoFail"] = false;
        $transconfig["IsCheckVideoBitrate"] = false;
        $transconfig["IsCheckVideoBitrateFail"] = false;
        $transconfig["IsCheckAudioBitrate"] = false;
        $transconfig["IsCheckAudioBitrateFail"] = false;
        $transcodeTemplate["TransConfig"] = $transconfig;
    
        // The configurations of encryption, which is supported only for M3U8 videos.
        //$encryptSetting= array();
        //$encryptSetting["EncryptType"] = "Private";
        //$transcodeTemplate["EncryptSetting"] = $encryptSetting;
    
        // The definition.
        $transcodeTemplate["Definition"] = "SD";
    
        // The name of the template.
        $transcodeTemplate["TemplateName"] = "testtemplate";
    
        // The ID of the template.
        $transcodeTemplate["TranscodeTemplateId"] = "214a67fab9fdf920f486faa7752****";
    
        // The IDs of associated watermarks.
        $watermarkIdList= array();
        $watermarkIdList[] = "263261bdc1ff65782f8995c6dd52****";
        // USER_DEFAULT_WATERMARK indicates the ID of the default watermark.
        $watermarkIdList[] = "USER_DEFAULT_WATERMARK";
        $transcodeTemplate["WatermarkIds"] = $watermarkIdList;
        $transcodeTemplateList[] = $transcodeTemplate;
    
        return json_encode($transcodeTemplateList);
    }
    
    /**
     * Modify a transcoding template group.
     */
    function updateTranscodeTemplateGroup($client) {
        $request = new vod\UpdateTranscodeTemplateGroupRequest();
        // The name of the transcoding template group.
        $request->setName("grouptest1");
        // The ID of the transcoding template group.
        $request->setTranscodeTemplateGroupId("014a67fab9fdf920f486faa7752****");
        // The configurations of the transcoding template group.
        $request->setTranscodeTemplateList(buildTranscodeTemplateList());
    
        return $client->getAcsResponse($request);
    }
    
    /**
     * Call example
     */
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
        $result = updateTranscodeTemplateGroup($client);
    
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Query transcoding template groups {#h2--div-id-listtranscodetemplategroup-div-4}
--------------------------------------------------------------------------------

You can call the ListTranscodeTemplateGroup operation to query transcoding template groups.
For more information about the request and response parameters of this operation, see [ListTranscodeTemplateGroup](). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    /**
     * Query transcoding template groups.
     */
    function listTranscodeTemplateGroup($client) {
        $request = new vod\ListTranscodeTemplateGroupRequest();
        return $client->getAcsResponse($request);
    }
    
    /**
     * Call example
     */
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
        $result = listTranscodeTemplateGroup($client);
    
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Query a transcoding template group {#h2--div-id-gettranscodetemplategroup-div-5}
--------------------------------------------------------------------------------

You can call the GetTranscodeTemplateGroup operation to query a transcoding template group.
For more information about the request and response parameters of this operation, see [GetTranscodeTemplateGroup](/intl.en-US/API Reference/Media processing/Snapshot Template/GetVodTemplate.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    /**
     * Query a transcoding template group.
     */
    function getTranscodeTemplateGroup($client) {
        $request = new vod\GetTranscodeTemplateGroupRequest();
        // The ID of the transcoding template group.
        $request->setTranscodeTemplateGroupId("014a67fab9fdf920f486faa7752****");
    
        return $client->getAcsResponse($request);
    }
    
    /**
     * Call example
     */
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
        $result = getTranscodeTemplateGroup($client);
    
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Specify a transcoding template group as the default one {#h2--div-id-setdefaulttranscodetemplategroup-div-6}
------------------------------------------------------------------------------------------------------------

You can call the SetDefaultTranscodeTemplateGroup operation to specify a transcoding template group as the default one.
For more information about the request and response parameters of this operation, see [SetDefaultTranscodeTemplateGroup](). Example: 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    /**
     * Specify a transcoding template group as the default one.
     */
    function setDefaultTranscodeTemplateGroup($client) {
        $request = new vod\SetDefaultTranscodeTemplateGroupRequest();
        // The ID of the transcoding template group.
        $request->setTranscodeTemplateGroupId("014a67fab9fdf920f486faa7752****");
    
        return $client->getAcsResponse($request);
    }
    
    /**
     * Call example
     */
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
        $result = setDefaultTranscodeTemplateGroup($client);
    
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Delete a transcoding template group {#h2--div-id-deletetranscodetemplategroup-div-7}
------------------------------------------------------------------------------------

You can call the DeleteTranscodeTemplateGroup operation to delete a transcoding template group.
For more information about the request and response parameters of this operation, see [DeleteTranscodeTemplateGroup](). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    /**
     * Delete a transcoding template group.
     */
    function deleteTranscodeTemplateGroup($client) {
        $request = new vod\DeleteTranscodeTemplateGroupRequest();
        // The ID of the transcoding template group.
        $request->setTranscodeTemplateGroupId("014a67fab9fdf920f486faa77352****");
    
        return $client->getAcsResponse($request);
    }
    
    /**
     * Call example
     */
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
        $result = deleteTranscodeTemplateGroup($client);
    
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Transcoding template 
=========================================

This topic provides examples on how to use the API operations of the transcoding template module. The API operations are encapsulated in ApsaraVideo VOD SDK for Node.js. You can call the API operations to create, modify, delete, and query transcoding template groups. You can also specify a transcoding template group as the default one.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/Node.js SDK/Initialization.md).

Create a transcoding template group {#h2--div-id-addtranscodetemplategroup-div-2}
---------------------------------------------------------------------------------

You can call the AddTranscodeTemplateGroup operation to create a transcoding template group.
For more information about the request and response parameters of this operation, see [AddTranscodeTemplateGroup](). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    var transcodeTemplateList = [
        {
            // The configurations of video stream transcoding.
            Video: {
                Width: 640,
                Bitrate: 400,
                Fps: 25,
                Remove: false,
                Codec: 'H.264',
                Gop: '250'
            },
            // The configurations of audio stream transcoding.
            Audio: {
                Codec: 'AAC',
                Bitrate: '64',
                Channels: '2',
                Samplerate: '32000'
            },
            // The container for encapsulation.
            Container: {
                Format: 'mp4'
            },
            // The configurations of conditional transcoding.
            TransConfig: {
                IsCheckReso: false,
                IsCheckResoFail: false,
                IsCheckVideoBitrate: false,
                IsCheckVideoBitrateFail: false,
                IsCheckAudioBitrate: false,
                IsCheckAudioBitrateFail: false
            },
            // The configurations of encryption, which is supported only for M3U8 videos.
            // EncryptSetting: {
            //     EncryptType: 'Private'
            // },
            // The definition.
            Definition: 'LD',
            // The name of the template.
            TemplateName: 'testtemplate',
            // The IDs of associated watermarks.
            WatermarkIds: ['USER_DEFAULT_WATERMARK','789456bdc1ff65782f8995c6dd45****']
        }
    ];
    client.request("AddTranscodeTemplateGroup", {
        // The name of the transcoding template group.
        Name: 'grouptest',
        // The configurations of the transcoding template.
        TranscodeTemplateList: JSON.stringify(transcodeTemplateList)
    }, {}).then(function (response) {
        console.log('TranscodeTemplateGroupId = ' + response.TranscodeTemplateGroupId);
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Modify a transcoding template group {#h2--div-id-updatetranscodetemplategroup-div-3}
------------------------------------------------------------------------------------

You can call the UpdateTranscodeTemplateGroup operation to modify a transcoding template group.
For more information about the request and response parameters of this operation, see [UpdateTranscodeTemplateGroup](). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    var transcodeTemplateList = [
        {
            // The ID of the transcoding template.
            TranscodeTemplateId: '9875824423bca267f931d3b25687****',
            // The configurations of video stream transcoding.
            Video: {
                Width: 640,
                Bitrate: 500,
                Fps: 25,
                Remove: false,
                Codec: 'H.264',
                Gop: '250'
            },
            // The configurations of audio stream transcoding.
            Audio: {
                Codec: 'AAC',
                Bitrate: '64',
                Channels: '2',
                Samplerate: '32000'
            },
            // The container for encapsulation.
            Container: {
                Format: 'mp4'
            },
            // The configurations of conditional transcoding.
            TransConfig: {
                IsCheckReso: false,
                IsCheckResoFail: false,
                IsCheckVideoBitrate: false,
                IsCheckVideoBitrateFail: false,
                IsCheckAudioBitrate: false,
                IsCheckAudioBitrateFail: false
            },
            // The configurations of encryption, which is supported only for M3U8 videos.
            // EncryptSetting: {
            //     EncryptType: 'Private'
            // },
            // The definition.
            Definition: 'LD',
            // The name of the template.
            TemplateName: 'testtemplate',
            // The IDs of associated watermarks.
            WatermarkIds: ['USER_DEFAULT_WATERMARK','854325bdc1ff65782f8995c6dd85****']
        }
    ];
    client.request("UpdateTranscodeTemplateGroup", {
        TranscodeTemplateGroupId: '789458252788dfd94e27d7358b254****',
        TranscodeTemplateList: JSON.stringify(transcodeTemplateList)
    }, {}).then(function (response) {
        console.log('TranscodeTemplateGroupId = ' + response.TranscodeTemplateGroupId);
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Query transcoding template groups {#h2--div-id-listtranscodetemplategroup-div-4}
--------------------------------------------------------------------------------

You can call the ListTranscodeTemplateGroup operation to query transcoding template groups.
For more information about the request and response parameters of this operation, see [ListTranscodeTemplateGroup](). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("ListTranscodeTemplateGroup", {}, {}).then(function (response) {
        if (response.TranscodeTemplateGroupList && response.TranscodeTemplateGroupList.length > 0){
            for (var i=0; i<response.TranscodeTemplateGroupList.length; i++){
                var transcodeTemplateGroup = response.TranscodeTemplateGroupList[i];
                console.log('The ' + i + ' TranscodeTemplateGroup.') ;
                // The ID of the transcoding template group.
                console.log('TranscodeTemplateGroupId = ' + transcodeTemplateGroup.TranscodeTemplateGroupId);
                // The name of the transcoding template group.
                console.log('Name = ' + transcodeTemplateGroup.Name);
                // The creation time of the transcoding template group.
                console.log('CreationTime = ' + transcodeTemplateGroup.CreationTime);
                // The last modification time of the transcoding template group.
                console.log('ModifyTime = ' + transcodeTemplateGroup.ModifyTime);
                // Whether the transcoding template group is default.
                console.log('IsDefault = ' + transcodeTemplateGroup.IsDefault);
            }
        }
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Query a transcoding template group {#h2--div-id-gettranscodetemplategroup-div-5}
--------------------------------------------------------------------------------

You can call the GetTranscodeTemplateGroup operation to query details about a transcoding template group.
For more information about the request and response parameters of this operation, see [GetTranscodeTemplateGroup](). Example: 
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("GetTranscodeTemplateGroup", {
        TranscodeTemplateGroupId: '81553142788dfd94e27d7358b285****'
    }, {}).then(function (response) {
        console.log(response);
        if (response.TranscodeTemplateGroup){
            // The ID of the transcoding template group.
            console.log('TranscodeTemplateGroupId = ' + response.TranscodeTemplateGroup.TranscodeTemplateGroupId);
            // The name of the transcoding template group.
            console.log('Name = ' + response.TranscodeTemplateGroup.Name);
            // The creation time of the transcoding template group.
            console.log('CreationTime = ' + response.TranscodeTemplateGroup.CreationTime);
            // The last modification time of the transcoding template group.
            console.log('ModifyTime = ' + response.TranscodeTemplateGroup.ModifyTime);
            // The configurations of the transcoding template.
            if (response.TranscodeTemplateGroup.TranscodeTemplateList && response.TranscodeTemplateGroup.TranscodeTemplateList.length > 0){
                for (var i=0; i<response.TranscodeTemplateGroup.TranscodeTemplateList.length; i++){
                    var transcodeTemplate = response.TranscodeTemplateGroup.TranscodeTemplateList[i];
                    console.log("The " + i + " TranscodeTemplate.") ;
                    // The ID of the transcoding template.
                    console.log('TranscodeTemplateId = ' + transcodeTemplate.TranscodeTemplateId);
                    // The name of the transcoding template.
                    console.log('TemplateName = ' + transcodeTemplate.TemplateName);
                    // The definition of the transcoding template.
                    console.log('Definition = ' + transcodeTemplate.Definition);
                    // The container for encapsulation that the transcoding template uses.
                    console.log('Container = ');
                    console.log(transcodeTemplate.Container);
                    // The configurations of video stream transcoding in the template.
                    console.log('Video = ');
                    console.log(transcodeTemplate.Video);
                    // The configurations of audio stream transcoding in the template.
                    console.log('Audio = ');
                    console.log(transcodeTemplate.Audio);
                    // The configurations of conditional stream transcoding in the template.
                    console.log('TransConfig = ');
                    console.log(transcodeTemplate.TransConfig);
                    // The IDs of associated watermarks for transcoding.
                    console.log('WatermarkIds = ');
                    console.log(transcodeTemplate.WatermarkIds);
                }
            }
        }
    
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Specify a transcoding template group as the default one {#h2--div-id-setdefaulttranscodetemplategroup-div-6}
------------------------------------------------------------------------------------------------------------

You can call the SetDefaultTranscodeTemplateGroup operation to specify a transcoding template group as the default one.
For more information about the request and response parameters of this operation, see [SetDefaultTranscodeTemplateGroup](). Example: 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("SetDefaultTranscodeTemplateGroup", {
        // The ID of the transcoding template group.
        TranscodeTemplateGroupId: '45628142788dfd94e27d7358b258****'
    }, {}).then(function (response) {
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Delete a transcoding template group {#h2--div-id-deletetranscodetemplategroup-div-7}
------------------------------------------------------------------------------------

You can call the DeleteTranscodeTemplateGroup operation to delete a transcoding template group.
For more information about the request and response parameters of this operation, see [DeleteTranscodeTemplateGroup](). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("DeleteTranscodeTemplateGroup", {
        TranscodeTemplateGroupId: '12356442788dfd94e27d7358b285****'
    }, {}).then(function (response) {
        console.log(response);
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



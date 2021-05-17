Video playback 
===================================

This topic provides examples on how to use the API operations of the video playback module. The API operations are encapsulated in ApsaraVideo VOD SDK for Node.js. You can call the API operations to query playback URLs and playback credentials.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/Node.js SDK/Initialization.md).

Query a playback URL {#h2--div-id-getplayinfo-div-2}
----------------------------------------------------

You can call the GetPlayInfo operation to query a playback URL.
For more information about the request and response parameters of this operation, see [GetPlayInfo](/intl.en-US/API Reference/Audio and video playback/GetPlayInfo.md). Example: 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("GetPlayInfo", {
        VideoId: 'VideoId'
    }, {}).then(function (response) {
        // play url
        if (response.PlayInfoList && response.PlayInfoList.PlayInfo && response.PlayInfoList.PlayInfo.length > 0){
            for (var i=0; i<response.PlayInfoList.PlayInfo.length; i++){
                console.log("PlayInfo.PlayURL = " + response.PlayInfoList.PlayInfo[i].PlayURL);
            }
        }
        // base metadata
        if (response.VideoBase){
            console.log('VideoBase.Title = ' + response.VideoBase.Title);
        }
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Query a playback credential {#h2--div-id-getvideoplayauth-div-3}
----------------------------------------------------------------

You can call the GetVideoPlayAuth operation to query a playback credential.
For more information about the request and response parameters of this operation, see [GetVideoPlayAuth](/intl.en-US/API Reference/Audio and video playback/GetVideoPlayAuth.md). Example: 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("GetVideoPlayAuth", {
        VideoId: 'VideoId'
    }, {}).then(function (response) {
        // play auth
        console.log('PlayAuth = ' + response.PlayAuth);
    
        // base metadata
        if (response.VideoMeta){
            console.log('VideoMeta.Title = ' + response.VideoMeta.Title);
        }
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



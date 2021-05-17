Video playback 
===================================

This topic provides examples on how to use the API operations of the video playback module. The API operations are encapsulated in ApsaraVideo VOD SDK for PHP. You can call the API operations to query playback URLs and playback credentials.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/PHP SDK/Install the SDK/Initialization.md).

Query a playback URL {#h2--div-id-getplayinfo-div-2}
----------------------------------------------------

You can call the GetPlayInfo operation to query a playback URL.
For more information about the request and response parameters of this operation, see [GetPlayInfo](/intl.en-US/API Reference/Audio and video playback/GetPlayInfo.md). Example: 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    function getPlayInfo($client, $videoId) {
        $request = new vod\GetPlayInfoRequest();
        $request->setVideoId($videoId);
        $request->setAuthTimeout(3600*24);
        $request->setAcceptFormat('JSON');
        return $client->getAcsResponse($request);
    }
    // Pay attention to the captured exceptions.
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
        $playInfo = getPlayInfo($client, 'videoId');
        print_r($playInfo->PlayInfoList->PlayInfo);
        var_dump($playInfo);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Query a playback credential {#h2--div-id-getvideoplayauth-div-3}
----------------------------------------------------------------

You can call the GetVideoPlayAuth operation to query a playback credential.
For more information about the request and response parameters of this operation, see [GetVideoPlayAuth](/intl.en-US/API Reference/Audio and video playback/GetVideoPlayAuth.md). Example: 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    function getPlayAuth($client, $videoId) {
        $request = new vod\GetVideoPlayAuthRequest();
        $request->setVideoId($videoId);
        $request->setAuthInfoTimeout(3000);
        $request->setAcceptFormat('JSON');
        $response = $client->getAcsResponse($request);
        return $response;
    }
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
        $playAuth = getPlayAuth($client, 'videoId');
        print($playAuth->PlayAuth."\n");
        print_r($playAuth->VideoMeta);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



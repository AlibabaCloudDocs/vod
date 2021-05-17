Video playback 
===================================

This topic provides examples on how to use the API operations of the video playback module. The API operations are encapsulated in ApsaraVideo VOD SDK for Python. You can call the API operations to query playback URLs and playback credentials.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/Python SDK/Initialization.md).

Query a playback URL {#h2--div-id-getplayinfo-div-2}
----------------------------------------------------

You can call the GetPlayInfo operation to query a playback URL.

For more information about the request and response parameters of this operation, see [GetPlayInfo](/intl.en-US/API Reference/Audio and video playback/GetPlayInfo.md). Example:

    from aliyunsdkvod.request.v20170321 import GetPlayInfoRequest
    def get_play_info(clt, videoId):
        request = GetPlayInfoRequest.GetPlayInfoRequest()
        request.set_accept_format('JSON')
        request.set_VideoId(videoId)
        request.set_AuthTimeout(3600*5)
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        playInfo = get_play_info(clt, '<videoId>')
        print(json.dumps(playInfo, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Query a playback credential {#h2--div-id-getvideoplayauth-div-3}
----------------------------------------------------------------

You can call the GetVideoPlayAuth operation to query a playback credential.
For more information about the request and response parameters of this operation, see [GetVideoPlayAuth](/intl.en-US/API Reference/Audio and video playback/GetVideoPlayAuth.md). Example: 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import GetVideoPlayAuthRequest
    def get_video_playauth(clt, videoId):
        request = GetVideoPlayAuthRequest.GetVideoPlayAuthRequest()
        request.set_accept_format('JSON')
        request.set_VideoId(videoId)
        request.set_AuthInfoTimeout(3000)
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        playAuth = get_video_playauth(clt, '<videoId>')
        print(json.dumps(playAuth, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Video playback 
===================================

This topic provides examples on how to use the API operations of the video playback module. The API operations are encapsulated in ApsaraVideo VOD SDK for Java. You can call the API operations to query playback URLs and playback credentials.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/SDK for Java/Initialization.md).

Query a playback URL {#h2--div-id-getplayinfo-div-}
---------------------------------------------------

You can call the GetPlayInfo operation to query a playback URL.

For more information about the request and response parameters of this operation, see [GetPlayInfo](/intl.en-US/API Reference/Video playback/GetPlayInfo.md). Example:

    import com.aliyuncs.vod.model.v20170321.GetPlayInfoRequest;
    import com.aliyuncs.vod.model.v20170321.GetPlayInfoResponse;
    
    /* Query a playback URL. */
    public static GetPlayInfoResponse getPlayInfo(DefaultAcsClient client) throws Exception {
        GetPlayInfoRequest request = new GetPlayInfoRequest();
        request.setVideoId("The video ID");
        return client.getAcsResponse(request);
    }
    
    /* Call example */
    public static void main(String[] argv) {
        DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        GetPlayInfoResponse response = new GetPlayInfoResponse();
        try {
            response = getPlayInfo(client);
            List<GetPlayInfoResponse.PlayInfo> playInfoList = response.getPlayInfoList();
            // The playback URL.
            for (GetPlayInfoResponse.PlayInfo playInfo : playInfoList) {
                System.out.print("PlayInfo.PlayURL = " + playInfo.getPlayURL() + "\n");
            }
            // The information about the video base.
            System.out.print("VideoBase.Title = " + response.getVideoBase().getTitle() + "\n");
        } catch (Exception e) {
            System.out.print("ErrorMessage = " + e.getLocalizedMessage());
        }
        System.out.print("RequestId = " + response.getRequestId() + "\n");
    }



Query a playback credential {#h2--div-id-getvideoplayauth-div-2}
----------------------------------------------------------------

You can call the GetVideoPlayAuth operation to query a playback credential.

For more information about the request and response parameters of this operation, see [GetVideoPlayAuth](/intl.en-US/API Reference/Video playback/GetVideoPlayAuth.md). Example:

    import com.aliyuncs.vod.model.v20170321.GetVideoPlayAuthRequest;
    import com.aliyuncs.vod.model.v20170321.GetVideoPlayAuthResponse;
    
    /* Query a playback credential. */
    public static GetVideoPlayAuthResponse getVideoPlayAuth(DefaultAcsClient client) throws Exception {
        GetVideoPlayAuthRequest request = new GetVideoPlayAuthRequest();
        request.setVideoId("The video ID");
        return client.getAcsResponse(request);
    }
    
    /* Call example */
    public static void main(String[] argv) {
        DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        GetVideoPlayAuthResponse response = new GetVideoPlayAuthResponse();
        try {
            response = getVideoPlayAuth(client);
            // The playback credential.
            System.out.print("PlayAuth = " + response.getPlayAuth() + "\n");
            // The metadata of the video.
            System.out.print("VideoMeta.Title = " + response.getVideoMeta().getTitle() + "\n");
        } catch (Exception e) {
            System.out.print("ErrorMessage = " + e.getLocalizedMessage());
        }
        System.out.print("RequestId = " + response.getRequestId() + "\n");
    }



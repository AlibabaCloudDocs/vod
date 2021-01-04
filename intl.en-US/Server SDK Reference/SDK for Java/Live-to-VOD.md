Live-to-VOD 
================================

This topic provides examples on how to use the API operations of the live-to-VOD module. The API operations are encapsulated in ApsaraVideo VOD SDK for Java. You can call the API operations to query live-to-VOD videos.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/SDK for Java/Initialization.md).

Query live-to-VOD videos {#h2-u67E5u8BE2u76F4u8F6Cu70B9u89C6u9891u5217u88682}
-----------------------------------------------------------------------------

You can call the ListLiveRecordVideo operation to query live-to-VOD videos.

For more information about the request and response parameters of this operation, see [ListLiveRecordVideo](/intl.en-US/API Reference/Conversion/ListLiveRecordVideo.md). Example:

    import com.aliyuncs.vod.model.v20170321.ListLiveRecordVideoRequest;
    import com.aliyuncs.vod.model.v20170321.ListLiveRecordVideoResponse;
    
    /* Query live-to-VOD videos. */
    public static ListLiveRecordVideoResponse listLiveRecordVideo(DefaultAcsClient client) throws Exception {
        ListLiveRecordVideoRequest request = new ListLiveRecordVideoRequest();
        request.setStartTime("2018-04-24T03:21:04Z");
        request.setEndTime("2018-05-21T03:21:44Z");
        request.setStreamName("testStreamName");
        request.setDomainName("testdomain.aliyun.com");
        request.setAppName("testAppName");
        return client.getAcsResponse(request);
    }
    
    /* Call example */
    public static void main(String[] argv) {
        DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        ListLiveRecordVideoResponse response = new ListLiveRecordVideoResponse();
        try {
            response = listLiveRecordVideo(client);
            // List the number of live-to-VOD videos.
            System.out.print("LiveRecordVideoList.size = " + response.getLiveRecordVideoList().size() + "\n");
        } catch (Exception e) {
            System.out.print("ErrorMessage = " + e.getLocalizedMessage());
        }
        System.out.print("RequestId = " + response.getRequestId() + "\n");
    }



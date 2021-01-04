Live-to-VOD 
================================

This topic provides examples on how to use the API operations of the live-to-VOD module. The API operations are encapsulated in ApsaraVideo VOD SDK for Python. You can call the API operations to query live-to-VOD videos.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/Python SDK/Initialization.md).

Query live-to-VOD videos {#h2-u67E5u8BE2u76F4u8F6Cu70B9u89C6u9891u5217u88682}
-----------------------------------------------------------------------------

You can call the ListLiveRecordVideo operation to query live-to-VOD videos.

For more information about the request and response parameters of this operation, see [ListLiveRecordVideo](/intl.en-US/API Reference/Conversion/ListLiveRecordVideo.md). Example:

    from aliyunsdkvod.request.v20170321 import ListLiveRecordVideoRequest
    def list_live_record_video(clt):
        request = ListLiveRecordVideoRequest.ListLiveRecordVideoRequest()
        request.set_StartTime("2018-04-24T03:21:04Z")
        request.set_EndTime("2018-05-21T03:21:44Z")
        request.set_StreamName("testStreamName")
        request.set_DomainName("testdomain.aliyun.com")
        request.set_AppName("testAppName")
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        videoList = list_live_record_video(clt)
        print(json.dumps(videoList, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



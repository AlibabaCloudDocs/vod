Live-to-VOD 
================================

This topic provides examples on how to use the API operations of the live-to-VOD module. The API operations are encapsulated in ApsaraVideo VOD SDK for Node.js. You can call the API operations to query live-to-VOD videos.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/Node.js SDK/Initialization.md).

Query live-to-VOD videos {#h2-u67E5u8BE2u76F4u8F6Cu70B9u89C6u9891u5217u88682}
-----------------------------------------------------------------------------

You can call the ListLiveRecordVideo operation to query live-to-VOD videos.

For more information about the request and response parameters of this operation, see [ListLiveRecordVideo](/intl.en-US/API Reference/Conversion/ListLiveRecordVideo.md). Example:

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("ListLiveRecordVideo", {
        StartTime: '2018-10-18T14:01:57Z',
        EndTime: '2018-10-20T14:01:57Z',
        StreamName: 'testStreamName',
        DomainName: 'testdomain.aliyun.com',
        AppName: 'AppName'
    }, {}).then(function (response) {
        if (response.LiveRecordVideoList && response.LiveRecordVideoList.LiveRecordVideo){
            console.log('LiveRecordVideoList.size = ' + response.LiveRecordVideoList.LiveRecordVideo.length);
        }
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



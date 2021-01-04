Live to VOD 
================================

This topic provides examples on how to use the API operations of the live-to-VOD module. The API operations are encapsulated in ApsaraVideo VOD SDK for Go. You can call the API operations to query live-to-VOD videos.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/Go SDK/Initialization.md).

Query live-to-VOD videos {#h2-u67E5u8BE2u76F4u8F6Cu70B9u89C6u9891u5217u88682}
-----------------------------------------------------------------------------

You can call the ListLiveRecordVideo operation to query live-to-VOD videos.

For more information about the request and response parameters of this operation, see [ListLiveRecordVideo](/intl.en-US/API Reference/Conversion/ListLiveRecordVideo.md). Example:

    package main
    
    import (
        "github.com/aliyun/alibaba-cloud-sdk-go/sdk"
        "github.com/aliyun/alibaba-cloud-sdk-go/services/vod"
        "github.com/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func MyListLiveRecordVideo(client *vod.Client) (response *vod.ListLiveRecordVideoResponse, err error) {
        request := vod.CreateListLiveRecordVideoRequest()
        request.StartTime = "2018-12-01T06:00:00Z"
        request.EndTime = "2018-12-25T06:00:00Z"
        request.StreamName = "testStreamName"
        request.AppName = "testAppName"
        request.PageNo = "1"
        request.PageSize = "10"
        request.SortBy = "CreationTime:Desc"
        request.AcceptFormat = "JSON"
    
        return client.ListLiveRecordVideo(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyListLiveRecordVideo(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
        //videoList := response.LiveRecordVideoList
    }



Video playback 
===================================

This topic provides examples on how to use the API operations of the video playback module. The API operations are encapsulated in ApsaraVideo VOD SDK for Go. You can call the API operations to query playback URLs and playback credentials.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/Go SDK/Initialization.md).

Query a playback URL {#h2--div-id-getplayinfo-div-2}
----------------------------------------------------

You can call the GetPlayInfo operation to query a playback URL.
For more information about the request and response parameters of this operation, see [GetPlayInfo](/intl.en-US/API Reference/Video playback/GetPlayInfo.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func MyGetPlayInfo(client *vod.Client, videoId string) (response *vod.GetPlayInfoResponse, err error) {
        request := vod.CreateGetPlayInfoRequest()
        request.VideoId = videoId
        request.AcceptFormat = "JSON"
    
        return client.GetPlayInfo(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyGetPlayInfo(client, "<videoId>")
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        playList := response.PlayInfoList.PlayInfo
        for _, playInfo := range playList {
            fmt.Printf("%s: %s\n", playInfo.Definition, playInfo.PlayURL)
        }
    }



Query a playback credential {#h2--div-id-getvideoplayauth-div-3}
----------------------------------------------------------------

You can call the GetVideoPlayAuth operation to query a playback credential.
For more information about the request and response parameters of this operation, see [GetVideoPlayAuth](/intl.en-US/API Reference/Video playback/GetVideoPlayAuth.md). Example: 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func MyGetPlayAuth(client *vod.Client, videoId string) (response *vod.GetVideoPlayAuthResponse, err error) {
        request := vod.CreateGetVideoPlayAuthRequest()
        request.VideoId = videoId
        request.AcceptFormat = "JSON"
    
        return client.GetVideoPlayAuth(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyGetPlayAuth(client, "<videoId>")
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Printf("%s: %s\n", response.VideoMeta, response.PlayAuth)
    }



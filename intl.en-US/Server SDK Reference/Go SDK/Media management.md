Media management 
=====================================

This topic provides examples on how to use the API operations of the media management module. The API operations are encapsulated in ApsaraVideo VOD SDK for Go. You can call the API operations to search for media asset information, modify video information, and query source file information. You can also query and delete videos and images.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/Go SDK/Initialization.md).

Search for media asset information {#h2--div-id-searchmedia-div-2}
------------------------------------------------------------------

You can call the SearchMedia operation to search for media asset information.
For more information about the request and response parameters of this operation, see [SearchMedia](/intl.en-US/API Reference/Media management/Media Search/SearchMedia.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func MySearchMedia(client *vod.Client) (response *vod.SearchMediaResponse, err error) {
        request := vod.CreateSearchMediaRequest()
        request.Fields = "Title,CoverURL,Status"
        request.Match = "Status in ('Normal','Checking') and CreationTime = ('2018-07-01T08:00:00Z','2018-08-01T08:00:00Z')"
        request.PageNo = "1"
        request.PageSize = "10"
        request.SearchType = "video"
        request.SortBy = "CreationTime:Desc"
        request.AcceptFormat = "JSON"
    
        return client.SearchMedia(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MySearchMedia(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        //fmt.Println(response.MediaList)
    }



Query a video {#h2--div-id-getvideoinfo-div-3}
----------------------------------------------

You can call the GetVideoInfo operation to query details about a video.
For more information about the request and response parameters of this operation, see [GetVideoInfo](/intl.en-US/API Reference/Media management/Audio&Video Management/GetVideoInfo.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func MyGetVideoInfo(client *vod.Client) (response *vod.GetVideoInfoResponse, err error) {
        request := vod.CreateGetVideoInfoRequest()
        request.VideoId = "<videoId>"
        request.AcceptFormat = "JSON"
    
        return client.GetVideoInfo(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyGetVideoInfo(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        //fmt.Println(response.Video)
    }



Query videos {#h2--div-id-getvideoinfos-div-4}
----------------------------------------------

You can call the GetVideoInfos operation to query videos.
For more information about the request and response parameters of this operation, see [GetVideoInfos](/intl.en-US/API Reference/Media management/Audio&Video Management/GetVideoInfos.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func MyGetVideoInfos(client *vod.Client) (response *vod.GetVideoInfosResponse, err error) {
        request := vod.CreateGetVideoInfosRequest()
        request.VideoIds = "VideoId1,VideoId2"
        request.AcceptFormat = "JSON"
    
        return client.GetVideoInfos(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyGetVideoInfos(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.NonExistVideoIds)
        //fmt.Println(response.VideoList)
    }



Modify the information about a video {#h2--div-id-updatevideoinfo-div-5}
------------------------------------------------------------------------

You can call the UpdateVideoInfo operation to modify the information about a video.
For more information about the request and response parameters of this operation, see [UpdateVideoInfo](/intl.en-US/API Reference/Media management/Audio&Video Management/UpdateVideoInfo.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func MyUpdateVideoInfo(client *vod.Client) (response *vod.UpdateVideoInfoResponse, err error) {
        request := vod.CreateUpdateVideoInfoRequest()
        request.VideoId = "<videoId>"
        request.Title = "new Title"
        request.Description = "new Description"
        request.Tags = "new Tag1,new Tag2"
        request.AcceptFormat = "JSON"
    
        return client.UpdateVideoInfo(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyUpdateVideoInfo(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
    }



Modify the information about videos {#h2--div-id-updatevideoinfos-div-6}
------------------------------------------------------------------------

You can call the UpdateVideoInfos operation to modify the information about videos.
For more information about the request and response parameters of this operation, see [UpdateVideoInfos](/intl.en-US/API Reference/Media management/Audio&Video Management/UpdateVideoInfos.md). Example: 
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
        "encoding/json"
    )
    
    func MyUpdateVideoInfos(client *vod.Client) (response *vod.UpdateVideoInfosResponse, err error) {
        request := vod.CreateUpdateVideoInfosRequest()
    
        updateContent := []map[string]interface{}{}
        updateItem1 := map[string]interface{}{"VideoId":"<VideoId1>", "Title":"New Title 1", "Tags": "NewTag1,NewTag2"}
        updateItem2 := map[string]interface{}{"VideoId":"<VideoId2>", "Title":"New Title 2", "Tags": "NewTag1,NewTag2"}
        updateContent = append(updateContent, updateItem1, updateItem2)
        jsonContent, err := json.Marshal(updateContent)
        if err ! = nil {
            fmt.Println("json.Marshal failed:", err)
            return
        }
        request.UpdateContent = string(jsonContent)
        request.AcceptFormat = "JSON"
    
        return client.UpdateVideoInfos(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyUpdateVideoInfos(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.NonExistVideoIds)
        fmt.Println(response.RequestId)
    }



Delete videos {#h2--div-id-deletevideo-div-7}
---------------------------------------------

You can call the DeleteVideo operation to delete videos.
For more information about the request and response parameters of this operation, see [DeleteVideo](/intl.en-US/API Reference/Media management/Audio&Video Management/DeleteVideo.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func MyDeleteVideo(client *vod.Client) (response *vod.DeleteVideoResponse, err error) {
        request := vod.CreateDeleteVideoRequest()
        // The IDs of the videos that you want to delete. Separate multiple IDs with commas (,).
        request.VideoIds = "VideoId1,VideoId2"
        request.AcceptFormat = "JSON"
    
        return client.DeleteVideo(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyDeleteVideo(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
    }



Query source file information (including the file URL) {#h2--div-id-getmezzanineinfo-div-8}
-------------------------------------------------------------------------------------------

You can call the GetMezzanineInfo operation to query source file information.
For more information about the request and response parameters of this operation, see [GetMezzanineInfo](/intl.en-US/API Reference/Media management/Audio&Video Management/GetMezzanineInfo.md). Example: 
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func MyGetMezzanineInfo(client *vod.Client) (response *vod.GetMezzanineInfoResponse, err error) {
        request := vod.CreateGetMezzanineInfoRequest()
        request.VideoId = "<VideoId>"
        request.AuthTimeout = "86400"
        //request.OutputType = "oss"
        request.AcceptFormat = "JSON"
    
        return client.GetMezzanineInfo(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyGetMezzanineInfo(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
        fmt.Println(response.Mezzanine.FileURL)
    }



Query videos by using filter conditions {#h2--div-id-getvideolist-div-9}
------------------------------------------------------------------------

You can call the GetVideoList operation to query videos by using filter conditions.
For more information about the request and response parameters of this operation, see [GetVideoList](/intl.en-US/API Reference/Media management/Audio&Video Management/GetVideoList.md). Example:
**Notice**
The time must be in UTC. For example, `2018-01-01T12:00:00Z` indicates `20:00:00 on January 1, 2018 (UTC+8)`. {#h2--div-id-getvideolist-div-9}
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func MyGetVideoList(client *vod.Client) (response *vod.GetVideoListResponse, err error) {
        request := vod.CreateGetVideoListRequest()
        request.StartTime = "2018-12-01T06:00:00Z"
        request.EndTime = "2018-12-25T06:00:00Z"
        //request.Status = "Uploading,Normal,Transcoding"
        request.PageNo = "1"
        request.PageSize = "10"
        request.SortBy = "CreationTime:Desc"
        request.AcceptFormat = "JSON"
    
        return client.GetVideoList(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyGetVideoList(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
        videoList := response.VideoList.Video
        for _, video := range videoList {
            fmt.Printf("%s: %s\n", video.VideoId, video.Title)
        }
    }



Delete a media stream {#h2--div-id-deletestream-div-10}
-------------------------------------------------------

You can call the DeleteStream operation to delete a media stream.
For more information about the request and response parameters of this operation, see [DeleteStream](/intl.en-US/API Reference/Media management/Audio&Video Management/DeleteStream.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func MyDeleteStream(client *vod.Client) (response *vod.DeleteStreamResponse, err error) {
        request := vod.CreateDeleteStreamRequest()
        request.VideoId = "<VideoId>"
        request.JobIds = "JobId1,JobId2"
        request.AcceptFormat = "JSON"
    
        return client.DeleteStream(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyDeleteStream(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
    }



Delete source files {#h2--div-id-deletemezzanines-div-11}
---------------------------------------------------------

You can call the DeleteMezzanines operation to delete source files.
For more information about the request and response parameters of this operation, see [DeleteMezzanines](/intl.en-US/API Reference/Media management/Audio&Video Management/DeleteMezzanines.md). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func MyDeleteMezzanines(client *vod.Client) (response *vod.DeleteMezzaninesResponse, err error) {
        request := vod.CreateDeleteMezzaninesRequest()
        request.VideoIds = "VideoId1,VideoId2"
        request.Force = "false"
        request.AcceptFormat = "JSON"
    
        return client.DeleteMezzanines(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyDeleteMezzanines(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
        fmt.Println(response.NonExistVideoIds)
    }



Modify the information about images {#h2--div-id-updateimageinfos-div-12}
-------------------------------------------------------------------------

You can call the UpdateImageInfos operation to modify the information about images.
For more information about the request and response parameters of this operation, see [UpdateImageInfos](/intl.en-US/API Reference/Media management/Image Management/UpdateImageInfos.md). Example: 
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
        "encoding/json"
    )
    
    func MyUpdateImageInfos(client *vod.Client) (response *vod.UpdateImageInfosResponse, err error) {
        request := vod.CreateUpdateImageInfosRequest()
    
        updateContent := []map[string]interface{}{}
        updateItem1 := map[string]interface{}{"ImageId":"<ImageId1>", "Title":"New Title 1", "Tags": "NewTag1,NewTag2"}
        updateItem2 := map[string]interface{}{"ImageId":"<ImageId2>", "Title":"New Title 2", "Tags": "NewTag1,NewTag2"}
        updateContent = append(updateContent, updateItem1, updateItem2)
        jsonContent, err := json.Marshal(updateContent)
        if err ! = nil {
            fmt.Println("json.Marshal failed:", err)
            return
        }
        request.UpdateContent = string(jsonContent)
        request.AcceptFormat = "JSON"
    
        return client.UpdateImageInfos(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyUpdateImageInfos(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
        fmt.Println(response.NonExistImageIds)
    }



Query an image {#h2--div-id-getimageinfo-div-13}
------------------------------------------------

You can call the GetImageInfo operation to query details about an image.
For more information about the request and response parameters of this operation, see [GetImageInfo](/intl.en-US/API Reference/Media management/Image Management/GetImageInfo.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func MyGetImageInfo(client *vod.Client) (response *vod.GetImageInfoResponse, err error) {
        request := vod.CreateGetImageInfoRequest()
        request.ImageId = "<ImageId>"
        request.AuthTimeout = "86400"
        request.AcceptFormat = "JSON"
    
        return client.GetImageInfo(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyGetImageInfo(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
        fmt.Println(response.ImageInfo.URL)
    }



Delete images {#h2--div-id-deleteimage-div-14}
----------------------------------------------

You can call the DeleteImage operation to delete images.
For more information about the request and response parameters of this operation, see [DeleteImage](/intl.en-US/API Reference/Media management/Image Management/DeleteImage.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func MyDeleteImage(client *vod.Client) (response *vod.DeleteImageResponse, err error) {
        request := vod.CreateDeleteImageRequest()
    
        // Delete image files based on ImageId.
        request.DeleteImageType = "ImageId"
        request.ImageIds = "ImageId1,ImageId2"
    
        /*
        // Delete an image file based on ImageURL.
        request.DeleteImageType = "ImageURL"
        request.ImageURLs = "http://out-20170320144157164-bjsdu4mihp.oss-cn-shanghai.aliyuncs.com.gif"
    
        // Delete image files based on VideoId and ImageType.
        request.DeleteImageType = "VideoId"
        request.VideoId = "<VideoId>"
        request.ImageType = "SpriteSnapshot"
        */
    
        request.AcceptFormat = "JSON"
    
        return client.DeleteImage(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyDeleteImage(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
    }



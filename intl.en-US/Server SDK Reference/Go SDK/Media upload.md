Media upload 
=================================

This topic provides examples on how to use the API operations of the media upload module. The API operations are encapsulated in ApsaraVideo VOD SDK for Go. You can call the API operations to create upload URLs and credentials and register media assets. You can also upload media files by using a source file URL.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/Go SDK/Initialization.md).

Create a URL and a credential for uploading videos {#h2--div-id-createuploadvideo-div-2}
----------------------------------------------------------------------------------------

You can call the CreateUploadVideo operation to create a URL and a credential for uploading videos.
For more information about the request and response parameters of this operation, see [CreateUploadVideo](/intl.en-US/API Reference/Media upload/CreateUploadVideo.md). Example: 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "github.com/aliyun/alibaba-cloud-sdk-go/sdk"
        "github.com/aliyun/alibaba-cloud-sdk-go/services/vod"
        "github.com/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func MyCreateUploadVideo(client *vod.Client) (response *vod.CreateUploadVideoResponse, err error) {
        request := vod.CreateCreateUploadVideoRequest()
    
        request.Title = "Sample Video Title"
        request.Description = "Sample Description"
        request.FileName = "/opt/video/sample/video_file.mp4"
        //request.CateId = "-1"
        request.CoverURL = "http://192.168.0.0/16/tps/TB1qnJ1PVXXXXXCXXXXXXXXXXXX-700-700.png"
        request.Tags = "tag1,tag2"
    
        request.AcceptFormat = "JSON"
        return client.CreateUploadVideo(request)
    }
    
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyCreateUploadVideo(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Printf("VideoId: %s\n UploadAddress: %s\n UploadAuth: %s",
            response.VideoId, response.UploadAddress, response.UploadAuth)
    }



Refresh the credential for uploading videos {#h2--div-id-refreshuploadvideo-div-3}
----------------------------------------------------------------------------------

You can call the RefreshUploadVideo operation to refresh the credential for uploading videos.
For more information about the request and response parameters of this operation, see [RefreshUploadVideo](/intl.en-US/API Reference/Media upload/RefreshUploadVideo.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "github.com/aliyun/alibaba-cloud-sdk-go/sdk"
        "github.com/aliyun/alibaba-cloud-sdk-go/services/vod"
        "github.com/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func MyRefreshUploadVideo(client *vod.Client) (response *vod.RefreshUploadVideoResponse, err error) {
        request := vod.CreateRefreshUploadVideoRequest()
        request.VideoId = "6657f89a86fa4f76a295ae95636e5aed"
        request.AcceptFormat = "JSON"
    
        return client.RefreshUploadVideo(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyRefreshUploadVideo(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Printf("UploadAddress: %s\n UploadAuth: %s", response.UploadAddress, response.UploadAuth)
    }



Create a URL and a credential for uploading images {#h2--div-id-createuploadimage-div-4}
----------------------------------------------------------------------------------------

You can call the CreateUploadImage operation to create a URL and a credential for uploading images.
For more information about the request and response parameters of this operation, see [CreateUploadImage](/intl.en-US/API Reference/Media upload/CreateUploadImage.md). Example: 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "github.com/aliyun/alibaba-cloud-sdk-go/sdk"
        "github.com/aliyun/alibaba-cloud-sdk-go/services/vod"
        "github.com/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func MyCreateUploadImage(client *vod.Client) (response *vod.CreateUploadImageResponse, err error) {
        request := vod.CreateCreateUploadImageRequest()
    
        request.ImageType = "cover"
        request.ImageExt = "jpg"
        request.Title = "Sample Image Title"
        //request.CateId = "-1"
        request.Tags = "tag1,tag2"
    
        request.AcceptFormat = "JSON"
        return client.CreateUploadImage(request)
    }
    
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyCreateUploadImage(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Printf("ImageId: %s\n ImageURL: %s\n UploadAddress: %s\n UploadAuth: %s",
            response.ImageId, response.ImageURL, response.UploadAddress, response.UploadAuth)
    }



Create a URL and a credential for uploading attached media assets {#h2--div-id-createuploadattachedmedia-div-5}
---------------------------------------------------------------------------------------------------------------

You can call the CreateUploadAttachedMedia operation to create a URL and a credential for uploading attached media assets.
For more information about the request and response parameters of this operation, see [CreateUploadAttachedMedia](/intl.en-US/API Reference/Media upload/CreateUploadAttachedMedia.md). Example: 
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "github.com/aliyun/alibaba-cloud-sdk-go/sdk"
        "github.com/aliyun/alibaba-cloud-sdk-go/services/vod"
        "github.com/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func MyCreateUploadAttachedMedia(client *vod.Client) (response *vod.CreateUploadAttachedMediaResponse, err error) {
        request := vod.CreateCreateUploadAttachedMediaRequest()
    
        request.BusinessType = "watermark"
        request.MediaExt = "gif"
        request.Title = "Sample watermark Title"
        //request.CateId = "-1"
        request.Tags = "tag1,tag2"
    
        request.AcceptFormat = "JSON"
        return client.CreateUploadAttachedMedia(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyCreateUploadAttachedMedia(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Printf("MediaId: %s\n MediaURL: %s\n FileURL: %s\n UploadAddress: %s\n UploadAuth: %s",
            response.MediaId, response.MediaURL, response.FileURL, response.UploadAddress, response.UploadAuth)
    }



Upload media files by using a source file URL {#h2-url-div-id-uploadmediabyurl-div-6}
-------------------------------------------------------------------------------------

You can call the UploadMediaByURL operation to upload media files by using a source file URL.
For more information about the request and response parameters of this operation, see [UploadMediaByURL](/intl.en-US/API Reference/Media upload/UploadMediaByURL.md). Example: 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "github.com/aliyun/alibaba-cloud-sdk-go/sdk"
        "github.com/aliyun/alibaba-cloud-sdk-go/services/vod"
        "github.com/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
        "encoding/json"
        "net/url"
        "strings"
    )
    
    func MyUploadMediaByURL(client *vod.Client) (response *vod.UploadMediaByURLResponse, err error) {
        request := vod.CreateUploadMediaByURLRequest()
    
        // Encode URLs.
        sourceUrls := []string{"https://sample.oss-cn-shanghai.aliyuncs.com/vod_sample1.mp4",
            "https://sample.oss-cn-shanghai.aliyuncs.com/vod_sample2.flv"}
        uploadUrls := []string{}
        metadatas := []map[string]interface{}{}
        for _, surl := range sourceUrls {
            encodeUrl := url.QueryEscape(surl)
            uploadUrls = append(uploadUrls, encodeUrl)
            metadata := map[string]interface{}{"SourceURL": encodeUrl, "Title":"UploadMediaByURL Sample Title"}
            metadatas = append(metadatas, metadata)
        }
    
        // The URLs that you want to use to upload media files. Separate multiple URLs with commas (,).
        request.UploadURLs = strings.Join(uploadUrls, ",")
    
        // Optional. The metadata that corresponds to the URLs.
        jsonMetas, err := json.Marshal(metadatas)
        if err ! = nil {
            fmt.Println("json.Marshal failed:", err)
            return
        }
        request.UploadMetadatas = string(jsonMetas)
    
        // Optional. The transcoding template group.
        //request.TemplateGroupId = "<TemplateGroupId>"
    
        request.AcceptFormat = "JSON"
        return client.UploadMediaByURL(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyUploadMediaByURL(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        for _, job := range response.UploadJobs {
            fmt.Printf("%s: %s\n", job.JobId, job.SourceURL)
        }
    }



Register media assets {#h2--div-id-registermedia-div-7}
-------------------------------------------------------

You can call the RegisterMedia operation to register media assets.
For more information about the request and response parameters of this operation, see [RegisterMedia](/intl.en-US/API Reference/Media upload/RegisterMedia.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "github.com/aliyun/alibaba-cloud-sdk-go/sdk"
        "github.com/aliyun/alibaba-cloud-sdk-go/services/vod"
        "github.com/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
        "encoding/json"
    )
    
    func MyRegisterMedia(client *vod.Client) (response *vod.RegisterMediaResponse, err error) {
        request := vod.CreateRegisterMediaRequest()
    
        metadatas := []map[string]interface{}{}
        metadata1 := map[string]interface{}{"FileURL":"https://sample.oss-cn-shanghai.aliyuncs.com/vod_sample1.mp4",
            "Title":"RegisterMedia sample Title 1"}
        metadata2 := map[string]interface{}{"FileURL":"https://sample.oss-cn-shanghai.aliyuncs.com/vod_sample2.mp4",
            "Title":"RegisterMedia sample Title 2"}
        metadatas = append(metadatas, metadata1, metadata2)
        jsonMetas, err := json.Marshal(metadatas)
        if err ! = nil {
            fmt.Println("json.Marshal failed:", err)
            return
        }
        request.RegisterMetadatas = string(jsonMetas)
        //request.TemplateGroupId = "<TemplateGroupId>"
    
        request.AcceptFormat = "JSON"
        return client.RegisterMedia(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyRegisterMedia(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.FailedFileURLs)
        fmt.Println(response.RegisteredMediaList)
    }



Query URLs that are used to upload media files {#h2--url-div-id-geturluploadinfos-div-8}
----------------------------------------------------------------------------------------

You can call the GetURLUploadInfos operation to query URLs that are used to upload media files.
For more information about the request and response parameters of this operation, see [GetURLUploadInfos](/intl.en-US/API Reference/Media upload/GetURLUploadInfos.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "github.com/aliyun/alibaba-cloud-sdk-go/sdk"
        "github.com/aliyun/alibaba-cloud-sdk-go/services/vod"
        "github.com/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
        "strings"
    )
    
    func MyGetURLUploadInfos(client *vod.Client) (response *vod.GetURLUploadInfosResponse, err error) {
        request := vod.CreateGetURLUploadInfosRequest()
    
        // Encode URLs.
        sourceUrls := []string{"https://192.168.0.0/16/vod_sample1.mp4",
            "https://sample.oss-cn-shanghai.aliyuncs.com/vod_sample2.flv"}
        uploadUrls := []string{}
        for _, surl := range sourceUrls {
            encodeUrl := url.QueryEscape(surl)
            uploadUrls = append(uploadUrls, encodeUrl)
        }
    
        // The URLs that you want to use to upload media files. Separate multiple URLs with commas (,).
        request.UploadURLs = strings.Join(uploadUrls, ",")
    
        // The job IDs that you use to query URLs.
        //request.JobIds = "jobId1,jobId2"
    
        request.AcceptFormat = "JSON"
        return client.GetURLUploadInfos(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyGetURLUploadInfos(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.NonExists)
        for _, uploadInfo := range response.URLUploadInfoList {
            fmt.Printf("%s: %s %s\n", uploadInfo.UploadURL, uploadInfo.Status, uploadInfo.MediaId)
        }
    }



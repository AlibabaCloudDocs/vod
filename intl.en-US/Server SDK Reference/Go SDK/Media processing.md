Media processing 
=====================================

This topic provides examples on how to use the API operations of the media processing module. The API operations are encapsulated in ApsaraVideo VOD SDK for Go. You can call the API operations to submit transcoding and snapshot jobs, query snapshot data, and preprocess videos in the production studio.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/Go SDK/Initialization.md).

Submit a transcoding job without encryption {#h2--amp-div-id-submittranscodejobs-div-2}
---------------------------------------------------------------------------------------

You can call the SubmitTranscodeJobs operation to submit a transcoding job without encryption.
For more information about the request and response parameters of this operation, see [SubmitTranscodeJobs](/intl.en-US/API Reference/Media processing/Initiate Process/SubmitTranscodeJobs.md). Example:
**Note**
The following code provides an example on transcoding without encryption. For more information about video encryption supported by Alibaba Cloud, see [Alibaba Cloud video encryption](/intl.en-US/Developer Guide/Video security/Alibaba Cloud video encryption.md). {#h2--amp-div-id-submittranscodejobs-div-2}
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "encoding/json"
        "fmt"
    )
    
    func NormalSubmitTranscodeJobs(client *vod.Client) (response *vod.SubmitTranscodeJobsResponse, err error) {
        request := vod.CreateSubmitTranscodeJobsRequest()
    
        // The ID of the video that you want to transcode.
        request.VideoId = "<VideoId>"
    
        // The transcoding template group.
        request.TemplateGroupId = "<TemplateGroupId>"
    
        /*
        // Optional.
        overrideParams := BuildOverrideParams()
        jsonParams, err := json.Marshal(overrideParams)
        if err ! = nil {
            fmt.Println("json.Marshal failed:", err)
            return
        }
        request.OverrideParams = string(jsonParams)
        fmt.Println(request.OverrideParams)
        */
    
        request.AcceptFormat = "JSON"
    
        return client.SubmitTranscodeJobs(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := NormalSubmitTranscodeJobs(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
        for _, job := range response.TranscodeJobs.TranscodeJob {
            fmt.Printf("%s\n", job.JobId)
        }
    }
    
    /*
    * Build overriding parameters, which override only the file URL of an image watermark or the content of a text watermark.
    * Make sure that the ID of the watermark is associated with the ID of the transcoding template that you use. The ID of the transcoding template is specified by TranscodeTemplateId.
    * You can call this operation to add only a watermark whose ID is associated with the ID of the transcoding template that you use.
    */
    func BuildOverrideParams() (overrideParams map[string]interface{}) {
        // The following code provides examples on overriding watermarks:
        watermarks := []map[string]interface{}{}
    
        // Override the file URL of an image watermark.
        watermark1 := map[string]interface{}{"WatermarkId": "<WatermarkId>", "FileUrl": "https://sample.oss-cn-shanghai.aliyuncs.com/watermarks/sample.png"}
        watermarks = append(watermarks, watermark1)
    
        // Override the content of a text watermark.
        watermark2 := map[string]interface{}{"WatermarkId": "<WatermarkId>", "Content": "new Text"}
        watermarks = append(watermarks, watermark2)
    
        overrideParams = map[string]interface{}{"Watermarks": watermarks}
    
        return overrideParams
    }



Submit a transcoding job with HLS encryption enabled {#h2--hls-div-id-submittranscodejobs-div-3}
------------------------------------------------------------------------------------------------

You can call the SubmitTranscodeJobs operation to submit a transcoding job with HTTP Live Streaming (HLS) encryption enabled.
For more information about the request and response parameters of this operation, see [SubmitTranscodeJobs](/intl.en-US/API Reference/Media processing/Initiate Process/SubmitTranscodeJobs.md). Example:
**Note**
The following code provides an example on transcoding with HLS encryption enabled. For more information, see [Standard HLS encryption](/intl.en-US/Developer Guide/Video security/Standard HLS encryption.md). {#h2--hls-div-id-submittranscodejobs-div-3}
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "encoding/json"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/kms"
        "fmt"
    )
    
    func HLSEncryptSubmitTranscodeJobs(client *vod.Client, kmsClient *kms.Client) (response *vod.SubmitTranscodeJobsResponse, err error) {
        request := vod.CreateSubmitTranscodeJobsRequest()
    
        // The ID of the video that you want to transcode.
        request.VideoId = "<VideoId>"
    
        // The transcoding template group.
        request.TemplateGroupId = "<TemplateGroupId>"
    
        // The random data key for encryption that is generated by using Key Management Service (KMS).
        encryptConfig, err := BuildEncryptConfig(kmsClient)
        if err ! = nil {
            panic(err)
        }
        jsonConfig, err := json.Marshal(encryptConfig)
        if err ! = nil {
            fmt.Println("json.Marshal failed:", err)
            return
        }
        request.EncryptConfig = string(jsonConfig)
    
        request.AcceptFormat = "JSON"
    
        return client.SubmitTranscodeJobs(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
        kmsClient, err := InitKmsClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := HLSEncryptSubmitTranscodeJobs(client, kmsClient)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
        for _, job := range response.TranscodeJobs.TranscodeJob {
            fmt.Printf("%s\n", job.JobId)
        }
    }
    
    /*
    * Optional. The configurations of HLS encryption. If you do not use HLS encryption, these configurations are not required.
    * HLS encryption configurations depends on KMS. You must install the KMS dependency package aliyun-php-sdk-kms. If you want to call an API operation, you must import related classes.
    * For more information about the API operation that you can call to generate data keys, see https://help.aliyun.com/document_detail/28948.html.
    */
    // Initialize a KMS client. The initialization method is similar to that of an ApsaraVideo VOD client.
    func InitKmsClient(accessKeyId  string, accessKeySecret string) (client *kms.Client, err error) {
    
        // The region where you want to call KMS API operations. You must can KMS and ApsaraVideo VOD API operations in the same region.
        regionId := "cn-shanghai"
    
        // Create an object for authentication.
        credential := &credentials.AccessKeyCredential{
            accessKeyId,
            accessKeySecret,
        }
    
        // The custom configuration parameters.
        config := sdk.NewConfig()
        config.AutoRetry = true      // Specifies whether to automatically retry an operation if the operation fails.
        config.MaxRetryTime = 3      // The maximum number of retry attempts.
        config.Timeout = 3000000000 // The timeout period of connections, in nanoseconds. The default value is 3000000000, which indicates 3 seconds.
    
        // Create a kmsClient instance.
        return kms.NewClientWithOptions(regionId, config, credential)
    }
    
    // The generated random data key for encryption.
    func BuildEncryptConfig(client *kms.Client) (encryptConfig map[string]interface{}, err error) {
        request := kms.CreateGenerateDataKeyRequest()
    
        // Generate a random data key for encryption. The response contains the plaintext and ciphertext of the data key.
        // Pass only the ciphertext of the data key for HLS encryption.
        request.KeyId = "<serviceKey>"
        request.KeySpec = "AES_128"
        request.AcceptFormat = "JSON"
        request.Scheme = "HTTPS"       // The URI scheme. Set the value to HTTPS for KMS API operations.
    
        response, err := client.GenerateDataKey(request)
        if err ! = nil {
            panic(err)
        }
    
        // The URI of the operation that is used to decrypt the data key. To obtain the URI, concatenate the URL of the decryption service and the ciphertext of the data key. The ciphertext to decrypt varies among videos.
        // You can customize the name of the Ciphertext parameter. The name in this example is for reference only.
        decryptKeyUri := "http://decrypt.demo.com/decrypt?" + "Ciphertext=" + response.CiphertextBlob
        encryptConfig = map[string]interface{}{"DecryptKeyUri": decryptKeyUri, "KeyServiceType": "KMS",
            "CipherText": response.CiphertextBlob}
    
        return  encryptConfig, nil
    }



Submit a snapshot job {#h2--div-id-submitsnapshotjob-div-4}
-----------------------------------------------------------

You can call the SubmitSnapshotJob operation to submit a snapshot job.
For more information about the request and response parameters of this operation, see [SubmitSnapshotJob](/intl.en-US/API Reference/Media processing/Initiate Process/SubmitSnapshotJob.md). Example:
**Note**
For more information about how to create a snapshot template, see [Create a snapshot template](/intl.en-US/API Reference/Media processing/Snapshot Template/AddVodTemplate.md). {#h2--div-id-submitsnapshotjob-div-4}
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "encoding/json"
        "fmt"
    )
    
    func MySubmitSnapshotJob(client *vod.Client) (response *vod.SubmitSnapshotJobResponse, err error) {
        request := vod.CreateSubmitSnapshotJobRequest()
    
        // The ID of the video for which you want to create snapshots.
        request.VideoId = "<VideoId>"
    
        // The ID of the snapshot template.
        //request.SnapshotTemplateId = "<snapshotTemplateId>"
    
        // If you specify the SnapshotTemplateId parameter, the following parameters are ignored:
        request.Count = "50"
        request.SpecifiedOffsetTime = "0"
        request.Interval = "1"
        request.Width = "200"
        request.Height = "200"
    
        // Optional. The configurations of the image sprites.
        spriteSnapshotConfig := map[string]interface{}{"CellWidth": 120, "CellHeight": 68, "Columns": 3,
            "Lines": 10, "Padding": 20, "Margin": 50}
        // Whether to retain the source image after an image sprite is generated.
        spriteSnapshotConfig["KeepCellPic"] = "keep"
        spriteSnapshotConfig["Color"] = "tomato"
        jsonSpriteConfig, err := json.Marshal(spriteSnapshotConfig)
        if err ! = nil {
            fmt.Println("json.Marshal failed:", err)
            return
        }
        request.SpriteSnapshotConfig = string(jsonSpriteConfig)
    
        request.AcceptFormat = "JSON"
    
        return client.SubmitSnapshotJob(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MySubmitSnapshotJob(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
        fmt.Println(response.SnapshotJob.JobId)
    }



Query snapshot data {#h2--div-id-listsnapshots-div-5}
-----------------------------------------------------

You can call the ListSnapshots operation to query snapshot data.
For more information about the request and response parameters of this operation, see [ListSnapshots](/intl.en-US/API Reference/Media management/Image Management/ListSnapshots.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func MyListSnapshots(client *vod.Client) (response *vod.ListSnapshotsResponse, err error) {
        request := vod.CreateListSnapshotsRequest()
    
        request.VideoId = "<VideoId>"
        request.SnapshotType = "CoverSnapshot"
        request.PageNo = "1"
        request.PageSize = "20"
        request.AuthTimeout = "86400"
    
        request.AcceptFormat = "JSON"
    
        return client.ListSnapshots(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyListSnapshots(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
        fmt.Println(response.MediaSnapshot.Total)
        for _, snapshot := range response.MediaSnapshot.Snapshots.Snapshot {
            fmt.Printf("%d: %s\n", snapshot.Index, snapshot.Url)
        }
    }



Preprocess videos in the production studio {#h2--div-id-submitpreprocessjobs-div-6}
-----------------------------------------------------------------------------------

You can call the SubmitPreprocessJobs operation to preprocess videos in the production studio.
For more information about the request and response parameters of this operation, see [SubmitPreprocessJobs](). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "encoding/json"
        "fmt"
    )
    
    func MySubmitPreprocessJobs(client *vod.Client) (response *vod.SubmitPreprocessJobsResponse, err error) {
        request := vod.CreateSubmitPreprocessJobsRequest()
    
        request.VideoId = "<VideoId>"
        request.PreprocessType = "LivePreprocess"
    
        request.AcceptFormat = "JSON"
    
        return client.SubmitPreprocessJobs(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MySubmitPreprocessJobs(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
        for _, job := range response.PreprocessJobs.PreprocessJob {
            fmt.Printf("%s\n", job.JobId)
        }
    }



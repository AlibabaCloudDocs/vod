Media processing 
=====================================

This topic provides examples on how to use the API operations of the media processing module. The API operations are encapsulated in ApsaraVideo VOD SDK for .NET. You can call the API operations to submit transcoding and snapshot jobs, query snapshot data, and preprocess videos in the production studio.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/.NET SDK/Initialization.md).

Submit a transcoding job {#h2--div-id-submittranscodejobs-div-2}
----------------------------------------------------------------

You can call the SubmitTranscodeJobs operation to submit a transcoding job.
For more information about the request and response parameters of this operation, see [SubmitTranscodeJobs](/intl.en-US/API Reference/Media processing/Initiate Process/SubmitTranscodeJobs.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.Kms.Model.V20160120;
    using Aliyun.Acs.vod.Model.V20170321;
    using Newtonsoft.Json.Linq;
    
    namespace Aliyun.Acs.vod.Sdk.SubmitTranscodeJobs
    {
        class MainClass
        {
            /// <summary>
            /// Main function
            /// </summary>
            /// <param name="args">The command-line arguments.</param>
            public static void Main(string[] args)
            {
                try
                {
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // Initiate the request and display the response.
                    SubmitTranscodeJobsResponse response = SubmitTranscodeJobs(client);
                    Console.WriteLine("RequestId = " + response.RequestId);
                }
                catch (ServerException e)
                {
                    if (e.RequestId ! = null)
                    {
                        Console.WriteLine("RequestId = " + e.RequestId);
                    }
                    Console.WriteLine("ErrorCode = " + e.ErrorCode);
                    Console.WriteLine("ErrorMessage = " + e.ErrorMessage);
                }
                catch (ClientException e)
                {
                    if (e.RequestId ! = null)
                    {
                        Console.WriteLine("RequestId = " + e.RequestId);
                    }
                    Console.WriteLine("ErrorCode = " + e.ErrorCode);
                    Console.WriteLine("ErrorMessage = " + e.ErrorMessage);
                }
                catch (Exception e)
                {
                    Console.WriteLine("ErrorMessage = " + e.ToString());
                }
            }
    
            /// <summary>
            /// Submit a transcoding job.
            /// </summary>
            /// <returns>Transcoding job ID</returns>
            /// <param name="client">Client</param>
            public static SubmitTranscodeJobsResponse SubmitTranscodeJobs(DefaultAcsClient client) 
            {
                // Create a request.
                SubmitTranscodeJobsRequest request = new SubmitTranscodeJobsRequest();
                // Specify the ID of the video that you want to transcode.
                request.VideoId = "1f7ed5623409489193e41d16f6c7****";
                // Specify the ID of the transcoding template.
                request.TemplateGroupId = "3cac80cddb4455e37460f491aecca588";
                // Build the parameters that are required to replace a watermark. You must build these parameters when you want to replace a watermark.
                request.OverrideParams = BuildOverrideParams();
                // The overriding parameters. You can change the values of some watermark-related parameters. You must specify these parameters when you want to replace a watermark.
                request.EncryptConfig = BuildEncryptConfig(client);
                return client.GetAcsResponse(request);
            }
    
            /// <summary>
            /// Create a data key for encryption. The response contains the plaintext and ciphertext of the data key. You need only to transfer the ciphertext to ApsaraVideo VOD.
            /// Note: You must set the value of the KeySpec parameter to AES_128. The NumberOfBytes parameter is not supported.
            /// </summary>
            /// <returns> DataKey </returns>
            /// <param name="client">KMS-SDK Client.</param>
            /// <param name="serviceKey">: The service key that is provided by ApsaraVideo VOD to generate data keys. The description of this service key is vod in the Key Management Service (KMS) console.</param>
            /// 
            public static GenerateDataKeyResponse GenerateDataKey(DefaultAcsClient client, string serviceKey)
            {
                GenerateDataKeyRequest request = new GenerateDataKeyRequest();
                request.KeyId = serviceKey;
                request.KeySpec = "AES_128";
    
                return client.GetAcsResponse(request);
            }
    
            /// <summary>
            /// Build the configurations of HTTP Live Streaming (HLS) encryption.
            /// </summary>
            /// <returns>Configurations</returns>
            /// <param name="client"> VoD Client.</param>
            /// 
            public static string BuildEncryptConfig(DefaultAcsClient client)
            {
                // The service key that is provided by ApsaraVideo VOD. To view the service key, you must select the region where the key resides and find the key whose description is vod in the KMS console.
                string serviceKey = "<Your Service Key>";
    
                // Generate a random data key for encryption. The response contains the plaintext and ciphertext of the data key.
                // Pass only the ciphertext of the data key for standard video encryption.
                GenerateDataKeyResponse response = GenerateDataKey(client, serviceKey);
    
                JObject encryptConfig = new JObject();
    
                // The URI of the operation that is used to decrypt the data key. To obtain the URI, concatenate the URL of the decryption service and the ciphertext of the data key. The ciphertext to decrypt varies among videos.
                // You can customize the name of the Ciphertext parameter. The name in this example is only for reference.
                encryptConfig.Add("DecryptKeyUri", "http://192.168.0.0/16/decrypt?" + "Ciphertext=" + response.CiphertextBlob);
    
                // The type of the key service. Set the value to KMS.
                encryptConfig.Add("KeyServiceType", "KMS");
                // The ciphertext of the data key.
                encryptConfig.Add("CipherText", response.CiphertextBlob);
    
                return encryptConfig.ToString();
            }
    
            /// <summary>
            /// 1. Build overriding parameters, which override only the file URL of an image watermark or the content of a text watermark. If you do not need these parameters, leave overrideParams empty.
            /// 2. Make sure that the ID of the watermark is associated with the ID of the transcoding template that you use. The ID of the transcoding template is specified by TranscodeTemplateId.
            /// 3. You can call this operation to add only a watermark whose ID is associated with the ID of the transcoding template that you use.
            /// Note: The image watermark file and the video that you want to transcode must be stored on the same origin server.
            /// </summary>
            /// <returns>The override parameters.</returns>
            /// 
            public static string BuildOverrideParams() {
                // Build overriding parameters.
                JObject overrideParams = new JObject();
    
                // Override the file URL of the image watermark.
                JArray watermarks = new JArray();
                JObject watermark1 = new JObject();
                // The ID of the watermark whose image you want to override. The ID must be associated with the transcoding template.
                watermark1.Add("WatermarkId", "2ea587477c5a1bc8b5742d7");
                // The file URL of the new image that is stored in an Object Storage Service (OSS) bucket. The new image and the video must be stored on the same origin server.
                watermark1.Add("FileUrl", "https://outin-40564284ef05113e1403e7.oss-cn-shanghai.aliyuncs.com/watermarks/02A1B22DF25D46C3C725A4-6-2.png");
                watermarks.Add(watermark1);
    
                // Override the content of the text watermark.
                JObject watermark2 = new JObject();
                // The ID of the watermark whose content you want to override. The ID must be associated with the transcoding template.
                watermark2.Add("WatermarkId", "d297ba31ac5242d207****");
                // The new content of the watermark.
                watermark2.Add("Content", "User ID: 52****");
                watermarks.Add(watermark2);
    
                overrideParams.Add("Watermarks", watermarks);
    
                return overrideParams.ToString();
            }
        }
    }



Submit a snapshot job {#h2--div-id-submitsnapshotjob-div-3}
-----------------------------------------------------------

You can call the SubmitSnapshotJob operation to submit a snapshot job.
For more information about the request and response parameters of this operation, see [SubmitSnapshotJob](/intl.en-US/API Reference/Media processing/Initiate Process/SubmitSnapshotJob.md). Example:
**Note**
For more information about how to create a snapshot template, see [Create a snapshot template](/intl.en-US/API Reference/Media processing/Snapshot Template/AddVodTemplate.md). {#h2--div-id-submitsnapshotjob-div-3}
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.vod.Model.V20170321;
    using Newtonsoft.Json.Linq;
    
    namespace Aliyun.Acs.vod.Sdk.SubmitSnapshotJob
    {
        class MainClass
        {
            public static void Main(string[] args)
            {
                try
                {
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // Initiate the request and display the response.
                    SubmitSnapshotJobResponse response = SubmitSnapshotJob(client);
                    Console.WriteLine("RequestId = " + response.RequestId);
                }
                catch (ServerException e)
                {
                    if (e.RequestId ! = null)
                    {
                        Console.WriteLine("RequestId = " + e.RequestId);
                    }
                    Console.WriteLine("ErrorCode = " + e.ErrorCode);
                    Console.WriteLine("ErrorMessage = " + e.ErrorMessage);
                }
                catch (ClientException e)
                {
                    if (e.RequestId ! = null)
                    {
                        Console.WriteLine("RequestId = " + e.RequestId);
                    }
                    Console.WriteLine("ErrorCode = " + e.ErrorCode);
                    Console.WriteLine("ErrorMessage = " + e.ErrorMessage);
                }
                catch (Exception e)
                {
                    Console.WriteLine("ErrorMessage = " + e.ToString());
                }
            }
    
            public static SubmitSnapshotJobResponse SubmitSnapshotJob(DefaultAcsClient client) 
            {
                // Create a request.
                SubmitSnapshotJobRequest request = new SubmitSnapshotJobRequest();
                // The ID of the video for which you want to create snapshots. We recommend that you specify SnapshotTemplateId.
                request.VideoId = "1f7ed5623409489193e41d16f6c7****";
                // The ID of the snapshot template.
                request.SnapshotTemplateId = "3cac80cddb4455e37460f491aecc****";
                // If you specify the SnapshotTemplateId parameter, the following parameters are ignored:
                request.Count = 50;
                request.SpecifiedOffsetTime = 0;
                request.Interval = 1;
                request.Width = "200";
                request.Height = "200";
                request.SpriteSnapshotConfig = BuildSnapshotTemplateConfig();
                return client.GetAcsResponse(request);
            }
    
            /// <summary>
            /// Build the configurations of the image sprite snapshot.
            /// </summary>
            /// <returns>Configurations of the image sprite snapshot</returns>
            public static string BuildSnapshotTemplateConfig()
            {
                // Build overriding parameters.
                JObject spriteSnapshotConfig = new JObject();
                spriteSnapshotConfig.Add("CellWidth", "120");
                spriteSnapshotConfig.Add("CellHeight", "68");
                spriteSnapshotConfig.Add("Columns", "3");
                spriteSnapshotConfig.Add("Lines", "10");
                spriteSnapshotConfig.Add("Padding", "20");
                spriteSnapshotConfig.Add("Margin", "50");
    
                // Determine whether to retain the source image after an image sprite is generated.
                spriteSnapshotConfig.Add("KeepCellPic", "keep");
                spriteSnapshotConfig.Add("Color", "tomato");
                return spriteSnapshotConfig.ToString();
            }
        }
    }



Query snapshot data {#h2--div-id-listsnapshots-div-4}
-----------------------------------------------------

You can call the ListSnapshots operation to query snapshot data.
For more information about the request and response parameters of this operation, see [ListSnapshots](/intl.en-US/API Reference/Media management/Image Management/ListSnapshots.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.vod.Sdk.ListSnapshots
    {
        class MainClass
        {
            public static void Main(string[] args)
            {
                try
                {
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // Initiate the request and display the response.
                    ListSnapshotsResponse response = ListSnapshots(client);
                    Console.WriteLine("RequestId = " + response.RequestId);
                }
                catch (ServerException e)
                {
                    if (e.RequestId ! = null)
                    {
                        Console.WriteLine("RequestId = " + e.RequestId);
                    }
                    Console.WriteLine("ErrorCode = " + e.ErrorCode);
                    Console.WriteLine("ErrorMessage = " + e.ErrorMessage);
                }
                catch (ClientException e)
                {
                    if (e.RequestId ! = null)
                    {
                        Console.WriteLine("RequestId = " + e.RequestId);
                    }
                    Console.WriteLine("ErrorCode = " + e.ErrorCode);
                    Console.WriteLine("ErrorMessage = " + e.ErrorMessage);
                }
                catch (Exception e)
                {
                    Console.WriteLine("ErrorMessage = " + e.ToString());
                }
            }
    
            public static ListSnapshotsResponse ListSnapshots(DefaultAcsClient client)
            {
                // Create a request.
                ListSnapshotsRequest request = new ListSnapshotsRequest();
                // The video ID.
                request.VideoId = "1f7ed5623409489193e41d16f6c7****";
                // The snapshot type.
                request.SnapshotType = "CoverSnapshot";
                request.PageNo = "1";
                request.PageSize = "20";
                return client.GetAcsResponse(request);
            }
        }
    }



Preprocess videos in the production studio {#h2--div-id-submitpreprocessjobs-div-5}
-----------------------------------------------------------------------------------

You can call the SubmitPreprocessJobs operation to preprocess videos in the production studio.
For more information about the request and response parameters of this operation, see [SubmitPreprocessJobs](). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.vod.Sdk.SubmitPreprocessJobs
    {
        class MainClass
        {
            public static void Main(string[] args)
            {
                try
                {
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // Initiate the request and display the response.
                    SubmitPreprocessJobsResponse response = SubmitPreprocessJobs(client);
                    Console.WriteLine("RequestId = " + response.RequestId);
                }
                catch (ServerException e)
                {
                    if (e.RequestId ! = null)
                    {
                        Console.WriteLine("RequestId = " + e.RequestId);
                    }
                    Console.WriteLine("ErrorCode = " + e.ErrorCode);
                    Console.WriteLine("ErrorMessage = " + e.ErrorMessage);
                }
                catch (ClientException e)
                {
                    if (e.RequestId ! = null)
                    {
                        Console.WriteLine("RequestId = " + e.RequestId);
                    }
                    Console.WriteLine("ErrorCode = " + e.ErrorCode);
                    Console.WriteLine("ErrorMessage = " + e.ErrorMessage);
                }
                catch (Exception e)
                {
                    Console.WriteLine("ErrorMessage = " + e.ToString());
                }
            }
    
            /// <summary>
            /// Preprocess videos in the production studio.
            /// </summary>
            /// <returns>The preprocess jobs.</returns>
            /// <param name="client">Vod Client.</param>
            public static SubmitPreprocessJobsResponse SubmitPreprocessJobs(DefaultAcsClient client)
            {
                // Create a request.
                SubmitPreprocessJobsRequest request = new SubmitPreprocessJobsRequest();
                // The ID of the video for which you want to create snapshots. We recommend that you specify SnapshotTemplateId.
                request.VideoId = "c86c0ceb8db54ae09796535****";
                // The snapshot type.
                request.PreprocessType = "PreprocessType";
    
                return client.GetAcsResponse(request);
            }
        }
    }



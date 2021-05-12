Media upload 
=================================

This topic provides examples on how to use the API operations of the media upload module. The API operations are encapsulated in ApsaraVideo VOD SDK for .NET. You can call the API operations to create upload URLs and credentials and register media assets. You can also upload multiple media files based on the URLs of mezzanine files at a time. 

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/.NET SDK/Initialization.md). 

Create a URL and a credential for uploading videos {#h2--div-id-createuploadvideo-div-2}
----------------------------------------------------------------------------------------

You can call the CreateUploadVideo operation to create a URL and a credential for uploading videos. 

For more information about the request and response parameters of this operation, see [CreateUploadVideo](/intl.en-US/API Reference/Media upload/CreateUploadVideo.md). Sample code:

    using System; using Aliyun.Acs.Core; using Aliyun.Acs.Core.Exceptions; using Aliyun.Acs.vod.Model.V20170321; namespace Aliyun.Acs.vod.Sdk.CreateUploadVideo { class MainClass { public static void Main(string[] args) { try { // Create a request. CreateUploadVideoRequest request = new CreateUploadVideoRequest(); request.Title = "this is a sample title"; request.FileName = "sample.mp4"; // request.Tags = "tags1,tags2"; // request.Description = "this is a sample description"; // request.CoverURL = "http://192.168.0.0/16/sample.jpg"; // request.CateId = -1; // request.TemplateGroupId = "278840921dee4963bb5862b43a52****"; // Initialize a client. DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>"); // Send the request and obtain the response. CreateUploadVideoResponse response = client.GetAcsResponse(request); Console.WriteLine("RequestId = " + response.RequestId); Console.WriteLine("UploadAddress = " + response.UploadAddress); Console.WriteLine("UploadAuth = " + response.UploadAuth); } catch (ServerException ex) { Console.WriteLine(ex.ToString()); } catch (ClientException ex) { Console.WriteLine(ex.ToString()); } } } }


**Notice**

When you call the CreateUploadVideo operation to create a credential, a URL, and a video ID for uploading a video, the video is in the **Uploading** state in the ApsaraVideo VOD console. The video remains in the **Uploading** state in the ApsaraVideo VOD console in the following cases: You do not upload the video in the client, an error occurs during the upload, or the upload job is interrupted, for example, the application process is terminated. In these cases, call the RefreshUploadVideo operation to pass the video ID to obtain a new URL and credential, and then upload the video. Alternatively, manually delete the video that is in the Uploading state. For more information, see [RefreshUploadVideo](/intl.en-US/API Reference/Media upload/RefreshUploadVideo.md). To upload videos, call the [UploadMediaByURL](/intl.en-US/API Reference/Media upload/UploadMediaByURL.md) operation.

Refresh the credential for uploading videos {#h2--div-id-refreshuploadvideo-div-3}
----------------------------------------------------------------------------------

You can call the RefreshUploadVideo operation to refresh the credential for uploading videos. 

For more information about the request and response parameters of this operation, see [RefreshUploadVideo](/intl.en-US/API Reference/Media upload/RefreshUploadVideo.md). Sample code:

    using System; using Aliyun.Acs.Core; using Aliyun.Acs.Core.Exceptions; using Aliyun.Acs.vod.Model.V20170321; namespace Aliyun.Acs.vod.Sdk.Sample { class MainClass { public static void Main(string[] args) { try { // Create a request. RefreshUploadVideoRequest request = new RefreshUploadVideoRequest(); request.VideoId = "Video ID"; // Initialize a client. DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>"); // Send the request and obtain the response. RefreshUploadVideoResponse response = client.GetAcsResponse(request); Console.WriteLine("RequestId = " + response.RequestId); Console.WriteLine("UploadAddress = " + response.UploadAddress); Console.WriteLine("UploadAuth = " + response.UploadAuth); } catch (ServerException ex) { Console.WriteLine(ex.ToString()); } catch (ClientException ex) { Console.WriteLine(ex.ToString()); } } } }



Create a URL and a credential for uploading images {#h2--div-id-createuploadimage-div-4}
----------------------------------------------------------------------------------------

You can call the CreateUploadImage operation to create a URL and a credential for uploading images. 

For more information about the request and response parameters of this operation, see [CreateUploadImage](/intl.en-US/API Reference/Media upload/CreateUploadImage.md). Sample code:

    using System; using Aliyun.Acs.Core; using Aliyun.Acs.Core.Exceptions; using Aliyun.Acs.vod.Model.V20170321; namespace Aliyun.Acs.vod.Sdk.Sample { class MainClass { public static void Main(string[] args) { try { // Create a request. CreateUploadImageRequest request = new CreateUploadImageRequest(); request.ImageType = "cover"; request.ImageExt = "jpg"; // Initialize a client. DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>"); // Send the request and obtain the response. CreateUploadImageResponse response = client.GetAcsResponse(request); Console.WriteLine("RequestId = " + response.RequestId); Console.WriteLine("UploadAddress = " + response.UploadAddress); Console.WriteLine("UploadAuth = " + response.UploadAuth); } catch (ServerException ex) { Console.WriteLine(ex.ToString()); } catch (ClientException ex) { Console.WriteLine(ex.ToString()); } } } }



Create a URL and a credential for uploading auxiliary media assets {#h2--div-id-createuploadattachedmedia-div-5}
----------------------------------------------------------------------------------------------------------------

You can call the CreateUploadAttachedMedia operation to create a URL and a credential for uploading auxiliary media assets. 

For more information about the request and response parameters of this operation, see [CreateUploadAttachedMedia](/intl.en-US/API Reference/Media upload/CreateUploadAttachedMedia.md). Sample code:

    using System; using Aliyun.Acs.Core; using Aliyun.Acs.Core.Exceptions; using Aliyun.Acs.vod.Model.V20170321; namespace CreateUploadAttachedMedia { class MainClass { public static void Main(string[] args) { try { // Create a request. CreateUploadAttachedMediaRequest request = new CreateUploadAttachedMediaRequest(); request.BusinessType = "watermark"; request.MediaExt = "gif"; request.Title = "this is a sample"; // Initialize a client. DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>"); // Send the request and obtain the response. CreateUploadAttachedMediaResponse response = client.GetAcsResponse(request); Console.WriteLine("RequestId = " + response.RequestId); Console.WriteLine("MediaId = " + response.MediaId); Console.WriteLine("MediaURL = " + response.MediaURL); Console.WriteLine("UploadAddress = " + response.UploadAddress); Console.WriteLine("UploadAuth = " + response.UploadAuth); } catch (ServerException ex) { Console.WriteLine(ex.ToString()); } catch (ClientException ex) { Console.WriteLine(ex.ToString()); } } } }



Upload multiple media files based on the URLs of mezzanine files at a time {#h2-url-div-id-uploadmediabyurl-div-6}
------------------------------------------------------------------------------------------------------------------

You can call the UploadMediaByURL operation to upload multiple media files based on the URLs of mezzanine files at a time. 

For more information about the request and response parameters of this operation, see [UploadMediaByURL](/intl.en-US/API Reference/Media upload/UploadMediaByURL.md). Sample code:

    using System; using Aliyun.Acs.Core; using Aliyun.Acs.Core.Exceptions; using Aliyun.Acs.vod.Model.V20170321; namespace Aliyun.Acs.vod.Sdk.UploadMediaByURL { class MainClass { public static void Main(string[] args) { try { UploadMediaByURLRequest request = new UploadMediaByURLRequest(); request.UploadMetadatas = "[{\"SourceUrl\":\"http://192.168.0.0/16/test.mp4\",\"Title\":\"upload by url sample\"}]"; // Initialize a client. DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>"); // Send the request and obtain the response. UploadMediaByURLResponse response = client.GetAcsResponse(request); Console.WriteLine("RequestId = " + response.RequestId); } catch (ServerException ex) { Console.WriteLine(ex.ToString()); } catch (ClientException ex) { Console.WriteLine(ex.ToString()); } } } }



Register media assets {#h2--div-id-registermedia-div-7}
-------------------------------------------------------

You can call the RegisterMedia operation to register media assets. 

For more information about the request and response parameters of this operation, see [RegisterMedia](/intl.en-US/API Reference/Media upload/RegisterMedia.md). Sample code:

    using System; using Aliyun.Acs.Core; using Aliyun.Acs.Core.Exceptions; using Aliyun.Acs.vod.Model.V20170321; namespace Aliyun.Acs.vod.Sdk.RegisterMedia { class MainClass { public static void Main(string[] args) { try { RegisterMediaRequest request = new RegisterMediaRequest(); request.RegisterMetadatas = "[{\"Title\":\"register media test\",\"FileURL\":\"https://test.oss-cn-shanghai.aliyuncs.com/vod-test/aaa.mp4\"}]"; // Initialize a client. DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>"); // Send the request and obtain the response. RegisterMediaResponse response = client.GetAcsResponse(request); Console.WriteLine("RequestId = " + response.RequestId); if (response.RegisteredMediaList != null && response.RegisteredMediaList.Count > 0) { foreach(var media in response.RegisteredMediaList) { Console.WriteLine("MediaId = " + media.MediaId); Console.WriteLine("FileURL = " + media.FileURL); Console.WriteLine("NewRegister = " + media.NewRegister); } } if (response.FailedFileURLs != null && response.FailedFileURLs.Count > 0) { foreach (var fileURL in response.FailedFileURLs) { Console.WriteLine("FailedFileURL = " + fileURL); } } } catch (ServerException ex) { Console.WriteLine(ex.ToString()); } catch (ClientException ex) { Console.WriteLine(ex.ToString()); } } } }



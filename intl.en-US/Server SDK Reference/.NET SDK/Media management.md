Media management 
=====================================

This topic provides examples on how to use the API operations of the media management module. The API operations are encapsulated in ApsaraVideo VOD SDK for .NET. You can call the API operations to search for media asset information, modify video information, and query source file information. You can also query and delete videos and images.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/.NET SDK/Initialization.md).

Search for media asset information {#h2--div-id-searchmedia-div-2}
------------------------------------------------------------------

You can call the SearchMedia operation to search for media asset information.
For more information about the request and response parameters of this operation, see [SearchMedia](/intl.en-US/API Reference/Media asset management/Media asset search/SearchMedia.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.vod.Sdk.SearchMedia
    {
        class MainClass
        {
            public static void Main(string[] args)
            {
                try
                {
                    // Create a request.
                    SearchMediaRequest request = new SearchMediaRequest();
                    request.SearchType = "video";
                    request.Fields = "Title,CoverURL,Status";
                    request.Match = "Status in ('Normal','Checking') and CreationTime = ('2018-07-01T08:00:00Z','2018-08-01T08:00:00Z')";
                    request.PageNo = 1;
                    request.PageSize = 10;
                    request.SearchType = "video";
                    request.SortBy = "CreationTime:Desc";
                    // Initialize a client.
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // Initiate the request and display the response.
                    SearchMediaResponse response = client.GetAcsResponse(request);
                    Console.WriteLine("RequestId = " + response.RequestId);
                    if (response.MediaList ! = null && response.MediaList.Count > 0)
                    {
                        Console.WriteLine("Total = " + response.Total + "\n");
                        Console.WriteLine("ScrollToken = " + response.ScrollToken + "\n");
                        foreach (var media in response.MediaList)
                        {
                            Console.WriteLine("MediaId = " + media.MediaId + "\n");
                            Console.WriteLine("MediaType = " + media.MediaType + "\n");
                            Console.WriteLine("CreationTime = " + media.CreationTime + "\n");
                            Console.WriteLine("Title = " + media.Video.Title + "\n");
                            Console.WriteLine("CoverURL = " + media.Video.CoverURL + "\n");
                            Console.WriteLine("Status = " + media.Video.Status + "\n");
                        }
                    }
                }
                catch (ServerException ex)
                {
                    Console.WriteLine(ex.ToString());
                }
                catch (ClientException ex)
                {
                    Console.WriteLine(ex.ToString());
                }
            }
        }
    }



Query a video {#h2--div-id-getvideoinfo-div-3}
----------------------------------------------

You can call the GetVideoInfo operation to query details about a video.
For more information about the request and response parameters of this operation, see [GetVideoInfo](/intl.en-US/API Reference/Media asset management/Audio and video management/GetVideoInfo.md). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.vod.Sdk.GetVideoInfo
    {
        class MainClass
        {
            public static void Main(string[] args)
            {
                try
                {
                    // Create a request.
                    GetVideoInfoRequest request = new GetVideoInfoRequest();
                    request.VideoId = "<your VideoId>";
                    // Initialize a client.
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // Initiate the request and display the response.
                    GetVideoInfoResponse response = client.GetAcsResponse(request);
                    Console.WriteLine("RequestId = " + response.RequestId);
                    Console.WriteLine("Title = " + response.Video.Title);
                    Console.WriteLine("CoverURL = " + response.Video.CoverURL);
                }
                catch (ServerException ex)
                {
                    Console.WriteLine(ex.ToString());
                }
                catch (ClientException ex)
                {
                    Console.WriteLine(ex.ToString());
                }
            }
        }
    }



Query videos {#h2--div-id-getvideoinfos-div-4}
----------------------------------------------

You can call the GetVideoInfos operation to query videos.
For more information about the request and response parameters of this operation, see [GetVideoInfos](/intl.en-US/API Reference/Media asset management/Audio and video management/GetVideoInfos.md). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.Core.Profile;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.vod.Sdk.GetVideoInfos
    {
        class MainClass
        {
            public static void Main(string[] args)
            {
                try
                {
                    // Create a request.
                    GetVideoInfosRequest request = new GetVideoInfosRequest();
                    request.VideoIds = "VideoId1,VideoId2";
                    // Initialize a client.
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // Initiate the request and display the response.
                    GetVideoInfosResponse response = client.GetAcsResponse(request);
                    Console.WriteLine("RequestId = " + response.RequestId);
                    if (response.NonExistVideoIds ! = null && response.NonExistVideoIds.Count > 0)
                    {
                        foreach (var videoId in response.NonExistVideoIds) {
                            Console.WriteLine("NonExist videoId = " + videoId);
                        }
                    }
                    if (response.VideoList ! = null && response.VideoList.Count > 0)
                    {
                        foreach (var video in response.VideoList)
                        {
                            Console.WriteLine("MediaId = " + video.VideoId);
                            Console.WriteLine("Title = " + video.Title);
                            Console.WriteLine("CreationTime = " + video.CreationTime);
                            Console.WriteLine("CoverURL = " + video.CoverURL);
                            Console.WriteLine("Status = " + video.Status);
                        }
                    }
                }
                catch (ServerException ex)
                {
                    Console.WriteLine(ex.ToString());
                }
                catch (ClientException ex)
                {
                    Console.WriteLine(ex.ToString());
                }
            }
        }
    }



Modify the information about a video {#h2--div-id-updatevideoinfo-div-5}
------------------------------------------------------------------------

You can call the UpdateVideoInfo operation to modify the information about a video.
For more information about the request and response parameters of this operation, see [UpdateVideoInfo](/intl.en-US/API Reference/Media asset management/Audio and video management/UpdateVideoInfo.md). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.vod.Sdk.UpdateVideoInfo
    {
        class MainClass
        {
            public static void Main(string[] args)
            {
                try
                {
                    // Create a request.
                    UpdateVideoInfoRequest request = new UpdateVideoInfoRequest();
                    request.VideoId = "<your VideoId>";
                    request.Title = "new Title";
                    request.Description = "new Description";
                    // Initialize a client.
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // Initiate the request and display the response.
                    UpdateVideoInfoResponse response = client.GetAcsResponse(request);
                    Console.WriteLine("RequestId = " + response.RequestId);
                }
                catch (ServerException ex)
                {
                    Console.WriteLine(ex.ToString());
                }
                catch (ClientException ex)
                {
                    Console.WriteLine(ex.ToString());
                }
            }
        }
    }



Modify the information about videos {#h2--div-id-updatevideoinfos-div-6}
------------------------------------------------------------------------

You can call the UpdateVideoInfos operation to modify the information about videos.
For more information about the request and response parameters of this operation, see [UpdateVideoInfos](/intl.en-US/API Reference/Media asset management/Audio and video management/UpdateVideoInfos.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.vod.Sdk.UpdateVideoInfos
    {
        class MainClass
        {
            public static void Main(string[] args)
            {
                try
                {
                    // Create a request.
                    UpdateVideoInfosRequest request = new UpdateVideoInfosRequest();
                    request.UpdateContent = "[{\"VideoId\":\"VideoId1\",\"Title\":\"new Title\"},{\"VideoId\":\"VideoId2\",\"Description\":\"new Description\"}]";
                    // Initialize a client.
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // Initiate the request and display the response.
                    UpdateVideoInfosResponse response = client.GetAcsResponse(request);
                    Console.WriteLine("RequestId = " + response.RequestId);
                    if (response.NonExistVideoIds ! = null && response.NonExistVideoIds.Count > 0)
                    {
                        foreach (var videoId in response.NonExistVideoIds)
                        {
                            Console.WriteLine("NonExist videoId = " + videoId);
                        }
                    }
                }
                catch (ServerException ex)
                {
                    Console.WriteLine(ex.ToString());
                }
                catch (ClientException ex)
                {
                    Console.WriteLine(ex.ToString());
                }
            }
        }
    }



Delete videos {#h2--div-id-deletevideo-div-7}
---------------------------------------------

You can call the DeleteVideo operation to delete videos.
For more information about the request and response parameters of this operation, see [DeleteVideo](/intl.en-US/API Reference/Media asset management/Audio and video management/DeleteVideo.md). Example: 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.vod.Sdk.DeleteVideo
    {
        class MainClass
        {
            public static void Main(string[] args)
            {
                try
                {
                    // Create a request.
                    DeleteVideoRequest request = new DeleteVideoRequest();
                    request.VideoIds = "VideoId1,VideoId2";
                    // Initialize a client.
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // Initiate the request and display the response.
                    DeleteVideoResponse response = client.GetAcsResponse(request);
                    Console.WriteLine("RequestId = " + response.RequestId);
                }
                catch (ServerException ex)
                {
                    Console.WriteLine(ex.ToString());
                }
                catch (ClientException ex)
                {
                    Console.WriteLine(ex.ToString());
                }
            }
        }
    }



Query source file information (including the file URL) {#h2--div-id-getmezzanineinfo-div-8}
-------------------------------------------------------------------------------------------

You can call the GetMezzanineInfo operation to query source file information.
For more information about the request and response parameters of this operation, see [GetMezzanineInfo](/intl.en-US/API Reference/Media asset management/Audio and video management/GetMezzanineInfo.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.vod.Sdk.GetMezzanineInfo
    {
        class MainClass
        {
            public static void Main(string[] args)
            {
                try
                {
                    // Create a request.
                    GetMezzanineInfoRequest request = new GetMezzanineInfoRequest();
                    request.VideoId = "f45cf4eba5c84d25b29023338955****";
                    // Initialize a client.
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // Initiate the request and display the response.
                    GetMezzanineInfoResponse response = client.GetAcsResponse(request);
                    Console.WriteLine("RequestId = " + response.RequestId);
                    Console.WriteLine("FileURL = " + response.Mezzanine.FileURL);
                    Console.WriteLine("Duration = " + response.Mezzanine.Duration);
                }
                catch (ServerException ex)
                {
                    Console.WriteLine(ex.ToString());
                }
                catch (ClientException ex)
                {
                    Console.WriteLine(ex.ToString());
                }
            }
        }
    }



Query videos by using filter conditions {#h2--div-id-getvideolist-div-9}
------------------------------------------------------------------------

You can call the GetVideoList operation to query videos by using filter conditions.
For more information about the request and response parameters of this operation, see [GetVideoList](/intl.en-US/API Reference/Media asset management/Audio and video management/GetVideoList.md). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.vod.Sdk.Sample
    {
        class MainClass
        {
            public static void Main(string[] args)
            {
                try
                {
                    // Create a request.
                    GetVideoListRequest request = new GetVideoListRequest();
                    // Use the time one month before the current time and the current time as the beginning and end of the time range to query videos. The time must be in UTC.
                    request.StartTime = DateTime.UtcNow.AddMonths(-2).ToString("yyyy-MM-ddTHH:mm:ssZ");
                    request.EndTime = DateTime.UtcNow.ToString("yyyy-MM-ddTHH:mm:ssZ");
                    request.Status = "Normal,Checking";
                    request.PageNo = 1;
                    request.PageSize = 20;
                    // Initialize a client.
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // Initiate the request and display the response.
                    GetVideoListResponse response = client.GetAcsResponse(request);
                    Console.WriteLine("RequestId = " + response.RequestId);
                    foreach (var videoInfo in response.VideoList)
                    {
                        Console.WriteLine("VideoList.VideoId = " + videoInfo.VideoId);
                        Console.WriteLine("VideoList.Title = " + videoInfo.Title);
                    }
                }
                catch (ServerException ex)
                {
                    Console.WriteLine(ex.ToString());
                }
                catch (ClientException ex)
                {
                    Console.WriteLine(ex.ToString());
                }
            }
        }
    }



Delete a media stream {#h2--div-id-deletestream-div-10}
-------------------------------------------------------

You can call the DeleteStream operation to delete a media stream.
For more information about the request and response parameters of this operation, see [DeleteStream](/intl.en-US/API Reference/Media asset management/Audio and video management/DeleteStream.md). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.vod.Sdk.Sample
    {
        class MainClass
        {
            public static void Main(string[] args)
            {
                try
                {
                    // Create a request.
                    DeleteStreamRequest request = new DeleteStreamRequest();
                    request.VideoId = "<your VideoId>";
                    request.JobIds = "JobId1,JobId2";
                    // Initialize a client.
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // Initiate the request and display the response.
                    DeleteStreamResponse response = client.GetAcsResponse(request);
                    Console.WriteLine("RequestId = " + response.RequestId);
                }
                catch (ServerException ex)
                {
                    Console.WriteLine(ex.ToString());
                }
                catch (ClientException ex)
                {
                    Console.WriteLine(ex.ToString());
                }
            }
        }
    }



Delete source files {#h2--div-id-deletemezzanines-div-11}
---------------------------------------------------------

You can call the DeleteMezzanines operation to delete source files.
For more information about the request and response parameters of this operation, see [DeleteMezzanines](/intl.en-US/API Reference/Media asset management/Audio and video management/DeleteMezzanines.md). Example: 
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.vod.Sdk.DeleteMezzanines
    {
        class MainClass
        {
            public static void Main(string[] args)
            {
                try
                {
                    // Create a request.
                    DeleteMezzaninesRequest request = new DeleteMezzaninesRequest();
                    // Specify the IDs of videos for which you want to delete source files.
                    request.VideoIds = "VideoId1,VideoId2";
                    // Initialize a client.
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // Initiate the request and display the response.
                    DeleteMezzaninesResponse response = client.GetAcsResponse(request);
                    // List the request ID.
                    Console.WriteLine("RequestId = " + response.RequestId);
                    if (response.NonExistVideoIds ! = null && response.NonExistVideoIds.Count > 0)
                    {
                        foreach (var videoId in response.NonExistVideoIds)
                        {
                            Console.WriteLine("NonExist videoId = " + videoId);
                        }
                    }
                    if (response.UnRemoveableVideoIds ! = null && response.UnRemoveableVideoIds.Count > 0)
                    {
                        foreach (var videoId in response.UnRemoveableVideoIds)
                        {
                            Console.WriteLine("UnRemoveable videoId = " + videoId);
                        }
                    }
                }
                catch (ServerException ex)
                {
                    Console.WriteLine(ex.ToString());
                }
                catch (ClientException ex)
                {
                    Console.WriteLine(ex.ToString());
                }
            }
        }
    }



Modify the information about images {#h2--div-id-updateimageinfos-div-12}
-------------------------------------------------------------------------

You can call the UpdateImageInfos operation to modify the information about images.
For more information about the request and response parameters of this operation, see [UpdateImageInfos](/intl.en-US/API Reference/Media asset management/Image management/UpdateImageInfos.md). Example: 
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.vod.Sdk.UpdateImageInfos
    {
        class MainClass
        {
            public static void Main(string[] args)
            {
                try
                {
                    // Create a request.
                    UpdateImageInfosRequest request = new UpdateImageInfosRequest();
    
                    request.UpdateContent = "[{\"ImageId\":\"ImageId1\",\"Title\":\"new Title\"},{\"ImageId\":\"ImageId2\",\"Description\":\"new Description\"}]";
                    // Initialize a client.
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // Initiate the request and display the response.
                    UpdateImageInfosResponse response = client.GetAcsResponse(request);
                    Console.WriteLine("RequestId = " + response.RequestId);
                    if (response.NonExistImageIds ! = null && response.NonExistImageIds.Count > 0)
                    {
                        foreach (var imageId in response.NonExistImageIds)
                        {
                            Console.WriteLine("NonExist ImageId = " + imageId);
                        }
                    }
                }
                catch (ServerException ex)
                {
                    Console.WriteLine(ex.ToString());
                }
                catch (ClientException ex)
                {
                    Console.WriteLine(ex.ToString());
                }
            }
        }
    }



Query an image {#h2--div-id-getimageinfo-div-13}
------------------------------------------------

You can call the GetImageInfo operation to query details about an image.
For more information about the request and response parameters of this operation, see [GetImageInfo](/intl.en-US/API Reference/Media asset management/Image management/GetImageInfo.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.vod.Sdk.GetImageInfo
    {
        class MainClass
        {
            public static void Main(string[] args)
            {
                try
                {
                    // Create a request.
                    GetImageInfoRequest request = new GetImageInfoRequest();
                    // Specify the image ID.
                    request.ImageId = "ImageId";
                    // Initialize a client.
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // Initiate the request and display the response.
                    GetImageInfoResponse response = client.GetAcsResponse(request);
                    // List the request ID.
                    Console.WriteLine("RequestId = " + response.RequestId);
                    if (response.ImageInfo ! = null)
                    {
                        Console.WriteLine("ImageId = " + response.ImageInfo.ImageId);
                        Console.WriteLine("ImageType = " + response.ImageInfo.ImageType);
                        Console.WriteLine("Title = " + response.ImageInfo.Title);
                    }
                }
                catch (ServerException ex)
                {
                    Console.WriteLine(ex.ToString());
                }
                catch (ClientException ex)
                {
                    Console.WriteLine(ex.ToString());
                }
            }
        }
    }



Delete images {#h2--div-id-deleteimage-div-14}
----------------------------------------------

You can call the DeleteImage operation to delete images.
For more information about the request and response parameters of this operation, see [DeleteImage](/intl.en-US/API Reference/Media asset management/Image management/DeleteImage.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.vod.Sdk.DeleteImage
    {
        class MainClass
        {
            public static void Main(string[] args)
            {
                try
                {
                    // Create a request.
                    DeleteImageRequest request = new DeleteImageRequest();
                    // Delete an image file based on ImageURL.
                    request.DeleteImageType = "ImageURL";
                    request.ImageURLs = "http://192.168.0.0/16/cover.jpg";
                    // Delete image files based on ImageId.
                    //request.DeleteImageType = "ImageId";
                    //request.ImageIds = "ImageId1,ImageId2";
                    // Delete image files based on VideoId and ImageType.
                    //request.DeleteImageType = "VideoId";
                    //request.VideoId = "VideoId";
                    //request.ImageType = "SpriteSnapshot";
                    // Initialize a client.
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // Initiate the request and display the response.
                    DeleteImageResponse response = client.GetAcsResponse(request);
                    // List the request ID.
                    Console.WriteLine("RequestId = " + response.RequestId);
                }
                catch (ServerException ex)
                {
                    Console.WriteLine(ex.ToString());
                }
                catch (ClientException ex)
                {
                    Console.WriteLine(ex.ToString());
                }
            }
        }
    }



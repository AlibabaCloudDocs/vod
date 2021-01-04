Live-to-VOD 
================================

This topic provides examples on how to use the API operations of the live-to-VOD module. The API operations are encapsulated in ApsaraVideo VOD SDK for .NET. You can call the API operations to query live-to-VOD videos.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/.NET SDK/Initialization.md).

Query live-to-VOD videos {#h2--div-id-listliverecordvideo-div-2}
----------------------------------------------------------------

You can call the ListLiveRecordVideo operation to query live-to-VOD videos.
For more information about the request and response parameters of this operation, see [ListLiveRecordVideo](/intl.en-US/API Reference/Conversion/ListLiveRecordVideo.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.vod.Sdk.ListLiveRecordVideo
    {
        class MainClass
        {
            public static void Main(string[] args)
            {
                try
                {
                    // Create a request.
                    ListLiveRecordVideoRequest request = new ListLiveRecordVideoRequest();
                    request.StartTime = "2018-04-24T03:21:04Z";
                    request.EndTime = "2018-05-21T03:21:44Z";
                    request.StreamName = "testStreamName";
                    request.DomainName = "testdomain.aliyun.com";
                    request.AppName = "testAppName";
                    // Initialize a client.
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // Initiate the request and display the response.
                    ListLiveRecordVideoResponse response = client.GetAcsResponse(request);
                    // List the request ID.
                    Console.WriteLine("RequestId = " + response.RequestId);
                    if (response.LiveRecordVideoList ! = null && response.LiveRecordVideoList.Count > 0)
                    {
                        // List the number of live-to-VOD videos.
                        Console.WriteLine("Total = " + response.Total);
                        foreach (var liveRecordVideo in response.LiveRecordVideoList)
                        {
                            Console.WriteLine("AppName = " + liveRecordVideo.AppName);
                            Console.WriteLine("DomainName = " + liveRecordVideo.DomainName);
                            Console.WriteLine("PlaylistId = " + liveRecordVideo.PlaylistId);
                        }
                    }
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
        }
    }



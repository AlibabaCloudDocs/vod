Video playback 
===================================

This topic provides examples on how to use the API operations of the video playback module. The API operations are encapsulated in ApsaraVideo VOD SDK for .NET. You can call the API operations to query playback URLs and playback credentials.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/.NET SDK/Initialization.md).

Query a playback URL {#h2--div-id-getplayinfo-div-2}
----------------------------------------------------

You can call the GetPlayInfo operation to query a playback URL.
For more information about the request and response parameters of this operation, see [GetPlayInfo](/intl.en-US/API Reference/Audio and video playback/GetPlayInfo.md). Example: 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Profile;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.vod.Model.V20170321;
    using System.Collections.Generic;
    
    namespace Aliyun.Acs.vod.Sdk.Sample
    {
        class MainClass
        {
            public static void Main(string[] args)
            {
                try
                {
                    // Create a request.
                    GetPlayInfoRequest request = new GetPlayInfoRequest();
                    request.VideoId = "<your VideoId>";
                    // request.AuthTimeout = 3600;
                    // Initialize a client.
                    DefaultAcsClient client = InitVodClient();
                    // Initiate the request and display the response.
                    GetPlayInfoResponse response = client.GetAcsResponse(request);
                    Console.WriteLine("RequestId = " + response.RequestId);
                    Console.WriteLine("VideoBase.Title = " + response.VideoBase.Title);
                    List<GetPlayInfoResponse.GetPlayInfo_PlayInfo> playInfoList = response.PlayInfoList;
                    foreach (var playInfo in response.PlayInfoList)
                    {
                        Console.WriteLine("PlayInfoList.PlayURL = " + playInfo.PlayURL);
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



Query a playback credential {#h2--div-id-getvideoplayauth-div-3}
----------------------------------------------------------------

You can call the GetVideoPlayAuth operation to query a playback credential.
For more information about the request and response parameters of this operation, see [GetVideoPlayAuth](/intl.en-US/API Reference/Audio and video playback/GetVideoPlayAuth.md). Example: 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Profile;
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
                    GetVideoPlayAuthRequest request = new GetVideoPlayAuthRequest();
                    request.VideoId = "<your VideoId>";
                    //request.AuthInfoTimeout = 3000;
                    // Initialize a client.
                    DefaultAcsClient client = InitVodClient();
                    // Initiate the request and display the response.
                    GetVideoPlayAuthResponse response = client.GetAcsResponse(request);
                    Console.WriteLine("RequestId = " + response.RequestId);
                    Console.WriteLine("VideoMeta.Title = " + response.VideoMeta.Title);
                    Console.WriteLine("PlayAuth = " + response.PlayAuth);
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



Video watermark 
====================================

This topic provides examples on how to use the API operations of the video watermark module. The API operations are encapsulated in ApsaraVideo VOD SDK for .NET. You can call the API operations to create, modify, delete, and query watermarks. You can also specify a watermark as the default one.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/.NET SDK/Initialization.md).

Create a watermark {#h2--div-id-addwatermark-div-2}
---------------------------------------------------

You can call the AddWatermark operation to create a watermark.

For more information about the request and response parameters of this operation, see [AddWatermark](/intl.en-US/API Reference/Media processing/Video Watermark/AddWatermark.md). Example:
**Note**

* For more information about how to obtain the upload URL and credential, see [CreateUploadAttachedMedia](/intl.en-US/API Reference/Media upload/CreateUploadAttachedMedia.md).

  

* For more information about how to upload a watermark file to an Object Storage Service (OSS) bucket, see [Upload OSS objects](/intl.en-US/API Reference/Media upload/Upload OSS objects.md).

  




    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.vod.Model.V20170321;
    using Newtonsoft.Json.Linq;
    
    namespace Aliyun.Acs.vod.Sdk.AddWatermark
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
                    AddWatermarkResponse response = AddWatermark(client);
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
            /// Create a watermark.
            /// </summary>
            /// <returns>The watermark.</returns>
            /// <param name="client">Client.</param>
            public static AddWatermarkResponse AddWatermark(DefaultAcsClient client)
            {
                // Create a request.
                AddWatermarkRequest request = new AddWatermarkRequest();
                // The name of the watermark.
                request.Name = "addwatermark";
                // If you want to create an image watermark, you must specify the URL of the watermark file. The OSS bucket that stores the watermark file must reside in the same region as the region where the video is stored. For example, if a video is stored in the China (Shanghai) region, it can use only a watermark file that is stored in the same region.
                request.FileUrl = "http://192.168.0.0/16/watermark/test.png";
    
                // The position configurations of an image watermark.
                request.WatermarkConfig = BuildImageWatermarkConfig();
    
                // The position configurations of a text watermark.
                request.WatermarkConfig = BuildTextWatermarkConfig();
    
                // The type of the watermark. Set the value to Text for text watermarks and Image for image watermarks.
                request.Type = "Image";
    
                return client.GetAcsResponse(request);
            }
    
            /// <summary>
            /// Build the parameters of an image watermark. Configure the parameters as required.
            /// </summary>
            /// <returns>The image watermark config.</returns>
            public static string BuildImageWatermarkConfig()
            {
                JObject watermarkConfig = new JObject();
                // The horizontal offset of the watermark on the output video.
                watermarkConfig.Add("Dx", "8");
                // The vertical offset of the watermark on the output video.
                watermarkConfig.Add("Dy", "8");
                // The width of the watermark on the output video.
                watermarkConfig.Add("Width", "55");
                // The height of the watermark on the output video.
                watermarkConfig.Add("Height", "55");
                // The approximate position of the watermark relative to the output video. The watermark can be in the upper-left corner, upper-right corner, lower-left corner, or lower-right corner.
                watermarkConfig.Add("ReferPos", "BottomRight");
    
                // The timeline of the watermark display. You can specify the start time and duration for the watermark display.
                JObject timeline = new JObject();
                // The start time for the watermark display.
                timeline.Add("Start", "2");
                // The duration for the watermark display.
                timeline.Add("Duration", "ToEND");
    
                watermarkConfig.Add("Timeline", timeline);
    
                return watermarkConfig.ToString();
            }
    
            /// <summary>
            /// Build the parameters of a text watermark. Configure the parameters as required.
            /// </summary>
            /// <returns>The text watermark config.</returns>
            public static string BuildTextWatermarkConfig()
            {
                JObject watermarkConfig = new JObject();
                // The text to use as the watermark.
                watermarkConfig.Add("Content", "testwatermark");
                // The font to use for the watermark.
                watermarkConfig.Add("FontName", "SimSun");
                // The font size to use for the watermark.
                watermarkConfig.Add("FontSize", 25);
                // The font color to use for the watermark. You can specify a color name or RGB color code, such as #000000.
                watermarkConfig.Add("FontColor", "Black");
                // The transparency to use for the watermark.
                watermarkConfig.Add("FontAlpha", "0.2");
                // The stroke color to use for the watermark. You can specify a color name or RGB color code, such as #ffffff.
                watermarkConfig.Add("BorderColor", "White");
                // The stroke width to use for the watermark.
                watermarkConfig.Add("BorderWidth", 1);
                // The distance between the upper-left vertex of the watermark and the upper edge of the output video.
                watermarkConfig.Add("Top", 20);
                // The distance between the upper-left vertex of the watermark and the left edge of the output video.
                watermarkConfig.Add("Left", 15);
    
                return watermarkConfig.ToString();
            }
        }
    }



Modify a watermark {#h2--div-id-updatewatermark-div-3}
------------------------------------------------------

You can call the UpdateWatermark operation to modify a watermark.
For more information about the request and response parameters of this operation, see [UpdateWatermark](/intl.en-US/API Reference/Media processing/Video Watermark/UpdateWatermark.md). Example: {#h2--div-id-updatewatermark-div-3}
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.vod.Model.V20170321;
    using Newtonsoft.Json.Linq;
    
    namespace Aliyun.Acs.vod.Sdk.UpdateWatermark
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
                    UpdateWatermarkResponse response = UpdateWatermark(client);
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
            /// Modify a watermark.
            /// </summary>
            /// <returns>The watermark.</returns>
            /// <param name="client">Client.</param>
            public static UpdateWatermarkResponse UpdateWatermark(DefaultAcsClient client)
            {
                // Create a request.
                UpdateWatermarkRequest request = new UpdateWatermarkRequest();
                // The name of the watermark.
                request.Name = "updateWatermark";
                // The ID of the watermark for which you want to modify the configurations.
                request.WatermarkId = "421ddddd4f6e734a526fd2****";
    
                // The position configurations of an image watermark.
                request.WatermarkConfig = BuildImageWatermarkConfig();
    
                // The position configurations of a text watermark.
                // request.WatermarkConfig = BuildTextWatermarkConfig();
    
                return client.GetAcsResponse(request);
            }
    
            /// <summary>
            /// Build the parameters of an image watermark. Configure the parameters as required.
            /// </summary>
            /// <returns>The image watermark config.</returns>
            public static string BuildImageWatermarkConfig()
            {
                JObject watermarkConfig = new JObject();
                // The horizontal offset of the watermark on the output video.
                watermarkConfig.Add("Dx", "8");
                // The vertical offset of the watermark on the output video.
                watermarkConfig.Add("Dy", "8");
                // The width of the watermark on the output video.
                watermarkConfig.Add("Width", "55");
                // The height of the watermark on the output video.
                watermarkConfig.Add("Height", "55");
                // The approximate position of the watermark relative to the output video. The watermark can be in the upper-left corner, upper-right corner, lower-left corner, or lower-right corner.
                watermarkConfig.Add("ReferPos", "BottomRight");
    
                // The timeline of the watermark display. You can specify the start time and duration for the watermark display.
                JObject timeline = new JObject();
                // The start time for the watermark display.
                timeline.Add("Start", "2");
                // The duration for the watermark display.
                timeline.Add("Duration", "ToEND");
    
                watermarkConfig.Add("Timeline", timeline);
    
                return watermarkConfig.ToString();
            }
    
            /// <summary>
            /// Build the parameters of a text watermark. Configure the parameters as required.
            /// </summary>
            /// <returns>The text watermark config.</returns>
            public static string BuildTextWatermarkConfig()
            {
                JObject watermarkConfig = new JObject();
                // The text to use as the watermark.
                watermarkConfig.Add("Content", "testwatermark");
                // The font to use for the watermark.
                watermarkConfig.Add("FontName", "SimSun");
                // The font size to use for the watermark.
                watermarkConfig.Add("FontSize", 25);
                // The font color to use for the watermark. You can specify a color name or RGB color code, such as #000000.
                watermarkConfig.Add("FontColor", "Black");
                // The transparency to use for the watermark.
                watermarkConfig.Add("FontAlpha", "0.2");
                // The stroke color to use for the watermark. You can specify a color name or RGB color code, such as #ffffff.
                watermarkConfig.Add("BorderColor", "White");
                // The stroke width to use for the watermark.
                watermarkConfig.Add("BorderWidth", 1);
                // The distance between the upper-left vertex of the watermark and the upper edge of the output video.
                watermarkConfig.Add("Top", 20);
                // The distance between the upper-left vertex of the watermark and the left edge of the output video.
                watermarkConfig.Add("Left", 15);
    
                return watermarkConfig.ToString();
            }
        }
    }



Delete a watermark {#h2--div-id-deletewatermark-div-4}
------------------------------------------------------

You can call the DeleteWatermark operation to delete a watermark.
For more information about the request and response parameters of this operation, see [DeleteWatermark](/intl.en-US/API Reference/Media processing/Video Watermark/DeleteWatermark.md). Example: {#h2--div-id-deletewatermark-div-4}
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.vod.Sdk.DeleteWatermark
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
                    DeleteWatermarkResponse response = DeleteWatermark(client);
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
            /// Delete a watermark.
            /// </summary>
            /// <returns>The watermark response.</returns>
            /// <param name="client">Client.</param>
            public static DeleteWatermarkResponse DeleteWatermark(DefaultAcsClient client)
            {
                // Create a request.
                DeleteWatermarkRequest request = new DeleteWatermarkRequest();
                // The ID of the watermark.
                request.WatermarkId = "53f9d796fad9d7b862b2e****";
                return client.GetAcsResponse(request);
            }
        }
    }



Query watermarks {#h2--div-id-listwatermark-div-5}
--------------------------------------------------

You can call the ListWatermark operation to query watermarks.
For more information about the request and response parameters of this operation, see [ListWatermark](/intl.en-US/API Reference/Media processing/Video Watermark/ListWatermark.md). Example: {#h2--div-id-listwatermark-div-5}
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.vod.Sdk.ListWatermark
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
                    ListWatermarkResponse response = ListWatermark(client);
    
                    if (response.WatermarkInfos ! = null && response.WatermarkInfos.Count > 0)
                    {
                        foreach (ListWatermarkResponse.ListWatermark_WatermarkInfo watermarkInfo in response.WatermarkInfos) 
                        {
                            // The ID of the watermark.
                            Console.WriteLine("WatermarkId = " + watermarkInfo.WatermarkId);
                            // The position and effect configurations of the watermark.
                            Console.WriteLine("WatermarkConfig = " + watermarkInfo.WatermarkConfig);
                            // The URL of the watermark file. If you want to query text watermarks, leave this parameter empty.
                            Console.WriteLine("FileUrl = " + watermarkInfo.FileUrl);
                        }
                    }
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
            /// Query watermarks.
            /// </summary>
            /// <returns>The watermark list.</returns>
            /// <param name="client">Client.</param>
            public static ListWatermarkResponse ListWatermark(DefaultAcsClient client)
            {
                // Create a request.
                ListWatermarkRequest request = new ListWatermarkRequest();
    
                return client.GetAcsResponse(request);
            }
    
        }
    }



Query a watermark {#h2--div-id-getwatermark-div-6}
--------------------------------------------------

You can call the GetWatermark operation to query details about a watermark.
For more information about the request and response parameters of this operation, see [GetWatermark](/intl.en-US/API Reference/Media processing/Video Watermark/GetWatermark.md). Example: {#h2--div-id-getwatermark-div-6}
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.vod.Sdk.GetWatermark
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
                    GetWatermarkResponse response = GetWatermark(client);
                    if (response.WatermarkInfo ! = null)
                    {
                        // The ID of the watermark.
                        Console.WriteLine("WatermarkId = " + response.WatermarkInfo.WatermarkId);
                        // The position and effect configurations of the watermark.
                        Console.WriteLine("WatermarkConfig = " + response.WatermarkInfo.WatermarkConfig);
                        // The URL of the watermark file. If you want to query details about a text watermark, leave this parameter empty.
                        Console.WriteLine("FileUrl = " + response.WatermarkInfo.FileUrl);
                    }
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
            /// Query a watermark.
            /// </summary>
            /// <returns>The watermark.</returns>
            /// <param name="client">Client.</param>
            public static GetWatermarkResponse GetWatermark(DefaultAcsClient client)
            {
                // Create a request.
                GetWatermarkRequest request = new GetWatermarkRequest();
                // The ID of the watermark that you want to query.
                request.WatermarkId = "96d4f6e734a526fd2e442";
                return client.GetAcsResponse(request);
            }
        }
    }



Specify a watermark as the default one {#h2--div-id-setdefaultwatermark-div-7}
------------------------------------------------------------------------------

You can call the SetDefaultWatermark operation to specify a watermark as the default one.
For more information about the request and response parameters of this operation, see [SetDefaultWatermark](/intl.en-US/API Reference/Media processing/Video Watermark/SetDefaultWatermark.md). Example: {#h2--div-id-setdefaultwatermark-div-7}
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.vod.Sdk.SetDefaultWatermark
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
                    SetDefaultWatermarkResponse response = SetDefaultWatermark(client);
    
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
            /// Specify a watermark as the default one.
            /// </summary>
            /// <returns>The default watermark.</returns>
            /// <param name="client">Client.</param>
            public static SetDefaultWatermarkResponse SetDefaultWatermark(DefaultAcsClient client)
            {
                // Create a request.
                SetDefaultWatermarkRequest request = new SetDefaultWatermarkRequest();
                // The ID of the watermark that you want to specify as the default one.
                request.WatermarkId = "82105a29c6e96d4f6e****";
    
                return client.GetAcsResponse(request);
            }
        }
    }



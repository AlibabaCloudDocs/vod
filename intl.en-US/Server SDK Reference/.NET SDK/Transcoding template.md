Transcoding template 
=========================================

This topic provides examples on how to use the API operations of the transcoding template module. The API operations are encapsulated in ApsaraVideo VOD SDK for .NET. You can call the API operations to create, modify, delete, and query transcoding template groups. You can also specify a transcoding template group as the default one.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/.NET SDK/Initialization.md).

Create a transcoding template group {#h2--div-id-addtranscodetemplategroup-div-2}
---------------------------------------------------------------------------------

You can call the AddTranscodeTemplateGroup operation to create a transcoding template group.
For more information about the request and response parameters of this operation, see [AddTranscodeTemplateGroup](/intl.en-US/API Reference/Media processing/Transcoding template/AddTranscodeTemplateGroup.md). Example: 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.Core.Profile;
    using Aliyun.Acs.vod.Model.V20170321;
    using Newtonsoft.Json.Linq;
    
    namespace Aliyun.Acs.VoD.Sdk.AddTranscodeTemplateGroup
    {
        class MainClass
        {
            /// <summary>
            /// The entry point of the program, where the program control starts and ends.
            /// </summary>
            /// <param name="args">The command-line arguments.</param>
            public static void Main(string[] args)
            {
                try
                {
                    // Initialize a client.
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // Initiate the request and display the response.
                    AddTranscodeTemplateGroupResponse response = AddTranscodeTemplateGroup(client);
                    // List the request ID.
                    Console.WriteLine("RequestId = " + response.RequestId);
                    // List the transcoding template ID.
                    Console.WriteLine("TranscodeTemplateGroupId = " + response.TranscodeTemplateGroupId);
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
            /// Create a transcoding template group.
            /// </summary>
            /// <returns>Transcoding template group</returns>
            /// <param name="client">Client.</param>
            public static AddTranscodeTemplateGroupResponse AddTranscodeTemplateGroup(DefaultAcsClient client)
            {
                // Create a request.
                AddTranscodeTemplateGroupRequest request = new AddTranscodeTemplateGroupRequest();
                // Specify a name for the transcoding template group.
                request.Name = "grouptest";
                request.TranscodeTemplateList = BuildTranscodeTemplateList();
    
                // The returned results.
                return client.GetAcsResponse(request);
    
            }
    
            private static String BuildTranscodeTemplateList()
            {
                JArray transcodeTemplateList = new JArray();
    
                JObject transcodeTemplate = new JObject();
                // The configurations of video stream transcoding.
                JObject video = new JObject();
                video.Add("Width", 640);
                video.Add("Bitrate", 400);
                video.Add("Fps", "25");
                video.Add("Remove", false);
                video.Add("Codec", "H.264");
                video.Add("Gop", 250);
                transcodeTemplate.Add("Video", video);
    
                // The configurations of audio stream transcoding.
                JObject audio = new JObject();
                audio.Add("Codec", "AAC");
                audio.Add("Bitrate", "64");
                audio.Add("Channels", "2");
                audio.Add("Samplerate", "32000");
                transcodeTemplate.Add("Audio", audio);
    
                // The container for encapsulation.
                JObject container = new JObject();
                container.Add("Format", "mp4");
                transcodeTemplate.Add("Container", container);
    
                // The configurations of conditional transcoding.
                JObject transconfig = new JObject();
                transconfig.Add("IsCheckReso", false);
                transconfig.Add("IsCheckResoFail", false);
                transconfig.Add("IsCheckVideoBitrate", false);
                transconfig.Add("IsCheckVideoBitrateFail", false);
                transconfig.Add("IsCheckAudioBitrate", false);
                transconfig.Add("IsCheckAudioBitrateFail", false);
                transcodeTemplate.Add("TransConfig", transconfig);
    
                // The configurations of encryption, which is supported only for M3U8 videos.
                //JObject encryptSetting = new JObject();
                //encryptSetting.Add("EncryptType", "Private");
                //transcodeTemplate.Add("EncryptSetting", encryptSetting);
    
                // The definition.
                transcodeTemplate.Add("Definition", "LD");
                // The name of the template.
                transcodeTemplate.Add("TemplateName", "testtemplate");
                // The IDs of associated watermarks.
                //JArray watermarkIdList = new JArray();
                //watermarkIdList.Add("263261bdc1ff65782f8995c6dd22****");
                // USER_DEFAULT_WATERMARK indicates the ID of the default watermark.
                //watermarkIdList.Add("USER_DEFAULT_WATERMARK");
                //transcodeTemplate.Add("WatermarkIds", watermarkIdList);
    
                transcodeTemplateList.Add(transcodeTemplate);
                return transcodeTemplateList.ToString();
            }
        }
    }



Modify a transcoding template group {#h2--div-id-updatetranscodetemplategroup-div-3}
------------------------------------------------------------------------------------

You can call the UpdateTranscodeTemplateGroup operation to modify a transcoding template group.
For more information about the request and response parameters of this operation, see [UpdateTranscodeTemplateGroup](/intl.en-US/API Reference/Media processing/Transcoding template/UpdateTranscodeTemplateGroup.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.Core.Profile;
    using Aliyun.Acs.vod.Model.V20170321;
    using Newtonsoft.Json.Linq;
    
    namespace Aliyun.Acs.VoD.Sdk.UpdateTranscodeTemplateGroup
    {
        class MainClass
        {
            /// <summary>
            /// The entry point of the program, where the program control starts and ends.
            /// </summary>
            /// <param name="args">The command-line arguments.</param>
            public static void Main(string[] args)
            {
                try
                {
                    // Initialize a client.
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // Initiate the request and display the response.
                    UpdateTranscodeTemplateGroupResponse response = UpdateTranscodeTemplateGroup(client);
                    // List the request ID.
                    Console.WriteLine("RequestId = " + response.RequestId);
                    // List the transcoding template ID.
                    Console.WriteLine("TranscodeTemplateGroupId = " + response.TranscodeTemplateGroupId);
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
            /// Modify a transcoding template group.
            /// </summary>
            /// <returns>Transcoding template group</returns>
            /// <param name="client">Client.</param>
            public static UpdateTranscodeTemplateGroupResponse UpdateTranscodeTemplateGroup(DefaultAcsClient client)
            {
                // Create a request.
                UpdateTranscodeTemplateGroupRequest request = new UpdateTranscodeTemplateGroupRequest();
                request.Name = "newgrouptest";
                // Specify the ID of the transcoding template group.
                request.TranscodeTemplateGroupId = "4c71a339fecec0152b4fa6f452****";
    
                request.TranscodeTemplateList = BuildTranscodeTemplateList();
    
                // The returned results.
                return client.GetAcsResponse(request);
    
            }
    
            private static String BuildTranscodeTemplateList()
            {
                JArray transcodeTemplateList = new JArray();
    
                JObject transcodeTemplate = new JObject();
                // The configurations of video stream transcoding.
                JObject video = new JObject();
                video.Add("Width", 640);
                video.Add("Bitrate", 400);
                video.Add("Fps", "25");
                video.Add("Remove", false);
                video.Add("Codec", "H.264");
                video.Add("Gop", 250);
                transcodeTemplate.Add("Video", video);
    
                // The configurations of audio stream transcoding.
                JObject audio = new JObject();
                audio.Add("Codec", "AAC");
                audio.Add("Bitrate", "64");
                audio.Add("Channels", "2");
                audio.Add("Samplerate", "32000");
                transcodeTemplate.Add("Audio", audio);
    
                // The container for encapsulation.
                JObject container = new JObject();
                container.Add("Format", "mp4");
                transcodeTemplate.Add("Container", container);
    
                // The configurations of conditional transcoding.
                JObject transconfig = new JObject();
                transconfig.Add("IsCheckReso", false);
                transconfig.Add("IsCheckResoFail", false);
                transconfig.Add("IsCheckVideoBitrate", false);
                transconfig.Add("IsCheckVideoBitrateFail", false);
                transconfig.Add("IsCheckAudioBitrate", false);
                transconfig.Add("IsCheckAudioBitrateFail", false);
                transcodeTemplate.Add("TransConfig", transconfig);
    
                // The configurations of encryption, which is supported only for M3U8 videos.
                //JObject encryptSetting = new JObject();
                //encryptSetting.Add("EncryptType", "Private");
                //transcodeTemplate.Add("EncryptSetting", encryptSetting);
    
                // The definition.
                transcodeTemplate.Add("Definition", "SD");
                // The name of the template.
                transcodeTemplate.Add("TemplateName", "testtemplate");
                // The ID of the transcoding template.
                transcodeTemplate.Add("TranscodeTemplateId", "85c2b18ac08fda33e8f6d9c56****");
                // The IDs of associated watermarks.
                //JArray watermarkIdList = new JArray();
                //watermarkIdList.Add("263261bdc1ff65782f8995c6dd22****");
                // USER_DEFAULT_WATERMARK indicates the ID of the default watermark.
                //watermarkIdList.Add("USER_DEFAULT_WATERMARK");
                //transcodeTemplate.Add("WatermarkIds", watermarkIdList);
    
                transcodeTemplateList.Add(transcodeTemplate);
                return transcodeTemplateList.ToString();
            }
        }
    }



Query transcoding template groups {#h2--div-id-listtranscodetemplategroup-div-4}
--------------------------------------------------------------------------------

You can call the ListTranscodeTemplateGroup operation to query transcoding template groups.
For more information about the request and response parameters of this operation, see [ListTranscodeTemplateGroup](/intl.en-US/API Reference/Media processing/Transcoding template/ListTranscodeTemplateGroup.md). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.Core.Profile;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.VoD.Sdk.ListTranscodeTemplateGroup
    {
        class MainClass
        {
            /// <summary>
            /// The entry point of the program, where the program control starts and ends.
            /// </summary>
            /// <param name="args">The command-line arguments.</param>
            public static void Main(string[] args)
            {
                try
                {
                    // Initialize a client.
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // Initiate the request and display the response.
                    ListTranscodeTemplateGroupResponse response = ListTranscodeTemplateGroup(client);
                    // List the request ID.
                    Console.WriteLine("RequestId = " + response.RequestId);
                    // List the information of a transcoding template group.
                    if (response.TranscodeTemplateGroupList ! = null && response.TranscodeTemplateGroupList.Count > 0)
                    {
                        foreach (ListTranscodeTemplateGroupResponse.ListTranscodeTemplateGroup_TranscodeTemplateGroup templateGroup in response.TranscodeTemplateGroupList)
                        {
                            Console.WriteLine("Name = " + templateGroup.Name);
                            Console.WriteLine("TranscodeTemplateGroupId = " + templateGroup.TranscodeTemplateGroupId);
                            Console.WriteLine("IsDefault = " + templateGroup.IsDefault);
                            Console.WriteLine("CreationTime = " + templateGroup.CreationTime);
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
    
            /// <summary>
            /// Query transcoding template groups.
            /// </summary>
            /// <returns>Transcoding template groups</returns>
            /// <param name="client">Client.</param>
            public static ListTranscodeTemplateGroupResponse ListTranscodeTemplateGroup(DefaultAcsClient client)
            {
                // Create a request.
                ListTranscodeTemplateGroupRequest request = new ListTranscodeTemplateGroupRequest();
                // The returned results.
                return client.GetAcsResponse(request);
    
            }
        }
    }



Query a transcoding template group {#h2--div-id-gettranscodetemplategroup-div-5}
--------------------------------------------------------------------------------

You can call the GetTranscodeTemplateGroup operation to query details about a transcoding template group.
For more information about the request and response parameters of this operation, see [GetTranscodeTemplateGroup](/intl.en-US/API Reference/Media processing/Transcoding template/GetTranscodeTemplateGroup.md). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.Core.Profile;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.VoD.Sdk.GetTranscodeTemplateGroup
    {
        class MainClass
        {
            /// <summary>
            /// The entry point of the program, where the program control starts and ends.
            /// </summary>
            /// <param name="args">The command-line arguments.</param>
            public static void Main(string[] args)
            {
                try
                {
                    // Initialize a client.
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // Initiate the request and display the response.
                    GetTranscodeTemplateGroupResponse response = GetTranscodeTemplateGroup(client);
                    // List the request ID.
                    Console.WriteLine("RequestId = " + response.RequestId);
                    // List the information of a transcoding template group.
                    Console.WriteLine("Name = " + response.TranscodeTemplateGroup.Name);
                    Console.WriteLine("TranscodeTemplateGroupId = " + response.TranscodeTemplateGroup.TranscodeTemplateGroupId);
                    Console.WriteLine("IsDefault = " + response.TranscodeTemplateGroup.IsDefault);
                    Console.WriteLine("CreationTime = " + response.TranscodeTemplateGroup.CreationTime);
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
            /// Query a transcoding template group.
            /// </summary>
            /// <returns>Transcoding template group</returns>
            /// <param name="client">Client.</param>
            public static GetTranscodeTemplateGroupResponse GetTranscodeTemplateGroup(DefaultAcsClient client)
            {
                // Create a request.
                GetTranscodeTemplateGroupRequest request = new GetTranscodeTemplateGroupRequest();
                request.TranscodeTemplateGroupId = "94bcd9366be0df7ffba3b6f7b715****";
                // The returned results.
                return client.GetAcsResponse(request);
            }
        }
    }



Specify a transcoding template group as the default one {#h2--div-id-setdefaulttranscodetemplategroup-div-6}
------------------------------------------------------------------------------------------------------------

You can call the SetDefaultTranscodeTemplateGroup operation to specify a transcoding template group as the default one.
For more information about the request and response parameters of this operation, see [SetDefaultTranscodeTemplateGroup](/intl.en-US/API Reference/Media processing/Transcoding template/SetDefaultTranscodeTemplateGroup.md). Example: 
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.Core.Profile;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.VoD.Sdk.SetDefaultTranscodeTemplateGroup
    {
        class MainClass
        {
            /// <summary>
            /// The entry point of the program, where the program control starts and ends.
            /// </summary>
            /// <param name="args">The command-line arguments.</param>
            public static void Main(string[] args)
            {
                try
                {
                    // Initialize a client.
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // Initiate the request and display the response.
                    SetDefaultTranscodeTemplateGroupResponse response = SetDefaultTranscodeTemplateGroup(client);
                    // List the request ID.
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
            /// Specify a transcoding template group as the default one.
            /// </summary>
            /// <returns>Default transcoding template group</returns>
            /// <param name="client">Client.</param>
            public static SetDefaultTranscodeTemplateGroupResponse SetDefaultTranscodeTemplateGroup(DefaultAcsClient client)
            {
                // Create a request.
                SetDefaultTranscodeTemplateGroupRequest request = new SetDefaultTranscodeTemplateGroupRequest();
                // Specify the template ID.
                request.TranscodeTemplateGroupId = "dc063078c1d845139e2a5bd8ff85****";
                // The returned results.
                return client.GetAcsResponse(request);
            }
        }
    }



Delete a transcoding template group {#h2--div-id-deletetranscodetemplategroup-div-7}
------------------------------------------------------------------------------------

You can call the DeleteTranscodeTemplateGroup operation to delete a transcoding template group.
For more information about the request and response parameters of this operation, see [DeleteTranscodeTemplateGroup](/intl.en-US/API Reference/Media processing/Transcoding template/DeleteTranscodeTemplateGroup.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.Core.Profile;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.VoD.Sdk.DeleteTranscodeTemplateGroup
    {
        class MainClass
        {
            /// <summary>
            /// The entry point of the program, where the program control starts and ends.
            /// </summary>
            /// <param name="args">The command-line arguments.</param>
            public static void Main(string[] args)
            {
                try
                {
                    // Initialize a client.
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // Initiate the request and display the response.
                    DeleteTranscodeTemplateGroupResponse response = DeleteTranscodeTemplateGroup(client);
                    // List the request ID.
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
            /// Delete a transcoding template group.
            /// </summary>
            /// <param name="client">Client.</param>
            public static DeleteTranscodeTemplateGroupResponse DeleteTranscodeTemplateGroup(DefaultAcsClient client)
            {
                // Create a request.
                DeleteTranscodeTemplateGroupRequest request = new DeleteTranscodeTemplateGroupRequest();
                request.TranscodeTemplateGroupId = "dc063078c1d845139e2a5bd8ff65****";
                // The returned results.
                return client.GetAcsResponse(request);
    
            }
        }
    }



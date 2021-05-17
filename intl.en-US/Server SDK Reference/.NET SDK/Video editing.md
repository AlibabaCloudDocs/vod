Video editing 
==================================

This topic provides examples on how to use the API operations of the video editing module. The API operations are encapsulated in ApsaraVideo VOD SDK for .NET. You can call the API operations to create, modify, and delete online editing projects. You can also query details about an online editing project, configure materials for an online project, and create a video assembly task.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/.NET SDK/Initialization.md).

Create a video assembly task based on a timeline {#h2--div-id-produceeditingprojectvideo-div-2}
-----------------------------------------------------------------------------------------------

You can call the ProduceEditingProjectVideo operation to create a video assembly task based on a timeline.

The timeline method is most commonly used to assemble videos. For more information about the request and response parameters of this operation, see [ProduceEditingProjectVideo](/intl.en-US/API Reference/Online editing/ProduceEditingProjectVideo.md). Example:
**Note**

For more examples on how to assemble videos based on timelines, see [Video assembly](/intl.en-US/Developer Guide/Online editing/Overview.md).

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.vod.Model.V20170321;
    using Newtonsoft.Json.Linq;
    
    namespace Aliyun.Acs.vod.Sdk.ProduceEditingProjectVideo
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
                    // Create a request.
                    ProduceEditingProjectVideoRequest request = new ProduceEditingProjectVideoRequest();
                    // Build a timeline to assemble videos.
                    request.Timeline = BuildTimeline();
                    // Configure metadata.
                    request.MediaMetadata = BuildMediaMetadata();
                    // Build project configurations.
                    request.ProduceConfig = BuildProduceConfig();
                    // Initialize a client.
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // Initiate the request and display the response.
                    ProduceEditingProjectVideoResponse response = client.GetAcsResponse(request);
                    Console.WriteLine("RequestId = " + response.RequestId);
                    Console.WriteLine("MediaId = " + response.MediaId);
                    Console.WriteLine("ProjectId = " + response.ProjectId);
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
            /// Builds the timeline.
            /// </summary>
            /// <returns>The timeline.</returns>
            private static string BuildTimeline() {
                JObject timeLine = new JObject();
                // Video Track
                JArray videoTracks = new JArray();
                JObject videoTrack = new JObject();
    
                // Video Track Clips
                JArray videoTrackClips = new JArray();
                JObject videoTrackClip1 = new JObject();
                videoTrackClip1.Add("MediaId", "11119b4d7cf14dc7b83b0e801cbe1ce6");
                videoTrackClips.Add(videoTrackClip1);
    
                JObject videoTrackClip2 = new JObject();
                videoTrackClip2.Add("MediaId", "22229b4d7cf14dc7b83b0e801cbe1ce6");
                videoTrackClips.Add(videoTrackClip2);
                videoTrack.Add("VideoTrackClips", videoTrackClips);
                videoTracks.Add(videoTrack);
    
                timeLine.Add("VideoTracks", videoTracks);
    
                return timeLine.ToString();
            }
    
            /// <summary>
            /// Builds the media metadata.
            /// </summary>
            /// <returns>The media metadata.</returns>
            private static string BuildMediaMetadata() {
                JObject mediaMetadata = new JObject();
                // Produce Media Title
                mediaMetadata.Add("Title", "Title");
                // Produce Media Description
                mediaMetadata.Add("Description", "Description");
                // Produce Media UserDefined Cover URL
                mediaMetadata.Add("CoverURL", "http://test.testvod123.com/media/cover/mediaid.jpg");
                // Produce Media Category ID
                mediaMetadata.Add("CateId", null);
                // Produce Media Category Name
                mediaMetadata.Add("Tags", "Tag1,Tag2,Test");
    
                return mediaMetadata.ToString();
            }
    
            /// <summary>
            /// Builds the produce config.
            /// </summary>
            /// <returns>The produce config.</returns>
            private static string BuildProduceConfig() {
                JObject produceConfig = new JObject();
                /**
                 * The produce process can generate media mezzanine file. You can use the mezzanine file to transcode other media files. This transcoding process is similar to that after file upload is finished. This field describe the Transocde TemplateGroup ID after produce mezzanine finished.
                 * 1. Not required 
                 * 2. Use default transcode template group id when empty
                **/
                produceConfig.Add("TemplateGroupId", null);
                return produceConfig.ToString();
            }
        }
    }



Create a video assembly task based on an online editing project {#h2--div-id-produceeditingprojectvideoprojectid-div-3}
-----------------------------------------------------------------------------------------------------------------------

You can call the ProduceEditingProjectVideo operation to create a video assembly task based on an online editing project.

If you have high requirements for online editing and management, we recommend that you use this method. For more information about the request and response parameters of this operation, see [ProduceEditingProjectVideo](/intl.en-US/API Reference/Online editing/ProduceEditingProjectVideo.md). Example:

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.Core.Profile;
    using Aliyun.Acs.vod.Model.V20170321;
    using Newtonsoft.Json.Linq;
    
    namespace Aliyun.Acs.vod.Sdk.ProduceEditingProjectVideoProjectId
    {
        class MainClass
        {
            /// <summary>
            /// The entry point of the program, where the program control starts and ends.
            /// </summary>
            /// <param name="args">The command-line arguments.</param>
            public static void Main(string[] args)
            {
                ProduceEditingProjectVideoResponse response = null;
                try
                {
                    // Create a request.
                    ProduceEditingProjectVideoRequest request = new ProduceEditingProjectVideoRequest();
                    // Build a timeline to assemble videos.
                    request.ProjectId = "ProjectId";
                    // Configure metadata.
                    request.MediaMetadata = BuildMediaMetadata();
                    // Build project configurations.
                    request.ProduceConfig = BuildProduceConfig();
                    // Initialize a client.
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // Initiate the request and display the response.
                    response = client.GetAcsResponse(request);
                    Console.WriteLine("RequestId = " + response.RequestId);
                    Console.WriteLine("MediaId = " + response.MediaId);
                    Console.WriteLine("ProjectId = " + response.ProjectId);
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
            /// Builds the media metadata.
            /// </summary>
            /// <returns>The media metadata.</returns>
            private static string BuildMediaMetadata()
            {
                JObject mediaMetadata = new JObject();
    
                // Produce Media Title
                mediaMetadata.Add("Title", "Title");
                // Produce Media Description
                mediaMetadata.Add("Description", "Description");
                // Produce Media UserDefined Cover URL
                mediaMetadata.Add("CoverURL", "http://test.testvod123.com/media/cover/mediaid.jpg");
                // Produce Media Category ID
                mediaMetadata.Add("CateId", null);
                // Produce Media Category Name
                mediaMetadata.Add("Tags", "Tag1,Tag2,Test");
    
                return mediaMetadata.ToString();
            }
    
            /// <summary>
            /// Builds the produce config.
            /// </summary>
            /// <returns>The produce config.</returns>
            private static string BuildProduceConfig()
            {
                JObject produceConfig = new JObject();
                /**
                 * The produce process can generate media mezzanine file. You can use the mezzanine file to transcode other media files. This transcoding process is similar to that after file upload is finished. This field describe the Transocde TemplateGroup ID after produce mezzanine finished.
                 * 1. Not required 
                 * 2. Use default transcode template group id when empty
                **/
                produceConfig.Add("TemplateGroupId", null);
    
                return produceConfig.ToString();
            }
        }
    }



Create an online editing project {#h2--div-id-addeditingproject-div-4}
----------------------------------------------------------------------

You can call the AddEditingProject operation to create an online editing project.
For more information about the request and response parameters of this operation, see [AddEditingProject](/intl.en-US/API Reference/Online editing/Project management for online editing/AddEditingProject.md). Example: 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.vod.Sdk.AddEditingProject
    {
        class MainClass
        {
            public static void Main(string[] args)
            {
                try
                {
                    // Create a request.
                    AddEditingProjectRequest request = new AddEditingProjectRequest();
                    request.Description = "new Description";
                    request.Title = "new Title";
                    // Initialize a client.
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // Initiate the request and display the response.
                    AddEditingProjectResponse response = client.GetAcsResponse(request);
                    Console.WriteLine("RequestId = " + response.RequestId);
                    if (response.Project ! = null) {
                        Console.WriteLine("ProjectId = " + response.Project.ProjectId);
                        Console.WriteLine("Title = " + response.Project.Title);
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



Modify an online editing project {#h2--div-id-updateeditingproject-div-5}
-------------------------------------------------------------------------

You can call the UpdateEditingProject operation to modify an online editing project.
For more information about the request and response parameters of this operation, see [UpdateEditingProject](/intl.en-US/API Reference/Online editing/Project management for online editing/UpdateEditingProject.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.vod.Sdk.UpdateEditingProject
    {
        class MainClass
        {
            public static void Main(string[] args)
            {
                try
                {
                    // Create a request.
                    UpdateEditingProjectRequest request = new UpdateEditingProjectRequest();
                    request.ProjectId = "YourProjectId";
                    request.Title = "new Title";
                    // Initialize a client.
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // Initiate the request and display the response.
                    UpdateEditingProjectResponse response = client.GetAcsResponse(request);
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
        }
    }



Delete an online editing project {#h2--div-id-deleteeditingproject-div-6}
-------------------------------------------------------------------------

You can call the DeleteEditingProject operation to delete an online editing project.
For more information about the request and response parameters of this operation, see [DeleteEditingProject](/intl.en-US/API Reference/Online editing/Project management for online editing/DeleteEditingProject.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.Core.Profile;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.vod.Sdk.DeleteEditingProject
    {
        class MainClass
        {
            public static void Main(string[] args)
            {
                try
                {
                    // Create a request.
                    DeleteEditingProjectRequest request = new DeleteEditingProjectRequest();
                    // Use comma to split Multi Editing Project IDs
                    request.ProjectIds = "projectid1,projectid2";
                    // Initialize a client.
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // Initiate the request and display the response.
                    DeleteEditingProjectResponse response = client.GetAcsResponse(request);
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
        }
    }



Query an online editing project {#h2--div-id-geteditingproject-div-7}
---------------------------------------------------------------------

You can call the GetEditingProject operation to query details about an online editing project.
For more information about the request and response parameters of this operation, see [GetEditingProject](/intl.en-US/API Reference/Online editing/Project management for online editing/GetEditingProject.md). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.vod.Sdk.GetEditingProject
    {
        class MainClass
        {
            public static void Main(string[] args)
            {
                try
                {
                    // Create a request.
                    GetEditingProjectRequest request = new GetEditingProjectRequest();
                    request.ProjectId = "projectid";
                    // Initialize a client.
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // Initiate the request and display the response.
                    GetEditingProjectResponse response = client.GetAcsResponse(request);
                    Console.WriteLine("RequestId = " + response.RequestId);
                    if (response.Project ! = null)
                    {
                        Console.WriteLine("ProjectId = " + response.Project.ProjectId);
                        Console.WriteLine("Title = " + response.Project.Title);
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



Search for online editing projects {#h2--div-id-searcheditingproject-div-8}
---------------------------------------------------------------------------

You can call the SearchEditingProject operation to search for online editing projects.
For more information about the request and response parameters of this operation, see [SearchEditingProject](/intl.en-US/API Reference/Online editing/Project management for online editing/SearchEditingProject.md). Example: 
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.vod.Sdk.SearchEditingProject
    {
        class MainClass
        {
            public static void Main(string[] args)
            {
                try
                {
                    // Create a request.
                    SearchEditingProjectRequest request = new SearchEditingProjectRequest();
                    request.Title = "Title Keywords";
                    request.StartTime = "2017-01-11T12:00:00Z";
                    request.EndTime = "2017-01-12T12:00:00Z";
                    request.PageSize = 10;
                    request.PageNo = 1;
                    // Initialize a client.
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // Initiate the request and display the response.
                    SearchEditingProjectResponse response = client.GetAcsResponse(request);
                    // List the request ID.
                    Console.WriteLine("RequestId = " + response.RequestId);
                    if (response.ProjectList ! = null && response.ProjectList.Count > 0)
                    {
                        foreach (var project in response.ProjectList)
                        {
                            Console.WriteLine("ProjectId = " + project.ProjectId);
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



Configure materials for an online editing project {#h2--div-id-seteditingprojectmaterials-div-9}
------------------------------------------------------------------------------------------------

You can call the SetEditingProjectMaterials operation to configure materials for an online editing project.
For more information about the request and response parameters of this operation, see [SetEditingProjectMaterials](/intl.en-US/API Reference/Online editing/Project management for online editing/SetEditingProjectMaterials.md). Example: 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.vod.Sdk.SetEditingProjectMaterials
    {
        class MainClass
        {
            public static void Main(string[] args)
            {
                try
                {
                    // Create a request.
                    SetEditingProjectMaterialsRequest request = new SetEditingProjectMaterialsRequest();
                    // Editing Project ID
                    request.ProjectId = "projectid";
                    // Set Editing Project Material IDs, use comma to split
                    request.MaterialIds = "materialId1,materialId2";
    
                    // Initialize a client.
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // Initiate the request and display the response.
                    SetEditingProjectMaterialsResponse response = client.GetAcsResponse(request);
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
        }
    }



Query the materials of an online editing project {#h2--div-id-geteditingprojectmaterials-div-10}
------------------------------------------------------------------------------------------------

You can call the GetEditingProjectMaterials operation to query the materials of an online editing project.
For more information about the request and response parameters of this operation, see [GetEditingProjectMaterials](/intl.en-US/API Reference/Online editing/Project management for online editing/GetEditingProjectMaterials.md). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.vod.Model.V20170321;
    
    Aliyun.Acs.vod.Sdk.GetEditingProjectMaterials
    {
        class MainClass
        {
            public static void Main(string[] args)
            {
                try
                {
                    // Create a request.
                    GetEditingProjectMaterialsRequest request = new GetEditingProjectMaterialsRequest();
                    request.ProjectId = "projectid";
                    request.Type = "video";
    
                    // Initialize a client.
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // Initiate the request and display the response.
                    GetEditingProjectMaterialsResponse response = client.GetAcsResponse(request);
                    Console.WriteLine("RequestId = " + response.RequestId);
                    if (response.MaterialList ! = null && response.MaterialList.Count > 0)
                    {
                        foreach (var material in response.MaterialList) 
                        {
                            Console.WriteLine("MaterialId = " + material.MaterialId);
                            Console.WriteLine("Title = " + material.Title);
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



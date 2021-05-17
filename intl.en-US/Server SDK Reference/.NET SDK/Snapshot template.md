Snapshot template 
======================================

This topic provides examples on how to use the API operations of the snapshot template module. The API operations are encapsulated in ApsaraVideo VOD SDK for .NET. You can call the API operations to create, delete, modify, and query snapshot templates.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/.NET SDK/Initialization.md).

Create a snapshot template {#h2--div-id-addvodtemplate-div-2}
-------------------------------------------------------------

You can call the AddVodTemplate operation to create a snapshot template.
For more information about the request and response parameters of this operation, see [AddVodTemplate](/intl.en-US/API Reference/Media processing/Snapshot template/AddVodTemplate.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.Core.Profile;
    using Aliyun.Acs.vod.Model.V20170321;
    using Newtonsoft.Json.Linq;
    
    namespace Aliyun.Acs.vod.Sdk.AddVodTemplate
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
                    AddVodTemplateResponse response = AddVodTemplate(client);
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
            /// Create a snapshot template.
            /// </summary>
            /// <returns>The vod template.</returns>
            /// <param name="client">Client.</param>
            public static AddVodTemplateResponse AddVodTemplate(DefaultAcsClient client)
            {
                // Create a request.
                AddVodTemplateRequest request = new AddVodTemplateRequest();
                // Specify the template name.
                request.Name = "addVodTemplate";
                // Specify the template type. Set the value to Snapshot.
                request.TemplateType = "Snapshot";
                // Build template configurations.
                request.TemplateConfig = BuildSnapshotTemplateConfig();
    
                return client.GetAcsResponse(request);
            }
    
            /// <summary>
            /// Build the parameters of a snapshot template. Configure the parameters as required.
            /// (The following sample code shows the complete configurations of image sprites.)
            /// </summary>
            /// <returns>Configurations of the snapshot template</returns>
            public static string BuildSnapshotTemplateConfig()
            {
                JObject templateConfig = new JObject();
                JObject snapshotConfig = new JObject();
                snapshotConfig.Add("Count", "50");
                snapshotConfig.Add("Interval", "1");
                snapshotConfig.Add("SpecifiedOffsetTime", "0");
                snapshotConfig.Add("Width", "200");
                snapshotConfig.Add("Height", "200");
                // The configurations of common snapshots. The configurations are also used by image sprites.
                templateConfig.Add("SnapshotConfig", snapshotConfig);
                // The configurations of image sprites. The configurations must be based on those of common snapshots.
                JObject spriteSnapshotConfig = new JObject();
                spriteSnapshotConfig.Add("CellWidth", "120");
                spriteSnapshotConfig.Add("CellHeight", "68");
                spriteSnapshotConfig.Add("Columns", "3");
                spriteSnapshotConfig.Add("Lines", "10");
                spriteSnapshotConfig.Add("Padding", "20");
                spriteSnapshotConfig.Add("Margin", "50");
                spriteSnapshotConfig.Add("KeepCellPic", "keep");
                spriteSnapshotConfig.Add("Color", "tomato");
                snapshotConfig.Add("SpriteSnapshotConfig", spriteSnapshotConfig);
    
                // The snapshot type. Set the value to SpriteSnapshot for image sprites and to NormalSnapshot in other scenarios.
                templateConfig.Add("SnapshotType", "SpriteSnapshot");
    
                return templateConfig.ToString();
            }
        }
    }



Modify a snapshot template {#h2--div-id-updatevodtemplate-div-3}
----------------------------------------------------------------

You can call the UpdateVodTemplate operation to modify a snapshot template.
For more information about the request and response parameters of this operation, see [UpdateVodTemplate](/intl.en-US/API Reference/Media processing/Snapshot template/UpdateVodTemplate.md). Example: 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.Core.Profile;
    using Aliyun.Acs.vod.Model.V20170321;
    using Newtonsoft.Json.Linq;
    
    namespace Aliyun.Acs.vod.Sdk.UpdateVodTemplate
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
                    UpdateVodTemplateResponse response = UpdateVodTemplate(client);
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
            /// Modify a snapshot template.
            /// </summary>
            /// <returns>UpdateVodTemplateResponse</returns>
            /// <param name="client">Client.</param>
            public static UpdateVodTemplateResponse UpdateVodTemplate(DefaultAcsClient client)
            {
                // Create a request.
                UpdateVodTemplateRequest request = new UpdateVodTemplateRequest();
                request.VodTemplateId = "53azf9d796fad9d7b862b2e****";
                // Specify the template name.
                request.Name = "new template name";
    
                // Build template configurations.
                request.TemplateConfig = BuildSnapshotTemplateConfig();
    
                return client.GetAcsResponse(request);
            }
    
            /// <summary>
            /// Build the parameters of a snapshot template. Configure the parameters as required.
            /// (The following sample code shows the complete configurations of common snapshots.)
            /// </summary>
            /// <returns>Configurations of the snapshot template</returns>
            public static string BuildSnapshotTemplateConfig()
            {
                JObject templateConfig = new JObject();
                JObject snapshotConfig = new JObject();
                snapshotConfig.Add("Count", "50");
                snapshotConfig.Add("Interval", "1");
                snapshotConfig.Add("SpecifiedOffsetTime", "0");
                snapshotConfig.Add("Width", "200");
                snapshotConfig.Add("Height", "200");
                // The configurations of common snapshots. The configurations are also used by image sprites.
                templateConfig.Add("SnapshotConfig", snapshotConfig);
    
                // The snapshot type. Set the value to SpriteSnapshot for image sprites and to NormalSnapshot in other scenarios.
                templateConfig.Add("SnapshotType", "SpriteSnapshot");
    
                return templateConfig.ToString();
            }
        }
    }



Delete a snapshot template {#h2--div-id-deletevodtemplate-div-4}
----------------------------------------------------------------

You can call the DeleteVodTemplate operation to delete a snapshot template.
For more information about the request and response parameters of this operation, see [DeleteVodTemplate](/intl.en-US/API Reference/Media processing/Snapshot template/DeleteVodTemplate.md). Example: 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.Core.Profile;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.vod.Sdk.DeleteVodTemplate
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
                    DeleteVodTemplateResponse response = DeleteVodTemplate(client);
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
            /// Deletes the vod template.
            /// </summary>
            /// <returns>The vod template.</returns>
            /// <param name="client">Client.</param>
            public static DeleteVodTemplateResponse DeleteVodTemplate(DefaultAcsClient client)
            {
                // Create a request.
                DeleteVodTemplateRequest request = new DeleteVodTemplateRequest();
                // Specify the ID of the template that you want to delete.
                request.VodTemplateId = "53azf9d796fad9d7b862b2e****";
    
                return client.GetAcsResponse(request);
            }
        }
    }



Query snapshot templates {#h2--div-id-listvodtemplate-div-5}
------------------------------------------------------------

You can call the ListVodTemplate operation to query snapshot templates.
For more information about the request and response parameters of this operation, see [ListVodTemplate](/intl.en-US/API Reference/Media processing/Snapshot template/ListVodTemplate.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.Core.Profile;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.vod.Sdk.ListVodTemplate
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
                    ListVodTemplateResponse response = ListVodTemplate(client);
    
                    if (response.VodTemplateInfoList ! = null && response.VodTemplateInfoList.Count > 0) 
                    {
                        foreach (ListVodTemplateResponse.ListVodTemplate_VodTemplateInfo templateInfo in response.VodTemplateInfoList) 
                        {
                            // Specify the template ID.
                            Console.WriteLine("VodTemplateId = " + templateInfo.VodTemplateId);
                            // Specify the template name. 
                            Console.WriteLine("Name = " + templateInfo.Name);
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
            /// Lists the vod template.
            /// </summary>
            /// <returns>The vod template.</returns>
            /// <param name="client">Client.</param>
            public static ListVodTemplateResponse ListVodTemplate(DefaultAcsClient client)
            {
                // Create a request.
                ListVodTemplateRequest request = new ListVodTemplateRequest();
                // Specify the template type. Set the value to Snapshot.
                request.TemplateType = "Snapshot";
    
                return client.GetAcsResponse(request);
            }
        }
    }



Query a snapshot template {#h2--div-id-getvodtemplate-div-6}
------------------------------------------------------------

You can call the GetVodTemplate operation to query details about a snapshot template.
For more information about the request and response parameters of this operation, see [GetVodTemplate](/intl.en-US/API Reference/Media processing/Snapshot template/GetVodTemplate.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.Core.Profile;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.vod.Sdk.GetVodTemplate
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
                    GetVodTemplateResponse response = GetVodTemplate(client);
                    if (response.VodTemplateInfo ! = null)
                    {
                        // Specify the template ID.
                        Console.WriteLine("VodTemplateId = " + templateInfo.VodTemplateId);
                        // Specify the template name. 
                        Console.WriteLine("Name = " + templateInfo.Name);
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
            /// Gets the vod template.
            /// </summary>
            /// <returns>The vod template.</returns>
            /// <param name="client">Client.</param>
            public static GetVodTemplateResponse GetVodTemplate(DefaultAcsClient client)
            {
                // Create a request.
                GetVodTemplateRequest request = new GetVodTemplateRequest();
                // Specify the ID of the template that you want to query.
                request.VodTemplateId = "53azf9d796fad9d7b862b2e****";
    
                return client.GetAcsResponse(request);
            }
        }
    }



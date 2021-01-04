Video AI 
=============================

This topic provides examples on how to use the API operations of the video AI module. The API operations are encapsulated in ApsaraVideo VOD SDK for .NET. You can call the API operations to submit or query AI jobs, specify an AI template as the default one, and query the default AI template. You can also create, delete, modify, and query AI templates.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/.NET SDK/Initialization.md).

Submit an AI job {#h2--ai-div-id-submitaijob-div-2}
---------------------------------------------------

You can call the SubmitAIJob operation to submit an AI job.
For more information about the request and response parameters of this operation, see [SubmitAIJob](). Example: 
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.vod.Sdk.SubmitAIJob
    {
        class MainClass
        {
            public static void Main(string[] args)
            {
                try
                {
                    // Create a request.
                    SubmitAIJobRequest request = new SubmitAIJobRequest();
                    // Specify the video ID.
                    request.MediaId = "3eb19a4585bc475e995bdd456****";
                    // Specify the AI type. Make sure that this AI type is enabled.
                    request.Types = "AIVideoCover";
                    // Initialize a client.
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // Initiate the request and display the response.
                    SubmitAIJobResponse response = client.GetAcsResponse(request);
                    // List the request ID.
                    Console.WriteLine("RequestId = " + response.RequestId);
                    if (response.AIJobList ! = null && response.AIJobList.Count > 0) 
                    {
                        foreach (var job in response.AIJobList) 
                        {
                            // The video ID.
                            Console.WriteLine("MediaId = " + job.MediaId);
                            // The job ID.
                            Console.WriteLine("JobId = " + job.JobId);
                            // The AI type.
                            Console.WriteLine("Type = " + job.Type);
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



Query AI jobs {#h2--ai-div-id-listaijob-div-3}
----------------------------------------------

You can call the ListAIJob operation to query AI jobs.
For more information about the request and response parameters of this operation, see [ListAIJob](). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    onsole.WriteLine("JobId = " + jobId)using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.vod.Sdk.ListAIJob
    {
        class MainClass
        {
            public static void Main(string[] args)
            {
                try
                {
                    // Create a request.
                    ListAIJobRequest request = new ListAIJobRequest();
                    // Specify the video IDs.
                    request.JobIds = "979d4d7a36ae41b1a945a258****,3eb19a4585bc475e995bddea56****";
                    // Initialize a client.
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // Initiate the request and display the response.
                    ListAIJobResponse response = client.GetAcsResponse(request);
                    // List the request ID.
                    Console.WriteLine("RequestId = " + response.RequestId);
                    // List details about jobs.
                    if (response.AIJobList ! = null && response.AIJobList.Count > 0)
                    {
                        foreach (var job in response.AIJobList)
                        {
                            // The video ID.
                            Console.WriteLine("MediaId = " + job.MediaId);
                            // The job ID.
                            Console.WriteLine("JobId = " + job.JobId);
                            // The AI type.
                            Console.WriteLine("Type = " + job.Type);
                            // The job status.
                            Console.WriteLine("Status = " + job.Status);
                            // The job result.
                            Console.WriteLine("Data = " + job.Data);
                        }
                    }
                    // List the IDs of jobs that do not exist.
                    if (response.NonExistAIJobIds ! = null && response.NonExistAIJobIds.Count > 0)
                    {
                        foreach(jobId in response.NonExistAIJobIds) 
                        {
                            // The job ID.
                            C;
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



Create an AI template {#h2--ai-div-id-addaitemplate-div-4}
----------------------------------------------------------

You can call the AddAITemplate operation to create an AI template.
For more information about the request and response parameters of this operation, see [AddAITemplate](). Example: 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.Core.Profile;
    using Aliyun.Acs.vod.Model.V20170321;
    using Newtonsoft.Json.Linq;
    
    namespace Aliyun.Acs.vod.Sdk.AddAITemplate
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
                    AddAITemplateResponse response = AddAITemplate(client);
                    // List the request ID.
                    Console.WriteLine("RequestId = " + response.RequestId);
                    // List the template ID.
                    Console.WriteLine("TemplateId = " + response.TemplateId);
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
            /// Create an AI template.
            /// </summary>
            /// <param name="client">Client.</param>
            public static AddAITemplateResponse AddAITemplate(DefaultAcsClient client)
            {
                // Create a request.
                AddAITemplateRequest request = new AddAITemplateRequest();
                // Specify the template type. For this example, specify an automated review template.
                request.TemplateType = "AIMediaAudit";
                // Specify the template name.
                request.TemplateName = "My custom template";
                // Build the detailed configurations of the template.
                JObject templateConfig = new JObject();
    
                JArray auditItem = new JArray();
                auditItem.Add("terrorism");
                auditItem.Add("porn");
                templateConfig.Add("AuditItem", auditItem);
    
                JArray auditRange = new JArray();
                auditRange.Add("video");
                auditRange.Add("image-cover");
                auditRange.Add("text-title");
                templateConfig.Add("AuditRange", auditRange);
    
                JArray auditContent = new JArray();
                auditContent.Add("screen");
                templateConfig.Add("AuditContent", auditContent);
    
                templateConfig.Add("AuditAutoBlock", "no");
    
                request.TemplateConfig = templateConfig.ToString();
                // The returned results.
                return client.GetAcsResponse(request);
            }
        }
    }



Delete an AI template {#h2--ai-div-id-deleteaitemplate-div-5}
-------------------------------------------------------------

You can call the DeleteAITemplate operation to delete an AI template.
For more information about the request and response parameters of this operation, see [DeleteAITemplate](). Example: 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.Core.Profile;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.vod.Sdk.DeleteAITemplate
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
                    DeleteAITemplateResponse response = DeleteAITemplate(client);
                    // List the request ID.
                    Console.WriteLine("RequestId = " + response.RequestId);
                    // List the template ID.
                    Console.WriteLine("TemplateId = " + response.TemplateId);
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
            /// Delete an AI template.
            /// </summary>
            /// <returns>Delete an AI template</returns>
            /// <param name="client">Client.</param>
            public static DeleteAITemplateResponse DeleteAITemplate(DefaultAcsClient client)
            {
                // Create a request.
                DeleteAITemplateRequest request = new DeleteAITemplateRequest();
                // Specify the template ID.
                request.TemplateId = "dc063078c1d845139e2a5bd8ff85****";
                // The returned results.
                return client.GetAcsResponse(request);
            }
        }
    }



Modify an AI template {#h2--ai-div-id-updateaitemplate-div-6}
-------------------------------------------------------------

You can call the UpdateAITemplate operation to modify an AI template.
For more information about the request and response parameters of this operation, see [UpdateAITemplate](). Example: 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.Core.Profile;
    using Aliyun.Acs.vod.Model.V20170321;
    using Newtonsoft.Json.Linq;
    
    namespace Aliyun.Acs.vod.Sdk.UpdateAITemplate
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
                    UpdateAITemplateResponse response = UpdateAITemplate(client);
                    // List the request ID.
                    Console.WriteLine("RequestId = " + response.RequestId);
                    // List the template ID.
                    Console.WriteLine("TemplateId = " + response.TemplateId);
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
            /// Modify an AI template.
            /// </summary>
            /// <param name="client">Client.</param>
            public static UpdateAITemplateResponse UpdateAITemplate(DefaultAcsClient client)
            {
                // Create a request.
                UpdateAITemplateRequest request = new UpdateAITemplateRequest();
                // Specify the template name.
                request.TemplateName = "My custom template";
                // Build the detailed configurations of the template.
                JObject templateConfig = new JObject();
    
                JArray auditItem = new JArray();
                //auditItem.Add("terrorism");
                auditItem.Add("porn");
                templateConfig.Add("AuditItem", auditItem);
    
                JArray auditRange = new JArray();
                auditRange.Add("video");
                auditRange.Add("image-cover");
                auditRange.Add("text-title");
                templateConfig.Add("AuditRange", auditRange);
    
                JArray auditContent = new JArray();
                auditContent.Add("screen");
                templateConfig.Add("AuditContent", auditContent);
    
                templateConfig.Add("AuditAutoBlock", "no");
    
                request.TemplateConfig = templateConfig.ToString();
                // The returned results.
                return client.GetAcsResponse(request);
            }
        }
    }



Query an AI template {#h2--ai-div-id-getaitemplate-div-7}
---------------------------------------------------------

You can call the GetAITemplate operation to query details about an AI template.
For more information about the request and response parameters of this operation, see [GetAITemplate](). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.Core.Profile;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.vod.Sdk.GetAITemplate
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
                    GetAITemplateResponse response = GetAITemplate(client);
                    // List the request ID.
                    Console.WriteLine("RequestId = " + response.RequestId);
                    // List the information about the template.
                    Console.WriteLine("TemplateId = " + response.TemplateInfo.TemplateId);
                    Console.WriteLine("TemplateType = " + response.TemplateInfo.TemplateType);
                    Console.WriteLine("TemplateName = " + response.TemplateInfo.TemplateName);
                    Console.WriteLine("TemplateConfig = " + response.TemplateInfo.TemplateConfig);
    
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
            /// Query an AI template.
            /// </summary>
            /// <returns>AI template</returns>
            /// <param name="client">Client.</param>
            public static GetAITemplateResponse GetAITemplate(DefaultAcsClient client)
            {
                // Create a request.
                GetAITemplateRequest request = new GetAITemplateRequest();
                // Specify the template ID.
                request.TemplateId = "dc063078c1d845139e2a5bd8ff99****";
                // The returned results.
                return client.GetAcsResponse(request);
            }
        }
    }



Query AI templates {#h2--ai-div-id-listaitemplate-div-8}
--------------------------------------------------------

You can call the ListAITemplate operation to query AI templates.
For more information about the request and response parameters of this operation, see [ListAITemplate](). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.Core.Profile;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.vod.Sdk.ListAITemplate
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
                    ListAITemplateResponse response = ListAITemplate(client);
                    // List the request ID.
                    Console.WriteLine("RequestId = " + response.RequestId);
                    // List the information about a template.
                    if (response.TemplateInfoList ! = null && response.TemplateInfoList.Count > 0) {
                        foreach (ListAITemplateResponse.ListAITemplate_TemplateInfoListItem templateInfo in response.TemplateInfoList) {
                            Console.WriteLine("TemplateId = " + templateInfo.TemplateId);
                            Console.WriteLine("TemplateType = " + templateInfo.TemplateType);
                            Console.WriteLine("TemplateName = " + templateInfo.TemplateName);
                            Console.WriteLine("TemplateConfig = " + templateInfo.TemplateConfig);
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
            /// Query AI templates.
            /// </summary>
            /// <returns>AI templates</returns>
            /// <param name="client">Client.</param>
            public static ListAITemplateResponse ListAITemplate(DefaultAcsClient client)
            {
                // Create a request.
                ListAITemplateRequest request = new ListAITemplateRequest();
                // Specify the template type. For this example, specify an automated review template.
                request.TemplateType = "AIMediaAudit";
                // The returned results.
                return client.GetAcsResponse(request);
            }
        }
    }



Specify an AI template as the default one {#h2--ai-div-id-setdefaultaitemplate-div-9}
-------------------------------------------------------------------------------------

You can call the SetDefaultAITemplate operation to specify an AI template as the default one.
For more information about the request and response parameters of this operation, see [SetDefaultAITemplate](). Example: 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.Core.Profile;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace SetDefaultAITemplate
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
                    SetDefaultAITemplateResponse response = SetDefaultAITemplate(client);
                    // List the request ID.
                    Console.WriteLine("RequestId = " + response.RequestId);
                    // List the template ID.
                    Console.WriteLine("TemplateId = " + response.TemplateId);
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
            /// Specify an AI template as the default one.
            /// </summary>
            /// <returns>Default AI template</returns>
            /// <param name="client">Client.</param>
            public static SetDefaultAITemplateResponse SetDefaultAITemplate(DefaultAcsClient client)
            {
                // Create a request.
                SetDefaultAITemplateRequest request = new SetDefaultAITemplateRequest();
                // Specify the template ID.
                request.TemplateId = "dc063078c1d845139e2a5bd8ff85****";
                // The returned results.
                return client.GetAcsResponse(request);
    
            }
        }
    }



Query the default AI template {#h2--ai-div-id-getdefaultaitemplate-div-10}
--------------------------------------------------------------------------

You can call the GetDefaultAITemplate operation to query details about the default AI template.
For more information about the request and response parameters of this operation, see [GetDefaultAITemplate](). Example: 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.Core.Profile;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace GetDefaultAITemplate
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
                    GetDefaultAITemplateResponse response = GetDefaultAITemplate(client);
                    // List the request ID.
                    Console.WriteLine("RequestId = " + response.RequestId);
                    // List the information about the template.
                    Console.WriteLine("TemplateId = " + response.TemplateInfo.TemplateId);
                    Console.WriteLine("TemplateType = " + response.TemplateInfo.TemplateType);
                    Console.WriteLine("TemplateName = " + response.TemplateInfo.TemplateName);
                    Console.WriteLine("TemplateConfig = " + response.TemplateInfo.TemplateConfig);
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
            /// Query the default AI template.
            /// </summary>
            /// <returns>Default AI template</returns>
            /// <param name="client">Client.</param>
            public static GetDefaultAITemplateResponse GetDefaultAITemplate(DefaultAcsClient client)
            {
                // Create a request.
                GetDefaultAITemplateRequest request = new GetDefaultAITemplateRequest();
                // Specify the template type. For this example, specify an automated review template.
                request.TemplateType = "AIMediaAudit";
                // The returned results.
                return client.GetAcsResponse(request);
    
            }
        }
    }



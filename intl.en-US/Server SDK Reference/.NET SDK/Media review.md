Media review 
=================================

This topic provides examples on how to use the API operations of the media review module. The API operations are encapsulated in ApsaraVideo VOD SDK for .NET. You can call the API operations to submit and query automated review jobs. You can also query automated review results, create manual reviews, and set an IP address whitelist for reviews.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/.NET SDK/Initialization.md).

Submit an automated review job {#h2--div-id-submitaimediaauditjob-div-2}
------------------------------------------------------------------------

You can call the SubmitAIMediaAuditJob operation to submit an automated review job.
For more information about the request and response parameters of this operation, see [SubmitAIMediaAuditJob](). Example: {#h2--div-id-submitaimediaauditjob-div-2}
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.Core.Profile;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.vod.Sdk.SubmitAIMediaAuditJob
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
                    SubmitAIMediaAuditJobResponse response = SubmitAIMediaAuditJob(client);
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
            /// Submit an automated review job.
            /// </summary>
            /// <param name="client">Client.</param>
            /// <summary>
            /// Submit an automated review job.
            /// </summary>
            /// <returns>Automated review job</returns>
            /// <param name="client">Client.</param>
            public static SubmitAIMediaAuditJobResponse SubmitAIMediaAuditJob(DefaultAcsClient client)
            {
            // Create a request.
            SubmitAIMediaAuditJobRequest request = new SubmitAIMediaAuditJobRequest();
            // Specify the video ID.
            request.MediaId = "dc063078c1d845139e2a5bd8ff89****";
            // The returned results.
            return client.GetAcsResponse(request);
            }
        }
    }



Query an automated review job {#h2--div-id-getaimediaauditjob-div-3}
--------------------------------------------------------------------

You can call GetAIMediaAuditJob operation to query details about an automated review job.
For more information about the request and response parameters of this operation, see [GetAIMediaAuditJob](). Example: {#h2--div-id-getaimediaauditjob-div-3}
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.Core.Profile;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.vod.Sdk.GetAIMediaAuditJob
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
                    GetAIMediaAuditJobResponse response = GetAIMediaAuditJob(client);
                    // List the request ID.
                    Console.WriteLine("RequestId = " + response.RequestId);
                    // List results.
                    Console.WriteLine("MediaId = " + response.MediaAuditJob.MediaId);
                    Console.WriteLine("JobId = " + response.MediaAuditJob.JobId);
                    Console.WriteLine("Type = " + response.MediaAuditJob.Type);
                    Console.WriteLine("Status = " + response.MediaAuditJob.Status);
                    Console.WriteLine("Code = " + response.MediaAuditJob.Code);
                    Console.WriteLine("Message = " + response.MediaAuditJob.Message);
                    Console.WriteLine("Data AbnormalModules = " + response.MediaAuditJob.Data.AbnormalModules);
                    Console.WriteLine("Data Label = " + response.MediaAuditJob.Data.Label);
                    Console.WriteLine("Data Suggestion = " + response.MediaAuditJob.Data.Suggestion);
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
            /// Query an automated review job.
            /// </summary>
            /// <returns>Automated review job</returns>
            /// <param name="client">Client.</param>
            public static GetAIMediaAuditJobResponse GetAIMediaAuditJob(DefaultAcsClient client)
            {
                // Create a request.
                GetAIMediaAuditJobRequest request = new GetAIMediaAuditJobRequest();
                // Specify the job ID.
                request.JobId = "7dc69b893c8b4f13b47aae8de059****";
                // The returned results.
                return client.GetAcsResponse(request);
    
            }
        }
    }



Query the summary of automated review results {#h2--div-id-getmediaauditresult-div-4}
-------------------------------------------------------------------------------------

You can call the GetMediaAuditResult operation to query the summary of automated review results.
For more information about the request and response parameters of this operation, see [GetMediaAuditResult](). Example: {#h2--div-id-getmediaauditresult-div-4}
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.Core.Profile;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.vod.Sdk.GetMediaAuditResult
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
                    GetMediaAuditResultResponse response = GetMediaAuditResult(client);
                    // List the request ID.
                    Console.WriteLine("RequestId = " + response.RequestId);
                    // List results.
                    Console.WriteLine("Data AbnormalModules = " + response.MediaAuditResult.AbnormalModules);
                    Console.WriteLine("Data Label = " + response.MediaAuditResult.Label);
                    Console.WriteLine("Data Suggestion = " + response.MediaAuditResult.Suggestion);
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
            /// Query the summary of automated review results.
            /// </summary>
            /// <returns>Summary of automated review results</returns>
            /// <param name="client">Client.</param>
            public static GetMediaAuditResultResponse GetMediaAuditResult(DefaultAcsClient client)
            {
                // Create a request.
                GetMediaAuditResultRequest request = new GetMediaAuditResultRequest();
                // Specify the video ID.
                request.MediaId = "7dc69b893c8b4f13b47aae8de053****";
                // The returned results.
                return client.GetAcsResponse(request);
    
            }
        }
    }



Query details about automated review results {#h2--div-id-getmediaauditresultdetail-div-5}
------------------------------------------------------------------------------------------

You can call the GetMediaAuditResultDetail operation to query details about automated review results.
For more information about the request and response parameters of this operation, see [GetMediaAuditResultDetail](). Example: {#h2--div-id-getmediaauditresultdetail-div-5}
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.Core.Profile;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.vod.Sdk.GetMediaAuditResultDetail
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
                    GetMediaAuditResultDetailResponse response = GetMediaAuditResultDetail(client);
                    // List the request ID.
                    Console.WriteLine("RequestId = " + response.RequestId);
                    // List results.
                    Console.WriteLine("Data Total = " + response.MediaAuditResultDetail.Total);
                    Console.WriteLine("Data List Size = " + response.MediaAuditResultDetail.List.Count);
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
            /// Query details about automated review results.
            /// </summary>
            /// <returns>Details about automated review results</returns>
            /// <param name="client">Client.</param>
            public static GetMediaAuditResultDetailResponse GetMediaAuditResultDetail(DefaultAcsClient client)
            {
                // Create a request.
                GetMediaAuditResultDetailRequest request = new GetMediaAuditResultDetailRequest();
                // Specify the video ID.
                request.MediaId = "7dc69b893c8b4f13b47aae8de0565****";
                // Specify the number of the page to return.
                request.PageNo = 1;
                // The returned results.
                return client.GetAcsResponse(request);
    
            }
        }
    }



Query the timeline of automated review results {#h2--div-id-getmediaauditresulttimeline-div-6}
----------------------------------------------------------------------------------------------

You can call the GetMediaAuditResultTimeline operation to query the timeline of automated review results.
For more information about the request and response parameters of this operation, see [GetMediaAuditResultTimeline](). Example: {#h2--div-id-getmediaauditresulttimeline-div-6}
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.Core.Profile;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.vod.Sdk.GetMediaAuditResultTimeline
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
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>","<Your AccessKeySecret>");
                    // Initiate the request and display the response.
                    GetMediaAuditResultTimelineResponse response = GetMediaAuditResultTimeline(client);
                    // List the request ID.
                    Console.WriteLine("RequestId = " + response.RequestId);
                    // List results.
                    Console.WriteLine("Terrorism = " + response.MediaAuditResultTimeline.Terrorism);
                    Console.WriteLine("Porn = " + response.MediaAuditResultTimeline.Porn);
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
            /// Query the timeline of automated review results.
            /// </summary>
            /// <returns>Timeline of automated review results</returns>
            /// <param name="client">Client.</param>
            public static GetMediaAuditResultTimelineResponse GetMediaAuditResultTimeline(DefaultAcsClient client)
            {
                // Create a request.
                GetMediaAuditResultTimelineRequest request = new GetMediaAuditResultTimelineRequest();
                // Specify the video ID.
                request.MediaId = "7dc69b893c8b4f13b47aae8de036****";
                // The returned results.
                return client.GetAcsResponse(request);
    
            }
        }
    }



Create a manual review {#h2--div-id-createaudit-div-7}
------------------------------------------------------

You can call the CreateAudit operation to create a manual review.
For more information about the request and response parameters of this operation, see [CreateAudit](/intl.en-US/API Reference/Content Moderation/Manual Audit/CreateAudit.md). Example: {#h2--div-id-createaudit-div-7}
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.vod.Model.V20170321;
    using Newtonsoft.Json.Linq;
    
    namespace Aliyun.Acs.vod.Sdk.CreateAudit
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
                    CreateAuditResponse response = CreateAudit(client);
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
            /// Creates the audit.
            /// </summary>
            /// <returns>The audit.</returns>
            /// <param name="client">Client.</param>
            public static CreateAuditResponse CreateAudit(DefaultAcsClient client) 
            {
                CreateAuditRequest request = new CreateAuditRequest();
                // set audit content
                request.AuditContent = BuildAuditContent();
    
                return client.GetAcsResponse(request);
            }
    
            /// <summary>
            /// Builds the content of the audit.
            /// </summary>
            /// <returns>The audit content.</returns>
            public static string BuildAuditContent() 
            {
                JArray auditContents = new JArray();
                JObject auditContent = new JObject();
                auditContent.Add("VideoId", "3ebc10160bda481ca9b6858a0b65****");
                auditContent.Add("Status", "Blocked");
                auditContent.Add("Reason", "Including porn");
    
                return auditContents.ToString();
            }
        }
    }



Query the historical records of manual reviews {#h2--div-id-getaudithistory-div-8}
----------------------------------------------------------------------------------

You can call the GetAuditHistory operation to query the historical records of manual reviews.
For more information about the request and response parameters of this operation, see [GetAuditHistory](/intl.en-US/API Reference/Content Moderation/Manual Audit/GetAuditHistory.md). Example: {#h2--div-id-getaudithistory-div-8}
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.Core.Profile;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.vod.Sdk.GetAuditHistory
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
                    GetAuditHistoryResponse response = GetAuditHistory(client);
                    Console.WriteLine("RequestId = " + response.RequestId);
                    // List the result of the current review.
                    Console.WriteLine("Status = " + response.Status);
                    // List the number of historical records.
                    Console.WriteLine("Total = " + response.Total);
    
                    if (response.Histories ! = null && response.Histories.Count > 0)
                    {
                        foreach (GetAuditHistoryResponse.GetAuditHistory_History history in response.Histories) {
                            Console.WriteLine("Status = " + history.Status);
                            Console.WriteLine("CreationTime = " + history.CreationTime);
                            Console.WriteLine("Reason = " + history.Reason);
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
            /// Gets the audit history.
            /// </summary>
            /// <returns>The audit history.</returns>
            /// <param name="client">Client.</param>
            public static GetAuditHistoryResponse GetAuditHistory(DefaultAcsClient client) {
                // Create a request.
                GetAuditHistoryRequest request = new GetAuditHistoryRequest();
                request.VideoId = "VideoId";
                request.PageNo = 1;
                request.PageSize = 10;
    
                return client.GetAcsResponse(request);
            }
        }
    }



Set an IP address whitelist for reviews {#h2--ip-div-id-setauditsecurityip-div-9}
---------------------------------------------------------------------------------

You can call the SetAuditSecurityIp operation to set an IP address whitelist for reviews.
For more information about the request and response parameters of this operation, see [SetAuditSecurityIp](/intl.en-US/API Reference/Content Moderation/Audit Config/SetAuditSecurityIp.md). Example: {#h2--ip-div-id-setauditsecurityip-div-9}
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.vod.Sdk.SetAuditSecurityIp
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
                    // Initialize a client.
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    
                    SetAuditSecurityIpResponse response = SetAuditSecurityIp(client);
    
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
            /// Sets the audit security ip.
            /// </summary>
            /// <returns>The audit security ip.</returns>
            /// <param name="client">Client.</param>
            public static SetAuditSecurityIpResponse SetAuditSecurityIp (DefaultAcsClient client)
            {
                // Create a request.
                SetAuditSecurityIpRequest request = new SetAuditSecurityIpRequest();
                // Specify the name of the IP address whitelist for reviews. The default value is Default.
                request.SecurityGroupName = "MyGroupName";
                // Specify the operation type. The default value is Append, which indicates that IP addresses are added to the whitelist.
                request.OperateMode = "Cover";
                // Specify the IP addresses to add to the whitelist.
                request.Ips = "10.23.12.20,10.23.12.21,10.23.12.22";
    
                return client.GetAcsResponse(request);
            }
        }
    }



Query the IP addresses in a whitelist {#h2--ip-div-id-listauditsecurityip-div-10}
---------------------------------------------------------------------------------

You can call the ListAuditSecurityIp operation to query the IP addresses in a whitelist.
For more information about the request and response parameters of this operation, see [ListAuditSecurityIp](/intl.en-US/API Reference/Content Moderation/Audit Config/ListAuditSecurityIp.md). Example: {#h2--ip-div-id-listauditsecurityip-div-10}
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace Aliyun.Acs.vod.Sdk.ListAuditSecurityIp
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
                    ListAuditSecurityIpResponse response = ListAuditSecurityIp(client);
    
                    Console.WriteLine("RequestId = " + response.RequestId);
    
                    if (response.SecurityIpList ! = null && response.SecurityIpList.Count > 0)
                    {
                        foreach (ListAuditSecurityIpResponse.ListAuditSecurityIp_SecurityIp securityIp in response.SecurityIpList)
                        {
                            Console.WriteLine("SecurityGroupName = " + securityIp.SecurityGroupName);
                            Console.WriteLine("Ips = " + securityIp.Ips);
                            Console.WriteLine("CreationTime = " + securityIp.CreationTime);
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
            /// Lists the audit security ip.
            /// </summary>
            /// <returns>The audit security ip.</returns>
            /// <param name="client">Client.</param>
            public static ListAuditSecurityIpResponse ListAuditSecurityIp(DefaultAcsClient client)
            {
                // Create a request.
                ListAuditSecurityIpRequest request = new ListAuditSecurityIpRequest();
                // Specify the name of the whitelist.
                request.SecurityGroupName = "MyGroupName";
    
                return client.GetAcsResponse(request);
            }
        }
    }



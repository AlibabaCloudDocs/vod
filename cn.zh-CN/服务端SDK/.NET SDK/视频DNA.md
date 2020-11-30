视频DNA 
==========================

本篇文档提供了.NET SDK视频DNA模块相关功能的API调用示例。包含提交视频DNA作业、查询视频DNA作业、获取视频DNA结果。

初始化客户端 {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
--------------------------------------------

使用前请先初始化客户端，请参见[初始化](/cn.zh-CN/服务端SDK/.NET SDK/初始化.md)。

提交视频DNA作业 {#h2--div-id-submitaijob-div-2}
-----------------------------------------

调用SubmitAIJob接口，完成提交视频DNA作业功能。
接口参数和返回字段请参见[SubmitAIJob](/cn.zh-CN/服务端API/视频AI/视频DNA/提交视频DNA作业.md)。调用示例如下： 
------------------------------------------------------------------------------------------------------------------------------------------------------------

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
                    // 构造请求
                    SubmitAIJobRequest request = new SubmitAIJobRequest();
                    // 设置视频ID
                    request.MediaId = "3eb19a4585bc475e995bdd7894****";
                    // 设置AI类型，类型为AIMediaDNA
                    request.Types = "AIMediaDNA";
                    // 初始化客户端
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // 发起请求，并得到 response
                    SubmitAIJobResponse response = client.GetAcsResponse(request);
                    // 请求ID
                    Console.WriteLine("RequestId = " + response.RequestId);
                    if (response.AIJobList != null && response.AIJobList.Count > 0) 
                    {
                        foreach (var job in response.AIJobList) 
                        {
                            // 视频ID
                            Console.WriteLine("MediaId = " + job.MediaId);
                            // 作业ID
                            Console.WriteLine("JobId = " + job.JobId);
                            // AI类型
                            Console.WriteLine("Type = " + job.Type);
                        }
                    }
                }
                catch (ServerException e)
                {
                    if (e.RequestId != null)
                    {
                        Console.WriteLine("RequestId = " + e.RequestId);
                    }
                    Console.WriteLine("ErrorCode = " + e.ErrorCode);
                    Console.WriteLine("ErrorMessage = " + e.ErrorMessage);
                }
                catch (ClientException e)
                {
                    if (e.RequestId != null)
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



查询视频DNA作业 {#h2--div-id-listaijob-div-3}
---------------------------------------

调用ListAIJob接口，完成查询视频DNA作业功能。
接口参数和返回字段请参见[ListAIJob](/cn.zh-CN/服务端API/视频AI/视频DNA/查询视频DNA作业.md)。调用示例如下： 
--------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
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
                    // 构造请求
                    ListAIJobRequest request = new ListAIJobRequest();
                    // 设置视频ID
                    request.JobIds = "979d4d7a36ae41b1a945a258****,3eb19a4585bc475e995bddea58****";
                    // 初始化客户端
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // 发起请求，并得到 response
                    ListAIJobResponse response = client.GetAcsResponse(request);
                    // 请求ID
                    Console.WriteLine("RequestId = " + response.RequestId);
                    // 打印作业列表
                    if (response.AIJobList != null && response.AIJobList.Count > 0)
                    {
                        foreach (var job in response.AIJobList)
                        {
                            // 视频ID
                            Console.WriteLine("MediaId = " + job.MediaId);
                            // 作业ID
                            Console.WriteLine("JobId = " + job.JobId);
                            // AI类型
                            Console.WriteLine("Type = " + job.Type);
                            // 作业状态
                            Console.WriteLine("Status = " + job.Status);
                            // 作业结果
                            Console.WriteLine("Data = " + job.Data);
                        }
                    }
                    // 打印不存在的作业ID
                    if (response.NonExistAIJobIds != null && response.NonExistAIJobIds.Count > 0)
                    {
                        foreach(jobId in response.NonExistAIJobIds) 
                        {
                            // 作业ID
                            Console.WriteLine("JobId = " + jobId);
                        }
                    }
                }
                catch (ServerException e)
                {
                    if (e.RequestId != null)
                    {
                        Console.WriteLine("RequestId = " + e.RequestId);
                    }
                    Console.WriteLine("ErrorCode = " + e.ErrorCode);
                    Console.WriteLine("ErrorMessage = " + e.ErrorMessage);
                }
                catch (ClientException e)
                {
                    if (e.RequestId != null)
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



获取视频DNA结果 {#h2--div-id-getmediadnaresult-div-4}
-----------------------------------------------

调用GetMediaDNAResult接口，完成获取视频DNA结果功能。
接口参数和返回字段请参见[GetMediaDNAResult](/cn.zh-CN/服务端API/视频AI/视频DNA/获取视频DNA结果.md)。调用示例如下： 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    using System;
    using Aliyun.Acs.Core;
    using Aliyun.Acs.Core.Exceptions;
    using Aliyun.Acs.vod.Model.V20170321;
    
    namespace GetMediaDNAResult
    {
        class MainClass
        {
            public static void Main(string[] args)
            {
                try
                {
                    // 构造请求
                    GetMediaDNAResultRequest request = new GetMediaDNAResultRequest();
                    // 设置视频ID
                    request.MediaId = "3eb19a4585bc475e995bdd62eaee0****";
                    // 初始化客户端
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // 发起请求，并得到 response
                    GetMediaDNAResultResponse response = client.GetAcsResponse(request);
                    // 请求ID
                    Console.WriteLine("RequestId = " + response.RequestId);
                    if (response.DNAResult != null)
                    {
                        // 打印DNA结果
                        Console.WriteLine("DNAResult = " + response.DNAResult.ToString());
                    }
                }
                catch (ServerException e)
                {
                    if (e.RequestId != null)
                    {
                        Console.WriteLine("RequestId = " + e.RequestId);
                    }
                    Console.WriteLine("ErrorCode = " + e.ErrorCode);
                    Console.WriteLine("ErrorMessage = " + e.ErrorMessage);
                }
                catch (ClientException e)
                {
                    if (e.RequestId != null)
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



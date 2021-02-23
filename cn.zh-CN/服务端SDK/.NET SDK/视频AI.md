视频AI 
=========================

本篇文档提供了.NET SDK视频AI模块相关功能的API调用示例。包含提交AI作业、查询AI作业、添加AI模板、修改AI模板、删除AI模板、查询AI模板、查询设置默认AI模板等。

初始化客户端 {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
--------------------------------------------

使用前请先初始化客户端，请参见[初始化](/cn.zh-CN/服务端SDK/.NET SDK/初始化.md)。

提交AI作业 {#h2--ai-div-id-submitaijob-div-2}
-----------------------------------------

调用SubmitAIJob接口，完成提交AI作业功能。

接口参数和返回字段请参见[SubmitAIJob](/cn.zh-CN/服务端API/视频AI/提交AI作业.md)。调用示例如下：

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
                    request.MediaId = "3eb19a4585bc475e995bdd456****";
                    // 设置AI类型，请确保已开通该类型AI
                    request.Types = "AIVideoCover";
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



查询AI作业 {#h2--ai-div-id-listaijob-div-3}
---------------------------------------

调用ListAIJob接口，完成查询AI作业功能。

接口参数和返回字段请参见[ListAIJob](/cn.zh-CN/服务端API/视频AI/查询AI作业.md)。调用示例如下：

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
                    // 构造请求
                    ListAIJobRequest request = new ListAIJobRequest();
                    // 设置视频ID
                    request.JobIds = "979d4d7a36ae41b1a945a258****,3eb19a4585bc475e995bddea56****";
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
                            C;
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



添加AI模板 {#h2--ai-div-id-addaitemplate-div-4}
-------------------------------------------

调用AddAITemplate接口，完成添加AI模板功能。

接口参数和返回字段请参见[AddAITemplate](/cn.zh-CN/服务端API/视频AI/AI模板/添加AI模板.md)。调用示例如下：

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
                    // 初始化客户端
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // 发起请求，并得到 response
                    AddAITemplateResponse response = AddAITemplate(client);
                    // 打印请求ID
                    Console.WriteLine("RequestId = " + response.RequestId);
                    // 打印模板ID
                    Console.WriteLine("TemplateId = " + response.TemplateId);
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
    
            /// <summary>
            /// 添加AI模板
            /// </summary>
            /// <param name="client">Client.</param>
            public static AddAITemplateResponse AddAITemplate(DefaultAcsClient client)
            {
                // 构造请求
                AddAITemplateRequest request = new AddAITemplateRequest();
                // 设置模板类型，以智能审核模板为例
                request.TemplateType = "AIMediaAudit";
                // 设置模板名称
                request.TemplateName = "My custom template";
                // 设置模板详细配置
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
                // 返回结果
                return client.GetAcsResponse(request);
            }
        }
    }



删除AI模板 {#h2--ai-div-id-deleteaitemplate-div-5}
----------------------------------------------

调用DeleteAITemplate接口，完成删除AI模板功能。

接口参数和返回字段请参见[DeleteAITemplate](/cn.zh-CN/服务端API/视频AI/AI模板/删除AI模板.md)。调用示例如下：

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
                    // 初始化客户端
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // 发起请求，并得到 response
                    DeleteAITemplateResponse response = DeleteAITemplate(client);
                    // 打印请求ID
                    Console.WriteLine("RequestId = " + response.RequestId);
                    // 打印模板ID
                    Console.WriteLine("TemplateId = " + response.TemplateId);
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
    
            /// <summary>
            /// 删除AI模板
            /// </summary>
            /// <returns>删除AI模板</returns>
            /// <param name="client">Client.</param>
            public static DeleteAITemplateResponse DeleteAITemplate(DefaultAcsClient client)
            {
                // 构造请求
                DeleteAITemplateRequest request = new DeleteAITemplateRequest();
                // 设置模板ID
                request.TemplateId = "dc063078c1d845139e2a5bd8ff85****";
                // 返回结果
                return client.GetAcsResponse(request);
            }
        }
    }



修改AI模板 {#h2--ai-div-id-updateaitemplate-div-6}
----------------------------------------------

调用UpdateAITemplate接口，完成修改AI模板功能。

接口参数和返回字段请参见[UpdateAITemplate](/cn.zh-CN/服务端API/视频AI/AI模板/修改AI模板.md)。调用示例如下：

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
                    // 初始化客户端
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // 发起请求，并得到 response
                    UpdateAITemplateResponse response = UpdateAITemplate(client);
                    // 打印请求ID
                    Console.WriteLine("RequestId = " + response.RequestId);
                    // 打印模板ID
                    Console.WriteLine("TemplateId = " + response.TemplateId);
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
    
            /// <summary>
            /// 修改AI模板
            /// </summary>
            /// <param name="client">Client.</param>
            public static UpdateAITemplateResponse UpdateAITemplate(DefaultAcsClient client)
            {
                // 构造请求
                UpdateAITemplateRequest request = new UpdateAITemplateRequest();
                // 设置模板名称
                request.TemplateName = "My custom template";
                // 设置模板详细配置
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
                // 返回结果
                return client.GetAcsResponse(request);
            }
        }
    }



查询AI模板 {#h2--ai-div-id-getaitemplate-div-7}
-------------------------------------------

调用GetAITemplate接口，完成查询AI模板功能。

接口参数和返回字段请参见[GetAITemplate](/cn.zh-CN/服务端API/视频AI/AI模板/查询AI模板.md)。调用示例如下：

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
                    // 初始化客户端
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // 发起请求，并得到 response
                    GetAITemplateResponse response = GetAITemplate(client);
                    // 打印请求ID
                    Console.WriteLine("RequestId = " + response.RequestId);
                    // 打印模板信息
                    Console.WriteLine("TemplateId = " + response.TemplateInfo.TemplateId);
                    Console.WriteLine("TemplateType = " + response.TemplateInfo.TemplateType);
                    Console.WriteLine("TemplateName = " + response.TemplateInfo.TemplateName);
                    Console.WriteLine("TemplateConfig = " + response.TemplateInfo.TemplateConfig);
    
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
    
            /// <summary>
            /// 查询AI模板
            /// </summary>
            /// <returns>AI模板</returns>
            /// <param name="client">Client.</param>
            public static GetAITemplateResponse GetAITemplate(DefaultAcsClient client)
            {
                // 构造请求
                GetAITemplateRequest request = new GetAITemplateRequest();
                // 设置模板ID
                request.TemplateId = "dc063078c1d845139e2a5bd8ff99****";
                // 返回结果
                return client.GetAcsResponse(request);
            }
        }
    }



查询AI模板列表 {#h2--ai-div-id-listaitemplate-div-8}
----------------------------------------------

调用ListAITemplate接口，完成查询AI模板列表功能。

接口参数和返回字段请参见[ListAITemplate](/cn.zh-CN/服务端API/视频AI/AI模板/查询AI模板列表.md)。调用示例如下：

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
                    // 初始化客户端
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // 发起请求，并得到 response
                    ListAITemplateResponse response = ListAITemplate(client);
                    // 打印请求ID
                    Console.WriteLine("RequestId = " + response.RequestId);
                    // 打印模板信息
                    if (response.TemplateInfoList != null && response.TemplateInfoList.Count > 0) {
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
    
            /// <summary>
            /// 查询AI模板列表
            /// </summary>
            /// <returns>AI模板列表</returns>
            /// <param name="client">Client.</param>
            public static ListAITemplateResponse ListAITemplate(DefaultAcsClient client)
            {
                // 构造请求
                ListAITemplateRequest request = new ListAITemplateRequest();
                // 设置模板类型，以智能审核模板为例
                request.TemplateType = "AIMediaAudit";
                // 返回结果
                return client.GetAcsResponse(request);
            }
        }
    }



设置默认AI模板 {#h2--ai-div-id-setdefaultaitemplate-div-9}
----------------------------------------------------

调用SetDefaultAITemplate接口，完成设置默认AI模板功能。

接口参数和返回字段请参见[SetDefaultAITemplate](/cn.zh-CN/服务端API/视频AI/AI模板/设置默认AI模板.md)。调用示例如下：

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
                    // 初始化客户端
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // 发起请求，并得到 response
                    SetDefaultAITemplateResponse response = SetDefaultAITemplate(client);
                    // 打印请求ID
                    Console.WriteLine("RequestId = " + response.RequestId);
                    // 打印模板ID
                    Console.WriteLine("TemplateId = " + response.TemplateId);
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
    
            /// <summary>
            /// 设置默认AI模板
            /// </summary>
            /// <returns>默认AI模板</returns>
            /// <param name="client">Client.</param>
            public static SetDefaultAITemplateResponse SetDefaultAITemplate(DefaultAcsClient client)
            {
                // 构造请求
                SetDefaultAITemplateRequest request = new SetDefaultAITemplateRequest();
                // 设置模板ID
                request.TemplateId = "dc063078c1d845139e2a5bd8ff85****";
                // 返回结果
                return client.GetAcsResponse(request);
    
            }
        }
    }



查询默认AI模板 {#h2--ai-div-id-getdefaultaitemplate-div-10}
-----------------------------------------------------

调用GetDefaultAITemplate接口，完成查询默认AI模板功能。

接口参数和返回字段请参见[GetDefaultAITemplate](/cn.zh-CN/服务端API/视频AI/AI模板/查询默认AI模板.md)。调用示例如下：

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
                    // 初始化客户端
                    DefaultAcsClient client = InitVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                    // 发起请求，并得到 response
                    GetDefaultAITemplateResponse response = GetDefaultAITemplate(client);
                    // 打印请求ID
                    Console.WriteLine("RequestId = " + response.RequestId);
                    // 打印模板信息
                    Console.WriteLine("TemplateId = " + response.TemplateInfo.TemplateId);
                    Console.WriteLine("TemplateType = " + response.TemplateInfo.TemplateType);
                    Console.WriteLine("TemplateName = " + response.TemplateInfo.TemplateName);
                    Console.WriteLine("TemplateConfig = " + response.TemplateInfo.TemplateConfig);
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
    
            /// <summary>
            /// 查询默认AI模板
            /// </summary>
            /// <returns>默认AI模板</returns>
            /// <param name="client">Client.</param>
            public static GetDefaultAITemplateResponse GetDefaultAITemplate(DefaultAcsClient client)
            {
                // 构造请求
                GetDefaultAITemplateRequest request = new GetDefaultAITemplateRequest();
                // 设置模板类型，以智能审核模板为例
                request.TemplateType = "AIMediaAudit";
                // 返回结果
                return client.GetAcsResponse(request);
    
            }
        }
    }



视频AI 
=========================

本篇文档提供了Java SDK视频AI模块相关功能的API调用示例。包含提交AI作业、添加AI模板、修改AI模板、删除AI模板、查询AI模板、查询AI模板列表、查询设置AI模板等。

初始化客户端 {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
--------------------------------------------

使用前请先初始化客户端，请参见[初始化](/cn.zh-CN/服务端SDK/Java SDK/初始化.md)。

提交AI作业 {#h2--ai-div-id-submitaijob-div-2}
-----------------------------------------

调用SubmitAIJob接口，完成提交AI作业功能。
接口参数和返回字段请参见[SubmitAIJob](/cn.zh-CN/服务端API/视频AI/提交AI作业.md)。调用示例如下： {#h2--ai-div-id-submitaijob-div-2}
------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.aliyuncs.vod.model.v20170321.SubmitAIJobRequest;
    import com.aliyuncs.vod.model.v20170321.SubmitAIJobResponse;
    
    /**
     * 提交作业
     */
    public static SubmitAIJobResponse submitAIJob(DefaultAcsClient client) throws Exception {
        SubmitAIJobRequest request = new SubmitAIJobRequest();
        // 设置视频ID
        request.setMediaId("3eb19a4585bc475e995bdd4a5c****");
        // 设置AI类型，请确保已开通该类型AI
        request.setTypes("AIVideoCover");
        // 返回结果
        return client.getAcsResponse(request);
    }
    
    
    /**
     * 以下为调用示例
     * @param args
     * @throws ClientException
     */
    public static void main(String[] args) throws ClientException {
       DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    
        try {
            // 提交作业
            SubmitAIJobResponse response = submitAIJob(client);
    
            // 打印请求ID
            System.out.println("ResquestId:" + response.getRequestId());
            // 打印结果信息
            if (response.getAIJobList() != null && response.getAIJobList().size() != 0) {
                for (SubmitAIJobResponse.AIJob aiJob : response.getAIJobList()) {
                  // 视频ID
                  System.out.println("MediaId:" + aiJob.getMediaId());
                  // 作业ID
                  System.out.println("JobId:" + aiJob.getJobId());
                  // AI类型
                  System.out.println("Type:" + aiJob.getType());
                }
            }
        } catch (Exception e) {
            System.out.println("ErrorMessage:" + e.getLocalizedMessage());
        }
    }



查询AI作业 {#h2--ai-div-id-listaijob-div-3}
---------------------------------------

调用ListAIJob接口，完成查询AI作业功能。
接口参数和返回字段请参见[ListAIJob ](/cn.zh-CN/服务端API/视频AI/查询AI作业.md)。调用示例如下： {#h2--ai-div-id-listaijob-div-3}
-------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.aliyuncs.vod.model.v20170321.ListAIJobRequest;
    import com.aliyuncs.vod.model.v20170321.ListAIJobResponse;
    
    /**
     * 查询作业
     */
    public static ListAIJobResponse listAIJob(DefaultAcsClient client) throws Exception {
        ListAIJobRequest request = new ListAIJobRequest();
        // 设置作业ID
        request.setJobIds("979d4d7a36ae41b1a945a2xxxxx,3eb19a4585bc475e995bddea****");
        // 返回结果
        return client.getAcsResponse(request);
    }
    
    /**
     * 以下为调用示例
     * @param args
     * @throws ClientException
     */
    public static void main(String[] args) throws Exception {
        DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    
        try {
            // 查询作业
            ListAIJobResponse response = listAIJob(client);
    
            // 打印请求ID
            System.out.println("ResquestId:" + response.getRequestId());
    
            // 打印作业列表
            System.out.println("============ AIJobList:");
            if (response.getAIJobList() != null && response.getAIJobList().size() != 0) {
                for (ListAIJobResponse.AIJob aiJob: response.getAIJobList()) {
                    // 视频ID
                    System.out.println("MediaId:" + aiJob.getMediaId());
                    // 作业ID
                    System.out.println("JobId:" + aiJob.getJobId());
                    // AI类型
                    System.out.println("Type:" + aiJob.getType());
                    // 作业状态
                    System.out.println("Status:" + aiJob.getStatus());
                    // 作业结果
                    System.out.println("Data:" + aiJob.getData());
                }
            }
    
            // 打印不存在的作业ID
            System.out.println("============ NonExistAIJobIds:");
            if (response.getNonExistAIJobIds() != null && response.getNonExistAIJobIds().size() != 0) {
                for (String jobId: response.getNonExistAIJobIds()) {
                    // 作业ID
                    System.out.println("NonExistAIJobId:" + jobId);
                }
            }
        } catch (Exception e) {
            System.out.println("ErrorMessage:" + e.getLocalizedMessage());
        }
    }



添加AI模板 {#h2--ai-div-id-addaitemplate-div-4}
-------------------------------------------

调用AddAITemplate接口，完成添加AI模板功能。
接口参数和返回字段请参见[AddAITemplate](/cn.zh-CN/服务端API/视频AI/AI模板/添加AI模板.md)。调用示例如下： {#h2--ai-div-id-addaitemplate-div-4}
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.alibaba.fastjson.JSONArray;
    import com.alibaba.fastjson.JSONObject;
    import com.aliyuncs.vod.model.v20170321.AddAITemplateRequest;
    import com.aliyuncs.vod.model.v20170321.AddAITemplateResponse;
    
    /**
     * 添加AI模板
     */
    public static AddAITemplateResponse addAITemplate(DefaultAcsClient client) throws Exception {
            AddAITemplateRequest request = new AddAITemplateRequest();
            // 设置模板类型，以智能审核模板为例
            request.setTemplateType("AIMediaAudit");
            // 设置模板名称
            request.setTemplateName("myaitemplate");
            // 设置模板详细配置
            JSONObject templateConfig = new JSONObject();
            JSONArray auditItem = new JSONArray();
            auditItem.add("terrorism");
            auditItem.add("porn");
            templateConfig.put("AuditItem", auditItem);
    
            JSONArray auditRange = new JSONArray();
            auditRange.add("video");
            auditRange.add("image-cover");
            auditRange.add("text-title");
            templateConfig.put("AuditRange", auditRange);
    
            JSONArray auditContent = new JSONArray();
            auditContent.add("screen");
            templateConfig.put("AuditContent", auditContent);
    
            templateConfig.put("AuditAutoBlock", "no");
            request.setTemplateConfig(templateConfig.toString());
    
            // 返回结果
            return client.getAcsResponse(request);
    }
    
    
    /**
     * 以下为调用示例
     * @param args
     * @throws ClientException
     */
    public static void main(String[] args) throws Exception {
            // 初始化客户端
            DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    
            try {
                // 获取执行结果
                AddAITemplateResponse response = addAITemplate(client);
    
                // 打印请求ID
                System.out.println("ResquestId:" + response.getRequestId());
                // 打印模板ID
                System.out.println("TemplateId:" + response.getTemplateId());
            } catch (Exception e) {
                System.out.println("ErrorMessage:" + e.getLocalizedMessage());
            }
    }



删除AI模板 {#h2--ai-div-id-deleteaitemplate-div-5}
----------------------------------------------

调用DeleteAITemplate接口，完成删除AI模板功能。
接口参数和返回字段请参见[DeleteAITemplate](/cn.zh-CN/服务端API/视频AI/AI模板/删除AI模板.md)。调用示例如下： {#h2--ai-div-id-deleteaitemplate-div-5}
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.aliyuncs.vod.model.v20170321.DeleteAITemplateRequest;
    import com.aliyuncs.vod.model.v20170321.DeleteAITemplateResponse;
    
    /**
     * 删除AI模板
     */
    public static DeleteAITemplateResponse deleteAITemplate(DefaultAcsClient client) throws Exception {
            DeleteAITemplateRequest request = new DeleteAITemplateRequest();
            // 设置模板ID
            request.setTemplateId("1d763dd8987a122ab8596eb7d57****");
    
            // 返回结果
            return client.getAcsResponse(request);
    }
    
    /**
     * 以下为调用示例
     * @param args
     * @throws ClientException
     */
    public static void main(String[] args) throws Exception {
            // 初始化客户端
            DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    
            try {
                // 获取执行结果
                DeleteAITemplateResponse response = deleteAITemplate(client);
    
                // 打印请求ID
                System.out.println("ResquestId:" + response.getRequestId());
                // 打印模板ID
                System.out.println("TemplateId:" + response.getTemplateId());
            } catch (Exception e) {
                System.out.println("ErrorMessage:" + e.getLocalizedMessage());
            }
    }



修改AI模板 {#h2--ai-div-id-updateaitemplate-div-6}
----------------------------------------------

调用UpdateAITemplate接口，完成修改AI模板功能。

接口参数和返回字段请参见[UpdateAITemplate](/cn.zh-CN/服务端API/视频AI/AI模板/修改AI模板.md)。调用示例如下：

    import com.alibaba.fastjson.JSONArray;
    import com.alibaba.fastjson.JSONObject;
    import com.aliyuncs.vod.model.v20170321.UpdateAITemplateRequest;
    import com.aliyuncs.vod.model.v20170321.UpdateAITemplateResponse;
    
    /**
     * 修改AI模板
     */
    public static UpdateAITemplateResponse updateAITemplate(DefaultAcsClient client) throws Exception {
            UpdateAITemplateRequest request = new UpdateAITemplateRequest();
            // 设置模板ID
            request.setTemplateId("1d763dd8987a122ab8596eb7d257****");
            // 设置模板名称
            request.setTemplateName("myaitemplate1");
            // 设置模板详细配置
            JSONObject templateConfig = new JSONObject();
            JSONArray auditItem = new JSONArray();
            //auditItem.add("terrorism");
            auditItem.add("porn");
            templateConfig.put("AuditItem", auditItem);
    
            JSONArray auditRange = new JSONArray();
            auditRange.add("video");
            auditRange.add("image-cover");
            //auditRange.add("text-title");
            templateConfig.put("AuditRange", auditRange);
    
            JSONArray auditContent = new JSONArray();
            auditContent.add("screen");
            templateConfig.put("AuditContent", auditContent);
    
            templateConfig.put("AuditAutoBlock", "no");
            request.setTemplateConfig(templateConfig.toString());
    
            // 返回结果
            return client.getAcsResponse(request);
    }
    
    /**
     * 以下为调用示例
     * @param args
     * @throws ClientException
     */
    public static void main(String[] args) throws Exception {
            // 初始化客户端
            DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    
            try {
                // 获取执行结果
                UpdateAITemplateResponse response = updateAITemplate(client);
    
                // 打印请求ID
                System.out.println("ResquestId:" + response.getRequestId());
                // 打印模板ID
                System.out.println("TemplateId:" + response.getTemplateId());
            } catch (Exception e) {
                System.out.println("ErrorMessage:" + e.getLocalizedMessage());
            }
    }



查询AI模板 {#h2--ai-div-id-getaitemplate-div-7}
-------------------------------------------

调用GetAITemplate接口，完成查询AI模板功能。
接口参数和返回字段请参见[GetAITemplate](/cn.zh-CN/服务端API/视频AI/AI模板/查询AI模板.md)。调用示例如下： {#h2--ai-div-id-getaitemplate-div-7}
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.aliyuncs.vod.model.v20170321.GetAITemplateRequest;
    import com.aliyuncs.vod.model.v20170321.GetAITemplateResponse;
    
    /**
     * 查询AI模板
     */
    public static GetAITemplateResponse getAITemplate(DefaultAcsClient client) throws Exception {
            GetAITemplateRequest request = new GetAITemplateRequest();
            // 设置模板ID
            request.setTemplateId("1d763dd8987a122ab8596eb7d257****");
    
            // 返回结果
            return client.getAcsResponse(request);
    }
    
    /**
     * 以下为调用示例
     * @param args
     * @throws ClientException
     */
    public static void main(String[] args) throws Exception {
            // 初始化客户端
            DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    
            try {
                // 获取执行结果
                GetAITemplateResponse response = getAITemplate(client);
    
                // 打印请求ID
                System.out.println("ResquestId:" + response.getRequestId());
                // 打印模板信息
                System.out.println("TemplateId:" + response.getTemplateInfo().getTemplateId());
                System.out.println("TemplateType:" + response.getTemplateInfo().getTemplateType());
                System.out.println("TemplateName:" + response.getTemplateInfo().getTemplateName());
                System.out.println("TemplateConfig:" + response.getTemplateInfo().getTemplateConfig());
            } catch (Exception e) {
                System.out.println("ErrorMessage:" + e.getLocalizedMessage());
            }
    }



查询AI模板列表 {#h2--ai-div-id-listaitemplate-div-8}
----------------------------------------------

调用ListAITemplate接口，完成查询AI模板列表功能。
接口参数和返回字段请参见[ListAITemplate](/cn.zh-CN/服务端API/视频AI/AI模板/查询AI模板列表.md)。调用示例如下： {#h2--ai-div-id-listaitemplate-div-8}
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.aliyuncs.vod.model.v20170321.ListAITemplateRequest;
    import com.aliyuncs.vod.model.v20170321.ListAITemplateResponse;
    
    /**
     * 查询AI模板列表
     */
    public static ListAITemplateResponse listAITemplate(DefaultAcsClient client) throws Exception {
            ListAITemplateRequest request = new ListAITemplateRequest();
            // 设置模板类型，以智能审核模板为例
            request.setTemplateType("AIMediaAudit");
    
            // 返回结果
            return client.getAcsResponse(request);
    }
    
    /**
     * 以下为调用示例
     * @param args
     * @throws ClientException
     */
    public static void main(String[] args) throws Exception {
            // 初始化客户端
            DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    
            try {
                // 查询结果
                ListAITemplateResponse response = listAITemplate(client);
    
                // 打印请求ID
                System.out.println("ResquestId:" + response.getRequestId());
                // 打印模板信息
                if (response.getTemplateInfoList() != null) {
                    for (ListAITemplateResponse.TemplateInfoListItem templateInfo : response.getTemplateInfoList()) {
                        System.out.println("================");
                        System.out.println("TemplateId:" + templateInfo.getTemplateId());
                        System.out.println("TemplateType:" + templateInfo.getTemplateType());
                        System.out.println("TemplateName:" + templateInfo.getTemplateName());
                        System.out.println("TemplateConfig:" + templateInfo.getTemplateConfig());
                    }
                }
            } catch (Exception e) {
                System.out.println("ErrorMessage:" + e.getLocalizedMessage());
            }
    }



设置默认AI模板 {#h2--ai-div-id-setdefaultaitemplate-div-9}
----------------------------------------------------

调用SetDefaultAITemplate接口，完成设置默认AI模板功能。
接口参数和返回字段请参见[SetDefaultAITemplate](/cn.zh-CN/服务端API/视频AI/AI模板/设置默认AI模板.md)。调用示例如下： {#h2--ai-div-id-setdefaultaitemplate-div-9}
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.aliyuncs.vod.model.v20170321.SetDefaultAITemplateRequest;
    import com.aliyuncs.vod.model.v20170321.SetDefaultAITemplateResponse;
    
    /**
     * 设置默认AI模板
     */
    public static SetDefaultAITemplateResponse setDefaultAITemplate(DefaultAcsClient client) throws Exception {
            SetDefaultAITemplateRequest request = new SetDefaultAITemplateRequest();
            // 设置模板ID
            request.setTemplateId("1d763dd8987a122ab8596eb757****");
    
            // 返回结果
            return client.getAcsResponse(request);
    }
    
    /**
     * 以下为调用示例
     * @param args
     * @throws ClientException
     */
    public static void main(String[] args) throws Exception {
            // 初始化客户端
            DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    
            try {
                // 获取执行结果
                SetDefaultAITemplateResponse response = setDefaultAITemplate(client);
    
                // 打印请求ID
                System.out.println("ResquestId:" + response.getRequestId());
                // 打印模板ID
                System.out.println("TemplateId:" + response.getTemplateId());
            } catch (Exception e) {
                System.out.println("ErrorMessage:" + e.getLocalizedMessage());
            }
    }



查询默认AI模板 {#h2--ai-div-id-getdefaultaitemplate-div-10}
-----------------------------------------------------

调用GetDefaultAITemplate接口，完成查询默认AI模板功能。
接口参数和返回字段请参见[GetDefaultAITemplate](/cn.zh-CN/服务端API/视频AI/AI模板/查询默认AI模板.md)。调用示例如下： {#h2--ai-div-id-getdefaultaitemplate-div-10}
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    import com.aliyuncs.vod.model.v20170321.GetDefaultAITemplateRequest;
    import com.aliyuncs.vod.model.v20170321.GetDefaultAITemplateResponse;
    
    /**
     * 查询默认AI模板
     */
    public static GetDefaultAITemplateResponse getDefaultAITemplate(DefaultAcsClient client) throws Exception {
            GetDefaultAITemplateRequest request = new GetDefaultAITemplateRequest();
            // 设置模板类型，以智能审核模板为例
            request.setTemplateType("AIMediaAudit");
    
            // 返回结果
            return client.getAcsResponse(request);
    }
    
    /**
     * 以下为调用示例
     * @param args
     * @throws ClientException
     */
    public static void main(String[] args) throws Exception {
            // 初始化客户端
            DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    
            try {
                // 获取执行结果
                GetDefaultAITemplateResponse response = getDefaultAITemplate(client);
    
                // 打印请求ID
                System.out.println("ResquestId:" + response.getRequestId());
                // 打印模板信息
                System.out.println("TemplateId:" + response.getTemplateInfo().getTemplateId());
                System.out.println("TemplateType:" + response.getTemplateInfo().getTemplateType());
                System.out.println("TemplateName:" + response.getTemplateInfo().getTemplateName());
                System.out.println("IsDefault:" + response.getTemplateInfo().getIsDefault());
                System.out.println("TemplateConfig:" + response.getTemplateInfo().getTemplateConfig());
            } catch (Exception e) {
                System.out.println("ErrorMessage:" + e.getLocalizedMessage());
            }
    }


